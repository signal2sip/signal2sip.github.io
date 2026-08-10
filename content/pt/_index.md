---
title: "signal2sip"
tagline: "Conecta chamadas do Signal à sua própria infraestrutura SIP/PABX."
---

## O que é

signal2sip é um daemon nativo que conecta as chamadas de voz privadas
do [Signal](https://signal.org) a um sistema SIP/PABX comum. Um único
processo atende qualquer número de contas do Signal ao mesmo tempo,
cada uma com seu próprio tronco SIP se necessário - tudo baseado no
protocolo real do Signal (mensagens e chamadas RingRTC), com o áudio
sendo ponteado para o SIP através do PJSIP.

## Por que isso importa

- Continue usando seu PABX existente (Asterisk, FreePBX, ...)
  adicionando o Signal como mais uma linha
- Ligue para um contato do Signal discando um ramal, ou receba uma
  chamada do Signal em um ramal SIP
- Totalmente self-hosted - nenhum gateway de terceiros jamais vê suas
  chamadas ou suas chaves
- TLS/SRTP no lado SIP, além da própria criptografia de ponta a ponta
  do Signal

## Recursos

- Qualquer número de contas do Signal por daemon, cada uma configurada
  de forma independente
- Registre um novo número do Signal, ou vincule como dispositivo
  secundário a um já existente
- Sinalização SIP criptografada (TLS) e mídia criptografada (SRTP)
- Gerencie as contas ao vivo - por uma interface de terminal ou uma CLI
  simples - sem reiniciar o daemon
- Gratuito e de código aberto, licenciado sob AGPL-3.0

## Como começar

As instruções de compilação, a referência de configuração e todo o
resto estão no
[repositório do GitHub](https://github.com/signal2sip/signal2sip).
