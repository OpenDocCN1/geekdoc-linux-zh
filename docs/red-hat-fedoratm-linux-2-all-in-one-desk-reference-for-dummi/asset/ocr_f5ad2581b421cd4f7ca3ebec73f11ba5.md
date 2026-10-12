```
: formerly NIC.NORDU.NET
:
3600000 NS I.ROOT-SERVERS.NET.
:
1.ROOT-SERVERS.NET. 3600000 A 192.36.148.17
:
: operated by VeriSign, Inc.
:
3600000 NS J.ROOT-SERVERS.NET.
:
J.ROOT-SERVERS.NET. 3600000 A 192.58.128.30
:
: operated by Ripe NCC
:
3600000 NS K.ROOT-SERVERS.NET.
:
K.ROOT-SERVERS.NET. 3600000 A 193.0.14.129
:
: operated by ICANN
:
3600000 NS L.ROOT-SERVERS.NET.
:
L.ROOT-SERVERS.NET. 3600000 A 198.32.64.12
:
: operated by WIDE
:
3600000 NS M.ROOT-SERVERS.NET.
:
M.ROOT-SERVERS.NET. 3600000 A 202.12.27.33
: End of File
```

This file contains **NS** and **A** resource records that specify the names of authoritative name servers and their addresses for the root zone (indicated by the . in the first field of each **NS** record).

The comment lines in the file begin with a semicolon. These comments give you hints about the location of the root name servers. There are 13 root name servers for the Internet; most root servers are located in the United States. This file is a necessity for any name server because the name server has to be able to reach at least one root name server.

# The */var/named/localhost.zone* file

The /etc/named.conf file includes a *zone statement for the localhost* zone that specifies the zone file as *localhost.zone*. That file is located in the /var/named directory of your Fedora Core system. Here's a listing of what the /var/named/localhost.zone file contains:

```
$TTL	86400
$ORIGIN localhost.
@		1D IN SOA	@ root (
				42			: serial (d. adams)
				3H			: refresh
				15M			: retry
				1W			: expire
				1D )

	1D IN NS		@
	1D IN A		127.0.0.1
```