identifier, and a 64-bit interface identifier associated with a network adapter hardware address. Link-local unicast addresses include a 10-bit prefix, 54 zeros, and the same 64-bit interface identifier. Link-local unicast addresses are not routable.

+   - **Multicast** A multicast address is used to send a message to multiple network adapters simultaneously. The organization of a multicast address varies.
+   - **Anycast** An anycast address is used to send a message to one of several optional network adapters. It's useful for systems with multiple backups, such as a group of Web servers. Anycast addresses have the same basic organization as a unicast address.

With that diversity of address formats, IPv4-style broadcast addresses aren't used. Instead, IPv6 addressing uses multicast addressing for the purpose. IPv6 addresses are also organized in a number of different ranges, as described in Table 3-3. The default IPv6 address is sometimes also listed as ::/128.

# How to Define a Network with IP Addresses

Three key IP addresses define a network: the network address, the broadcast address, and the subnet mask. The network address is always the first IP address in a range; the broadcast address is always the last address in the same range. The subnet mask helps your computer define the difference between the two addresses. You can assign IP addresses between the network and broadcast addresses (not including these addresses) to any computer on the network.

> *A subnet mask is also known as a network mask or netmask. An example of an IPv4 netmask is 255.255.255.0. An example of an IPv6 netmask is /64.*

![](bbox=[0.07, 0.75, 0.18, 0.88])

TABLE 3-3
IP Address Classes

| Address | Description |
|---|---|
| ::1 | Loopback address |
| :: | Default address |
| ::ffff:0000:0000 | IPv4 mapped IPv6 addresses in the last 8 zeros |
| fe80:: | Link-local addresses; no routing between networks |
| fec0:: | Site-local addresses, for a single network |
| ff:: | Multicast addresses |
| 2000:: | Global unicast addressees are routable |