---
title: "Encrypted everywhere"
weight: 4
---

Both legs of a bridged call can be encrypted - what that encryption
actually covers is different on each side, worth understanding rather
than assuming.

## The Signal side

signal2sip is a real Signal client from the protocol's point of view -
it registers or links like any other device and places/receives calls
using RingRTC, the same calling stack the official apps use. Call media
between signal2sip and the other Signal party is protected exactly the
way a normal Signal call is: Signal's own key exchange, SRTP with keys
negotiated out-of-band over the encrypted signaling channel. Nobody
between the two Signal endpoints - including signal2sip's own network
path to Signal's servers - can see into that media.

signal2sip is itself a genuine endpoint of that Signal call, the same
way any linked device is - it decodes the audio to bridge it onward, the
same way a phone's speaker eventually does.

## The SIP/PBX side

Independently, the leg between signal2sip and your PBX can also be
secured, per account:

- **Signaling**: `sip_transport=tls` (SIPS) instead of plain UDP - the
  SIP messages themselves (including any SRTP key exchange in the SDP)
  travel encrypted.
- **Media**: `sip_srtp=mandatory` requires SRTP on the RTP leg and
  refuses plain RTP; `optional` offers SRTP but falls back to plain RTP
  if your PBX endpoint isn't configured for it; `disabled` is plain RTP,
  same as a typical unencrypted SIP trunk.

For SDES-SRTP (the key-exchange method used here), the exchange itself
travels inside the SIP signaling - pairing `sip_srtp` with
`sip_transport=tls` closes the one gap that plain-UDP signaling would
otherwise leave (SRTP keys visible to anything that can see the SIP
signaling, even though the RTP stream itself is already protected).

## Together

A call bridged through signal2sip therefore has independently-encrypted
media on each leg, with signal2sip itself as the one place both legs
meet - not a single end-to-end tunnel spanning both parties, since
bridging Signal calling to an entirely different protocol (SIP/RTP)
structurally requires a real point where the media is decoded and
re-encoded.
