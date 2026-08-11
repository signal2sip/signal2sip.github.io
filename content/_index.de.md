---
title: signal2sip
layout: hextra-home
---

{{< hextra/hero-badge >}}
  <div class="hx:w-2 hx:h-2 hx:rounded-full hx:bg-primary-400"></div>
  <span>Kostenlos, quelloffen, AGPL-3.0</span>
{{< /hextra/hero-badge >}}

<div class="hx:mt-6 hx:mb-6">
{{< hextra/hero-headline >}}
  Verbindet Signal-Anrufe&nbsp;<br class="hx:sm:block hx:hidden" />mit Ihrer eigenen SIP/TK-Anlage
{{< /hextra/hero-headline >}}
</div>

<div class="hx:mb-12">
{{< hextra/hero-subtitle >}}
  Ein nativer Daemon, der die private Sprachtelefonie von Signal&nbsp;<br class="hx:sm:block hx:hidden" />mit einer gewöhnlichen SIP/TK-Anlage verbindet - durchgehend selbst gehostet
{{< /hextra/hero-subtitle >}}
</div>

<div class="hx:mb-6">
{{< hextra/hero-button text="Auf GitHub ansehen" link="https://github.com/signal2sip/signal2sip" >}}
</div>

<div class="hx:mt-6"></div>

{{< hextra/feature-grid >}}
  {{< hextra/feature-card
    title="Behalten Sie Ihre TK-Anlage"
    link="/docs/keep-your-pbx"
    subtitle="Fügen Sie Signal zu Asterisk, FreePBX oder jeder SIP/TK-Anlage als weitere Leitung hinzu - nichts muss ersetzt werden."
    icon="phone"
  >}}
  {{< hextra/feature-card
    title="Erreichbarkeit in beide Richtungen"
    link="/docs/two-way-reachability"
    subtitle="Erreichen Sie einen Signal-Kontakt über eine SIP-Nebenstelle, oder nehmen Sie einen Signal-Anruf direkt in Ihrer TK-Anlage entgegen."
    icon="switch-horizontal"
  >}}
  {{< hextra/feature-card
    title="Durchgehend selbst gehostet"
    link="/docs/self-hosted"
    subtitle="Kein Drittanbieter-Gateway sieht jemals Ihre Anrufe oder Schlüssel."
    icon="shield-check"
  >}}
  {{< hextra/feature-card
    title="Überall verschlüsselt"
    link="/docs/encryption"
    subtitle="TLS/SRTP auf der SIP-Seite, zusätzlich zur eigenen Ende-zu-Ende-Verschlüsselung von Signal."
    icon="lock-closed"
  >}}
  {{< hextra/feature-card
    title="Mehrere Konten"
    link="/docs/multi-account"
    subtitle="Beliebig viele Signal-Konten pro Daemon, jedes unabhängig konfigurierbar, mit eigenem SIP-Trunk bei Bedarf."
    icon="users"
  >}}
  {{< hextra/feature-card
    title="Live verwalten"
    link="/docs/live-management"
    subtitle="Terminal-Oberfläche oder einfache CLI - ohne Neustart des Daemons bei Konfigurationsänderungen."
    icon="terminal"
  >}}
{{< /hextra/feature-grid >}}

{{< callout type="info" >}}
  🧪 **Teststatus**: signal2sip wurde live an echter TK-Anlagen-Hardware getestet, in mehreren Konfigurationen und Anrufszenarien - hat aber noch keine breite, unabhängige Erprobung erfahren. Haben Sie einen Fehler gefunden, oder hat alles gut funktioniert? Rückmeldungen sind willkommen - eröffnen Sie ein [Issue oder einen PR](https://github.com/signal2sip/signal2sip) auf GitHub, oder schreiben Sie uns einfach eine E-Mail.
{{< /callout >}}

{{< disclaimer >}}
