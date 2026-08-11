---
title: signal2sip
layout: hextra-home
---

{{< hextra/hero-badge >}}
  <div class="hx:w-2 hx:h-2 hx:rounded-full hx:bg-primary-400"></div>
  <span>Gratuito, código aberto, AGPL-3.0</span>
{{< /hextra/hero-badge >}}

<div class="hx:mt-6 hx:mb-6">
{{< hextra/hero-headline >}}
  Conecta chamadas do Signal&nbsp;<br class="hx:sm:block hx:hidden" />ao seu próprio PABX SIP
{{< /hextra/hero-headline >}}
</div>

<div class="hx:mb-12">
{{< hextra/hero-subtitle >}}
  Um daemon nativo que conecta as chamadas de voz privadas do Signal&nbsp;<br class="hx:sm:block hx:hidden" />a um sistema SIP/PABX comum - self-hosted de ponta a ponta
{{< /hextra/hero-subtitle >}}
</div>

<div class="hx:mb-6">
{{< hextra/hero-button text="Ver no GitHub" link="https://github.com/signal2sip/signal2sip" >}}
</div>

<div class="hx:mt-6"></div>

{{< hextra/feature-grid >}}
  {{< hextra/feature-card
    title="Mantenha seu PABX atual"
    link="/docs/keep-your-pbx"
    subtitle="Adicione o Signal ao Asterisk, FreePBX ou qualquer sistema SIP/PABX como mais uma linha - não precisa substituir nada."
    icon="phone"
  >}}
  {{< hextra/feature-card
    title="Alcance nos dois sentidos"
    link="/docs/two-way-reachability"
    subtitle="Ligue para um contato do Signal a partir de um ramal SIP, ou receba uma chamada do Signal direto no seu PABX."
    icon="switch-horizontal"
  >}}
  {{< hextra/feature-card
    title="Self-hosted de ponta a ponta"
    link="/docs/self-hosted"
    subtitle="Nenhum gateway de terceiros jamais vê suas chamadas ou suas chaves."
    icon="shield-check"
  >}}
  {{< hextra/feature-card
    title="Criptografado em tudo"
    link="/docs/encryption"
    subtitle="TLS/SRTP no lado SIP, além da própria criptografia de ponta a ponta do Signal."
    icon="lock-closed"
  >}}
  {{< hextra/feature-card
    title="Múltiplas contas"
    link="/docs/multi-account"
    subtitle="Qualquer número de contas do Signal por daemon, cada uma configurada de forma independente, com seu próprio tronco SIP se necessário."
    icon="users"
  >}}
  {{< hextra/feature-card
    title="Gerenciamento ao vivo"
    link="/docs/live-management"
    subtitle="Interface de terminal ou CLI simples - sem reiniciar o daemon para mudar a configuração."
    icon="terminal"
  >}}
{{< /hextra/feature-grid >}}

{{< callout type="info" >}}
  🧪 **Status dos testes**: o signal2sip foi testado ao vivo em hardware PBX real, em várias configurações e cenários de chamada - mas ainda não passou por testes independentes em larga escala. Encontrou um bug, ou tudo funcionou bem? Feedback é bem-vindo - abra uma [issue ou PR](https://github.com/signal2sip/signal2sip) no GitHub, ou simplesmente nos envie um email.
{{< /callout >}}

{{< disclaimer >}}
