```
nmap -sV -sC curling.htb -p-
Starting Nmap 7.95 ( https://nmap.org ) at 2025-04-18 18:22 CEST
Nmap scan report for curling.htb (10.10.10.150)
Host is up (0.10s latency).
Not shown: 65533 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 8a:d1:69:b4:90:20:3e:a7:b6:54:01:eb:68:30:3a:ca (RSA)
|   256 9f:0b:c2:b2:0b:ad:8f:a1:4e:0b:f6:33:79:ef:fb:43 (ECDSA)
|_  256 c1:2a:35:44:30:0c:5b:56:6a:3f:a5:cc:64:66:d9:a9 (ED25519)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-generator: Joomla! - Open Source Content Management
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: Home
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel 
```


if we curl the 
`curl http://curling.htb/secret.txt`
```
</body>
      <!-- secret.txt -->
</html>
```

```
curl http://curling.htb/secret.txt
Q3VybGluZzIwMTgh

```

```
echo Q3VybGluZzIwMTgh | base64 -d 
Curling2018!   
```

Now we have what looks like a password 