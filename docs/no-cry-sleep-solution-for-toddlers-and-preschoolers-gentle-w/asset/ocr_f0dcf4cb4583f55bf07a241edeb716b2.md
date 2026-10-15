The loopback address 0000000000000001 can be reduced to just the following.

```
::1
```

To ease the transition from IPv4 addressing to IPv6, a form of addressing incorporating IPv4 addresses is also supported. In this case, the IPv4 address (32 bits) can be used to represent the last two segments of an IPv6 address, and can be written using IPv4 notation.

```
FE80::192.168.0.3
```

# IPv6 Interface Identifiers

The identifier part of the IPv6 address takes up the second 64 bits, consisting of 4 segments containing four hexadecimal numbers. The interface ID is an 64 bit (4 segments) Extended Unique Identifier (EUI-64) generated from a network device’s Media Access Control (MAC) address.

# IPv6 Address Types

There are three basic kinds of IPv6 addresses: unicast, multi-cast, and anycast. These, in turn, can have their own types of addresses.

+   - A unicast address is used for a packet that is sent to a single destination.

+   - A anycast address is used for a packet that can be sent to more than one destination.

+   - A multicast address is used to broadcast a packet to a range of destinations.

In IPv6, addressing is controlled by the format prefix that operates as a kind of address type. The format prefix is the first field of the IP address. The three major kinds of unicast network addresses are global, link-local, and site-local. Global, site-local, and link-local are indicated by their own format prefix (see Table 38-6).

+   - Global addresses begin with the address type 3, site local with FEC, and link-local with FE8. Global addresses can be sent across the Internet.

+   - Link-local addresses are used for physically connected systems on a local network.

+   - Site-local can be used for any hosts on a local network. Site-local addresses operate similarly to IPv4 private addresses, but are used only for local access and cannot be used to transmit over the Internet.

In addition, IPv6 has two special reserved addresses. The address 0000000000000001 is reserved for the loopback address used for a system’s localhost address, and the address 0000000000000000 is the unspecified address.

# IPv6 Unicast Global Addresses

IPv6 global address currently uses four fields: the format prefix, a global routing prefix, the sub-net identifier, and the interface identifier. The format prefix for a unicast global address is 3 (3 bits). The global routing prefix references the network address (45 bits), and the sub-net id references a subnet within the site (16 bits).