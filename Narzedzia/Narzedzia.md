# Zbiór wszystkich narzędzi

- **Nmap:**

## Polecenie
```bash
nmap -sV -sS -p- -A <adres_IP>

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
```
---
- **gobuster:**  
  ```bash
  gobuster dir -u 10.82.166.29 -w /usr/share/dirb/wordlists/common.txt
  ```
  ```bash
  gobuster vhost -k --append-domain -u 10.82.180.25 -w /usr/share/seclists/Discovery/Web-Content/common.txt
  ```
---
- **SMB:**
  Sprawdzenie czy SMB pozwala na dostęp anonimowy
     ```bash
  smbclient -L //IP -N
-L - lista udziałów
-N - bez hasła (tryb anonymous)
  ```bash
    smbclient //IP/Anonymous -N
    smb: \>
    smb: \> get plik.txt
  ```
---
- **hydra:**
    ```bash
  hydra -l jan -P -u /usr/share/wordlists/rockyou.txt ssh://IP -V (bez -V nie widać postępu skanowania haseł)
   ```
---
- **ssh:**
    ```bash
  ssh jan@IP
   ```
  ```bash
  ssh -i id(nazwa klucza) kay@IP
   ```
  ---
- **john:**
  ```bash
  ssh2john id > hash.txt
   ``` 
   John musi mieć zawartość jako hash i dlatego zamieniamy zwykły tekst na hash

  ```bash
  john hash.txt --wordlist=/usr/share/wordlists/rockyou.txt
  ```
  ---
  - **ffuz** - (Fast web Fuzzer) to narzędzie do szybkiego fuzzingu stron WWW, używane do wykrywania ukrytych katalogów, plików, parametrów i subdomen
  ```bash
  ffuf -u http://futurevera.thm -w /usr/share/wordlists/amass/subdomains-top1mil-110000.txt -H "Host: FUZZ.futurevera.thm"  
  ```
