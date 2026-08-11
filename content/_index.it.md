---
title: signal2sip
layout: hextra-home
---

{{< hextra/hero-badge >}}
  <div class="hx:w-2 hx:h-2 hx:rounded-full hx:bg-primary-400"></div>
  <span>Gratuito, open source, AGPL-3.0</span>
{{< /hextra/hero-badge >}}

<div class="hx:mt-6 hx:mb-6">
{{< hextra/hero-headline >}}
  Collega le chiamate Signal&nbsp;<br class="hx:sm:block hx:hidden" />al tuo PBX SIP
{{< /hextra/hero-headline >}}
</div>

<div class="hx:mb-12">
{{< hextra/hero-subtitle >}}
  Un demone nativo che collega le chiamate vocali private di Signal&nbsp;<br class="hx:sm:block hx:hidden" />a un normale sistema SIP/PBX - completamente self-hosted
{{< /hextra/hero-subtitle >}}
</div>

<div class="hx:mb-6">
{{< hextra/hero-button text="Vedi su GitHub" link="https://github.com/signal2sip/signal2sip" >}}
</div>

<div class="hx:mt-6"></div>

{{< hextra/feature-grid >}}
  {{< hextra/feature-card
    title="Tieni il tuo PBX esistente"
    link="/docs/keep-your-pbx"
    subtitle="Aggiungi Signal ad Asterisk, FreePBX o qualsiasi sistema SIP/PBX come un'altra linea - non serve sostituire nulla."
    icon="phone"
  >}}
  {{< hextra/feature-card
    title="Raggiungibilità bidirezionale"
    link="/docs/two-way-reachability"
    subtitle="Chiama un contatto Signal componendo un interno SIP, oppure ricevi una chiamata Signal direttamente nel tuo PBX."
    icon="switch-horizontal"
  >}}
  {{< hextra/feature-card
    title="Self-hosted end-to-end"
    link="/docs/self-hosted"
    subtitle="Nessun gateway di terze parti vede mai le tue chiamate o le tue chiavi."
    icon="shield-check"
  >}}
  {{< hextra/feature-card
    title="Cifratura ovunque"
    link="/docs/encryption"
    subtitle="TLS/SRTP sul lato SIP, insieme alla cifratura end-to-end propria di Signal."
    icon="lock-closed"
  >}}
  {{< hextra/feature-card
    title="Multi-account"
    link="/docs/multi-account"
    subtitle="Un numero qualsiasi di account Signal per demone, ciascuno configurato in modo indipendente, con il proprio trunk SIP se necessario."
    icon="users"
  >}}
  {{< hextra/feature-card
    title="Gestione dal vivo"
    link="/docs/live-management"
    subtitle="Interfaccia a terminale o semplice CLI - senza riavviare il demone per cambiare configurazione."
    icon="terminal"
  >}}
{{< /hextra/feature-grid >}}

{{< callout type="info" >}}
  🧪 **Stato dei test**: signal2sip è stato testato dal vivo su hardware PBX reale, in diverse configurazioni e scenari di chiamata - ma non ha ancora ricevuto test indipendenti su larga scala. Avete trovato un bug, o tutto ha funzionato bene? Il feedback è benvenuto - aprite una [issue o una PR](https://github.com/signal2sip/signal2sip) su GitHub, oppure scriveteci semplicemente via email.
{{< /callout >}}

{{< disclaimer >}}
