---
title: "signal2sip"
tagline: "Conecta las llamadas de Signal con tu propia infraestructura SIP/PBX."
---

## Qué es

signal2sip es un demonio nativo que conecta las llamadas de voz
privadas de [Signal](https://signal.org) con un sistema SIP/PBX
estándar. Un solo proceso atiende cualquier cantidad de cuentas de
Signal a la vez, cada una con su propio troncal SIP si es necesario -
todo impulsado por el protocolo real de Signal (mensajería y llamadas
RingRTC), con el audio puenteado a SIP a través de PJSIP.

## Por qué importa

- Sigue usando tu PBX existente (Asterisk, FreePBX, ...) añadiendo
  Signal como una línea más
- Llama a un contacto de Signal marcando una extensión, o recibe una
  llamada de Signal en una extensión SIP
- Autoalojado de principio a fin - ninguna pasarela de terceros ve
  jamás tus llamadas ni tus claves
- TLS/SRTP en el lado SIP, junto al propio cifrado de extremo a extremo
  de Signal

## Características

- Cualquier cantidad de cuentas de Signal por demonio, cada una
  configurada de forma independiente
- Registra un número nuevo de Signal, o vincúlalo como dispositivo
  secundario a uno existente
- Señalización SIP cifrada (TLS) y medios cifrados (SRTP)
- Administra las cuentas en vivo - mediante una interfaz de terminal o
  una CLI sencilla - sin reiniciar el demonio
- Gratuito y de código abierto, con licencia AGPL-3.0

## Empezar

Las instrucciones de compilación, la referencia de configuración y todo
lo demás están en el
[repositorio de GitHub](https://github.com/signal2sip/signal2sip).
