

# scan ports 

You can use nmap or rustscan

`rustscan -a IP`

Do a deep nmap scan with as well as checking udp ports 

`sudo nmap -sV -sC ip --top-ports 100`

`sudo nmap -sS -sU -T4 10.10.11.48`