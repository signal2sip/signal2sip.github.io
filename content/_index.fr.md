---
title: signal2sip
layout: hextra-home
---

{{< hextra/hero-badge >}}
  <div class="hx:w-2 hx:h-2 hx:rounded-full hx:bg-primary-400"></div>
  <span>Gratuit, open source, AGPL-3.0</span>
{{< /hextra/hero-badge >}}

<div class="hx:mt-6 hx:mb-6">
{{< hextra/hero-headline >}}
  Relie les appels Signal&nbsp;<br class="hx:sm:block hx:hidden" />à votre propre PBX SIP
{{< /hextra/hero-headline >}}
</div>

<div class="hx:mb-12">
{{< hextra/hero-subtitle >}}
  Un démon natif qui relie les appels vocaux privés de Signal&nbsp;<br class="hx:sm:block hx:hidden" />à un système SIP/PBX standard - auto-hébergé de bout en bout
{{< /hextra/hero-subtitle >}}
</div>

<div class="hx:mb-6">
{{< hextra/hero-button text="Voir sur GitHub" link="https://github.com/signal2sip/signal2sip" >}}
</div>

<div class="hx:mt-6"></div>

{{< hextra/feature-grid >}}
  {{< hextra/feature-card
    title="Gardez votre PBX existant"
    link="/docs/keep-your-pbx"
    subtitle="Ajoutez Signal à Asterisk, FreePBX ou tout système SIP/PBX comme une ligne de plus - rien à remplacer."
    icon="phone"
  >}}
  {{< hextra/feature-card
    title="Joignable dans les deux sens"
    link="/docs/two-way-reachability"
    subtitle="Appelez un contact Signal depuis un poste SIP, ou recevez un appel Signal directement dans votre PBX."
    icon="switch-horizontal"
  >}}
  {{< hextra/feature-card
    title="Auto-hébergé de bout en bout"
    link="/docs/self-hosted"
    subtitle="Aucune passerelle tierce ne voit jamais vos appels ni vos clés."
    icon="shield-check"
  >}}
  {{< hextra/feature-card
    title="Chiffré partout"
    link="/docs/encryption"
    subtitle="TLS/SRTP côté SIP, en plus du chiffrement de bout en bout propre à Signal."
    icon="lock-closed"
  >}}
  {{< hextra/feature-card
    title="Multi-comptes"
    link="/docs/multi-account"
    subtitle="Un nombre quelconque de comptes Signal par démon, chacun configuré indépendamment, avec son propre trunk SIP si nécessaire."
    icon="users"
  >}}
  {{< hextra/feature-card
    title="Gestion en direct"
    link="/docs/live-management"
    subtitle="Interface terminal ou simple CLI - sans redémarrer le démon pour changer la configuration."
    icon="terminal"
  >}}
{{< /hextra/feature-grid >}}

{{< disclaimer >}}
