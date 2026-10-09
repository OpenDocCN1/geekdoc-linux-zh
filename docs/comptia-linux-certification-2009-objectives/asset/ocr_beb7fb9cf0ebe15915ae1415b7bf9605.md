+   2.  Enter the TTL directive and the SOA record for the forward zone.

+   a.  Enter $TTL 86400 to specify it as the TTL value.
b.  Type @ and press Tab.
c.  Type IN and press Tab.
d.  Type SOA and press Tab.
e.  Enter srvA.ourglobalcompany.com. root.srvA.ourglobalcompany.com. ( 
f.  Enter 1001 as the serial number for the zone file.
g.  Enter 28800 as the length of the refresh cycle.
h.  Enter 7200 as the length of the retry cycle.
i.  Enter 3600000 as the time for which slave server can respond to queries without updating its zone file.
j.  Enter 86400 as the default TTL for negative caching servers.
k.  Enter ) to complete the SOA record.

See Code Sample 1.

# Code Sample 1

```
$TTL  86400
@       IN      SOA     srvA.ourglobalcompany.com. root.srvA.ourglobalcompany.com. (
                1001
                28800
                7200
                3600000
                86400
                )
```