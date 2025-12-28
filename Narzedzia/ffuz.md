 ## ffuz :  
 
 ***Fast web Fuzzer*** - to narzędzie do szybkiego fuzzingu stron WWW, używane do wykrywania ukrytych katalogów, plików, parametrów i subdomen
  
  ```bash
  ffuf -u http://futurevera.thm -w /usr/share/wordlists/amass/subdomains-top1mil-110000.txt -H "Host: FUZZ.futurevera.thm"  
  ```

 ## Przełączniki :

 - u - url
 - w wordlista
 - H dodawania własnego nagłówka
   ffuf będzie wstawiał kolejne słowa z wordlisty w miejsce FUZZ, np.:

Host: admin.futurevera.thm
Host: dev.futurevera.thm
Host: test.futurevera.thm

To klasyczna technika fuzzowania subdomen przez nagłówek Host,  
gdy DNS nie odpowiada lub gdy serwer obsługuje wiele vhostów na jednym IP.
