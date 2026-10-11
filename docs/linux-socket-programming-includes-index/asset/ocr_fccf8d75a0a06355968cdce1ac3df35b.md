| Class | Address | Address Range, Description |
| :--- | :--- | :--- |
| D | 224.0.0.0 to 239.255.255.255 | 2^23—2 or 268,435,454 nodes. These addresses are not allocated but are reserved for multicasting addresses. |
| E | 240.0.0.0 to 255.255.255.255 | 2^23—2 or 268,435,454 nodes. These are reserved for future use. Please note that 255.255.255.255 is a general broadcast IP address. It is never a legal address. |

The network classes are numbered peculiarly, because the addressing uses the first bits of the address to determine the class. For example, the Class A network has a zero in the first bit of the address. Likewise, the Class B has a one in the first bit and a zero in the second bit:

+   Class A: 0 (0000,0000) to 126 (0111,1110)
+   Class B: 128 (1000,0000) to 191 (1011,1111)
+   Class C: 192 (1100,0000) to 223 (1101,1111)
+   Class D: 224 (1110,0000) to 239 (1110,1111)
+   Class E: 240 (1111,0000) to 255 (1111,1111)

Using this approach historically, the routers on the network can quickly determine (within four bits) whether to let the message enter the gate. Today the routing is more efficient, using Classless Internet Domain Routing (CIDR). These new definitions (found in RFCs 1517–1519) identify the location and route of a host using the upper bits of the address.

The IP protocol introduced this numbering scheme for computer identification to cluster these computers in an efficient way. With it, a router can quickly determine whether to block a packet or move it to the interface that leads to the destination subnet. Propagation is very important: Simply receiving a packet, checking it, and passing it on is not acceptable. Each bit that the router accepts means a delay on the network. The router must delay no more bits than necessary to determine the relevance. In other words, it must be invisible to propagation delays. For example, typical telephone switching in the United States of America does not try to resolve the whole phone number at once; the first three digits indicate an area or region, and the next three digits indicate the station.

# Subnetwork Masks

Some of the classes require more filtering. A network with 16 million nodes is excessive if all are clumped in one space. As you set up your Linux computer and configured the network, you may have noticed the term subnet mask. The introduction of CIDR has helped to simplify the complexity of large subnets [RFC950].