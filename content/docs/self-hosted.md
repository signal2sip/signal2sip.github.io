---
title: "Self-hosted, end to end"
weight: 3
---

signal2sip is a single native daemon you run on your own infrastructure
- there's no hosted service, no third-party relay, and no external
component that ever sees your calls, your Signal credentials, or your
encryption keys.

## What actually runs

One process, `signal2sip-daemon`, handles any number of Signal accounts
at once. Everything it needs - Signal Protocol state, SIP trunk
settings, per-account configuration - lives in a single local SQLCipher
(encrypted SQLite) database file that only your box ever touches.

## What you deploy

- `signal2sip-daemon` - the long-running bridge itself.
- `signal2sip-gendb` - a companion CLI for account lifecycle
  (register/link a Signal account, manage config) that doesn't need the
  daemon running.
- `signal2sip-tui` - an optional terminal UI over the same account/config
  data, for interactive management.

A `systemd` unit is provided for running the daemon as a proper service.
Source is fully available and licensed AGPL-3.0 - see the
[repository](https://github.com/signal2sip/signal2sip) and
[`THIRD_PARTY_LICENSES.md`](https://github.com/signal2sip/signal2sip/blob/main/THIRD_PARTY_LICENSES.md)
for why (it statically links Signal's own AGPL-3.0-licensed
`libsignal`/`ringrtc`).

signal2sip is not affiliated with, endorsed by, or sponsored by Signal
Messenger, LLC or the Signal Technology Foundation.
