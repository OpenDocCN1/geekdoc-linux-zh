```
alice% nslookup -d gilligan.ncc.com
:: res_mkquery(0, 52.6.72.194.in-addr.arpa, 1, 12)
----------------------------------
Got answer:
HEADER:
opcode = QUERY, id = 33005, rcode = NOERROR
header flags: response, auth. answer, want recursion. recursion avail.
questions = 1, answers = 1, authority records = 3, additional = 3
QUESTIONS:
52.6.72.194.in-addr.arpa, type = PTR, class = IN
ANSWERS:
-> 52.6.72.194.in-addr.arpa    name = ns1.bt.net      ttl = 86400 (1D)
AUTHORITY RECORDS:
-> 6.72.194.in-addr.arpa    nameserver = ns0.bt.net ttl = 86400 (1D)
-> 6.72.194.in-addr.arpa    nameserver = ns1.bt.net ttl = 86400 (1D)
-> 6.72.194.in-addr.arpa    nameserver = ns2.bt.net ttl = 86400 (1D)
ADDITIONAL RECORDS:
-> ns0.bt.net    internet address = 194.72.6.51 ttl = 86400 (1D)
-> ns1.bt.net    internet address = 194.72.6.52 ttl = 86400 (1D)
-> ns2.bt.net    internet address = 193.113.212.38 ttl = 86400 (1D)
Server: ns1.bt.net
Address: 194.72.6.52
:: res_mkquery(0, gilligan.ncc.com, 1, 1)
----------------------------------
Got answer:
HEADER:
opcode = QUERY, id = 33006, rcode = NOERROR
header flags: response, auth. answer, want recursion. recursion avail
questions = 1, answers = 1, authority records = 2, additional = 2
QUESTIONS:
gilligan.ncc.com, type = A, class = IN
ANSWERS:
-> gilligan.ncc.com    internet address = 192.43.160.247 ttl = 3600 (1H)
AUTHORITY RECORDS:
-> ncc.com    nameserver = ns.ncc.com    ttl = 3600 (1H)
-> ncc.com    nameserver = ns.UU.NET    ttl = 3600 (1H)
ADDITIONAL RECORDS:
-> ns.ncc.com    internet address = 192.43.160.250 ttl = 3600 (1H)
-> ns.UU.NET    internet address = 137.39.1.3 ttl = 162401 (1d)
Name:    gilligan.ncc.com
Address: 192.43.160.247
```

packet 1 - get name of
the DNS server we're

packet 2 - reply giving name
of DNS server

packet 3 - query for
gilligan.ncc.com

packet 4 - reply giving the
IP number we asked for

# Figure 7.8 Annotated example of nslookup's debug output

```
alice% tcpdump -n -t -s300
192.0.2.34.1025 > 194.72.6.52.53: 33005* PTR? 52.6.72.194.in-addr.arpa. (42)
194.72.6.52.53 > 192.0.2.34.1025: 33005* 1/3/3 PTR ns1.bt.net. (164) (DF)
192.0.2.34.1025 > 194.72.6.52.53: 33006* A? gilligan.ncc.com. (34)
194.72.6.52.53 > 192.0.2.34.1025: 33006* 1/2/2 A 192.43.160.247 (129) (DF)
```

# Figure 7.9 Actual packet flow for the query in Figure 7.8