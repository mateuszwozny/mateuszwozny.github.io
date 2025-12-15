# Raport z testów penetracyjnych – TryHackMe „Pickle Rick”

## 1. Informacje ogólne
- **Cel testów:** Eksploracja podatnej aplikacji webowej w celu uzyskania dostępu do systemu i odnalezienia trzech sekretów Ricka.  
- **Zakres:** Maszyna CTF „Pickle Rick” (adres IP przydzielony przez TryHackMe).  

---

## 2. Metodologia 
- **Narzędzia:** Nmap, Gobuster, podstawowe polecenia Linuksa.  

---


## 3. Szczegóły podatności
- **Opis:** Nmap ujawnił otwarty port HTTP. Analiza strony wskazała ukryte dane logowania w kodzie źródłowym (`R1ckRul3s`).

   
- **nmap:**  
  ```html
  nmap -sV -sS -p- -A

- **gobuster:**  
  ```html
  gobuster dir -u 10.82.166.29 -w /usr/share/dirb/wordlists/common.txt

- **dirbuster:** - narzędzie GUI
- **komendy Linux:**
   - cat , less, ls -la , sudo 

  
