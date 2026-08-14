---
title: "Proxy & censorship circumvention"
weight: 8
---

Each Signal account signal2sip manages can be routed through a proxy -
the same mechanism the official Signal apps' "Set Proxy" feature uses,
for the same reason: reaching Signal's servers from a network where
they're blocked, without a VPN.

## How it works

- signal2sip's proxy support uses the identical protocol real Signal
  clients use for a manually-configured proxy (the `org.signal.tls`
  scheme carried by `signal.tube` links): a **transparent TCP/TLS
  relay** to `chat.signal.org`.
- The relay never terminates or inspects the TLS session it's carrying
  - your client's real end-to-end TLS handshake to `chat.signal.org`
  (Signal's own pinned certificate, real SNI) happens exactly as it
  would without a proxy in between; the relay just forwards ciphertext
  bytes it can't itself read. A proxy hides *that a connection to
  Signal is happening at all* from a network observer - it doesn't add
  a decryption point, and doesn't weaken any of Signal's own
  end-to-end guarantees.
- This is separate from Signal's own automatic domain-fronting layer
  (fronting connections through generic, hard-to-block CDN endpoints),
  which signal2sip's manual proxy field doesn't control directly - see
  the independent flag below.

## Configuring it, per account

Two independent settings, both editable live - no daemon restart
needed, see [Manage it live](../live-management) - via
`signal2sip-gendb` or the TUI's Signal-settings screen:

```
signal2sip-gendb <account-name> config set signal_proxy proxy.example.com
signal2sip-gendb <account-name> config set signal_proxy proxy.example.com:8443
signal2sip-gendb <account-name> config set signal_proxy ""
```

- **`signal_proxy`** - host, optionally `host:port` (default `443`),
  of a transparent TLS relay; empty (the default) connects directly.
  Same relay a real Signal client's "Set Proxy" screen would point at.
- **`signal_censorship_circumvention`** - `yes`/`no`, independent
  toggle for Signal's own automatic domain-fronting behavior.

## Running your own relay

No custom protocol is involved server-side - a transparent TCP/TLS
passthrough to `chat.signal.org:443` is all it takes (an `nginx
stream {}` block, `socat`, or HAProxy TCP mode all work). For a
ready-to-deploy option, signal2sip also publishes
[`signal-proxy-caddy`](https://github.com/signal2sip/signal-proxy-caddy)
(Apache-2.0, its own repository) - a Caddy-based relay with one real
improvement over the official
[`signalapp/Signal-TLS-Proxy`](https://github.com/signalapp/Signal-TLS-Proxy):
non-Signal probe traffic gets redirected to a decoy response instead
of dropped, closing an active-probing fingerprint gap
([net4people/bbs#60](https://github.com/net4people/bbs/issues/60))
the official proxy still has. It also supports an optional IP
allowlist if you'd rather keep a relay private to your own accounts
than open to the public.

{{< callout type="info" emoji="✅" >}}
  **Verified live**: tested end to end against a real deployed relay -
  a raw TLS-relay check, a real official Signal app, and a real
  signal2sip account all confirmed correctly routing through it.
{{< /callout >}}
