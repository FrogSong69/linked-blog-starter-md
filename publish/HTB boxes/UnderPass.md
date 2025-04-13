rustscan -a 10.10.11.48
we see that port 22 and 80 is open.

do a deeper scan
sudo nmap -sS -sU -T4 10.10.11.48
(highly recommend adding --top-ports 50)

load the page and we can see 

![[Pasted image 20250412161601.png]]


fuck I have not been updaing this 


see udp port 161

 snmpwalk -v2c -c public 10.10.11.48

SNMPv2-MIB::sysDescr.0 = STRING: Linux underpass 5.15.0-126-generic #136-Ubuntu SMP Wed Nov 6 10:38:22 UTC 2024 x86_64
SNMPv2-MIB::sysObjectID.0 = OID: NET-SNMP-MIB::netSnmpAgentOIDs.10
DISMAN-EVENT-MIB::sysUpTimeInstance = Timeticks: (1073236) 2:58:52.36
SNMPv2-MIB::sysContact.0 = STRING: steve@underpass.htb
**SNMPv2-MIB::sysName.0 = STRING: UnDerPass.htb is the only daloradius server in the basin!**
SNMPv2-MIB::sysLocation.0 = STRING: Nevada, U.S.A. but not Vegas
SNMPv2-MIB::sysServices.0 = INTEGER: 72


feroxbuster -u http://underpass.htb/daloradius/ -w /usr/share/seclists/Discovery/Web-Content/common.txt -x php,txt,conf,bak

leads up to 
http://underpass.htb/daloradius//app/operators/login.php

use defult creds 

and ssh into the user with 
svcMosh
underwaterfriends
which is the the product of 412DD4759978ACFCC81DEAB01B382403 cracked with [here](https://crackstation.net/)


