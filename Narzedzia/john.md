## John The Ripper:  

***John the Ripper*** to narzędzie służące do łamania haseł i analizowania ich bezpieczeństwa.

  ```bash
  john hash.txt --wordlist=/usr/share/wordlists/rockyou.txt
  ```
  ---

  ```bash
  zip2john 8702.zip > 8702.txt
  john --wordlist=/usr/share/wordlists/rockyou.txt 8702.txt
  ```
  ```bash
  ssh2john id > hash.txt
   ``` 
  John musi mieć zawartość jako hash i dlatego zamieniamy zwykły tekst na hash

  W przypadku plików które są zahashowane jakims formatem :

  ```bash
  john --format=gost --wordlist=easypeasy.txt hash.txt
  ```
  GOST to rosyjski algorytm haszujący (podobny do SHA‑256, ale inny). John musi wiedzieć, jaki algorytm zastosować,  
  żeby poprawnie łamać hash.

