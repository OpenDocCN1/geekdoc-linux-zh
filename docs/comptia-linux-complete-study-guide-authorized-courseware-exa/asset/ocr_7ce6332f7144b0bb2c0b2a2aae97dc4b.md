When configured properly, ifConfig should show a hardware address ($\mathbb { H w a d d } \mathrm { r }$), an IP address ($\mathtt { i n e t }$ addr), and additional statistics. There should be few or no errors, dropped packets, or overruns for both received (RX) and transmited (TX) packets. Ideally, few (if any) collisions should occur, but some are unavoidable if your network uses a hub rather than a switch. If collisions total more than a few percent of the total transmitted and received packets, you may want to consider replacing a hub with a switch. To use route for diagnostic purposes, you might try the following:

```
# route
Kernel IP routing table
Destination Gateway  Genmask     Flags  Metric Ref    Use Iface
192.168.29.0 *       255.255.255.0 U      0      0      0  eth0
127.0.0.0   *       255.0.0.0     U      0      0      0  lo
default       192.168.29.1  0.0.0.0     UG     0      0      0  eth0
```

This shows that data destined for $1 9 2 . 1 6 8 . 2 9 . 0$ (that is, any computer with an IP address between $1 9 2 . 1 6 8 . 2 9 . 1$ and $1 9 2 . 1 6 8 . 2 9 . 2 5 4 )$ goes directly over eth0. The 127.0.0.0 network is a special interface that “loops back” to the originating computer. Linux uses this for some internal networking purposes. The last line shows the default route, which describes what to do with everything that doesn’t match any other entry in the routing table. This line specifies the default route’s gateway system as $1 9 2 . 1 6 8 . 2 9 . 1$. If it’s missing or misconfigured, some or all traffic destined for external networks, such as the Internet, won’t make it beyond your local network segment.

As with DHCP configuration, it’s almost always easier to use a GUI configuration tool to set up static IP addresses, at least for new administrators. The exact locations of the configuration files differ from one distribution to another, so the examples listed earlier may not apply to your system.

# Configuring Routing

As explained earlier, routers pass traffic from one network to another. You configure your Linux system to directly contact systems on the local network. You also give the computer a router’s address, which your system uses as a gateway to the Internet at large. Any traffic that’s not destined for the local network is directed at this router, which passes it on to its destination. In practice, there are likely to be a dozen or more routers between you and most Internet sites. Each router has at least two network interfaces and keeps a table of rules concerning where to send data based on the destination IP address. Your own Linux computer has such a table, but it’s probably very simple compared to those on major Internet routers.

Linux can function as a router, which means it can link two or more networks together, directing traffic between them on the basis of its routing table. This task is handled, in part, by the route command. This command can be used to do much more than specify a