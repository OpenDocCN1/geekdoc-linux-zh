reverse DNS service themselves, which is why you always need to have a
special zone statement in your /etc/named.conf file that looks like the
following:

```
zone "0.0.127.in-addr.arpa" {
type master;
file "named.local";
};
```

You also must have the named.local zone file in the working directory
of your nameserver. This file is shown in Listing 8-4.

# **Listing 8-4** *The named.local file*

```
@ IN SOA localhost. root.localhost. (
```

```
1999020100 ; Serial
```

```
7200 ; Refresh - 2 hours
```

```
3600 ; Retry - 1 hour
```

```
43200 ; Expire - 12 hours
```

```
3600 ) ; Minimum - 1 hour
```

```
IN NS localhost.
```

```
1 IN PTR localhost.
```

# Configuring a cache-only/slave DNS server

Technically, all DNS servers are cache-enabled; in other words, DNS
servers use cache by default. However, if you don't want to provide DNS
service for any Internet domains and desire only to improve DNS query
performance for your network, you can run a cache-only DNS server. Such
a server will have an /etc/named.conf file, as shown in Listing 8-5.

# **Listing 8-5** *A cache-only DNS server's /etc/named.conf file*

```
zone "" {
```

```
type hint;
```

```
file "named.ca";
```

```
};
```