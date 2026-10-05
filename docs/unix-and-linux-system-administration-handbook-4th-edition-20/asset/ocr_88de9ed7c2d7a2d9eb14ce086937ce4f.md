# Packet forwarding: a closer look

handled as a special case. eth0 is host A's Ethernet interface, and lo is the loopback interface, a virtual interface emulated in software. Entries such as these are nor-added automatically by ifconfig when a network interface is configured.

Some systems treat the loopback route as a "host route" to one particular IP address rather than an entire network. 127.0.0.1 is the only IP address that will ever exist on the loopback network, it doesn't matter how it's defined. The only changes would be in the routing table where the destination clause instead of 127.0.0.0 and an h in the Flags column.

There is no substantive difference between a host route and a network route. They are treated exactly as when the kernel goes to look up addresses in the routing table; only the implicit is default.

The default route on host A forwards all packets not addressed to the loopback address or to 199.165.145 network to the address on this network is 199.165.145.24. The G flag indicates that this route goes to a gateway, not one of A's local interfaces. Gateways must be only one hop away.

Suppose a process on A sends a packet to B, whose address is 199.165.146.4. The IP implementation looks for the target network, 199.165.146, but none of the routes match. The default route is invoked and the packet is forwarded to R1. Exhibit B shows the packet that actually goes out on the Ethernet (the addresses in the Ethernet header are the MAC addresses of A and R1's interfaces on 145 net).

# Exhibit B Ethernet packet

| Ethernet header | IP header | UDP header and data |
|---|---|---|
| From: A | From: 199.165.145.17 | 11001010101010101101101010101010 |
| To: R1 | To: 199.165.146.4 | 01110110101110111010001010000010 |
| Type: IP | Type: UDP | 01011111110110111010101110100000 |

The Ethernet destination hardware address is that of router R1, but the IP packet hidden within the Ethernet frame does not mention R1 at all. When R1 receives the packet it has received, it sees from the IP destination address that it is not the ultimate destination of the packet. It then uses its own routing table to forward the packet to host B without rewriting the IP header; the header still shows the packet coming from A.