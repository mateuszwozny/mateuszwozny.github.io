# NMAP:  
Nmap to narzędzie służące do skanowania sieci i wykrywania usług, portów oraz systemów operacyjnych działających na zdalnych hostach.

```bash
nmap -sV -sS -p- -A <adres_IP>
```

 Opis przełączników:

🔹 -sV — Wykrywanie wersji usług
    Nmap próbuje połączyć się z otwartymi portami i ustalić, jaka aplikacja tam działa (np. Apache 2.4.57, OpenSSH 8.9).
    Bardzo przydatne w pentestach, bo pozwala szybko sprawdzić, czy dana wersja ma znane podatności.

🔹 -sS — SYN scan (półotwarty)
    Nmap wysyła pakiet SYN i czeka na odpowiedź:

   SYN/ACK → port otwarty
   RST → port zamknięty

   Nie wykonuje pełnego handshake TCP, więc:

    * jest szybszy
    * mniej widoczny w logach niż pełne połączenie (-sT)
    * najczęściej używany tryb skanowania portów.

🔹 -p- — Skanowanie wszystkich portów
    Oznacza: skanuj wszystkie porty od 1 do 65535.
    Domyślnie Nmap sprawdza tylko najpopularniejsze 1000 portów.

    -p- daje pełny obraz, ale trwa dłużej.

🔹 -A — Agresywny tryb skanowania
    Włącza kilka funkcji jednocześnie:

    -O → wykrywanie systemu operacyjnego

    -sV → wykrywanie wersji usług

    --script=default → uruchomienie podstawowych skryptów NSE

      traceroute → analiza ścieżki sieciowej

    Uwaga: Tryb bardzo informacyjny, ale głośny — łatwo zauważalny w logach IDS/IPS.

✅ Podsumowanie przełączników:

  -sV → wykrywanie wersji usług
  -sS → szybki i dyskretny SYN scan
  -p- → skan wszystkich portów
  -A → agresywny tryb (OS, wersje, skrypty, traceroute)




  
