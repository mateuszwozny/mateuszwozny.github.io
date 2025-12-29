## Hydra :
Hydra to narzędzie służące do automatycznego łamania haseł poprzez szybkie testowanie wielu loginów i haseł na różnych usługach sieciowych.

  ```bash
  hydra -l jan -P -u /usr/share/wordlists/rockyou.txt ssh://IP -V 
  ```
### Przełączniki :  
- l - mała litera mówik że posiadamy dane wej. w tym przypadku login
- P - duża litera oznacza że tej zmiennej szukamy
- u - loop user - wymuszenie aby hydra przeszukała cału plik.txt np haseł pod usera (imie)
- V widać postęp skanu (bez -V nie widać postępu skanowania haseł)
---
