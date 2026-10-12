record. The data includes the name of the primary name server (in this case, @ or the current domain), the e-mail address of the technical contact, and five different times enclosed in parentheses.

The NS record specifies the authoritative name servers for a zone. A typical NS record looks like the following:

```
. 3600000 IN NS A.ROOT-SERVERS.NET.
```

In this case, the NS record lists the authoritative name server for the root zone (notice that the name of the first field is a single dot). The Time-To-Live field specifies the record to be valid for 1,000 hours (3,600,000 seconds). The class is IN, for Internet; and the record type is NS. The final field lists the name of the name server (A.ROOT-SERVERS.NET.), which ends with a dot.

An A record specifies the address corresponding to a name. For example, the following A record shows the address of A.ROOT-SERVERS.NET. as 198.41.0.4:

```
A.ROOT-SERVERS.NET. 3600000 A 198.41.0.4
```

In this case, the network class isn't specified because the field is optional, and the default is IN. PTR records are used for reverse mapping — converting an address to a name. Consider the following example:

```
1 IN PTR localhost.
```

This record comes from a file for a zone named 0.0.127.in-addr.arpa. Therefore, this record says that the name associated with the address 127.0.0.1 is localhost. An MX record specifies the name of a host that accepts mail on behalf of a specific domain. For example, here's a typical MX record: naba IN MX 10 mailhub.lnbsoft.com. This says that mail addressed to the host named naba in the current domain should be sent to mailhub.lnbsoft.com (this host is called a mail exchanger). The number 10 is the preference value. For a list of multiple MX records with different preference values, the ones with lower preference values are tried first. Armed with this bit of information about resource records, you can go through the zone files for the caching name server.