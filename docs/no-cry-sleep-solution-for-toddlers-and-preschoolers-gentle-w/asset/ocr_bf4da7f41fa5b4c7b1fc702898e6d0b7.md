```
UP BROADCAST LOOPBACK RUNNING MTU:2000 Metric:1
RX packets:0 errors:0 dropped:0 overruns:0
TX packets:12 errors:0 dropped:0 overruns:0
```

# Routing

A packet that is part of a transmission takes a certain route to reach its destination. On a large network, packets are transmitted from one computer to another until the destination computer is reached. The route determines where the process starts and to what computer your system needs to send the packet for it to reach its destination. On small networks, routing may be static—that is, the route from one system to another is fixed. One system knows how to reach another, moving through fixed paths. On larger networks and on the Internet, however, routing is dynamic. Your system knows the first computer to send its packet off to, and then that computer takes the packet from there, passing it on to another computer, which then determines where to pass it on. For dynamic routing, your system needs to know little. Static routing, however, can become complex because you have to keep track of all the network connections.

Your routes are listed in your routing table in the /proc/net/route file. To display the routing table, enter route with no arguments (the netstat -r command will also display the routing table):

```
# route
Kernel routing table
Destination Gateway Genmask Flags Metric Ref Use Iface
loopback * 255.0.0.0 U 0 0 12 lo
pangol.train.com * 255.255.255.0 U 0 0 eth0
```

| Option | Description |
|---|---|
| Interface | Name of the network interface, such as eth0 for the first Ethernet device or ppp0 for the first PPP device (modem) |
| up | Activates an interface; implied if IP address is specified |
| down | Deactivates an interface |
| allmulti | Turns on or off the promiscuous mode; preceding hyphen (-) turns it off; this allows network monitoring |
| mtu n | Maximum number of bytes that can be sent on this interface per transmission |
| dstaddr address | Destination IP address on a point-to-point connection |
| netmask address | IP network mask; preceding hyphen (-) turns it off |
| broadcast address | Broadcast address; preceding hyphen (-) turns it off |
| point-to-point address | Point-to-point mode for interface; if address is included, it is assigned to remote system |
| hw | Sets hardware address of interface |
| Address | IP address assigned to interface |

TABLE 38-11 The Ifconfig Options