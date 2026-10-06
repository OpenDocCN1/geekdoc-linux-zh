# C.6 Using traceroute to Trace Packets 583

You can use traceroute to identify the route that packets actually take to the specified computer (host). Within local area networks, the path is only one hop, because the communication peer itself is within this LAN—it is simply the next hop. In contrast, the communication relationships in larger networks (e.g., in the Internet) can use larger routes (as in the accompanying example).

Another benefit of traceroute is that it is suitable for analyzing connection problems. For example, if a computer in the Internet is not reachable, you can use traceroute to list all reachable routers on the path to this computer. If one of the intermediate systems does not respond, it is easy to find the source of error.

To identify a router on the way to the desired computer, traceroute applies a trick rather than using the IP option record route. Specifically, it creates IP packets with the destination address of the specified computer and sends these packets to that computer. The trick is that the TTL value in the IP header is initially set to one. This is dropped in the first router, because its maximum time to live (TTL) has expired. According to the IP standard, the router has return an ICMP message to the sender. From this ICMP message, the sender learns the IP address of the router and can identify the first switching node. This method is repeated—each time with a TTL value of one—until the destination is reached.

Example: Connection in a LAN—Direct Connected Station

```
root@tux # traceroute www
troute to www.linux-netzwerkarchitektur.de (129.13.42.100),
30 hops max, 40-byte packets
1 www.linux-netzwerkarchitektur.de (129.13.42.100) 13 ms 9 ms 9 ms
```

Example: Connection in the Internet

```
root@tux # traceroute www.tux.org
troute to www.tux.org (207.96.122.8), 30 hops max. 40 Byte packets
1 router1.linux-netzwerkarchitektur.de (129.13.42.244) 20 ms 20 ms 20 ms
2 141.3.1.1 (141.3.1.1) 10 ms 10 ms 10 ms
3 Karlsruhe.Belwue.de (129.143.167) 10 ms 10 ms 10 ms
4 ZR-Karlsruhe.Win-IP.DFN.de (188.1.174.1) 30 ms 30 ms 30 ms
5 ZR-Hannover1.Win-IP.DFN.de (188.144.177) 30 ms 30 ms 30 ms
6 IR-York-1.Win-IP.DFN.de (188.144.186) 80 ms 130 ms 290 ms
7 dfn.ny1.dyante.net (212.1.200.65) 60 ms 120 ms 270 ms
8 * * *
9 A0ITM3-0.XR2.NYC4.ALTER (152.63.22.6) 280 ms 270 ms 120 ms
10 ATM2-0-00.BR1.EWR1.ALTER (146.188.176) 260 ms 280 ms 290 ms
11 UUET-EWR-1-PEER.cw.net (137.39.23.66) 280 ms 140 ms 130 ms
12 corouter1.WestOrange.cw.net (204.70.9.138) 290 ms 290 ms 130 ms
13 core4.Washington.cw.net (204.70.4.105) 290 ms 290 ms 230 ms
14 fe0-1-0.gwl.spa.rcn.net (207.172.0.5) 140 ms 300 ms 270 ms
15 gwyn.tux.org (207.96.122.8) 160 ms 270 ms 270 ms
```