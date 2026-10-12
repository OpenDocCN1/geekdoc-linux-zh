```
#ifconfig -a
eth0
Link encap:Ethernet HWaddr 00:10:5A:28:5D:7C
inet addr:10.0.2.201 Bcast:10.0.2.255
Mask:255.255.255.0
UP BROADCAST RUNNING PROMISC MULTICAST MTU:1500 Metric:1
RX packets:822 errors:1 dropped:0 overruns:0 frame:1
TX packets:108 errors:0 dropped:0 overruns:0 carrier:0
collisions:10 txqueuelen:100
Interrupt:10 Base address:0xfc00
lo
Link encap:Local Loopback
inet addr:127.0.0.1 Mask:255.0.0.0
UP LOOPBACK RUNNING MTU:3924 Metric:1
RX packets:92 errors:0 dropped:0 overruns:0 frame:0
TX packets:92 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:0
ppp0
Link encap:Point-to-Point Protocol
POINTOPOINT NOARP MULTICAST MTU:1500 Metric:1
RX packets:0 errors:0 dropped:0 overruns:0 frame:0
TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:10
```

The -a option indicates that ifconfig should display all interfaces installed within the system regardless of their present configuration or operational state.

The example displayed above indicates that three interfaces are defined. The first, eth0, represents the physical hardware interfaces for 10MBs Ethernet using the 3Com Ethernet driver. The second, lo, is the loopback interface, primarily used for internal communication and diagnostics. The loopback interface can be used to determine if the TCP/IP software is operating correctly on a local level. For instance, it is possible to ping the loopback address to determine valid responses. The final (ppp0) interface represents a point-to-point dial-up link for connectivity to a local Internet Service Provider (ISP).

For each interface, the display includes the following fields:

Link encap: This specifies the link encapsulation protocol that the interface will use when transmitting datalink frames. Supported types include Ethernet, Local Loopback, and Point-to-Point Protocol.