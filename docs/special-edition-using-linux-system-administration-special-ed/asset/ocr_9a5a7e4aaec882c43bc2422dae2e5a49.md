Like the foo.edu zone file, this file contains an SOA record and at least one NS record.

In addition, it contains a series of PTR records, which define the IP addresses that can be used as pointers for reverse name lookup. The form of the PTR records is as follows:

```
<IP address>  IN  PTR  <host name>
```

Notice that the IP addresses are specified without the trailing dots. This makes them relative to the network for which the zone file provides reverse name lookup data. Therefore, the following entry:

```
3  IN  PTR  brain.foo.edu.
```

indicates that the IP address 192.168.1.3 points to the host brain.foo.edu.

The reverse name lookup file for the local loopback network, /var/named/127.0.0, is similar to the reverse lookup zone for foo.edu:

```
;
; File: zone.127.0.0
@       IN      SOA     fake.foo.edu.        hostmaster.foo.edu. (
                19960101401              ;Serial
                8H                       ;Refresh
                2H                       ;Retry
                1W                       ;Expire
                1D                       ;Minimum
        IN      NS      fake.foo.edu.
1       IN      PTR     localhost.
```

This file contains an SOA record, one or more NS records and one or more PTR records.

**STARTING** named  We are now ready to start named. In version 8 a new program called ndc has been introduced for managing and controlling named but you can still invoke named directly if you prefer. However, ndc provides a clean way of starting, stopping, and checking the status of named.

With the configuration file /etc/named.conf, and the zone files defined in /var/named, we can start named using ndc as follows:

```
# ndc start
```

Check /var/log/messages after you start named and make sure no errors are reported. If there are errors the log entries will give you an idea of what’s wrong. You will need to fix any errors you might have made in the configuration or zone files and restart named.

After it is started you can check the status of named with the command:

```
# ndc status
```

You can also stop named using the ndc command:

```
# ndc stop
```