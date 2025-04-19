A quick way to identify a WordPress site is by browsing to the `/robots.txt` file. A typical robots.txt on a WordPress installation may look like:

```shell-session
User-agent: *
Disallow: /wp-admin/
Allow: /wp-admin/admin-ajax.php
Disallow: /wp-content/uploads/wpforms/

Sitemap: https://inlanefreight.local/wp-sitemap.xml
```

WordPress stores its plugins in the `wp-content/plugins` directory. This folder is helpful to enumerate vulnerable plugins. Themes are stored in the `wp-content/themes` directory. These files should be carefully enumerated as they may lead to RCE.


### Commands
 Look at which plugins we can uncover.
```shell-session
curl -s http://blog.inlanefreight.local/ | grep plugins
```

Browsing to `http://blog.inlanefreight.local/wp-content/plugins/...`

```
 Look at which themes we can uncover.
```shell-session
curl -s http://blog.inlanefreight.local/ | grep themes
```

Look for wordpress version.
```shell-session
curl -s http://blog.inlanefreight.local | grep WordPress
```



### Types of users 
 There are five types of users on a standard WordPress installation.

1. Administrator: This user has access to administrative features within the website. This includes adding and deleting users and posts, as well as editing source code.
2. Editor: An editor can publish and manage posts, including the posts of other users.
3. Author: They can publish and manage their own posts.
4. Contributor: These users can write and manage their own posts but cannot publish them.
5. Subscriber: These are standard users who can browse posts and edit their profiles.