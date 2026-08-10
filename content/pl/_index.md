---
title: "signal2sip"
tagline: "Łączy połączenia Signal z Twoją własną infrastrukturą SIP/PBX."
---

## Czym to jest

signal2sip to natywny demon, który łączy prywatne połączenia głosowe
[Signal](https://signal.org) ze standardowym systemem SIP/PBX. Jeden
proces obsługuje dowolną liczbę kont Signal jednocześnie, każde
z własnym trunkiem SIP w razie potrzeby - w oparciu o prawdziwy protokół
Signal (przesyłanie wiadomości i połączenia RingRTC), z dźwiękiem
mostkowanym do SIP przez PJSIP.

## Dlaczego to ważne

- Korzystaj nadal ze swojej istniejącej centrali (Asterisk, FreePBX, ...),
  dodając do niej Signal jako kolejną linię
- Zadzwoń do kontaktu na Signalu, wybierając numer wewnętrzny, lub odbierz
  połączenie z Signala na numerze SIP
- W pełni self-hosted - żadna zewnętrzna bramka nigdy nie widzi Twoich
  połączeń ani kluczy
- TLS/SRTP po stronie SIP, obok własnego szyfrowania end-to-end Signala

## Funkcje

- Dowolna liczba kont Signal na jeden demon, każde konfigurowane
  niezależnie
- Rejestracja nowego numeru Signal lub powiązanie jako urządzenie
  dodatkowe do istniejącego
- Szyfrowana sygnalizacja SIP (TLS) i media (SRTP)
- Zarządzanie kontami na żywo - przez interfejs terminalowy lub zwykłe
  CLI - bez restartu demona
- Darmowe i open source, licencja AGPL-3.0

## Zaczynamy

Instrukcje budowania, konfiguracja i reszta dokumentacji znajdują się w
[repozytorium na GitHub](https://github.com/signal2sip/signal2sip).
