
set vhost
```
etc/hosts/
10.10.10.37 blocky.htb
```


```
feroxbuster -u http://blocky.htb/ -w /usr/share/wordlists/seclists/PathBANGER.txt  -x php,sh,txt,jar -C 404 -r 
```
