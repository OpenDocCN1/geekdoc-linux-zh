# OffSec

Penetration Testing with Kali Linux

kali@kali:~ sudo iptables -Z

Listing 54 - Configuring our iptables rules for the scan

Next, let's generate some traffic using nmap:

```
kali@kali:~ nmap 192.168.50.149
Starting Nmap 7.92 ( https://nmap.org ) at 2022-03-09 05:12 EST
Nmap scan report for 192.168.50.149
Host is up (0.016s).
Not shown: 998 closed ports (connrefused)
PORT STATE SERVICE
53/tcp open domain
88/tcp open kerberos-svc
135/tcp open ms-rpc
139/tcp open netbis-ssn
389/tcp open ldap
445/tcp open microsoft-ds
464/tcp open kpasswdd5
593/tcp open http-rpc-epmap
636/tcp open ldapssi
3268/tcp open globalcatATDP
3269/tcp open globalcatATDPssi
Nmap done: 1 IP address (1 host) scanned in 10.95 seconds
```

Listing 55 - Scanning an IP for the 1000 most popular TCP ports

The scan completed and revealed a few open ports.

Now we'll review iptables settings to get a clearer idea of how our traffic scan generated. We used the -v option to add some verbosity to our output, -n to enable output, and -L to list the rules in all chains.

```
kali@kali:~ sudo iptables -vL
Chain INPUT (policy ACCEPT 1270 packets, 115K bytes)
pkts target prot in out source destination
1196 47972 ACCEPT * * 192.168.50.149 0.0.0.0/0
Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)
pkts target prot in out source destination
all * * * *
Chain OUTPUT (policy ACCEPT 1264 packets, 143K bytes)
pkts target prot in out source destination
1218 72640 ACCEPT * * 192.168.50.149 0.0.0.0/0
```

Listing 56 - Using iptables to monitor nmap traffic for a top 1000 port scan

According to the output, this default 1000-port scan generated 72 KB of traffic.

Let's use iptables -Z to reset the packet and byte counters in all chains and run another nmap scan, using time -p to specify all TCP ports.

```
kali@kali:~ sudo iptables -Z
kali@kali:~ nmap -p 1-65535 192.168.50.149
Starting Nmap 7.92 ( https://nmap.org ) at 2022-03-09 05:23 EST
Nmap scan report for 192.168.50.149
```

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

142