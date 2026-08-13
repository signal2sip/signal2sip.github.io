---
title: "Keep your existing PBX"
weight: 1
---

signal2sip doesn't replace any part of your telephony setup - it registers
against your existing Asterisk, FreePBX, or any other SIP-compatible PBX
as an ordinary SIP endpoint, the same way a desk phone or softphone would.

## How it connects

Each Signal account signal2sip manages gets its own dedicated SIP
transport and registration, configured per account:

- `sip_host` / `sip_extension` / `sip_password` - a normal SIP
  registration against your PBX.
- `sip_transport=udp` or `sip_transport=tls` (SIPS) - plain UDP or a
  TLS-secured signaling transport, your choice per account.
- `sip_srtp=disabled|optional|mandatory` - whether the RTP media itself
  is secured (SDES-SRTP) on top of the signaling transport.

Nothing on the PBX side needs to know signal2sip isn't a regular phone -
your existing dialplan, inbound routes, and extension numbering all keep
working unchanged.

## Both directions

- **Signal call in, bridged to the PBX**: `sip_bridge_destination` (a
  plain extension) or `sip_bridge_did` (an Inbound-Route-style DID,
  letting FreePBX's own routing/IVR/ring-group logic decide the real
  destination) - see [Two-way reachability](../two-way-reachability).
- **PBX call out, bridged to Signal**: dial through signal2sip's
  extension and it places a real outgoing Signal call, resolving the
  dialed number via Signal's own Contact Discovery.

## Codec: your PBX endpoint must allow L16/48000 (slin48)

{{< callout type="warning" emoji="⚠️" >}}
  signal2sip offers **only one codec** on the SIP leg - if your PBX
  endpoint doesn't allow it, call setup fails outright (SDP `m=audio 0`,
  PBX responds `488 Not Acceptable Here`).
{{< /callout >}}

signal2sip's internal audio bridge moves raw, uncompressed audio between
RingRTC and PJSIP with no transcoding step at all - by design, to avoid
the CPU cost and quality loss of encoding/decoding on every packet. That
only works if PJSIP negotiates the *exact* format the bridge already
uses internally, so the daemon deliberately offers a single codec on
every SIP call: **L16/48000/1** (16-bit linear PCM, 48kHz, mono) - every
other codec PJSIP knows about (G.711, G.722, Opus, GSM, ...) is
explicitly disabled, not just deprioritized.

**What this means for your PBX config**: the endpoint/trunk signal2sip
registers against must have this codec allowed, or the call never gets
media at all. In Asterisk/FreePBX (`chan_pjsip`), this codec is called
**`slin48`** - make sure it's in the endpoint's allowed codec list, e.g.:

```ini
[signal2sip-trunk]
allow=!all,slin48
```

If a call's SIP signaling looks fine (registration succeeds, INVITE
goes out) but audio never comes up and the PBX rejects with `488`,
this codec mismatch is the first thing to check.

## Caller ID on your phones

When a Signal call comes in and gets bridged out to the PBX, signal2sip
attaches the caller's real Signal identity to the outgoing INVITE as
custom SIP headers:

- `X-Signal-UUID` - always present, the caller's Signal account
  identifier.
