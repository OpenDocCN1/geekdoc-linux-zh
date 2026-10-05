# The localhost zone

# The localhost zone

The address 127.0.0.1 refers to a itself and should be mapped to the name "localhost."23 Some sites map the address to "localhost.localdomain." and some do both. The corresponding IPv6 address is ::1.

If you forget to configure the localhost zone, your site may end up querying the root servers for localhost information. The root servers receive so many of the queries that the operators are considering adding a generic mapping between localhost and 127.0.0.1 at the root level. In measurements at the K root server in Europe in January 2010 (k.root-servers.org/statistics), "local" was the fourth most popular domain queried, behind just com, arp and net. There are a lot of useless queries (1,500/second) for a busy name server. Other unusual names in the popular bogus TLD category are home, localhost, and domain.

The forward mapping for the name localhost can be defined in the forward zone file for the domain (with an appropriate ORIGIN statement) or in its own reverse file. Each server, even a caching server, is usually the master for its own reverse-host domain.

Here are the lines in named.conf that configure localhost:

```
zone "localhost" // localhost forward zone
  type master;
  file "localhost";n  allow-update { none };
```

```
zone "0.0.127-in.addr.arpa" // localhost reverse zone
  type master;
  file "127.0.0";n  allow-update { none };
```

The forward zone file, localhost, contains

```
$TTL 30
; localhost.
  IN SOA localhost. postmaster.localhost. (
      199805081 ;serial
      3600 ;refresh
      1800 ;retry
      604800 ;expiration
      3600 ;minimum)

  NS localhost.
  A 127.0.0.1
```

+   21. Actually, the whole class A network 127/8 refers back to localhost, but most folks just use 127.0.0.1.