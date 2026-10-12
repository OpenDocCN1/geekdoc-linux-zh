# **4.2 The historical IP address classes**

TCP/IP routing views any IP address as two parts – *a network part* and *a host part*:

+   • the network part of the address identifies the network the machine is connected to
+   
+   • the rest of the address – the host part – identifies the particular machine on that network.

Routing on your machine uses the network part to decide whether the destination machine is on the same network as your own. If the network part of the destination address is the same as the network part of your own address, then the two machines are locally connected; otherwise they’re not.

Historically, TCP/IP used *address classes* to decide how to extract the host and network parts. Addresses are divided into five classes, A, B, C, D, and E.

+   • D is used for multicasting (see Module 4.11)
+   
+   • E is reserved and not yet used
+   
+   • A, B, and C, which are all we are concerned with here, are used for normal addresses.

The class an IP address belongs to is determined by its top few bits, as shown in Figure 4.2. Just by looking at these bits TCP/IP can tell immediately from an address which class it belongs to, so class-based routing decisions can be processed quickly in the routing code.

![](bbox=[0.1, 0.45, 0.95, 0.64])

**Figure 4.2** The IP address classes

Because a specific number of bytes or bits is used for network/host parts in each class, it follows automatically how many networks of each type there are, and how big each of them is (Table 4.1).

**Table 4.1** Network types and sizes

|   | Address range | Network part | Number of networks | Host part | No. hosts per network |
|---|---|---|---|---|---|
| A | 0.0.0.0–127.255.255.255 | 1 + 7 bits | 128 | 24 bits | 16,777,216 |
| B | 128.0.0.0–191.255.255.255 | 2 + 14 bits | 16,384 | 16 bits | 65,536 |
| C | 192.0.0.0–223.255.255.255 | 3 + 21 bits | 2,097,152 | 8 bits | 256 |