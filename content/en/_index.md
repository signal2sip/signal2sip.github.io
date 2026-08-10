---
title: "signal2sip"
tagline: "Bridge Signal calls to your own SIP/PBX infrastructure."
---

## What it is

signal2sip is a native daemon that connects [Signal](https://signal.org)'s
private voice calling to a standard SIP/PBX system. One process serves any
number of Signal accounts at once, each with its own SIP trunk if needed -
driven entirely by real Signal Protocol messaging and RingRTC calling, with
audio bridged to SIP through PJSIP.

## Why it matters

- Keep using your existing PBX (Asterisk, FreePBX, ...) while adding Signal
  as another line into it
- Reach a Signal contact by dialing an extension, or reach a SIP extension
  from a Signal call
- Self-hosted end to end - no third-party gateway ever sees your calls or
  your keys
- TLS/SRTP on the SIP leg, alongside Signal's own end-to-end encrypted
  calling

## Features

- Any number of Signal accounts per daemon, each configured independently
- Register a new Signal number, or link as a secondary device to an
  existing one
- Encrypted SIP signaling (TLS) and media (SRTP)
- Manage accounts live - via a terminal UI or a plain CLI - with no daemon
  restart needed
- Free and open source, licensed under AGPL-3.0

## Get started

Build instructions, configuration reference, and everything else lives in
the [GitHub repository](https://github.com/signal2sip/signal2sip).
