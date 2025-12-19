# TryHackMe „TakeOver”

## 1. Informacje ogólne
- **Cel testów:**  
 Pokój Takeover na TryHackMe uczy, jak wykrywać i wykorzystywać podatność subdomain takeover, czyli przejmowanie subdomen wskazujących na nieistniejące zasoby. W praktyce pokazuje, jak błędna konfiguracja DNS pozwala atakującemu utworzyć własny zasób i przejąć kontrolę nad daną subdomeną.  
 

---

## 2. Metodologia 
- **Narzędzia:** Nmap, Gobuster, podstawowe polecenia Linuksa.  

---


## 3. Szczegóły podatności
- **Opis:**
  Gobuster ujawnił otwarty port HTTP. Analiza strony wskazała ukryte dane logowania w kodzie źródłowym (`R1ckRul3s`).

   
- **nmap:**  
  ```bash
  nmap -sV -sS -p- -A

- **gobuster:**  
  ```bash
  gobuster vhost -o subdom2 -k --append-domain -u futurevera.thm -w /usr/share/seclists/Discovery/Web-Content/common.txt 
  ```
  odkryte subdomeny dopisujemy do pliku /etc/hosts
  /etc/hosts pozwala komputerowi „na skróty” przypisać nazwę strony do konkretnego adresu IP — bez pytania DNS.
  Plik /etc/hosts służy do ręcznego mapowania nazw domen na adresy IP, zanim system zapyta o to DNS.

  Możesz tam wpisać np.: 10.10.10.10 example.thm i system zawsze będzie kierował ruch na ten IP, nawet jeśli DNS mówi coś innego.
---

- **komendy Linux:**
   - cat , less, ls -la , sudo , cd

  

