# Configure DHCP Pools and Failover

On the secondary server, the corresponding messages look like:

```
Jul 4 12:00:20 da12 dhcpcd: DHCPREQUEST for 149.44.85.16 from 00:04:ac:d6:58:96 via eth1: ignored (not authoritative).
Jul 4 12:00:25 da12 dhcpcd: DHCPREQUEST for 149.44.85.16 from 00:04:ac:d6:58:96 via eth1: ignored (not authoritative).
Jul 4 12:00:30 da12 dhcpcd: pool 800e40f8 10.0.0.111 total 20 free 10 backup 10 its 0
Jul 4 12:00:30 da12 dhcpcd: DHCPDISCOVER from 00:04:ac:d6:58:96 via eth1
Jul 4 12:00:31 da12 dhcpcd: DHCPOFFER on 10.0.0.111 to 00:04:ac:d6:58:96 (linux-5ncs) via eth1
Jul 4 12:00:31 da12 dhcpcd: DHCPREQUEST for 10.0.0.111 (10.0.0.111) from 00:04:ac:d6:58:96 (linux-5ncs) via eth1
Jul 4 12:00:31 da12 dhcpcd: DHCPACK on 10.0.0.111 to 00:04:ac:d6:58:96 (linux-5ncs) via eth1
```

On this server, the DHCPOFFER message is printed as this server offers the IP address. The final message is DHCPACK from the client.