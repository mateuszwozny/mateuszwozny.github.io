
# TryHackMe „Agent Sudo”

## 1. Informacje ogólne
- **Cel testów:** Maszyna, która uczy analizowania uprawnień i wykorzystywania błędnych konfiguracji sudo.  
                  Zadanie prowadzi krok po kroku do zrozumienia, jak niewielkie misconfigi mogą otworzyć drogę do eskalacji uprawnień.    

---

## 2. Metodologia 
 **Narzędzia:** Nmap, burpsuit , wtyczka ff user-agent switcher , steghide , binwalk , zpi2john , john , strona tineye

## 3. Podsumowanie zadania
  **Skanowanie wstępne:**
  
Na początku wykonano skanowanie usług, aby ustalić otwarte porty, wersje usług i potencjalne punkty wejścia.  

Użyte narzędzie:  

 ***nmap:*** 

```bash
sudo nmap -sV -sC -sS 10.80.148.214
``` 

**Analiza aplikacji webowej**  

  W aplikacji webowej zauważono zależność od nagłówka User-Agent.   
  Zmiana jego wartości wpływała na odpowiedzi serwera.

Użyte narzędzia:

***-BurpSuite (Intercept + Repeater)***  

***-User-Agent Switcher (plugin)***  

***Przykład payloadu:***  

Zmiana liter A–Z w nagłówku User-Agent, aby obserwować zmiany w URL.  
Efektem było ujawnienie nazwy użytkownika: chris.

***Dostęp do FTP***  

Po ustaleniu nazwy użytkownika wykonano próbę odnalezienia hasła przy użyciu słownika.

***Narzędzie:***  

***hydra:***

```bash
hydra -l chris -P /usr/share/wordlists/rockyou.txt -u ftp://10.80.178.187
```
Po uzyskaniu dostępu pobrano pliki:

```bash
get plik.txt
get foto1.jpg
get foto2.jpg
```
**Analiza plików graficznych:**  

Pliki graficzne sprawdzono pod kątem ukrytych danych.  

***Narzędzia i komendy:***  

```bash
strings foto.jpg
binwalk foto.jpg
binwalk -e foto.jpg
exiftool foto.jpg
steghide extract -sf foto.jpg
```
Wskazówki z pliku tekstowego sugerowały obecność ukrytych danych oraz dodatkowego archiwum ZIP.  

**Analiza archiwum ZIP:**
Archiwum wymagało hasła, więc skonwertowano je do formatu hash i porównano ze słownikiem.  

***Narzędzia i komendy:***

```bash
zip2john 8702.zip > 8702.txt
john --wordlist=/usr/share/wordlists/rockyou.txt 8702.txt
```
W przypadku problemów z unzip użyto alternatywy:  

```bash
7z x 8702.zip 
```

**Dalsza analiza ukrytych danych:**  
Znaleziony ciąg zakodowany w base64 zdekodowano:

```bash
echo qweadad | base64 -d
```
Dodatkowe dane wyodrębniono z kolejnego obrazu:

```bash
steghide extract -sf cute-alien.jpg
```

***Przesyłanie plików z maszyny zdalnej:***
Do pobrania plików z maszyny zdalnej na lokalną użyto bezpiecznego transferu.  

```bash
scp użytkownik@IP:/ścieżka/do/pliku.jpg .
```
Kropka oznacza zapis w bieżącym katalogu.   

Jeśli SSH działa na innym porcie:   

```bash
scp -P 2222 area51@10.80.178.187:/home/area51/test.jpg .
```

**Weryfikacja obrazów**
Do sprawdzenia pochodzenia obrazów użyto wyszukiwarki odwrotnej:  

Narzędzie: https://tineye.com/  

**Analiza uprawnień i eskalacja**

Sprawdzono konfigurację uprawnień:  

```bash
sudo -l
```
Zauważono możliwość wykorzystania znanego błędu konfiguracyjnego:  

CVE‑2019‑14287 Mechanizm błędnej interpretacji identyfikatora użytkownika.  
