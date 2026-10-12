```
Binary                     Decimal
    11000000.10101000.00000001.00001010 => 192.168.1.10
AND 11111111.11111111.11111111.10000000 => 255.255.255.128
    -----------------------------
    11000000.10101000.00000001.00000000 => 192.168.1.0
```

As you can see, the netmask 255.255.255.128 tells us that the given IP address belongs to the 192.168.1.0 network. Now see which network an IP address called 192.168.1.200 belongs to:

```
Binary                     Decimal
    11000000.10101000.00000001.11001000 => 192.168.1.200
AND 11111111.11111111.11111111.10000000 => 255.255.255.128
    -----------------------------
    11000000.10101000.00000001.10000000 => 192.168.1.128
```

As you can see again, the same netmask gives us a different network address (192.168.1.128) for the given IP address. Using this netmask, you have effectively separated the 192.168.1.0 networks into two subnets — 192.168.1.0 and 192.168.1.128.

Because a full class C network has 256 possible IP addresses, the separate subnets have 128 IP addresses. However, not all of them are ever usable as host (interface) IP addresses. In a full class C network such as 192.168.1.0 (with netmask 255.255.255.0), we use 192.168.1.0 as the network address and 192.168.1.255 as the broadcast address. We use a broadcast address to communicate with all host computers in the network, so these two addresses are in a sense reserved. Therefore, in a full class C network, you have 254 (255 – network IP address – broadcast IP address) possible IP addresses. Similarly, when a network is subdivided, each subnet gets a network address and a broadcast address; therefore, when a class C network is divided into two subnets, four IP addresses become unusable for host addressing. In our example, this looks like the following:

```
Network: 192.168.1.0
Netmask: 255.255.255.128
First usable host IP address: 192.168.1.1
Last usable host IP address: 192.168.1.126
Broadcast address: 192.168.1.127
```