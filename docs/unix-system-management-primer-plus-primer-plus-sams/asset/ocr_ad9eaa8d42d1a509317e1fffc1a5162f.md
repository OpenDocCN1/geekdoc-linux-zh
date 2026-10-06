# UNIX SYSTEM MANAGEMENT PRIMER PLUS

whois.arin.net: if you wanted to query 192.168.1.0 (a private reserved network), you could
type the following:
$ whois -h whois.arin.net 192.168.0.0
IANA (CBLK-RESERVED)
Internet Assigned Numbers Authority
4676 Admiralty Way, Suite 330
Marina del Rey, CA 90292-6695

Netname: IANA-CBLK1
Netblock: 192.168.0.0 - 192.168.255.255

Coordinator:
Internet Corporation for Assigned Names and Numbers (IANA-ARIN)
res-ip@iana.org
(310) 823-9358

Domain System inverse mapping provided by:

```
BLACKHOLE-1.IANA.ORG      192.0.32.18
BLACKHOLE-2.IANA.ORG      192.0.32.19
```

These blocks are reserved for special purposes.
Please see RFC 1918 for additional information.

Record last updated on 12-Oct-2001.
Database last updated on 8-Apr-2002 20:01:32 EDT.

This output is a bit different than the domain output, as it lists only one contact—the coordinator. This is the address you should contact if you are having problems that originate from that network.

![](bbox=[0.135, 0.613, 0.175, 0.653])

> Find Addresses with nslookup address
If you have an IP address, you may want to try looking up that address in DNS with nslookup address. If its DNS records are accurate, the IP address will reveal the domain name and give a better idea of who you are dealing with.

Outside of ARIN's domain, the following international registrars are available to query:

+   - European Registry
RIPE Network Coordination Centre
http://www.ripe.net
- Asia Pacific Registry (including Australia)
APNIC
http://www.apnic.net