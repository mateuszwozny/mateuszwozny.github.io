
# Lo-Fi

## 1. Informacje ogólne
  **LFI** (Local file inclusiion) to błąd w stronie internetowej, który pozwala komuś podejrzeć pliki znajdujące się na serwerze,  
  jeśli aplikacja wczytuje pliki na podstawie danych od użytkownika i nie sprawdza ich poprawności.  
  W praktyce oznacza to, że ktoś może zobaczyć pliki, których nie powinien — np. konfiguracje, hasła albo kod źródłowy.

  **Path Traversal** to technika, w której atakujący używa specjalnych ciągów typu ../ aby cofnąć się w strukturze folderów i dostać do plików poza katalogiem strony.  
  To tak, jakby w przeglądarce plików klikać „wróć do folderu wyżej”, tylko że z poziomu URL. 

---

## 2. Metodologia 
 **Narzędzia:** - manipulacja adresem URL
 
## 3. Podsumowanie zadania
 Korzystamy z Path traversal i manipulujemy ../../../  
 
 Otrzymujemy strone z danymi : 
 
 ```url
?page=../../../../etc/passwd
```
Podpowiedź w zadaniu to znalazenie flagi w katalogu root:  

```url
?page=../../../../flag.txt
```
