---
title: "signal2sip"
tagline: "Relie les appels Signal à votre propre infrastructure SIP/PBX."
---

## Qu'est-ce que c'est

signal2sip est un démon natif qui relie les appels vocaux privés de
[Signal](https://signal.org) à un système SIP/PBX standard. Un seul
processus dessert un nombre quelconque de comptes Signal à la fois,
chacun avec son propre trunk SIP si nécessaire - le tout piloté par le
vrai protocole Signal (messagerie et appels RingRTC), avec l'audio
relayé vers le SIP via PJSIP.

## Pourquoi c'est utile

- Continuez à utiliser votre PBX existant (Asterisk, FreePBX, ...) en y
  ajoutant Signal comme une ligne supplémentaire
- Joignez un contact Signal en composant un poste, ou recevez un appel
  Signal sur un poste SIP
- Auto-hébergé de bout en bout - aucune passerelle tierce ne voit jamais
  vos appels ni vos clés
- TLS/SRTP côté SIP, en plus du chiffrement de bout en bout propre à
  Signal

## Fonctionnalités

- Un nombre quelconque de comptes Signal par démon, chacun configuré
  indépendamment
- Enregistrez un nouveau numéro Signal, ou liez l'appareil comme
  appareil secondaire à un numéro existant
- Signalisation SIP chiffrée (TLS) et média chiffré (SRTP)
- Gérez les comptes en direct - via une interface terminal ou une simple
  CLI - sans redémarrer le démon
- Gratuit et open source, sous licence AGPL-3.0

## Pour commencer

Les instructions de compilation, la référence de configuration et tout
le reste se trouvent dans le
[dépôt GitHub](https://github.com/signal2sip/signal2sip).
