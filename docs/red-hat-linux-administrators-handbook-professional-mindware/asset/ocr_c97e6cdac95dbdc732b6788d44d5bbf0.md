In a TCP/IP network, when a computer wants to send a packet to an IP address, it determines whether or not the IP address is local by performing a bitwise AND operation. For example, to determine whether 192.168.1.1 is local to a network with subnet mask 255.255.255.0, a host computer does the following:

```
Binary          Decimal
11000000.10101000.00000001.00000001  => 192.168.1.1
AND 11111111.11111111.11111111.00000000 => 255.255.255.0
-------------------------------------------------------
11000000.10101000.00000001.00000000  => 192.168.1.0
```

As you can see, a bitwise AND operation returns the network address (192.168.1.0) of the IP address 192.168.1.1. Because a host computer knows to what network it belongs, it can very easily determine how to handle packets for such an IP address.

Because you are likely to deal with class C networks a lot, this class is used in all the examples in this section.

When a class C network is left in its entirety, the netmask is 255.255.255.0. To divide the network into subnets, you need to create a new netmask by setting one or more bits in the host interface part of the default class netmask (255.255.255.0) to 1. Consider the ongoing example class C network—192.168.1.0. By setting the most significant bit in the host interface number part of the address to 1, you get:

```
11111111.11111111.11111111.10000000 => 255.255.255.128
```

This is a new netmask that splits the class in half. All IP addresses from 192.168.1.0 to 192.168.1.127 belong to the 192.168.1.0 network, and the rest of the IP addresses, 192.168.1.128 to 192.168.1.255, belong to the 192.168.1.128 network. Both networks use the 255.255.255.128 netmask. For example, to determine to which network an IP address called 192.168.1.10 belongs, perform the following bitwise AND operation:

```
Binary          Decimal
11000000.10101000.00000001.00001010 => 192.168.1.10
AND 11111111.11111111.11111111.10000000 =>
255.255.255.128
-------------------------------------------------------
11000000.10101000.00000001.00000000 => 192.168.1.0
```