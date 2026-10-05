# OffSec

Penetration Testing with Kali Linux

| PORT STATE SERVICE VERSION |
| 80/tcp open Apache 2.4.41 ((Ubuntu))
Listing 98 - Running Nmap scan to discover web server host.
|

Our scans show that Apache version 2.4.41 is running on the Ubuntu host.

To take our enumeration further, we use service-specific Nmap NSE scripts, like http-enum, which performs an initial fingerprinting of the web server.

```
kali@kali:$ sudo nmap -p80 --script=http-enum 192.168.50.20
Starting Nmap 7.92 (https://nmap.org) at 2022-03-29 06:30:26 EDT\Nmap scan report for 192.168.50.20
Host is up (0.10s latency).

PORT STATE SERVICE
80/tcp open http
| http-enum:
| /login/: Possible admin folder
| /db/: BlogWork Database
| /css/: Potentially interesting directory w/ listing on 'apache/2.4.41 (ubuntu)
| /db/: Potentially interesting directory w/ listing on 'apache/2.4.41 (ubuntu)
| /images/: Potentially interesting directory w/ listing on 'apache/2.4.41 (ubuntu)
| /js/: Potentially interesting directory w/ listing on 'apache/2.4.41 (ubuntu)
| /uploads/: Potentially interesting directory w/ listing on 'apache/2.4.41
(ubuntu)'
```

Nmap done: 1 IP address (1 host up) scanned in 16.82 seconds
Listing 99 - Running Nmap NSE http enumeration script against the target

As shown above, we discovered several interesting folders that could lead to further details about the target web application.

By using Nmap, we managed to discover more application-specific information that we can add to the web server enumeration we performed earlier.

# 8.2.2 Technology Stack Identification with Wappalyzer

Along with the active gathering we performed by Nmap, we can also passively fetch a wealth of technology stack by Wappalyzer.³342

Once we have registered a free account, we can perform a Technology Lookup on the megacorpone domain.

> 342 (Wappalyzer, 2022), https://www.wappalyzer.com/

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

201