# Linux Hack

Ajay Kumar Tiwari

# Display Active Connections with Process ID and Program Name

This could be very helpful to identify which program has initiated a specific network connection.

```
# netstat -tap
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local AddressForeign
AddressStatePID/Program name
tcp00 *:nrpe*:*
LISTEN16277/xinetd
tcp00 localhost.localdomain:smtp *:*
LISTEN7263/sendmail: acce
tcp340 localhost.localdomain:54221
localhost.localdomain:4089 CLOSE_WAIT 29881/httpd
tcp03216 dev-db:sshcpe-76-
94-215-154.soca:4682 ESTABLISHED 11717/sshd: ramesh
```

# Display Routing Table

```
# netstat —route
Kernel IP routing table
DestinationGateway
Window irtt Iface
192.168.1.0*
0 eth0
162.244.0.0*
0 eth0
default192.168.1.1
0 eth0
Genmask
255.255.255.0
255.255.0.0
0.0.0.0
U
```