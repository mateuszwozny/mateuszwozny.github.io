# Brooklyn Nine Nine

## 1. Opis:

Wpisujemy ip w url i dosajemy strone ze djęciem , badamy źródło strony i dostajemy podpowiedz o wykorzystaniu scenanografii.  

Pobieramy fotkę na dysk i badamy narzędziami :
- strings
- binwalk
- exiftool

Nic nie znajdujemy.  
Po przeprowadzenie skanu nmap dostajemy info ,że otwarty jest port ftp i ssh.  
Do ftp można się zalogowac przez konto anonymous.  
Ściagamy plik txt z wiadomością z adresatem jake – login do ssh2john.  
Wykorzystujemy hydre.   

```bash
hydra -l jake -P /usr/share/wordlists/rockyou.txt ssh://10.67.148.139    - zmienić w gitlubie
```
Dostajemy hasło   
Logujemy się do ssh

Sprawdzamy zawartośc 
Sprawdzamy co user może uruchomić jako root

```bash
sudo -l
```

(ALL) NOPASSWD: /usr/bin/less


Wpisujemy np. sudo less /etc/profile i dostajemy root

Mamy możliwość odczytania flagi.
