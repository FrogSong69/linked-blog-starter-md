#### Nmap - Web Discovery

```
nmap -p- <IP>
# scans all ports open TCP ports for a given IP
```

```
nmap <IP> -p- -oA web_discovery
```

**`-oA <basename>`**  
This is a shorthand to save your scan results in **all three** of Nmap’s major output formats, using the given `<basename>` as the file prefix. It creates:
1. `<basename>.nmap` – the normal human-readable output
2. `<basename>.xml` – XML format, useful for automated parsing or importing into other tools
3. `<basename>.gnmap` – a greppable plain‑text summary you can `grep` through quickly
In your case, `-oA web_discovery` will produce:
```
web_discovery.nmap
web_discovery.xml
web_discovery.gnmap
```

If we are dealing with a large environment that have a enormous amount of hosts with services running on open ports we can use tool like  [EyeWitness](https://github.com/FortyNorthSecurity/EyeWitness) and [Aquatone](https://github.com/michenriksen/aquatone). Both of these tools can be fed raw Nmap XML scan output (Aquatone can also take Masscan XML; EyeWitness can take Nessus XML output) and be used to quickly inspect all hosts running web applications and take screenshots of each. The screenshots are then assembled into a report that we can work through in the web browser to assess the web attack surface.

TODO: try these out and give examples on how to use them


Enumerating one of the hosts further using an Nmap service scan (`-sV`) against the default top 1,000 ports can tell us more about what is running on the webserver.

```shell-session
sudo nmap -sV <IP>
```


