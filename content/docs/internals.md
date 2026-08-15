---
title: "Internals & operational nuances"
weight: 7
---

This page collects operational details that don't fit neatly into the
other pages - exactly how config resolution works, what every
`signal2sip-gendb` account-lifecycle command does (and doesn't) touch,
and the daemon's own internal timers. For admins who want to know
precisely what's happening under the hood, not just how to get started.

## Config file resolution

Both `signal2sip-daemon` and `signal2sip-gendb` resolve their config
file the same way, checked in order:

1. An explicit path passed as the first argument.
2. `/etc/signal2sip/signal2sip.conf`, if it exists.
3. `./signal2sip.conf` (relative to the current working directory) -
   the fallback for a dev checkout, not a real installed deployment.

The Signal root CA certificate every native TLS client in this project
pins follows the identical pattern:
`/etc/signal2sip/certs/signal-root-ca.pem` if present, else
`./certs/signal-root-ca.pem`.

## What lives where: `[global]` file vs. per-account database

The config file only ever has one `[global]` section - a handful of
process-wide settings. Everything else lives in the SQLCipher database
`[global]` itself points at (`db_path`):

| `[global]` key | Default | What it controls |
|---|---|---|
| `db_path` / `db_key` | *(required)* | The one SQLCipher database file every account's data lives in, and its passphrase. |
| `sip_reg_watchdog_sec` | 60 | How long a SIP account may sit unregistered before the daemon forces a fresh registration attempt itself (PJSIP's own auto-retry doesn't cover every failure code, e.g. `403`). |
| `resolved_contact_ttl_sec` | 86400 (1 day) | How long a cached e164→ACI/PNI resolution (from a real Contact Discovery lookup) is trusted before re-resolving. |
| `storage_sync_interval_sec` | 43200 (12h) | How often a linked account (one with real Signal contact-sync access) re-fetches its contact list from Signal's StorageService. |
| `config_poll_interval_sec` | 30 | How often the daemon re-reads every account's config from the database as a fallback, independent of SIGHUP (see below). |
| `on_account_error_cmd` | *(empty = disabled)* | Optional shell command run when an account hits a known, unrecoverable-without-admin-action problem (today: Signal rejecting this device's credentials) or recovers from one - see [Signal PIN & Registration Lock](../signal-pin) for why this can happen even without a SIP-side problem. |

Everything else - `sip_host`, `sip_extension`, `sip_password`,
`sip_transport`, `sip_srtp`, `sip_bridge_destination`/`sip_bridge_did`,
the enabled flag, and more - lives in the database's `account` table,
one row per account, edited via `signal2sip-gendb <name> config
set/get/list` or `enable`/`disable`, never by hand-editing a file.

## One misconfigured account doesn't block the others

Every account is brought up independently, both at startup and on every
live reload - a typo'd `sip_tls_ca_file` path, an unreachable PBX, or
any other per-account problem only ever takes down that one account,
never any other:

- The entire per-account startup sequence runs inside a single
  `try`/`catch` - on any failure it logs `account setup failed: ... -
  skipping this account, continuing with the rest` and moves on. An
  account with no SIP configured at all (Signal-only) is completely
  unaffected by another account's PBX trunk being broken.
- The SIP/PBX side has its own extra layer on top: a bad
  `sip_tls_ca_file` (pointing at a file that doesn't exist or can't be
  read) only fails that one account's SIP transport (logged as `TLS
  transport setup failed: ...`) - its Signal side, if already connected,
  keeps running regardless.

This can't help with a resource every account shares identically, though
- e.g. a wrong path to the Signal root CA certificate (a `[global]`
concern, not per-account) fails every account the same way, since
there's no "good vs. bad account" distinction to make there. That's a
different failure mode from a per-account typo, not something
account-level isolation can fix by itself.

## How a config change actually reaches a running daemon

Two independent mechanisms, whichever fires first:

- **SIGHUP** - `gendb config set`/`enable`/`disable` send the running
  daemon a `SIGHUP` on a best-effort basis (reads its pidfile, confirms
  `/proc/<pid>/exe` actually resolves to a real `signal2sip-daemon`
  binary before signaling - a stale or reused PID is silently skipped,
  not signaled). Near-instant when it works.
- **The poll fallback** - regardless of whether SIGHUP reached the
  daemon (not running at the time, stale pidfile, permission issue), the
  daemon re-reads `[global]` plus every enabled account's config every
  `config_poll_interval_sec` (default 30s) on its own. This is the real
  guarantee; SIGHUP is just the fast path.

Either path runs the exact same reload logic: diff the freshly-loaded
config against what's currently running - accounts no longer present
(disabled, or deleted) get torn down, new/newly-enabled accounts get set
up, and an already-running account whose `config_version` changed
(bumped automatically by every `config set`) gets torn down and rebuilt
with the new settings. An account untouched by the change keeps running
exactly as it was - no other account's calls or registration are
affected.

## The daemon's main loop: independent timers, not one shared tick

Deliberately separate, each for its own reason:

- **Config poll** (`config_poll_interval_sec`, default 30s) - see above.
- **SIP registration watchdog** (`sip_reg_watchdog_sec`, default 60s) -
  per account, forces a fresh registration attempt if it's been
  unregistered longer than this, covering failure codes PJSIP's own
  auto-retry doesn't. See [Two-way reachability](../two-way-reachability)
  for the separate, Signal-connection-drives-SIP-state watchdog this
  cooperates with.
- **Resolved-contact cache** (`resolved_contact_ttl_sec`, default 1 day)
  - governs how long an outgoing call target's cached Contact Discovery
  result is reused before a fresh lookup. Kept long deliberately, since
  real CDS lookups are rate-limited per account.
- **StorageService contact re-sync** (`storage_sync_interval_sec`,
  default 12h) - per linked account, re-fetches the real contact list
  from Signal's servers. Runs synchronously on the same loop as
  everything else (nothing in this daemon's main loop is async) - a slow
  network round-trip here can delay the loop's other checks by up to
  ~90s worst case, but only once per account per interval, not on every
  tick.

## `signal2sip-gendb` account lifecycle, precisely

The exact effect of every lifecycle command - what changes locally (in
the database) versus on Signal's real servers, and whether it's
reversible:

| Command | Reversible? | Local database | Signal's servers |
|---|---|---|---|
| `register --e164 <e164> sms\|voice` | - | creates the account row | starts a real SMS/voice-verified registration session (Flow A) |
| `verify <code>` | - | fills in the account's real identity (ACI/PNI/keys) | completes registration |
| `link` | - | creates the account row | links as a secondary device via QR code (Flow B) |
| `deactivate` (alias: `unregister`) | **Yes** (`reactivate`) | untouched | flips `fetchesMessages=false` - senders can't reach this number, nothing else changes |
| `reactivate` | - | untouched | flips `fetchesMessages=true` back |
| `enable` / `disable` | **Yes** (the other one) | flips the row's `enabled` flag only | untouched - a disabled account is simply not loaded by the daemon |
| `unlink` | **No** | **wipes this account's row entirely** | untouched - the real Signal account (and its phone number) is completely unaffected |
| `delete-account` | **No** | wiped, but *only on a confirmed success response* - see below | `DELETE /v1/accounts/me` - destroys the account and every linked device, frees the number for anyone to re-register |

Two things worth calling out explicitly:

- **`deactivate` is the safe, reversible one** - a pure server-side flag
  flip, no local data is ever touched, and `reactivate` undoes it
  completely. `unlink` and `delete-account` are the commands that
  actually remove local data. The old name `unregister` still works as
  an alias.
- **`delete-account`'s server response can be genuinely ambiguous.**
  Signal's own protocol documents this endpoint as sometimes completing
  via a WebSocket close (code `4401`) instead of a normal HTTP response -
  signal2sip doesn't yet decode that close code, so a connection that
  closes before any response arrives is indistinguishable from a plain
  network failure. On that ambiguous outcome, **local data is
  deliberately left untouched** rather than guessing - verify manually
  (e.g. try registering the same e164 fresh elsewhere) before running
  `unlink` yourself to clear the local row.

## Signaling account problems to the admin

Unlike a plain SIP registration drop (which the daemon just retries on
its own, purely from memory), some Signal-side failures can't be
recovered without a human: today that means
`AuthSocket::isDeauthorized()` firing (the account was unlinked/deleted
elsewhere, or - once Registration Lock support exists, see [Signal PIN &
Registration Lock](../signal-pin) - a takeover attempt was correctly
rejected for lack of the right PIN, which also freezes the real owner's
own credentials as a side effect). The daemon gives up retrying that
specific account and needs `signal2sip-gendb <name> link` (or `unlink`
then `link`) followed by a restart.

Three independent, complementary ways this reaches an admin:

1. **`account.last_error`/`last_error_at`** - written to the database the
   moment this happens, cleared automatically the next time the account
   connects successfully (always after a restart, since the daemon stops
   retrying in-process). Visible via `signal2sip-gendb list` (shown as an
   `ERROR (since ...)` suffix) and the TUI's account list (red "problem"
   status) - both were previously blind to this, since it only ever
   existed in the running daemon's own memory before.
2. **A `journalctl -p err`-visible log line** - the daemon's own stderr
   message is tagged with systemd's `<3>` (LOG_ERR) syslog-level prefix,
   so it's greppable/alertable via journald without any extra
   configuration (the packaged systemd unit already sends stderr to the
   journal).
3. **`on_account_error_cmd`** (see the config table above) - an optional
   shell hook for wiring this into whatever notification channel you
   actually want (email, a Telegram/ntfy.sh bot, a Slack webhook -
   signal2sip deliberately doesn't pick one for you). Called as
   `/bin/sh -c '<your command>' sh <account-name> <e164> <error-type>` -
   the three values arrive as `$1`/`$2`/`$3` inside your command, e.g.:

   ```
   on_account_error_cmd=curl -s -d "signal2sip: $1 ($2) is $3" ntfy.sh/your-topic
   ```

   `<error-type>` is currently `deauthorized` or `recovered`. Fire-and-
   forget - the daemon never waits on it or checks its exit code, so a
   slow or hanging script can't stall any other account's handling.

{{< callout type="info" emoji="🚧" >}}
  **Planned, not yet implemented**: startup hardening for both
  `signal2sip-daemon` and `signal2sip-gendb` - refusing to start at all
  when run as `root`, and verifying the config file and database are
  owned by the running user with the config file at exactly `0600`
  before opening either. Neither binary checks this today.
{{< /callout >}}
