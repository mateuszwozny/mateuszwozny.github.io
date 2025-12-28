## SMB:

SMB to protokół sieciowy służący do udostępniania plików, folderów i zasobów (np. drukarek) pomiędzy komputerami,  
głównie w środowiskach Windows.

  Sprawdzenie czy SMB pozwala na dostęp anonimowy
  ```bash
  smbclient -L //IP -N
```
-L - lista udziałów
-N - bez hasła (tryb anonymous)

```bash
    smbclient //IP/Anonymous -N
    smb: \>
    smb: \> get plik.txt
```
---
