# TryHackMe „LookUP”

## 1. Informacje ogólne
- **Cel testów:** Odkrycie i wykorzystanie ukrytych usług oraz podatności webowych, aby przećwiczyć rekonesans, enumerację i techniki eskalacji uprawnień w realistycznym środowisku..  
- **Zakres:** Maszyna CTF „LookUP” (adres IP przydzielony przez TryHackMe).  

---

## 2. Metodologia 
- **Narzędzia:** Nmap, Gobuster, BurpSuite, podstawowe polecenia Linuksa.  

---


## 3. Szczegóły podatności
- **Opis:** Nmap ujawnił otwarty port HTTP. Analiza strony wskazała ukryte dane logowania w kodzie źródłowym .

   
- **nmap:**  
  ```html
  nmap -sV -sS -p- -A

- **gobuster:**  
  ```html
  gobuster dir -u 10.82.166.29 -w /usr/share/dirb/wordlists/common.txt

- **dirbuster:** - narzędzie GUI
- **komendy Linux:**
   - cat , less, ls -la , sudo , cd

  

