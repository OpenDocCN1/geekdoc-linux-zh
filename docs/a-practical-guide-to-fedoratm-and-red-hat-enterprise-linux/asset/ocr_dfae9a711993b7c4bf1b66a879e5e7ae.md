A resource record has the following fields:

+   * Name—The domain name or IP address
+   * TTL—Time to live (not in all resource records; see page 1278)
+   * Class—Always IN for Internet (the only class supported by DNS)
+   * Type—Record type (discussed in the next section)
+   * Data—Varies with record type

If the Name field is missing, the resource record inherits the name from the previous resource record in the same file. If the Name field ends in a period (.), it specifies an FQDN; otherwise it is relative to the zone named in named.conf.

Cached resource records become out-of-date when the information in the record changes on the authoritative server. The TTL field indicates the maximum amount of time a server might keep a record in cache before checking whether a newer one is available. Typically the TTL is on the order of days. A TTL of 0 (zero) means that the resource record should not be cached.

More than 30 types of resource records exist, ranging from common types, such as address records that store the address of a host, to those that contain geographical information. The following paragraphs describe the types of resource records you are most likely to encounter.

A IPv4 Address Maps a domain name to the IPv4 address of a host. There must be at least one address record for each domain; multiple address records can point to the same IP address. The Name field holds the domain name, which is assumed to be in the same zone as the domain. The Data field holds the IP address associated with the name. The following address resource record maps the ns domain in the zone to 192.168.0.1:

```
```
ns IN A 192.168.0.1
```
```

AAAA IPv6 Address Maps a domain name to the IPv6 address of a host. The following address resource record maps the ns domain in the zone to an IPv6 address:

```
```
ns IN AAAA 2001:630:d0:131:a00::20ff:feb5:ef1e
```
```

CNAME Canonical Name Maps an alias or nickname to a domain name. The Name field holds the alias or nickname; the Data field holds the official or canonical name. CNAME is useful for specifying an easy-to-remember name or multiple names for the same domain. It is also useful when a system changes names or IP addresses. In this case the alias can point to the real name that must resolve to an IP address.

When a query returns a CNAME, a client or DNS tool performs a DNS lookup on the domain name returned with the CNAME. It is acceptable to provide multiple CNAME records all pointing to the name that has the A record. The following resource record maps ftp in the zone to www.sam.net:

```
```
ftp IN CNAME www.sam.net.
```
```