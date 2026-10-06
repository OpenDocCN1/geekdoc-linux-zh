# 298 Chapter 16 IP Routing

![](bbox=[0.155, 0.068, 0.945, 0.312])

FIGURE 16-4 Assigning IP addresses to end systems and network interfaces in routers (example).

# 16.1.4 Forwarding Procedure

For a router, an IP packet received over a network interface falls into one of three categories, depending on its destination address:

The packet is addressed to the router: In this case, the packet is not forwarded, passed to a protocol instance of the transport layer in the router.

The packet is addressed to an end system in a neighboring network: Packets addressed to an end system in a network that is connected directly to the router can be forwarded directly to this end system. When the packet is passed to the data-link layer, the physical address of the destination system, which might have been discovered by the ARP protocol, is used. The packet is addressed to an end system in a remote network: If the destination system is not in a neighboring network, the packet has to be forwarded to an additional router. This router is identified by the forwarding information, and its physical address is used as destination towards the physical layer.

The first case is characterized by the fact that the IP destination address belongs to an internal network interface. The second case can be detected by AND-combining the destination address with the network masks of neighboring networks. If the result of this operation matches the network prefix of the respective network, then the destination system is in this network. The third case applies when none of the two previous conditions are true.

In practice, the second case can be conveniently covered by the mechanism used to identify the next router in the third case, and “rule-based routing” is implemented in the recent kernel versions of Linux, so that the first case is also handled in this way. (See Section 16.1.6.).

The exact procedure involved in identifying the next router for the third case is strongly linked to the data structure used to store the forwarding information in the router. This data structure will be discussed in the next section.