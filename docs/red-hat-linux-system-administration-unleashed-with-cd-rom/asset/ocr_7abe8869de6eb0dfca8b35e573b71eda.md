Switches can also reduce a network's vulnerability to certain security problems. A host or hub on a given port of a switch is on its own Ethernet; this makes it considerably harder for would-be attackers to snoop on data being transmitted using trace tools. Such data could include passwords or other sensitive data, for example. Obviously, the advantages of this approach are limited if several hosts are placed on a switched Ethernet segment using a hub, but switches are nonetheless particularly beneficial for multi-user machines.

# Using Switches

When should you use a switch? In many environments, the increased flexibility of switched Ethernet is unnecessary, and would be wasted. However, if you start seeing many collisions on a network, it is well worth examining the situation carefully. Under Linux, you can use the ifconfig command to check how many collisions have been detected on a network. Listing 14.1 shows some sample output.

# LISTING 14.1 Using ifconfig to Examine Ethernet Collisions

```
$ ifconfig eth0
eth0 Link encap:Ethernet HWaddr 00:E0:98:04:37:59
inet addr:192.168.1.1 Bcast:192.168.1.255 Mask:255.255.255.0
UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
RX packets:455299 errors:6 dropped:0 overruns:0 frame:25
TX packets:403376 errors:14 dropped:0 overruns:0 carrier:14
collisions:7004 txqueuelen:100
Interrupt:10 Base address:0x300
```

In this case, there have been 7004 collisions, out of 403,376 packets transmitted (TX), giving a collision rate of slightly under 2%. I know from experience that this rate is considerably higher than normal for this network. In this instance, it's a direct result of running several concurrent flood-pings (that is, sending ICMP Echo Request packets as fast as possible) specifically to acquire some interesting data on Ethernet collisions. In general, collision rates below 5% are nothing to worry about. If collision rates above 5% are seen consistently, and among a broad sampling of hosts on the network, it may well be time to consider splitting the network with a switch.

# Choosing Ethernet Media

Which type of physical Ethernet media should you choose when setting up a new network? Each type has advantages and disadvantages.