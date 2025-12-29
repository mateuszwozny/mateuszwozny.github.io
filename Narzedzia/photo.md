## Wyciaganie informacji ze zdjęć:

```bash
strings foto.jpg
```
Wyszukuje w pliku czytelne dla człowieka ciągi znaków.
Używasz tego, żeby znaleźć:
-ukryte wiadomości,
-podejrzane ścieżki,
-fragmenty haseł,
-zaszyte dane w binariach.
To szybki pierwszy krok przy analizie każdego pliku.

---
```bash
binwalk -e foto.jpg
```
Skanuje plik w poszukiwaniu osadzonych danych, takich jak:
-archiwa ZIP,
-pliki PNG/JPG,
-systemy plików,
-nagłówki innych formatów.
Pokazuje, czy w pliku jest coś „doklejonego”.
-e = extract
Jeśli w JPG jest ukryty ZIP, PNG, PDF lub cokolwiek innego — binwalk wypakuje to do folderu _foto.jpg.extracted.

---

```bash
exiftool foto.jpg
```
Wyświetla metadane pliku, np.:
-autor,
-data wykonania,
-użyty program,
-komentarze,
-geolokalizacja,
-niestandardowe tagi.
---

```bash
steghide extract -sf foto.jpg
```
Próbuje wyciągnąć dane ukryte metodą steganografii w pliku JPG.

-sf = stego file (plik z ukrytą treścią)

Jeśli plik zawiera zaszyte dane (np. TXT, ZIP), steghide spróbuje je odzyskać.  
Czasem wymaga hasła — jeśli nie podasz, zapyta o nie.
