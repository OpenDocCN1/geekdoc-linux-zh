# Part III: Ubuntu System Administrators

to refer to the root domain in MX records because, again, this makes it easier for me to use a generic template for all of my zone files.

After the name server and mail server records, the rest of a simple zone file typically consists of address (A) and canonical name (CNAME) records for hosts in the zone. Address records look like the following:

```
64bit      IN A      192.168.6.64
64x2       IN A      192.168.6.80
ubuntu32   IN A      192.168.6.90
```

Note that no period follows the short names I want the root name of the zone to be appended to them. No trailing period is necessary after the IP address.

Canonical name records look like the following and identify aliases for a host:

```
dualcore      IN      CNAME 64x2
```

No period follows the canonical name or name of the host that this record provides an alias for. CNAME records require two DNS lookups, for the name of the alias and a second to find out the IP address of the host that is an alias for, and so should be used sparingly. CNAME records are most commonly used to map generic server names such as www, ftp, and so on to a specific machine.

A sample, complete zone file for the domain vonhagen.org on one of my local name servers looks like the following:

```
$TTL 1d
@ 1d IN SOA ubuntu32.vonhagen.org. vwh.vonhagen.org. (
    2008090108 : Serial
    21600       : Refresh
    1800        : Retry
    604800      : Expire
    900         : Negative Cache TTL
)
@ IN NS ubuntu32.vonhagen.org.
@ IN MX 10 mail.vonhagen.org.

64bit      IN A      192.168.6.64
64x2       IN A      192.168.6.80
ubuntu32   IN A      192.168.6.90
mail       IN A      207.44.142.34

dualcore    IN      CNAME 64x2.vonhagen.org.
www        IN      CNAME mail.vonhagen.org.
tp        IN      CNAME:mail.vonhagen.org.
```