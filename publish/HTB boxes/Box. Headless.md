

Once we start the box with are given an IP 

I use rustScan to look for open ports and we can see that port 80 and 5000 is open

if we go to IP:5000 we see a landing page where we can contact support, since we were told in the machine information that this box was vunerable to Cross-Site Scripting (XXS) so what we can do is check if that is to the case by using 
`<p><script>window.alert()</script></p>` if we do this we an page that says # Hacking Attempt Detected ups sry about that :)

my next thought was to try the other fields to see if any of them are not check which was not the case

```
ffuf -w /path/to/wordlist -u https://target/FUZZ
```

ffuf -w subdomains-top1million-20000.txt -u http://10.10.11.8:5000/FUZZT