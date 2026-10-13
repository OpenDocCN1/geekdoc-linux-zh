These four times—refresh, retry, expire, and TTL—give you a good indicator of how long it will take a DNS change to propagate through the Internet. Remember that in the instant before you did a restart, a secondary might have refreshed. If, just before the secondary came back to the primary to refresh (3 hours later), a foreign DNS query returned the old value with the TTL, it might be more than 27 hours from the change before the change propagates out. This is assuming, too, that the secondary had no problems connecting to the primary at its first refresh.

> **Tip**  
> The entire SOA entry (minus comments and parentheses) can be put on one line, but it is best to follow the preceding template because the order of the values is important.

# db FILE ENTRIES

Each db file has entries that correspond to hosts in the domain. The first entries look like the following:

```
bar.org.    IN NS foo.bar.org.
bar.org.    IN NS baz.bar.org.
```

These entries are the name servers for this domain. Again, note the trailing . on each entry.

The next RR that is found in the db file is the A or address record. These appear as follows:

```
foo.bar.org.        IN A 192.168.0.1
;
baz.bar.org.        IN A 192.168.0.2
baz.bar.org.        IN A 192.168.10.90
;
baz2.bar.org.       IN A 192.168.0.2
baz90.bar.org.      IN A 192.168.10.90
```

Nothing is special about the first entry. The host baz either has two Ethernet cards, each on a different network, or one card with two addresses on different networks. This host is what's known as a multihomed host. You can use comments with blank lines to separate parts of the file. A good recommendation is to separate multihomed hosts from those with only one address. The same separation can be used for other sections. This just makes it easier to read and troubleshoot.

The last two entries are additional names that each map specifically to only one interface of the multihomed host. These entries are here because a lookup on baz.bar.org returns both addresses—you can't pick out the one that you want to ping specifically for debugging. Therefore, additional entries exist for each interface that are particular to only one interface. This is especially useful for routers that might have several NICs.

The next RR of interest is the CNAME. This is used to map aliases to A records as follows:

```
www.bar.org.    IN CNAME foo.bar.org.
ftp.bar.org.     IN CNAME baz.bar.org.
```

Note that, because host baz has more than one address, you'll want to either make sure that FTP is binding all addresses or have ftp.bar.org point to a specific interface. Using the