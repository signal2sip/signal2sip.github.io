---
title: "signal2sip"
tagline: "Collega le chiamate Signal alla tua infrastruttura SIP/PBX."
---

## Cos'è

signal2sip è un demone nativo che collega le chiamate vocali private di
[Signal](https://signal.org) a un normale sistema SIP/PBX. Un unico
processo serve un numero qualsiasi di account Signal contemporaneamente,
ciascuno con il proprio trunk SIP se necessario - il tutto basato sul
vero protocollo Signal (messaggistica e chiamate RingRTC), con l'audio
instradato verso il SIP tramite PJSIP.

## Perché è utile

- Continua a usare il tuo PBX esistente (Asterisk, FreePBX, ...)
  aggiungendo Signal come un'altra linea
- Chiama un contatto Signal componendo un interno, oppure ricevi una
  chiamata Signal su un interno SIP
- Completamente self-hosted - nessun gateway di terze parti vede mai le
  tue chiamate o le tue chiavi
- TLS/SRTP sul lato SIP, insieme alla cifratura end-to-end propria di
  Signal

## Funzionalità

- Un numero qualsiasi di account Signal per demone, ciascuno configurato
  in modo indipendente
- Registra un nuovo numero Signal, oppure collega come dispositivo
  secondario a uno esistente
- Segnalazione SIP cifrata (TLS) e media cifrati (SRTP)
- Gestisci gli account dal vivo - tramite un'interfaccia a terminale o
  una semplice CLI - senza riavviare il demone
- Gratuito e open source, con licenza AGPL-3.0

## Per iniziare

Le istruzioni di compilazione, il riferimento di configurazione e tutto
il resto si trovano nel
[repository GitHub](https://github.com/signal2sip/signal2sip).
