---
title: signal2sip
layout: hextra-home
---

{{< hextra/hero-badge >}}
  <div class="hx:w-2 hx:h-2 hx:rounded-full hx:bg-primary-400"></div>
  <span>Darmowe, open source, AGPL-3.0</span>
{{< /hextra/hero-badge >}}

<div class="hx:mt-6 hx:mb-6">
{{< hextra/hero-headline >}}
  Łączy połączenia Signal&nbsp;<br class="hx:sm:block hx:hidden" />z Twoją centralą SIP/PBX
{{< /hextra/hero-headline >}}
</div>

<div class="hx:mb-12">
{{< hextra/hero-subtitle >}}
  Natywny demon łączący prywatne połączenia głosowe Signal&nbsp;<br class="hx:sm:block hx:hidden" />ze standardowym systemem SIP/PBX - w pełni self-hosted
{{< /hextra/hero-subtitle >}}
</div>

<div class="hx:mb-6">
{{< hextra/hero-button text="Zobacz na GitHub" link="https://github.com/signal2sip/signal2sip" >}}
</div>

<div class="hx:mt-6"></div>

{{< hextra/feature-grid >}}
  {{< hextra/feature-card
    title="Zachowaj swoją centralę"
    link="/docs/keep-your-pbx"
    subtitle="Dodaj Signal do Asterisk, FreePBX lub dowolnego systemu SIP/PBX jako kolejną linię - niczego nie trzeba wymieniać."
    icon="phone"
  >}}
  {{< hextra/feature-card
    title="Łączność dwukierunkowa"
    link="/docs/two-way-reachability"
    subtitle="Zadzwoń do kontaktu na Signalu z numeru wewnętrznego SIP, albo odbierz połączenie z Signala wprost w swojej centrali."
    icon="switch-horizontal"
  >}}
  {{< hextra/feature-card
    title="W pełni self-hosted"
    link="/docs/self-hosted"
    subtitle="Żadna zewnętrzna bramka nigdy nie widzi Twoich połączeń ani kluczy."
    icon="shield-check"
  >}}
  {{< hextra/feature-card
    title="Szyfrowanie wszędzie"
    link="/docs/encryption"
    subtitle="TLS/SRTP po stronie SIP, obok własnego szyfrowania end-to-end Signala."
    icon="lock-closed"
  >}}
  {{< hextra/feature-card
    title="Wiele kont"
    link="/docs/multi-account"
    subtitle="Dowolna liczba kont Signal na jeden demon, każde konfigurowane niezależnie, z własnym trunkiem SIP w razie potrzeby."
    icon="users"
  >}}
  {{< hextra/feature-card
    title="Zarządzanie na żywo"
    link="/docs/live-management"
    subtitle="Interfejs terminalowy lub zwykłe CLI - bez restartu demona przy zmianie konfiguracji."
    icon="terminal"
  >}}
{{< /hextra/feature-grid >}}

{{< callout type="info" >}}
  🧪 **Status testów**: signal2sip był testowany na żywo na prawdziwym sprzęcie PBX, w kilku konfiguracjach i scenariuszach połączeń - ale nie przeszedł jeszcze szerokich, niezależnych testów. Znalazłeś błąd, czy wszystko zadziałało dobrze? Opinie są mile widziane - otwórz [issue lub PR](https://github.com/signal2sip/signal2sip) na GitHubie, albo po prostu napisz do nas e-mail.
{{< /callout >}}

{{< disclaimer >}}
