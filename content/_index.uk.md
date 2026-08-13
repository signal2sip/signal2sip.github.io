---
title: signal2sip
layout: hextra-home
---

{{< hextra/hero-badge >}}
  <div class="hx:w-2 hx:h-2 hx:rounded-full hx:bg-primary-400"></div>
  <span>Безкоштовний, з відкритим кодом, AGPL-3.0</span>
{{< /hextra/hero-badge >}}

<div class="hx:mt-6 hx:mb-6">
{{< hextra/hero-headline >}}
  Зв'язує дзвінки месенджера Signal&nbsp;<br class="hx:sm:block hx:hidden" />з вашою SIP/АТС
{{< /hextra/hero-headline >}}
</div>

<div class="hx:mb-12">
{{< hextra/hero-subtitle >}}
  Нативний демон, що з'єднує приватні голосові дзвінки Signal&nbsp;<br class="hx:sm:block hx:hidden" />зі звичайною SIP/АТС-системою - повністю self-hosted
{{< /hextra/hero-subtitle >}}
</div>

<div class="hx:mb-6">
{{< hextra/hero-button text="Дивитись на GitHub" link="https://github.com/signal2sip/signal2sip" >}}
</div>

<div class="hx:mt-6"></div>

{{< hextra/feature-grid >}}
  {{< hextra/feature-card
    title="Залиште свою АТС"
    link="/docs/keep-your-pbx"
    subtitle="Додайте Signal до Asterisk, FreePBX чи будь-якої SIP/АТС як ще одну лінію - нічого замінювати не треба."
    icon="phone"
  >}}
  {{< hextra/feature-card
    title="Двосторонній зв'язок"
    link="/docs/two-way-reachability"
    subtitle="Дзвоніть контакту в Signal із SIP-екстеншна, або приймайте дзвінок із Signal прямо у вашій АТС."
    icon="switch-horizontal"
  >}}
  {{< hextra/feature-card
    title="Self-hosted наскрізь"
    link="/docs/self-hosted"
    subtitle="Жоден сторонній шлюз ніколи не бачить ваші дзвінки чи ключі."
    icon="shield-check"
  >}}
  {{< hextra/feature-card
    title="Шифрування всюди"
    link="/docs/encryption"
    subtitle="TLS/SRTP на SIP-плечі, поруч із наскрізним шифруванням самого Signal."
    icon="lock-closed"
  >}}
  {{< hextra/feature-card
    title="Багато акаунтів"
    link="/docs/multi-account"
    subtitle="Будь-яка кількість акаунтів Signal на один демон, кожен налаштовується окремо, з власним SIP-транком за потреби."
    icon="users"
  >}}
  {{< hextra/feature-card
    title="Керування наживо"
    link="/docs/live-management"
    subtitle="Термінальний інтерфейс або звичайний CLI - без перезапуску демона для зміни конфігурації."
    icon="terminal"
  >}}
{{< /hextra/feature-grid >}}

{{< callout type="info" >}}
  🧪 **Стан тестування**: signal2sip перевірявся наживо на реальному АТС-обладнанні, у кількох конфігураціях і сценаріях дзвінків - але ще не пройшов широкого, незалежного тестування. Знайшли баг, чи все спрацювало добре? Зворотний зв'язок вітається - відкрийте [issue чи PR](https://github.com/signal2sip/signal2sip) на GitHub, або просто напишіть нам на пошту.
{{< /callout >}}

{{< disclaimer >}}
