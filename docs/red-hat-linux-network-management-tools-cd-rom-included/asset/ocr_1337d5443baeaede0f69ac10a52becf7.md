The tcpdump command supports several expression (or operator) types and can be combined with primitives and qualifiers to produce compound filters. These expressions include the arithmetic and Boolean operators listed in Table 4.14. Operators can build powerful expressions to search for specific packets. Expressions can be composed of numbers, packet field selections, length primitives, and arithmetic operators. To use the value of a field in an expression within a packet, use the following syntax:

```
primitive [offset [: size]]
```

where the word *primitive* is replaced by *ether, ip, udp, tcp*, or *icmp*. The *offset* is used in the base of the protocol primitive, and the *size* specifies the length of the field. If not supplied, they default to 1.

Packet field sections can be used in a variety of ways. Consider the following examples:

```
tcpdump "ether[1:4] 0xffffffff = 0xffffffff"
```

In this example, *tcpdump* will display all broadcast packets transmitted on the local network--this means all frames with a destination address of all 1s (255 in decimal, 0xff in hexadecimal). The 1 in *ether*[1:4] indicates the first addressable byte of the frame (the destination address), and the 4 value specifies the length of this field. Despite the fact that Ethernet addresses are six bytes, we can examine the first four bytes to determine if it is a broadcast address.

# Table 4.14 Arithmetic and Boolean operators

| Arithmetic Operators | Description |
| :--- | :--- |
| > | Greater than |
| < | Less than |
| >= | Greater than or equal |
| <= | Less than or equal |
| = | Equal to |