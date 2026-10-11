```
Nmap done: 1 IP address (1 host up) scanned in 46.29 seconds
```

Listing 230 - Scanning an IP for the 1000 most popular TCP ports

The scan completed and revealed a few open ports.

Now let’s look at some **iptables** statistics to get an idea of how much traffic our scan generated. We will use the **-v** option to add some verbosity to our output, **-n** to enable numeric output, and **-L** to list the rules present in all chains:

```
kali@kali:~$ sudo iptables -vn -L
Chain INPUT (policy ACCEPT 1528 packets, 226K bytes)
 pkts bytes target prot opt in out source destination
1263 51264 ACCEPT all -- * * 10.11.1.220 0.0.0.0/0

Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)
 pkts bytes target prot opt in out source destination

Chain OUTPUT (policy ACCEPT 1323 packets, 191K bytes)
 pkts bytes target prot opt in out source destination
1314 78300 ACCEPT all -- * * 0.0.0.0/0 10.11.1.220
```

Listing 231 - Using iptables to monitor nmap traffic for a top 1000 port scan

According to this output, this default 1000-port scan has generated around 78 KB of traffic.

Let’s use **iptables -Z** to zero the packet and byte counters in all chains again and run another **nmap** scan using **-p** to specify ALL TCP ports:

```
kali@kali:~$ sudo iptables -Z
kali@kali:~$ nmap -p 1-65535 10.11.1.220
Starting Nmap 7.70 ( https://nmap.org ) at 2019-03-04 11:27 EST
Nmap scan report for 10.11.1.220
Host is up (0.00067s latency).
Not shown: 65507 closed ports
PORT STATE SERVICE
21/tcp open ftp
53/tcp open domain
88/tcp open kerberos-sec
135/tcp open msrpc
139/tcp open netbios-ssn
389/tcp open ldap
445/tcp open microsoft-ds
464/tcp open kpasswd5
593/tcp open http-rpc-epmap
636/tcp open ldapsssl
1291/tcp filtered seagullms
3268/tcp open globalcatLDAP
3269/tcp open globalcatLDAPssl
3389/tcp open ms-wbt-server
5722/tcp open msdfs
9389/tcp open adws
12777/tcp filtered unknown
46056/tcp filtered unknown
```