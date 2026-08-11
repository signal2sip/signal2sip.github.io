---
title: "Multi-account"
weight: 5
---

One `signal2sip-daemon` process serves any number of Signal accounts at
once - there's no per-account process to manage, and no fixed limit
baked into the architecture.

## Independent configuration

Each account is configured separately and can differ from every other
one:

- Its own Signal identity - either registered directly (a primary
  device) or linked to an existing real phone (a secondary device),
  independently of how any other account on the same daemon was set up.
- Its own SIP trunk, if it has one at all - host, credentials, transport
  (UDP or TLS), SRTP mode, and bridge destination are all per account.
  Some accounts can be Signal-only with no SIP bridging configured.
- Its own enabled/disabled state - disable one account without
  affecting any other.

## Isolated at runtime

Accounts don't share call state or media with each other - each gets
its own dedicated SIP transport, and audio from one account's call
never crosses into another's, even when several calls are active on
different accounts simultaneously.

## Add or remove without downtime

Accounts can be added, removed, enabled, or disabled while the daemon
keeps running - no restart, and no interruption to any other account's
active calls or registration. See [Manage it live](../live-management)
for how that hot-apply mechanism works.
