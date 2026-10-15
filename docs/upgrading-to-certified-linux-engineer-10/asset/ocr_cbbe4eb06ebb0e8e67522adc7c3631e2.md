When a client requests an IP address, you will see messages like this in /var/log/messages:

```
Jul 4 11:59:26 dal0 dhcpd: DHCPREQUEST for 192.168.5.16 from 00:04:ac:d6:58:96 via eth0: ignored (not authoritative).
Jul 4 11:59:30 dal0 dhcpd: DHCPREQUEST for 192.168.5.16 from 00:04:ac:d6:58:96 via eth0: ignored (not authoritative).
Jul 4 11:59:36 dal0 dhcpd: pool 800e4138 10.0.0/24 total 20 free 10 backup 10 its 0
Jul 4 11:59:36 dal0 dhcpd: DHCPDISCOVER from 00:04:ac:d6:58:96 via eth0
Jul 4 11:59:36 dal0 dhcpd: DHCPREQUEST for 10.0.0.111 (10.0.0.12) from 00:04:ac:d6:58:96 via eth0: lease owned by peer
Jul 4 11:59:37 dal0 dhcpd: DHCPOFFER on 10.0.0.110 to 00:04:ac:d6:58:96 (linux-5ncs) via eth0
```

In this case, the client send a DHCPREQUEST in order to get same the IP address as the last time (192.168.5.16). This address is not available from a range definition, so the server refuses to offer this address. The the client send a DHCPDISCOVER to detect a DHCP server.

The next message from the client is a DHCPREQUEST for the IP address 10.0.0.111, this address is provided from the secondary server ("lease owned by peer"). The last message is the DHCPOFFER from the secondary server.