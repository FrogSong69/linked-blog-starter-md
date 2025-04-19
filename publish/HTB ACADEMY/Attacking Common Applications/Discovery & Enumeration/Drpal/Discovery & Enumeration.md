
A Drupal website can be identified in several ways, including by the header or footer message `Powered by Drupal`, the standard Drupal logo, the presence of a `CHANGELOG.txt` file or `README.txt file`, via the page source, or clues in the robots.txt file such as references to `/node`.

```shell-session
curl -s http://drupal.inlanefreight.local | grep Drupal
```


Another way to identify Drupal CMS is through [nodes](https://www.drupal.org/docs/8/core/modules/node/about-nodes). Drupal indexes its content using nodes. A node can hold anything such as a blog post, poll, article, etc. The page URIs are usually of the form `/node/<nodeid>`.
```
http://drupal.inlanefreight.local/node/1
```


Newer installs of Drupal by default block access to the `CHANGELOG.txt` and `README.txt` files, so we may need to do further enumeration. Let's look at an example of enumerating the version number using the `CHANGELOG.txt` file. To do so, we can use `cURL` along with `grep`, `sed`, `head`, etc.
```shell-session
curl -s http://drupal-acc.inlanefreight.local/CHANGELOG.txt | grep -m2 ""
```

```shell-session
curl -s http://drupal.inlanefreight.local/CHANGELOG.txt
```

we can also use droopescan

```shell-session
droopescan scan drupal -u http://drupal.inlanefreight.local
```




Drupal supports three types of users by default:

1. `Administrator`: This user has complete control over the Drupal website.
2. `Authenticated User`: These users can log in to the website and perform operations such as adding and editing articles based on their permissions.
3. `Anonymous`: All website visitors are designated as anonymous. By default, these users are only allowed to read posts.