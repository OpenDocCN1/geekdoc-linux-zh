# IPv6 Addressing

IPv6 addresses introduce major changes into the format and method of addressing systems under the Internet Protocol (see RFC 3513 at www.left.org/rfc or www.faqs.org for more details). There are several different kinds of addressing with different fields for the network segment. The host segment has been expanded to a 64 bit address, allowing direct addressing for a far larger number of systems. Each address begins with a type field specifying the kind of address, which will then determine how its network segment is organized. These changes are designed not only to expand the address space but to also provide greater control over transmissions at the address level.

# IPv6 Address Format

An IPv6 address consists of 128 bits, up from the 32 bits used in IPv4 addresses. The first 64 bits are used for network addressing, of which the first few bits are reserved for indicating the address type. The last 64 bits are used for the interface address, known as the interface identifier field. The number of bits used for sub-netting can be adjusted with a CIDR mask, much like that in IPv4 CIDR addressing (see previous section).

An IPv6 address is written as 8 segments representing 16 bits each (128 bits total). To more easily represent 16 bit binary numbers, hexadecimal numbers are used. Hexadecimal numbers use 16 unique numbers, instead of the 8 used in octal numbering. These are 0 through 9, continuing with the characters A through F.

In the following example, the first four segments represent the network part of the IPv6 address, and the following four segments represent the interface (host) address.

```
FEC0:0000:0000:0000:0008:0800:200C:417A
```

You can cut any preceding zeros, but not trailing zeros in any given segment. Segments with all zeros can be reduced to a single zero.

```
FEC0:0:0:0:8:800:200C:417A
```

The loopback address used for localhost addressing can be written with seven preceding zeros and a 1.

```
0:0:0:0:0:0:0:1
```

Many addresses will have sequences of zeros. IPv6 supports a shorthand symbol for representing a sequence of several zeros in adjacent fields. This consists of a double colon ::. There can be only one use of the :: symbol per address.

```
FEC0::8:800:200C:417A
```

The loopback address 0000000000000001 can be reduced to just the following.

```
::1
```

To ease the transition from IPv4 addressing to IPv6, a form of addressing incorporating IPv4 addresses is also supported. In this case, the IPv4 address (32 bits) can be used to represent the last two segments of an IPv6 address, and can be written using IPv4 notation.

```
FEC0::192.168.0.3
```

# IPv6 Interface Identifiers

The identifier part of the IPv6 address takes up the second 64 bits, consisting of 4 segments containing four hexadecimal numbers. The interface ID is an 64 bit (4 segments) Extended Unique Identifier (EUI-64) generated from a network device's Media Access Control (MAC) address.

# IPv6 Address Types

There are three basic kinds of IPv6 addresses: unicast, multi-cast, and anycast. These, in turn, can have