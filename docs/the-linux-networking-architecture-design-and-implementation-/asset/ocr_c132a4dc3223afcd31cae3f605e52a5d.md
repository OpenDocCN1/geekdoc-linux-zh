# 23.2 IPv6 Features 445

ARP is no longer supported in IPv6. It was replaced by Neighbor Discovery, which was integrated into ICMP6.

The structuring of the IPv6 address space is implemented by prefixes. A prefix is a sort of logical interconnection of a network, similarly to the subnets known from IPv4. A prefix virtually groups all IPv6 nodes with addresses beginning in the same way. For example, all IPv4 addresses of the Karlsruhe University begin with 129.13, using the notation 129.13.0/16. Subnetworks in IPv6 are denoted accordingly. The number of leading bits denoting the network are written after the complete IPv6 address and a slash. For example, the University of Münster, Germany, has the gonebone prefix 3FFE:400:10::/48. Normally, the bits in an address not belonging to the prefix are set to null; however, stating the IPv6 address of a computer connected to the subnetwork by the prefix. In this representation, it is important to note that the compressed notation is also extended to 128 bits, rather than to the prefix length. This means that 3:16/64 is the subnetwork with prefix 0003:0000:0000:0000 and not prefix 0003:0000:0000:0016.

We can basically distinguish between multicast addresses and "other" addresses. Multicast addresses begin with eight ones (= FF). All other addresses are unicast or anycast addresses, and of which the two the case cannot be told from the address-self. The 64 bits of all (nonmulticast) addresses not beginning with the bit string 000 must have an interface identifier corresponding to the EUI64 format; for Ethernet, this would be the MAC address of the network card.

Like IPv4, IPv6 uses special addresses for specific purposes:

+   * Unspecified (:: = 0:0:0:0:0:0:0)
This address, entirely consisting of zeros, does not stand for a real address, but for the absence of it. It must be selected only for source addresses and is, for example, to configure the address of a computer automatically.

+   * Loopback (::1)
Similarly, the loopback address does not stand for an actual network address either; it is used by a computer to send packets to itself. For this reason, it is inadmissible to send packets with the source or destination address set to ::1 to other computers. In addition, it would not be meaningful to use this address for a network interface. IPv6-capable routers have to drop packets.

+   * IPv4-compatible addresses (::d.d.d.d)

To be able to dynamically tunnel IPv6 packets over an existing IPv4 infrastructure, special IPv4-compatible IPv6 unicast addresses are assigned to the computers involved. These IPv6 addresses contain the IPv4 address in the lower 32 bits of their address; the remaining bits are set to null.

+   * Embedded IPv4 addresses (::FFFF:d.d.d.d)

On the IPv6 side, an embedded IPv4 address is assigned to all computers actually supporting IPv4 only, so that these computers can be addressed by IPv6 computers. This type is also called IPv4 mapped IPv6 Address; it consists of 80 zeros, 16 ones, and finally the 32-bit IPv4 address.

![](bbox=[0.067, 0.955, 0.135, 0.971])