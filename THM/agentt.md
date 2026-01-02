
# TryHackMe „Agent T”

## 1. Informacje ogólne
- **Cel testów:** Maszyna, która uczy analizowania uprawnień i wykorzystywania błędnych konfiguracji sudo.  
                  Zadanie prowadzi krok po kroku do zrozumienia, jak niewielkie misconfigi mogą otworzyć drogę do eskalacji uprawnień.    

---

## 2. Metodologia 
 **Narzędzia:** devtools, exploitdatabase.com
 
## 3. Podsumowanie zadania
  **Skanowanie wstępne:**
  
Przegladając stronę napotykamy na nagłówek w response : X-Powered-By: PHP/8.1.0-dev  

Oznacza to, że serwer w odpowiedzi HTTP ujawnia jaką technologią został wygenerowany dany zasób — w tym przypadku:  

X-Powered-By: PHP/8.1.0-dev  
To nagłówek HTTP, który informuje, że strona działa na PHP w wersji 8.1.0-dev (czyli wersji rozwojowej, nieprodukcyjnej).

### Co to dokładnie znaczy?  
  • X-Powered-By to niestandardowy nagłówek, który ujawnia technologię backendu (np. PHP, Express, ASP.NET).
  • Wartość PHP/8.1.0-dev mówi, że serwer używa wersji developerskiej PHP, co może oznaczać:
      ◦ środowisko testowe,
      ◦ potencjalnie większą podatność na błędy,
      ◦ niezalecaną konfigurację dla produkcji.
      
Na stronie exploit database znajdujemy podatność RCE dla php 

Pobieramy poleceniem wget

Odpalamy
```bash
python3 49933
``` 
Jesteśmy root,

```bash
ls -la /
```
dostajemy flag.txt

```bash
cat /flag.txt
```
