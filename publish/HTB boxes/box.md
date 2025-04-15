


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

```
feroxbuster -u http://10.10.10.68/ -w /usr/share/wordlists/seclists/PathBANGER.txt -r -C 404 -x php
                                                                             
 ___  ___  __   __     __      __         __   ___
|__  |__  |__) |__) | /  `    /  \ \_/ | |  \ |__
|    |___ |  \ |  \ | \__,    \__/ / \ | |__/ |___
by Ben "epi" Risher 🤓                 ver: 2.11.0
───────────────────────────┬──────────────────────
 🎯  Target Url            │ http://10.10.10.68/
 🚀  Threads               │ 50
 📖  Wordlist              │ /usr/share/wordlists/seclists/PathBANGER.txt
 💢  Status Code Filters   │ [404]
 💥  Timeout (secs)        │ 7
 🦡  User-Agent            │ feroxbuster/2.11.0
 💉  Config File           │ /etc/feroxbuster/ferox-config.toml
 🔎  Extract Links         │ true
 💲  Extensions            │ [php]
 🏁  HTTP methods          │ [GET]
 📍  Follow Redirects      │ true
 🔃  Recursion Depth       │ 4
───────────────────────────┴──────────────────────
 🏁  Press [ENTER] to use the Scan Management Menu™
──────────────────────────────────────────────────
404      GET        9l       32w        -c Auto-filtering found 404-like response and created new filter; toggle off with --dont-filter
403      GET       11l       32w        -c Auto-filtering found 404-like response and created new filter; toggle off with --dont-filter
200      GET        7l       23w     1322c http://10.10.10.68/images/favicon.png
200      GET      154l      394w     7477c http://10.10.10.68/single.html
200      GET      161l      397w     7743c http://10.10.10.68/index.html
200      GET        8l       35w     2447c http://10.10.10.68/images/logo.png
200      GET       32l      116w     1222c http://10.10.10.68/css/carouFredSel.css
200      GET       12l       63w     1392c http://10.10.10.68/js/jquery.mousewheel.min.js
200      GET        8l       73w     2429c http://10.10.10.68/js/html5.js
200      GET       13l      113w     4313c http://10.10.10.68/js/jquery.touchSwipe.min.js
200      GET       15l      672w    36079c http://10.10.10.68/js/jquery.carouFredSel-6.0.0-packed.js
200      GET      118l      550w    60153c http://10.10.10.68/js/jquery.nicescroll.min.js
200      GET        1l        1w       14c http://10.10.10.68/uploads/
200      GET       58l      254w     1783c http://10.10.10.68/js/jquery.easing.1.3.js
200      GET      117l      685w     4689c http://10.10.10.68/css/sm-clean.css
200      GET       96l      166w     1661c http://10.10.10.68/css/clear.css
200      GET      680l     1154w    10723c http://10.10.10.68/css/common.css
200      GET      262l      560w     8904c http://10.10.10.68/js/main.js
200      GET      893l     3885w    26643c http://10.10.10.68/js/imagesloaded.pkgd.js
200      GET        4l       66w    29063c http://10.10.10.68/css/font-awesome.min.css
200      GET        3l      206w    24476c http://10.10.10.68/js/jquery.smartmenus.min.js
200      GET     1412l     2291w    24164c http://10.10.10.68/style.css
200      GET        6l       20w     1537c http://10.10.10.68/images/arrow.png
200      GET       19l       88w     1564c http://10.10.10.68/images/
200      GET       38l       76w      909c http://10.10.10.68/js/custom_google_map_style.js
200      GET      154l     1009w    73725c http://10.10.10.68/images/ajax-document-loader.gif
200      GET        6l     1435w    97184c http://10.10.10.68/js/jquery.js
200      GET      161l      397w     7743c http://10.10.10.68/
200      GET        0l        0w        0c http://10.10.10.68/php/sendMail.php
200      GET       16l       59w      939c http://10.10.10.68/php/
200      GET       20l       96w     1758c http://10.10.10.68/css/
200      GET      216l      489w     8151c http://10.10.10.68/dev/phpbash.php
200      GET        1l      255w     4559c http://10.10.10.68/dev/phpbash.min

```

as we can see there we have http://10.10.10.68/dev/phpbash.php

We are told that the server is build on [phpbash]([https://github.com/Arrexel/phpbash](https://github.com/Arrexel/phpbash))

with that we can go the the site an

where we have a bash shell 
```
www-data@bashed

:/var/www/html/dev# ls

phpbash.min.php  
phpbash.php  

www-data@bashed

:/var/www/html/dev# cd /home

  

www-data@bashed

:/home# ls

  
arrexel  
scriptmanager  

www-data@bashed

:/home# cd arrexel

  

www-data@bashed

:/home/arrexel# ls

  
user.txt  

www-data@bashed

:/home/arrexel# cat user.txt

  
1ce2c16b4364f457a0c1626122f5025c
```