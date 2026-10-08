# 492 CONFIGURATION AND OPERATION OF A NAME SERVER

current localhost. This file consists of only a few entries which are important if users also want to use the entry localhost in their ~/hosts files.

```
@ IN SOA carrot.example.org. hostmaster.example.org.
    1986020101 ; Serial
    3600 ; Refresh
    300 ; Retry
    360000 ; Expire
    14400 ); Minimum
IN NS carrot.example.org.
0 IN PTR loopback.
0 IN PTR localhost.
```

Listing 20.15 The file named.local.

# 20.9 The file named.rev

The file named.rev stores the computer names belonging to given IP addresses. This makes it relatively quick and easy to find a corresponding name for an IP address; this function is also reverse lookup. The file named.rev is stored in Masterfile format. An example is shown in Listing 20.16.

Some people generate both from an external database by means of perl or awk script. In any case you may want to use a program like nslookup that checks your zones in detail.

```
@ IN SOA carrot.example.org. hostmaster.example.org.
    1986020501 ; Serial
    10800 ; Refresh 3 hours
    3600 ; Retry 1 hour
    360000 ; Expire 1000 hours
    86400 ); Minimum 24 hours
IN NS carrot.example.org.
0.0 IN PTR carrot.example.org.
IN PTR A example.org.255.255.255.0
151.31 IN PTR corn.example.org.
155.31 IN PTR pea.example.org.
```

Listing 20.16 The file named.rev.

Please note that you must terminate each host name with a dot. Otherwise, the domain in-addr.arpa would be automatically appended. Also, you should ensure consistency between the files named.data and named.rev.