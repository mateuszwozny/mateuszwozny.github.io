# Gobuster :

***Gobuster:***  
 to szybkie narzędzie do enumeracji, które pozwala sprawdzać ukryte katalogi,   
 pliki i subdomeny na serwerach WWW przy użyciu wordlist.  
 Jest proste w użyciu i świetnie sprawdza się w początkowej fazie rekonesansu,  
 gdy chcemy szybko odkryć zasoby, których nie widać na pierwszy rzut oka.  
 
 
  ```bash
  gobuster dir -u 10.82.166.29 -w /usr/share/dirb/wordlists/common.txt
  ```
## Przełączniki:
dir — tryb skanowania katalogów i plików na serwerze WWW  
-u — adres URL, który ma zostać przeskanowany  
-w — ścieżka do wordlisty używanej do brute‑force katalogów

---

  ```bash
  gobuster vhost -k --append-domain -u 10.82.180.25 -w /usr/share/seclists/Discovery/Web-Content/common.txt
  ```
## Przełączniki:  
vhost — tryb skanowania wirtualnych hostów (Virtual Hosts)  
-k — ignorowanie błędów certyfikatu SSL (np. self‑signed)  
--append-domain — automatyczne dodawanie domeny do każdej pozycji z wordlisty  
-u — adres URL / host, który ma zostać przeskanowany  
-w — ścieżka do wordlisty używanej do brute‑force vhostów  

---
