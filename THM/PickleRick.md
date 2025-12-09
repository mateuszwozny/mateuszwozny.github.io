# Raport z testów penetracyjnych – TryHackMe „Pickle Rick”

## 1. Informacje ogólne
- **Cel testów:** Eksploatacja podatnej aplikacji webowej w celu uzyskania dostępu do systemu i odnalezienia trzech sekretów Ricka.  
- **Zakres:** Maszyna CTF „Pickle Rick” (adres IP przydzielony przez TryHackMe).  
- **Daty przeprowadzenia:** Sesja treningowa.  
- **Osoba testująca:** Mateusz (uczestnik CTF).  

---

## 2. Metodologia
- **Standardy:** OWASP Web Security Testing Guide.  
- **Podejście:** Black-box (brak dostępu do kodu źródłowego).  
- **Narzędzia:** Nmap, Gobuster, Burp Suite, podstawowe polecenia Linuksa.  

---

## 3. Podsumowanie wyników
- **Liczba podatności:** 3 kluczowe punkty prowadzące do eskalacji.  
- **Poziomy ryzyka:**  
  - Wysokie – brak zabezpieczeń w panelu logowania.  
  - Wysokie – możliwość zdalnego wykonania poleceń.  
  - Średnie – słabe zabezpieczenia plików systemowych.  
- **Ogólna ocena:** Maszyna celowo podatna, idealna do nauki podstaw web exploitation i privilege escalation.  

---

## 4. Szczegóły podatności

### 4.1 Rekonesans i dostęp do panelu (High)
- **Opis:** Nmap ujawnił otwarty port HTTP. Analiza strony wskazała ukryte dane logowania w kodzie źródłowym (`R1ckRul3s`).  
- **Dowody:**  
  ```html
  <!-- Username: R1ckRul3s -->

  
