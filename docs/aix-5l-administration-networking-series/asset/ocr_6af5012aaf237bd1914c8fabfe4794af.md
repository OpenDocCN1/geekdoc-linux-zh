# ## IPv6 Addressing

IP version 6 is the new version of the Internet Protocol. Currently, it is used mostly for experimental purposes, either on private networks or on a global network called the $\mathbf{\Phi}$bone. However, its popularity is increasing, and it is beginning to be used on production networks.

The IPv6 address is a 128-bit number represented as eighteen 16-bit hexadecimal fields separated by colons. A short syntax is allowed to represent multiple adjacent fields of zero as “::” only once in the address and to omit leading insignificant zeros within each field.

It is common for interfaces to have multiple IPv6 addresses—for example, one that is valid only for communication on the local network link and one that is global. This concept is called address scope.

IPv6 also defines two types of addresses that are used for compatibility with IPv4. The first type has a prefix of 0:0:0:0:0:ffff:/96. The final 32 bits of the address will be an IPv4 address. This type of address is used simply to represent an IPv4 address in IPv6 format and is called an IPv4 mapped address. The other type of address has a prefix of 0:0:0:0:0:0:/96. The final 32 bits will again be an IPv4 address. This is called an IPv4- compatible address and is used for IPv6 automatic tunneling. Automatic tunneling is used for IPv6 nodes that must send to other IPv6 nodes across an IPv4 network. If both systems have IPv4-compatible addresses, the sender can send the packet to the receiver's IPv4-compatible address and the packet will be automatically encapsulated within an IPv4 packet so that it can be sent across the IPv4 network.

For more details about IPv6 addressing, see RFC 2373.

# ## NDP

Neighbor Discovery Protocol (NDP) is the IPv6 replacement for ARP. It performs the functions that ARP performed for IPv4, and also adds some more functionality.

The basic function of mapping IPv6 addresses to hardware addresses is performed using the Neighbor Solicitation and Neighbor Advertisement packets. These are very similar to ARP requests and responses. NDP also makes use of two other types of packets called router solicitations and router advertisements. Router solicitations are multicast by hosts to all routers on their local links. Routers respond with router advertisements, which can include information about prefixes the host should use and what destinations this router is able to route to. For more information about NDP, see RFC 2461.

# ## IPv6 Autoconfiguration

One important feature of IPv6 is that it allows for automatic configuration of addresses on hosts. IPv6 uses the hardware address of each network adapter to derive a 64-bit identifier. Since hardware addresses for each media type are globally unique, this 64-bit identifier will be unique on its network link. The 64-bit identifier can then be used to create a link local address. Once each interface has been configured with a link