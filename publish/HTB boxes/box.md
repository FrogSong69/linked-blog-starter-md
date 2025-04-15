


IP = 10.10.10.68

we right away see a website


```
sudo nmap -sV 10.10.10.68                                             
Starting Nmap 7.95 ( https://nmap.org ) at 2025-04-15 15:47 CEST
Nmap scan report for 10.10.10.68
Host is up (0.10s latency).
Not shown: 999 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 8.71 seconds

```

```
feroxbuster -u http://10.10.10.68/ -w /usr/share/wordlists/seclists/PathBANGER.txt -r -C 404 -x php
```




We are told that the server is build on [phpbash]([https://github.com/Arrexel/phpbash](https://github.com/Arrexel/phpbash))