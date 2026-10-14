```
zone "." in {
    type hint;
    file "db.cache"
};

zone "0.0.127.in-addr.arpa" in {
    type master;
    file "db.0.0.127.in-addr.arpa"
};

zone "sniglets.com"    in {
    type master;
    file "db.sniglets";
};

zone "3.168.192.in-addr.arpa" in {
    type master;
    file "db.3.168.192.in-addr.arpa"
};
; end for named.boot
```

The options directive provides a single entry to specify program options to named. For our example, the only option we have specified is database directory /var/named. The zone directive, coupled with the type master, replaces the primary directive in the BIND 4 named.boot. While in this case the migration from BIND 4 to BIND 8 is rather straightforward and obvious, for complicated BIND 4 DNS installations, porting the named.boot file by hand is quite difficult. Programs are available to automatically convert BIND 4 to BIND 8, so be sure to do your homework before you attempt a major DNS upgrade.