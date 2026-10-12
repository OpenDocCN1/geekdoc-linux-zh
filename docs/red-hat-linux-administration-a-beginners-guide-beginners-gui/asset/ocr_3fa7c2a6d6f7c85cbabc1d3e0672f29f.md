```
file "named.local";
};
```

This is the reverse entry for resolving the local host address back to the local host name. The **named.local** file contains the following:

```
$TTL 86400
@     IN  SOA    localhost. root.localhost. (
                                2002103100  ; Serial
                                28800       ; Refresh
                                14400       ; Retry
                                3600000     ; Expire
                                86400 )     ; Minimum

        IN      NS      localhost.

1           IN      PTR     localhost.
```

If this doesn’t make sense to you yet, don’t worry. Just know that this is enough for a caching server. The following sections will help you make sense of this file.

# # DNS Records Types

Okay, I kind of lied. You aren’t ready to create the **example.org.db** and **example.org.rev** files—not quite yet. First you need to understand all the record types for DNS: SOA, NS, A, PTR, CNAME, MX, TXT, and RP.

# ## SOA: Start of Authority

The SOA record starts the description of a site’s DNS entries. The format of this entry is as follows:

```
domain.com. IN SOA ns.domain.com. hostmaster.domain.com. (
0202112400      ; serial number
10800           ; refresh rate in seconds (3 hours)
1800            ; retry in seconds (30 minutes)
1209600         ; expire in seconds (2 weeks)
604800          ) ; minimum in seconds (1 week)
```

The first line contains some details we need to pay attention to:

+   * **domain.com.** is of course to be replaced with your domain name. Notice that last period at the end of domain.com.? It’s supposed to be there—indeed, the DNS configuration files are extremely picky about it. The ending period is necessary for the server to differentiate relative host names from fully qualified domain names (FQDNs); for example, to