
linux box

sudo nmap 10.10.10.7

```bash
sudo nmap 10.10.10.7                
Starting Nmap 7.95 ( https://nmap.org ) at 2025-04-14 03:02 CEST
Nmap scan report for 10.10.10.7
Host is up (0.11s latency).
Not shown: 988 closed tcp ports (reset)
PORT      STATE SERVICE
22/tcp    open  ssh
25/tcp    open  smtp
80/tcp    open  http
110/tcp   open  pop3
111/tcp   open  rpcbind
143/tcp   open  imap
443/tcp   open  https
993/tcp   open  imaps
995/tcp   open  pop3s
3306/tcp  open  mysql
4445/tcp  open  upnotifyp
10000/tcp open  snet-sensor-mgmt

Nmap done: 1 IP address (1 host up) scanned in 1.56 seconds
```

sudo nmap -sV 10.10.10.7 

```
sudo nmap -sV 10.10.10.7               
Starting Nmap 7.95 ( https://nmap.org ) at 2025-04-14 03:03 CEST
Nmap scan report for 10.10.10.7
Host is up (0.11s latency).
Not shown: 988 closed tcp ports (reset)
PORT      STATE SERVICE    VERSION
22/tcp    open  ssh        OpenSSH 4.3 (protocol 2.0)
25/tcp    open  smtp       Postfix smtpd
80/tcp    open  http       Apache httpd 2.2.3
110/tcp   open  pop3       Cyrus pop3d 2.3.7-Invoca-RPM-2.3.7-7.el5_6.4
111/tcp   open  rpcbind    2 (RPC #100000)
143/tcp   open  imap       Cyrus imapd 2.3.7-Invoca-RPM-2.3.7-7.el5_6.4
443/tcp   open  ssl/http   Apache httpd 2.2.3 ((CentOS))
993/tcp   open  ssl/imap   Cyrus imapd
995/tcp   open  pop3       Cyrus pop3d
3306/tcp  open  mysql?
4445/tcp  open  upnotifyp?
10000/tcp open  http       MiniServ 1.570 (Webmin httpd)
Service Info: Hosts:  beep.localdomain, 127.0.0.1, example.com

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 193.78 seconds
```



1. `feroxbuster -u http://nocturnal.htb/   -w /usr/share/seclists/Discovery/Web-Content/common.txt   -x php,doc,docx,txt,conf,bak   -H "Cookie: PHPSESSID=3a9fudjom19l0ua5i7vdmsjnc9"   -C 200`