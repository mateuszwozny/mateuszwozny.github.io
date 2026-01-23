# Billing

gobuster
```bash
gobuster dir -u 10.67.133.0 -w /usr/share/wordlists/dirb/common.txt
```
Ukazuje nam ukryty folder /billing  

Po wejściu otrzymujemy strone logowania Magnus Billing.  

Magnus Billing to system do zarządzania usługami telekomunikacyjnymi i rozliczeniami (billingiem),  
używany głównie przez operatorów VoIP, ISP i firmy świadczące usługi komunikacyjne.   

Wyszukujemy w necie magnus billing rce na githubie , pobieramy kod , 
w środku jest instrukcja jak wywołać
nasłuchujemy nc -lvnp 1234 i po uruchmieniu otrzymujemy reverse shella i flagę usera.  

---

## Eskalacja uprawnień do root:
```bash
sudo -l
```
Matching Defaults entries for asterisk on ip-10-65-142-205:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin

Runas and Command-specific defaults for asterisk:
    Defaults!/usr/bin/fail2ban-client !requiretty

User asterisk may run the following commands on ip-10-65-142-205:
    (ALL) NOPASSWD: /usr/bin/fail2ban-client

czyli user może odpalić jako root bez hasła  /usr/bin/fail2ban-client

Na stronie poniżej otrzymujemy gotową liste komend aby podnieść uprawnienia do root
```url
https://exploit-notes.hdks.org/exploit/linux/privilege-escalation/sudo/fail2ban-command/
```
