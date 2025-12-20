# TryHackMe „Corridor”

## 1. Informacje ogólne
- **Cel testów:**  
 Pokój Corridor na TryHackMe to krótkie, liniowe wyzwanie, w którym przechodzisz przez kolejne „drzwi”, rozwiązując proste zadania logiczne i techniczne. Uczy podstawowego myślenia analitycznego i pokazuje, jak krok po kroku eliminować przeszkody, aby dotrzeć do końca ścieżki. 
 
 ---

## 2. Metodologia 
- **Narzędzia:** Cyberchef , CrackStation, 

---

## 3. Szczegóły podatności
- **Opis:**
  W zadaniu Corridor poruszamy się między kolejnymi „pokojami”, klikając drzwi opisane jako hashe MD5.  
  Każdy hash należy zdekodować, aby ustalić, które drzwi prowadzą dalej, ponieważ większość z nich kieruje do pustych, błędnych pomieszczeń.  
  Ostatecznie flaga nie znajduje się w żadnym z podanych pokoi, lecz ukryta jest w pokoju oznaczonym jako 0,  
  do którego można trafić ponieważ w językach programowania zaczynamy liczenie od 0 - i to okazało się trafnym tropem.  


  


