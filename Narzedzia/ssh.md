## SSH: 

SSH to protokół, który umożliwia bezpieczne, zaszyfrowane logowanie do zdalnego systemu i wykonywanie na nim poleceń tak,  
jakbyś siedział przy jego terminalu.


  ```bash
  ssh jan@IP
  ```

  ```bash
  ssh -i id(nazwa klucza) kay@IP
  ```
  ---

### Kopiowanie danych z maszyny wirtualnej na fizyczną:

#### Włączenie SSH w kali:

```bash
sudo systemctl start ssh
```

#### Pobranie z poziomu powershell danych:

```bash
scp kali@IP:/home/kali/Desktop/THM-DG0Y21HITI.pdf .
```
```bash
scp -P 2222 area51@10.80.178.187:/home/area51/test.jpg .
```
-P - podajemy port w przypadku kiedy działa na innym
Kropka na końcu oznacza że wklejamy dane do bieżącego katalogu
