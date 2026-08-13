---
title: signal2sip
layout: hextra-home
---

{{< hextra/hero-badge >}}
  <div class="hx:w-2 hx:h-2 hx:rounded-full hx:bg-primary-400"></div>
  <span>Free, open source, AGPL-3.0</span>
{{< /hextra/hero-badge >}}

<div class="hx:mt-6 hx:mb-6">
{{< hextra/hero-headline >}}
  Bridge Signal messenger calls&nbsp;<br class="hx:sm:block hx:hidden" />to your own SIP/PBX
{{< /hextra/hero-headline >}}
</div>

<div class="hx:mb-12">
{{< hextra/hero-subtitle >}}
  A native daemon connecting Signal's private voice calling&nbsp;<br class="hx:sm:block hx:hidden" />to a standard SIP/PBX system - self-hosted, end to end
{{< /hextra/hero-subtitle >}}
</div>

<div class="hx:mb-6">
{{< hextra/hero-button text="View on GitHub" link="https://github.com/signal2sip/signal2sip" >}}
</div>

<div class="hx:mt-6"></div>

{{< hextra/feature-grid >}}
  {{< hextra/feature-card
    title="Keep your existing PBX"
    link="/docs/keep-your-pbx"
    subtitle="Add Signal to Asterisk, FreePBX, or any SIP/PBX system as just another line - no need to replace anything."
    icon="phone"
  >}}
  {{< hextra/feature-card
    title="Two-way reachability"
    link="/docs/two-way-reachability"
    subtitle="Dial a Signal contact from a SIP extension, or receive a Signal call routed straight into your PBX."
    icon="switch-horizontal"
  >}}
  {{< hextra/feature-card
    title="Self-hosted, end to end"
    link="/docs/self-hosted"
    subtitle="No third-party gateway ever sees your calls or your keys."
    icon="shield-check"
  >}}
  {{< hextra/feature-card
    title="Encrypted everywhere"
    link="/docs/encryption"
    subtitle="TLS/SRTP on the SIP leg, alongside Signal's own end-to-end encrypted calling."
    icon="lock-closed"
  >}}
  {{< hextra/feature-card
    title="Multi-account"
    link="/docs/multi-account"
    subtitle="Any number of Signal accounts per daemon, each configured independently, each with its own SIP trunk if needed."
    icon="users"
  >}}
  {{< hextra/feature-card
    title="Manage it live"
    link="/docs/live-management"
    subtitle="A terminal UI or a plain CLI - no daemon restart needed for config changes."
    icon="terminal"
  >}}
{{< /hextra/feature-grid >}}

{{< callout type="info" >}}
  🧪 **Testing status**: signal2sip has been tested live against real PBX hardware, across several configurations and call scenarios - but it hasn't seen broad, independent testing yet. Found a bug, or has it worked well for you? Feedback is welcome - open an [issue or PR](https://github.com/signal2sip/signal2sip) on GitHub, or just email us.
{{< /callout >}}

{{< disclaimer >}}
