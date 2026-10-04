# Chapter 5 • Attacking and Defending Windows 2000

```
C:\>sl -h-r 192.168.25.1-192.168.25.100
```

ScanLine (TM) 1.01
Copyright (c) Foundstone, Inc. 2002
http://www.foundstone.com

Scan of 100 IPs started at Mon Jan 20 12:01:13 2003

192.168.25.66
Hostname: EXCW2KAS
Responded in 0 ms.
0 hops away
Responds with ICMP unreachable: Yes
TCP ports: 21 25 53 80 88 110 135 139 389 443 445 593 636 1026 1029 3268
3372 3389
UDP ports: 53 123 135 137 138 161 445 500 1028 3456

Scan finished at Mon Jan 20 12:01:36 2003
Following this scanning visit and an indication of potential targets, it is time to visit the enumeration process to further identify potential victims and openings for the target systems.
Windows 2000 uses specific ports in the default configuration to provide services and access. Table 5.4 lists the most common ports that are active in the default configuration.

# Table 5.4 Windows 2000 Common Port Assignments

| Service Name | UDP | TCP |
|---|---|---|
| Browsing datagram responses of NetBIOS over TCP/IP | 138 | |
| Browsing requests of NetBIOS over TCP/IP | 137 | |
| Client/Server Communication | | 135 |
| Common Internet File System (CIFS) | 445 | 139, 445 |
| Content Replication Service | | 560 |
| Cybercash Administration | | 8001 |
| Cybercash Coin Gateway | | 8002 |
| Continued | | |