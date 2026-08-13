---
title: signal2sip
layout: hextra-home
---

{{< hextra/hero-badge >}}
  <div class="hx:w-2 hx:h-2 hx:rounded-full hx:bg-primary-400"></div>
  <span>Gratuito, de código abierto, AGPL-3.0</span>
{{< /hextra/hero-badge >}}

<div class="hx:mt-6 hx:mb-6">
{{< hextra/hero-headline >}}
  Conecta las llamadas del mensajero Signal&nbsp;<br class="hx:sm:block hx:hidden" />con tu propio PBX SIP
{{< /hextra/hero-headline >}}
</div>

<div class="hx:mb-12">
{{< hextra/hero-subtitle >}}
  Un demonio nativo que conecta las llamadas de voz privadas de Signal&nbsp;<br class="hx:sm:block hx:hidden" />con un sistema SIP/PBX estándar - autoalojado de principio a fin
{{< /hextra/hero-subtitle >}}
</div>

<div class="hx:mb-6">
{{< hextra/hero-button text="Ver en GitHub" link="https://github.com/signal2sip/signal2sip" >}}
</div>

<div class="hx:mt-6"></div>

{{< hextra/feature-grid >}}
  {{< hextra/feature-card
    title="Conserva tu PBX actual"
    link="/docs/keep-your-pbx"
    subtitle="Añade Signal a Asterisk, FreePBX o cualquier sistema SIP/PBX como una línea más - no hace falta reemplazar nada."
    icon="phone"
  >}}
  {{< hextra/feature-card
    title="Alcance en ambos sentidos"
    link="/docs/two-way-reachability"
    subtitle="Llama a un contacto de Signal desde una extensión SIP, o recibe una llamada de Signal directamente en tu PBX."
    icon="switch-horizontal"
  >}}
  {{< hextra/feature-card
    title="Autoalojado de principio a fin"
    link="/docs/self-hosted"
    subtitle="Ninguna pasarela de terceros ve jamás tus llamadas ni tus claves."
    icon="shield-check"
  >}}
  {{< hextra/feature-card
    title="Cifrado en todas partes"
    link="/docs/encryption"
    subtitle="TLS/SRTP en el lado SIP, junto al propio cifrado de extremo a extremo de Signal."
    icon="lock-closed"
  >}}
  {{< hextra/feature-card
    title="Multi-cuenta"
    link="/docs/multi-account"
    subtitle="Cualquier cantidad de cuentas de Signal por demonio, cada una configurada de forma independiente, con su propio troncal SIP si es necesario."
    icon="users"
  >}}
  {{< hextra/feature-card
    title="Gestión en vivo"
    link="/docs/live-management"
    subtitle="Interfaz de terminal o CLI sencilla - sin reiniciar el demonio para cambiar la configuración."
    icon="terminal"
  >}}
{{< /hextra/feature-grid >}}

{{< callout type="info" >}}
  🧪 **Estado de las pruebas**: signal2sip se ha probado en vivo con hardware PBX real, en varias configuraciones y escenarios de llamada - pero aún no ha recibido pruebas independientes a gran escala. ¿Encontraste un error, o todo funcionó bien? Los comentarios son bienvenidos - abre un [issue o PR](https://github.com/signal2sip/signal2sip) en GitHub, o simplemente escríbenos por correo.
{{< /callout >}}

{{< disclaimer >}}
