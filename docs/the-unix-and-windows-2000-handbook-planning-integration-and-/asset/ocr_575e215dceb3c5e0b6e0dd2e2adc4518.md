take advantage of this feature. Also, make sure each PTR record ends with a period. Failure to include the period can and will cause problems with your DNS server.

> Failure to include a period at the end of a PTR record will cause inconsistencies in your DNS server and may be difficult to debug.

# Localhost Database File

With your forward and reverse files complete, you have enough host information to have a useful and functional DNS server. However, you as the astute reader at this point may ask, “How do I handle the loopback IP address of 127.0.0.1?” Since network 127.0.0 isn’t directly owned by anyone, you have to define this network yourself. While omitting this file may not cause problems, it is always best to take the time to define file db.127.0.0.

```
: 
:           db.127.0.0.in-addr.arpa
: 
@       IN      SOA     dns.sniglets.com. host-person.ee.gatech.edu. (
                        19970701      :Serial
                        10800     : Refresh
                        3600      : Retry
                        604800    : Expire
                        86400 )   : Minimum

                    IN      NS      dns.sniglets.com.
IN      NS                  duchess.sniglets.com.

1       IN      PTR      localhost.
```

As you can see, the only difference in the db.127.0.0 file is the following entry: