---
title: "Manage it live"
weight: 6
---

Every account-lifecycle and configuration action is available without
ever touching the daemon's config file by hand or restarting it -
through a CLI, or a terminal UI over the same data.

## `signal2sip-gendb` - the CLI

A companion binary, separate from the daemon, for everything account
related:

```
signal2sip-gendb <name> register --e164 <e164> sms   # new account, SMS-verified
signal2sip-gendb <name> link                          # link as a secondary device (QR code)
signal2sip-gendb <name> config get|set|list            # read/write SIP & deployment config
signal2sip-gendb <name> enable|disable                 # toggle without deleting anything
```

All of it operates on the daemon's own database directly - `gendb`
doesn't need the daemon running to register or configure an account.

## `signal2sip-tui` - the terminal UI

The same account list, per-account detail/status, and SIP configuration
editor as the CLI, navigable interactively: account list → detail →
config editor, with inline validation (e.g. a TLS transport requires
either a pinned CA certificate or an explicit insecure opt-in before it
lets you save) and confirmation prompts before anything destructive.

## Changes apply live

Once the daemon is running, it picks up configuration changes two ways,
whichever fires first:

- **Immediately** via a signal sent by `gendb`/the TUI right after a
  change.
- **Within a short poll interval** regardless, as a fallback - so even a
  change made while the daemon couldn't be signaled directly still
  applies on its own shortly after.

Only the account that actually changed gets rebuilt (its SIP
registration re-established, its config reloaded) - every other
account's active calls and registration are left untouched.
