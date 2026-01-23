# Hashcat

Hashcat to niezwykle wydajne narzędzie do łamania haseł, które wykorzystuje moc GPU, aby znacząco przyspieszyć obliczenia.  
Dzięki obsłudze wielu algorytmów i trybów pracy świetnie sprawdza się w analizie bezpieczeństwa i testach odporności haseł.

```bash
hashcat -m 0 hash /usr/share/wordlists/rockyou.txt
```
```url
https://hashcat.net/wiki/doku.php?id=example_hashes
```
-m 0
Określa typ hasha, który będzie łamany.

0 oznacza MD5.

W przypadku gdy był już wcześniej sprawdzany taki hash to wyświetlamy go poleceniem

```bash
hashcat -m 0 hash --show
```
