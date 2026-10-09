```
```
;; ADDITIONAL SECTION:
a.root-servers.net. 3600000 IN A 198.41.0.4
a.root-servers.net. 3600000 IN AAAA 2001:503:ba3e::2:30
b.root-servers.net. 3600000 IN A 192.228.79.201
c.root-servers.net. 3600000 IN A 192.33.4.12
d.root-servers.net. 3600000 IN A 199.7.91.13
...
;; Query time: 78 msec
;; SERVER: 198.41.0.4#53(198.41.0.4)
;; WHEN: Mon Jan 28 15:33:31 2013
;; MSG SIZE rcvd: 699
```
```

# named.empty

```
```
# cat /var/named/named.empty
$TTL 3H
@ IN SOA @ rname.invalid. (
0 ; serial
1D ; refresh
1H ; retry
1W ; expire
3H ) ; minimum
NS @
A 127.0.0.1
AAAA ::1
```
```

# named.localhost

The named.localhost zone file defines the localhost zone, the normal server on the local system. It starts with a $TTL directive and holds four resource records: SOA, NS, A, and AAAA. The $TTL directive in the following file specifies that the default time to live for the resource records specified in this file is one day (1D):

```
```
# cat /var/named/named.localhost
$TTL 1D
@ IN SOA @ rname.invalid. (
0 ; serial
1D ; refresh
1H ; retry
1W ; expire
3H ) ; minimum
NS @
A 127.0.0.1
AAAA ::1
```
```

As explained earlier, the @ stands for the origin (the name of the zone), which is localhost, as specified in named.rfc1912.zones. The last three lines are the NS resource record that specifies the nameserver for the zone as localhost (@), the A resource record that specifies the IPv4 address of the host as 127.0.0.1, and the AAAA resource record that specifies the IPv6 address of the host as ::1. Because these three records have blank Name fields, each inherits this value from the preceding resource record—in this case, @.

# named.loopback

The named.loopback zone file provides information about the 1.0.0.127.in-addr.arpa reverse lookup zone and the equivalent IPv6 zone. It follows the same pattern as the