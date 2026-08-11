---
title: signal2sip
layout: hextra-home
---

{{< hextra/hero-badge >}}
  <div class="hx:w-2 hx:h-2 hx:rounded-full hx:bg-primary-400"></div>
  <span>Бесплатный, с открытым кодом, AGPL-3.0</span>
{{< /hextra/hero-badge >}}

<div class="hx:mt-6 hx:mb-6">
{{< hextra/hero-headline >}}
  Связывает звонки Signal&nbsp;<br class="hx:sm:block hx:hidden" />с вашей SIP/АТС
{{< /hextra/hero-headline >}}
</div>

<div class="hx:mb-12">
{{< hextra/hero-subtitle >}}
  Нативный демон, соединяющий приватные голосовые звонки Signal&nbsp;<br class="hx:sm:block hx:hidden" />с обычной SIP/АТС-системой - полностью self-hosted
{{< /hextra/hero-subtitle >}}
</div>

<div class="hx:mb-6">
{{< hextra/hero-button text="Смотреть на GitHub" link="https://github.com/signal2sip/signal2sip" >}}
</div>

<div class="hx:mt-6"></div>

{{< hextra/feature-grid >}}
  {{< hextra/feature-card
    title="Оставьте свою АТС"
    link="/docs/keep-your-pbx"
    subtitle="Добавьте Signal в Asterisk, FreePBX или любую SIP/АТС как ещё одну линию - ничего заменять не нужно."
    icon="phone"
  >}}
  {{< hextra/feature-card
    title="Двусторонняя связь"
    link="/docs/two-way-reachability"
    subtitle="Звоните контакту в Signal с SIP-экстеншна, или принимайте звонок из Signal прямо в вашей АТС."
    icon="switch-horizontal"
  >}}
  {{< hextra/feature-card
    title="Self-hosted насквозь"
    link="/docs/self-hosted"
    subtitle="Ни один сторонний шлюз никогда не видит ваши звонки или ключи."
    icon="shield-check"
  >}}
  {{< hextra/feature-card
    title="Шифрование везде"
    link="/docs/encryption"
    subtitle="TLS/SRTP на SIP-плече, наряду со сквозным шифрованием самого Signal."
    icon="lock-closed"
  >}}
  {{< hextra/feature-card
    title="Много аккаунтов"
    link="/docs/multi-account"
    subtitle="Любое количество аккаунтов Signal на один демон, каждый настраивается независимо, с собственным SIP-транком при необходимости."
    icon="users"
  >}}
  {{< hextra/feature-card
    title="Управление вживую"
    link="/docs/live-management"
    subtitle="Терминальный интерфейс или обычный CLI - без перезапуска демона для изменения конфигурации."
    icon="terminal"
  >}}
{{< /hextra/feature-grid >}}

{{< disclaimer >}}
