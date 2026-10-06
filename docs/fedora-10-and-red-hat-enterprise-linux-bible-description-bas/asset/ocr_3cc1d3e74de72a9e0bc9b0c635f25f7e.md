# Chapter 25: Making Servers Public with DNS 979

# Setting up the zone files (reverse lookup)

The other new file in the example is the yourlan.db file, which contains the information necessary to perform reverse IP lookups for the computers on your LAN. Here's an example:

```
STTL    86400
IN      SOA nsl.yourdomain.com hostmaster.yourdomain.com. (
                2006042701 : Serial
                28800 : Refresh
                0 : Retry
                360000 : Expire
                86400 ) : Minimum
IN      NS    nsl.yourdomain.com.
IN      PTR yourdomain.com.
IN      PTR red.yourdomain.com.
IN      PTR blue.yourdomain.com.
IN      PTR green.yourdomain.com.
IN      PTR yellow.yourdomain.com.
; EOCF
```

The SOA record identifies 0.0.10.in-addr.arpa, as the start of the zone. The NS lines define 0.0.10.in-addr.arpa, as the name server for the zone. Other records are pointers to hostnames that reverse-map on the 10.0.0. network. The records represent the address of the DNS server (yourdomain.com) and each of the clients on the LAN (red, blue, green, and yellow).

After you finish your zone files, you can use the named-checkzone command to make sure that each zone file is formed correctly. Here is how you'd run the named-checkzone command (as root user) to check the two yourdomain.com zone files (be sure to type each command on one line, even though is shown here):

```
# named-checkzone yourdomain.com
/var/named/chroot/var/named/db.yourdomain.com.inside
zone zone.com/IN: loaded serial 2008042701
# named-checkzone yourdomain.com
/var/named/chroot/var/named/db.yourdomain.com.outside
zone zone.com/IN: loaded serial 2008042701
```

The output indicates that both files are ok and named-checkzone command is able to load the new serial numbers. In this case, the serial number represents the first serial number (01) on April 27, 2008 (2008042701).

NOTE: Instead of using the named-checkzone command, you can use the named-compilezone. The difference between the two commands is that named-compilezone dumps the zone contents into a file you choose.