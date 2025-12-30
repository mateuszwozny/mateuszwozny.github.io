# Cyber Heros

## 1. Informacje ogólne  

Bypass authentication to sytuacja, w której atakujący omija proces logowania i uzyskuje dostęp do systemu bez podania poprawnych danych uwierzytelniających.  
Dzieje się tak z powodu błędów w logice aplikacji, luk bezpieczeństwa lub złej konfiguracji.

---

## 2. Metodologia 
 **Narzędzia:** burpsuit 

## 3. Podsumowanie zadania
  **Skanowanie wstępne:**
  
Na początku wykonano skanowanie usług, aby ustalić otwarte porty, wersje usług i potencjalne punkty wejścia.  

Użyte narzędzie:  

 ***nmap:*** 

```bash
sudo nmap -sV -sC -sS IP
``` 

**Analiza aplikacji webowej**  

  Wstępna analiza stron , podstron nic nie wykazała.
  Badamy strone logowania , dlatego odpalamy Burpsit i przechodizmy do analizy Response
  Napotykamy na script który bardziej analizujemy.

```html
<script>
    function authenticate() {
      a = document.getElementById('uname')
      b = document.getElementById('pass')
      const RevereString = str => [...str].reverse().join('');
      if (a.value=="h3ck3rBoi" & b.value==RevereString("54321@terceSrepuS")) { 
        var xhttp = new XMLHttpRequest();
        xhttp.onreadystatechange = function() {
          if (this.readyState == 4 && this.status == 200) {
            document.getElementById("flag").innerHTML = this.responseText ;
            document.getElementById("todel").innerHTML = "";
            document.getElementById("rm").remove() ;
          }
        };
        xhttp.open("GET", "RandomLo0o0o0o0o0o0o0o0o0o0gpath12345_Flag_"+a.value+"_"+b.value+".txt", true);
        xhttp.send();
      }
      else {
        alert("Incorrect Password, try again.. you got this hacker !")
      }
    }
  </script>
  ```
W skrypcie widzimy wartości a jako uname oraz b jako pass


admin – a.value
password -
```bash
echo 54321@terceSrepuS | rev   → SuperSecret@12345
```

