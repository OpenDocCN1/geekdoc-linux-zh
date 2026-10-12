**Gateway Address** (or **Gateway**): if this is different from the **Interface** field, this route is using the router specified in the **Gateway Address** field (and would have a **G** flag on Linux). Otherwise (i.e. the same as the **Interface** field) this is a route for something that’s connected directly, not forwarded via a router. If the gateway is 127.0.0.1, the route refers to one of my own addresses – talking to myself. The interface will also be 127.0.0.1.

**Metric**: you can ignore this (see **Notes**).

It’s easier to understand the listing reading it line by line, and from bottom to top:

```
255.255.255.255  255.255.255.255  192.168.20.22  192.168.20.22  1
```

the limited broadcast address (Module 4.10) reachable on the local wire via our single (real) interface, IP address 192.168.20.22

```
224.0.0.0  224.0.0.0  192.168.20.22  192.168.20.22  1
```

multicast addresses (Module 4.11). Forget about this entry.

```
192.168.20.255  255.255.255.255  192.168.20.22  192.168.20.22  1
```

broadcast address for our specific network, again reachable directly on our single real interface, 192.168.20.22. (NT derives this from the historical address class of the IP address. If your network isn’t an exact class A, B, or C, the **Network Destination** shown here will not be what you expected. For example, for 192.168.20.150 netmask 255.255.255.224 you’d expect a broadcast address of 192.168.20.191 but you get 192.168.20.255. On the other hand, when NT actually broadcasts, it uses the correct broadcast address, 192.168.20.191)

```
192.168.20.22  255.255.255.255  127.0.0.1  127.0.0.1  1
```

my own IP address. I can contact this by sending packets to 127.0.0.1, which is my loopback address, i.e. this is talking to myself

```
192.168.20.0  255.255.255.0  192.168.20.22  192.168.20.22  1
```

The range of 256 addresses making up the network on my wire. I can contact these directly, using **ARP** if necessary, sending out on my single interface 192.168.20.22

```
127.0.0.0  255.0.0.0  127.0.0.1  127.0.0.1  1
```

My loopback address, talking to myself again

```
0.0.0.0  0.0.0.0  192.168.20.254  192.168.20.22  1
```

As we saw with Linux, this range includes all possible IP addresses, so this line represents my default gateway router, with address 192.168.20.254, reached via my 192.168.20.22 interface.

In the next module we explain how to create and delete routes on Windows.