---
title: "signal2sip"
tagline: "Verbindet Signal-Anrufe mit Ihrer eigenen SIP/TK-Anlage."
---

## Was es ist

signal2sip ist ein nativer Daemon, der die private Sprachtelefonie von
[Signal](https://signal.org) mit einer gewöhnlichen SIP/TK-Anlage
verbindet. Ein Prozess bedient beliebig viele Signal-Konten gleichzeitig,
jedes bei Bedarf mit eigenem SIP-Trunk - vollständig auf Basis des echten
Signal-Protokolls (Messaging und RingRTC-Anrufe), mit Audio, das über
PJSIP zu SIP gebrückt wird.

## Warum das wichtig ist

- Nutzen Sie weiterhin Ihre bestehende TK-Anlage (Asterisk, FreePBX, ...)
  und fügen Sie Signal einfach als weitere Leitung hinzu
- Erreichen Sie einen Signal-Kontakt, indem Sie eine Nebenstelle wählen,
  oder nehmen Sie einen Signal-Anruf auf einer SIP-Nebenstelle entgegen
- Durchgehend selbst gehostet - kein Drittanbieter-Gateway sieht jemals
  Ihre Anrufe oder Schlüssel
- TLS/SRTP auf der SIP-Seite, zusätzlich zur eigenen Ende-zu-Ende-
  Verschlüsselung von Signal

## Funktionen

- Beliebig viele Signal-Konten pro Daemon, jedes unabhängig konfigurierbar
- Neue Signal-Nummer registrieren oder als Zweitgerät mit einer
  bestehenden verknüpfen
- Verschlüsselte SIP-Signalisierung (TLS) und Medien (SRTP)
- Konten live verwalten - über eine Terminal-Oberfläche oder eine
  einfache CLI - ohne Neustart des Daemons
- Kostenlos und quelloffen, lizenziert unter AGPL-3.0

## Loslegen

Bauanleitung, Konfigurationsreferenz und alles andere finden Sie im
[GitHub-Repository](https://github.com/signal2sip/signal2sip).
