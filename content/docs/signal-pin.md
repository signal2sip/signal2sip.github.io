---
title: "Signal PIN & Registration Lock"
weight: 9
---

Signal's PIN protects an account against a specific takeover scenario:
someone else gaining control of the phone number itself (a carrier
reissuing a dropped number, SIM-swap fraud, physical SIM theft).
Without a PIN, Signal's only proof of ownership at registration time is
"can receive the verification code" - whoever holds the number can
re-register with it and disconnect every device the real owner had.
With a PIN and Registration Lock enabled, the server refuses to
complete that re-registration without it too, even given a valid
verification code.

{{< callout type="warning" emoji="⚠️" >}}
  **Every account `signal2sip-gendb register` creates today has no PIN
  at all** - registration deliberately skips it (the equivalent of
  tapping "Skip" on a real client's PIN-creation screen), so none of
  these accounts currently benefit from this protection. See the
  planned-work callout at the bottom of this page.
{{< /callout >}}

## How it works under the hood

The PIN itself never leaves your device in a recoverable form. It's
used to derive a secret that's stored in **SVR2** (Secure Value
Recovery, v2) - an SGX-attested enclave service that can confirm a
guess matches without the operator (Signal, or anyone else) ever being
able to read the stored value directly. The wire protocol
(`svr2.proto`, vendored inside `libsignal`) is a three-step exchange:

1. **Backup** - store the derived secret, with a maximum number of
   guesses you're allowed before it self-destructs.
2. **Expose** - a required confirmation step after a successful
   Backup.
3. **Restore** - later, present the PIN again to get the secret back
   (or find out it doesn't match).

One operational detail worth knowing even as an end user: an
implementation must not restart the Backup+Expose pair once it has
already succeeded once - doing so resets the guess counter and
weakens the anti-brute-force guarantee it exists to provide.

## What happens after too many wrong guesses

This is where three genuinely separate limits get conflated in casual
explanations - they're independent, and only one of them is
permanent:

| Limit | Scope | What happens | Recoverable? |
|---|---|---|---|
| SVR2 enclave guess counter | Set when the PIN was first backed up (Signal's own apps use 10) | Reaching 0 makes the enclave **permanently erase** the stored secret - nobody, including Signal, can undo this | **No** |
| Server-side PIN verification rate limit | 10 attempts per 24 hours | Just a rate limit on checking the Registration Lock token during registration/change-number - resets daily | Yes, automatically |
| Registration Lock freeze window | 7 days | Starts the moment someone verifies the phone number correctly (real SMS/call code) but supplies a wrong or missing PIN - the account is frozen and every device disconnected until this expires or the correct PIN is supplied | Yes, after 7 days |

The practical upshot: losing the PIN doesn't permanently strand the
phone number itself. Even in the worst case - the SVR2 secret is gone
for good - the account-level freeze is time-boxed. After 7 days with
no successful match, the server stops requiring the PIN and lets
registration proceed. What's lost permanently is whatever was
protected *by* the SVR2 secret - for Registration Lock specifically,
that's just the lock itself, not message history (which isn't stored
there).

{{< callout type="info" emoji="🚧" >}}
  **Planned, not yet implemented.** signal2sip has researched the full
  protocol and the libsignal-ffi calls needed (the same
  attested-enclave pattern already used for Contact Discovery), but no
  PIN/Registration Lock support exists yet - `gendb register`/`verify`
  never sets one. Proposed surface once built:
  `signal2sip-gendb <name> pin set`,
  `signal2sip-gendb <name> pin verify`, and
  `signal2sip-gendb <name> registration-lock enable/disable`. Given
  that a bug here can burn real, attempt-limited SVR2 guesses on a
  live account, this will get extra testing care before shipping,
  more than most other signal2sip features have needed.
{{< /callout >}}
