

# scan ports 

You can use nmap or rustscan

`rustscan -a IP`

Do a deep nmap scan with as well as checking udp ports 

`sudo nmap -sV -sC ip --top-ports 100`

`sudo nmap -sS -sU -T4 10.10.11.48`


Path fuzzing 
```
feroxbuster -u http://10.10.11.58/ -w /usr/share/wordlists/seclists/PathBANGER.txt  -x php,sh 
gets us a shit ton of hits so here are some of the intersting ones
```

git dump
```
https://github.com/internetwache/GitTools/tree/master
```