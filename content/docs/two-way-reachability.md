---
title: "Two-way reachability"
weight: 2
---

A signal2sip-managed number is a full member of both worlds - it can be
called from either side, and calls placed on either side reach the
other.

## Signal call in → PBX

When someone calls a signal2sip account on Signal, the daemon answers
only once the PBX side actually picks up (it doesn't steal the call
from your other real/linked Signal devices before that), then bridges
the audio to whichever destination that account is configured to dial:

- `sip_bridge_destination` - dial a specific extension directly.
- `sip_bridge_did` - dial a DID and let the PBX's own Inbound Route
  decide the real destination (ring group, IVR, time conditions,
  failover) - useful if you want that logic to live in your PBX config
  instead of signal2sip's.

## PBX call out → Signal

Dial through a signal2sip account's own SIP extension like any other
outbound call, and it places a real Signal call to whatever number you
dialed. The destination is resolved through Signal's Contact Discovery
Service the same way a real Signal client would, so no manual mapping
between phone numbers and Signal identities is needed.

## DTMF (dialing digits into an IVR)

{{< callout type="info" emoji="🚧" >}}
  **In development.** A Signal caller landing on a PBX IVR or a
  digit-driven menu can't yet send touch-tones into it - this is planned,
  not shipped.
{{< /callout >}}

Signal's own apps have no in-call dialpad, so the plan is the same
pattern already proven in this project's sibling bridge for Telegram
([tg2sip-webrtc](https://github.com/vladonv/tg2sip-webrtc)), which hits
the identical limitation there: while a call is up, sending digits as a
plain text message in the same conversation gets picked up and relayed
as a real SIP DTMF event (RFC 2833) into the call, without needing any
in-call UI Signal doesn't have.

## Hangup propagates both ways

Ending the call on either side - Signal or the PBX - ends it on the
other side too, instead of leaving a dangling half-connected call on
one leg.
