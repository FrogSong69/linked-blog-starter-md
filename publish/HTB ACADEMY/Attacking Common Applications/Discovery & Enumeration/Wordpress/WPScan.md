
[WPScan](https://github.com/wpscanteam/wpscan) is an automated WordPress scanner and enumeration tool.


WPScan is also able to pull in vulnerability information from external sources. We can obtain an API token from [WPVulnDB](https://wpvulndb.com/), which is used by WPScan to scan for PoC and reports. The free plan allows up to 75 requests per day. To use the WPVulnDB database, just create an account and copy the API token from the users page. This token can then be supplied to wpscan using the `--api-token parameter`.

```shell-session
wpscan --url http://block.inlanefreight.local
```


WPScan can be used to brute force usernames and passwords. The scan report in the previous section returned two users registered on the website (admin and john). The tool uses two kinds of login brute force attacks, [xmlrpc](https://kinsta.com/blog/xmlrpc-php/) and wp-login. The `wp-login` method will attempt to brute force the standard WordPress login page, while the `xmlrpc` method uses WordPress API to make login attempts through `/xmlrpc.php`. The `xmlrpc` method is preferred as it’s faster.

```shell-session
sudo wpscan --password-attack xmlrpc -t 20 -U john -P /usr/share/wordlists/rockyou.txt --url http://blog.inlanefreight.local
```

The `--password-attack` flag is used to supply the type of attack. The `-U` argument takes in a list of users or a file containing user names. This applies to the `-P` passwords option as well. The `-t` flag is the number of threads which we can adjust up or down depending.

We can use
```
wpscan --url http://blog.inlanefreight.local --enumerate u
```
to enumerate from users


brute force

```
sudo wpscan --password-attack xmlrpc -t 20 -U doug -P /usr/share/wordlists/rockyou.txt --url http://blog.inlanefreight.local
```

