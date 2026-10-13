their own types of addresses.

+   - A unicast address is used for a packet that is sent to a single destination.
+   - A anycast address is used for a packet that can be sent to more than one destination.
+   - A multicast address is used to broadcast a packet to a range of destinations.

In IPv6, addressing is controlled by the format prefix that operates as a kind of address type. The format prefix is the first field of the IP address. The three major kinds of unicast network addresses are global, link-local, and site-local. Global, site-local, and link-local are indicated by their own format prefix (see Table 38-6).

Global addresses begin with the address type 3, site local with FEC, and link-local with FE8.

Global addresses can be sent across the Internet.

Link-local addresses are used for physically connected systems on a local network.

Site-local can be used for any hosts on a local network. Site-local addresses operate similarly to IPv4 private addresses, but are used only for local access and cannot be used to transmit over the Internet.

Table 38-6: IPv6 Format Prefixes and Reserved Addresses

| IPv6 Addresses Format Prefixes and Reserved Addresses | Description |
|---|---|
| 3 | Unicast Global Addresses |
| FE8 | Unicast link-local addresses, used for physically connected hosts on a network |
| FEC | Unicast Site-local addresses, comparable to IPv4 private addresses |
| 0000000000000001 | Unicast Loopback address (for system self-communication, localhost) |
| 0000000000000000 | Unspecified address |
| FF | Multicast Addresses |

In addition, IPv6 has two special reserved addresses. The address 0000000000000001 is reserved for the loopback address used for a system's localhost address, and the address 0000000000000000 is the unspecified address.

# IPv6 Unicast Global Addresses

IPv6 global address currently uses four fields: the format prefix, a global routing prefix, the sub-net identifier, and the interface identifier. The format prefix for a unicast global address is 3 (3 bits). The global routing prefix references the network address (45 bits), and the sub-net id references a subnet within the site (16 bits).

# IPv6 unicast Local Use Addresses: Link-local and Site-local Addresses

For local use, IPv6 provides both link-local and site-local addresses. Link-local addressing is used for interfaces (hosts) that are physically connected to a network. This is usually a small local network. A link-local address uses only three fields: the format prefix FE8 (10 bits), an empty field (54 bits), and the interface identifier (host address) (64 bits). In effect, the network section is empty.

IPv6 site-local addresses have three fields: the format prefix (10 bits), the sub-net identifier (54 bits), and the interface identifier (64 bits). Except for any local subnetting, there is no network address.

# IPv6 Multicast Addresses

Multicast addresses have a format prefix of FF (8 bits) with flag and scope fields to indicate whether the multicast group is permanent or temporary and whether it is local or global in scope. A group identifier (112 bits) references the multicast group. For the scope, 2 is link-local, 5 is site-local, and E is global. In addition