- `X-Signal-Phone` / `X-Signal-Name` - best-effort, populated when
  that contact's phone number/display name is already known locally
  (synced from Signal's contact sync) - not guaranteed for every caller.

FreePBX/Asterisk don't read custom SIP headers by default, so your
dialplan needs an explicit step to pick them up and map them onto real
Caller ID. A minimal FreePBX example, in a custom context read via
`PJSIP_HEADER`:

```
[from-signal2sip-headers]
exten => _X.,1,Set(CALLERID(name)=${IF($["${PJSIP_HEADER(read,X-Signal-Name)}"!=""]?${PJSIP_HEADER(read,X-Signal-Name)}:Signal#${PJSIP_HEADER(read,X-Signal-UUID)})})
 same => n,Set(CALLERID(num)=${IF($["${PJSIP_HEADER(read,X-Signal-Phone)}"!=""]?${PJSIP_HEADER(read,X-Signal-Phone)}:${PJSIP_HEADER(read,X-Signal-UUID)})})
 same => n,Dial(PJSIP/${EXTEN},30)
```

Point the relevant Inbound Route (the specific DID, not a catch-all -
catch-all routes are evaluated last and would never see this) at that
context instead of dialing straight through. Once wired up, a bridged
Signal call shows the real caller's name/number on your desk phones,
the same as any other trunk.

## Step-by-step: doing this entirely from the FreePBX web UI

If you've never hand-edited Asterisk dialplan before, the minimal example
above can be confusing to actually wire up - here's the same result done
end to end through the web UI, with a slightly more defensive version of
the dialplan that holds up better in practice than the minimal one.

{{% steps %}}

### Add the context

FreePBX's own **Config Edit** module (Admin -> Config Edit) can add this
without ever opening an SSH terminal: pick `extensions_custom.conf`,
paste the block below, and save. It does the same thing as the minimal
example above, plus three real improvements worth having once you're
pasting this into a production PBX anyway:

```
[from-signal2sip-headers]
exten => _.,1,NoOp(Incoming Signal call via signal2sip)
 same => n,Set(SIG_UUID=${PJSIP_HEADER(read,X-Signal-UUID)})
 same => n,Set(SIG_PHONE=${PJSIP_HEADER(read,X-Signal-Phone)})
 same => n,Set(SIG_NAME=${PJSIP_HEADER(read,X-Signal-Name)})
 same => n,Set(CALLERID(name)=${IF($["${SIG_NAME}"!=""]?${SIG_NAME}:Signal#${SIG_UUID})})
 same => n,Set(CALLERID(num)=${IF($["${SIG_PHONE}"!=""]?${SIG_PHONE}:${SIG_UUID})})
 same => n,Dial(PJSIP/106,30)
 same => n,Hangup()
```

- **`_.` instead of `_X.`** - this context is entered via a Custom
  Destination (below), not a normal number match, so the extension
  pattern needs to accept whatever FreePBX hands it through, not just
  digits.
- **Each header read once, into `SIG_UUID`/`SIG_PHONE`/`SIG_NAME`**,
  instead of calling `PJSIP_HEADER(read,...)` inline inside `IF(...)` -
  Asterisk substitutes every `${...}` in a line *before* evaluating
  `IF()`, so the inline version silently reads each header twice per
  line (once for the condition, once for the branch) regardless of which
  branch wins. Harmless here, but worth knowing before relying on that
  inline pattern elsewhere in your dialplan.
- **Replace `106` with the real extension you want Signal calls to ring
  at your site.** Unlike the minimal example, this doesn't dial
  `${EXTEN}` dynamically - by the time execution reaches here, `${EXTEN}`
  is whatever the Custom Destination passed through, not necessarily a
  real PJSIP endpoint name.
- **The trailing `Hangup()`** makes call teardown explicit if `Dial()`
  returns without an answer (busy/no-answer/timeout), instead of relying
  on Asterisk's own implicit end-of-dialplan handling.

Apply the config (the usual red bar) after saving.

### Register it as a Custom Destination

**Admin -> Custom Destinations -> Add Destination.** Set **Target** to
`from-signal2sip-headers,${EXTEN},1` (the context you just added,
priority 1), and give it a description you'll recognize later, e.g.
"SIGNAL2SIP Caller Info":

![FreePBX Custom Destinations, Target set to from-signal2sip-headers,${EXTEN},1](/images/docs/freepbx-custom-destination.png)

Submit and apply config.

### Point an Inbound Route at it

**Connectivity -> Inbound Routes**, open the specific DID signal2sip's
`sip_bridge_did` sends calls to (not a catch-all - catch-all routes are
evaluated last and would never see this), and set its **Destination** to
the Custom Destination you just created, instead of dialing an extension
directly.

{{% /steps %}}

## Live config, no restart

Every per-account setting lives in the daemon's own database, not
a static config file - only a handful of process-wide settings (the
database path/key, watchdog/poll intervals) live in
`/etc/signal2sip/signal2sip.conf`'s single `[global]` section. Change an
account's settings with `signal2sip-gendb <name> config set <field>
<value>` or through the terminal UI, and the daemon picks the change up
live (SIGHUP or a periodic poll), no restart needed. See [Manage it
live](../live-management).

This per-account database row isn't touched by a soft `unregister` (a
reversible, server-side-only flag flip - all local data stays put,
`reactivate` undoes it) - only `unlink` (wipes this account's local row,
leaves the real Signal account untouched) or a successful
`delete-account` (which also destroys the account on Signal's own
servers) actually deletes it.
