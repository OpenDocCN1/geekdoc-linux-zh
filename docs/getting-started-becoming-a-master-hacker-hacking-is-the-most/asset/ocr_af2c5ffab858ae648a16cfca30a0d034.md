```
msf5 > use auxiliary/scanner/portscan/tcp
msf5 auxiliary(scanner/portscan/tcp) > info

Name: TCP Port Scanner
Module: auxiliary/scanner/portscan/tcp
License: Metasploit Framework License (BSD)
Rank: Normal

Provided by:
hdm <x@hdm.io>
Kris Katterjohn <katterjohn@gmail.com>

Check supported:
Yes

Basic options:
Name Current Setting Required Description
---- -------------- -------- -----------------------------------------
CONCURRENCY 10 yes The number of concurrent ports to check per host
DELAY 0 yes The delay between connections, per thread, in milliseconds
JITTER 0 yes The delay jitter factor (maximum value by which to +/- DELAY) in milliseconds

PORTS 1-10000 yes Ports to scan (e.g. 22-25,80,110-900)
RHOSTS The target address range or CIDR identifier
THREADS 1 yes The number of concurrent threads
TIMEOUT 1000 yes The socket connect timeout in milliseconds

Description:
Enumerate open TCP services by performing a full TCP connect on each port. This does not need administrative privileges on the source machine, which may be useful if pivoting.
```

```
msf5 auxiliary(scanner/portscan/tcp) > set RHOSTS 192.168.0.114
RHOSTS => 192.168.0.114
msf5 auxiliary(scanner/portscan/tcp) > run

[+] 192.168.0.114:	-	192.168.0.114:139 - TCP OPEN
[+] 192.168.0.114:	-	192.168.0.114:135 - TCP OPEN
[+] 192.168.0.114:	-	192.168.0.114:445 - TCP OPEN
[+] 192.168.0.114:	-	192.168.0.114:3306 - TCP OPEN
[+] 192.168.0.114:	-	192.168.0.114:3357 - TCP OPEN
[*] 192.168.0.114:	- Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
```

To use this module to do a portscan of our Windows 7 system, we simply need to set the IP address of our RHOSTS (remote hosts or our target system) and enter run.

msf5 > set RHOSTS 192.169.0.114

msf5 > run

As you can see, the Metasploit port scanning module finds identical results as our nmap scan in Chapter 6.