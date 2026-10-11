volumes of traffic, and wide geographic separations. To manage the hosts on a network, you have to break the network into smaller subnets. TCP/IP allows you to extend the network ID portion beyond its default boundary by using a subnet mask. This is a 32-bit number that is applied to an IP address to identify the network and node addresses. The dotted decimal notation used for subnet masks is the same as the notation used for IP addresses. You can extend the network address portion of a Class B address by reserving the three bytes for your subnet network address. If you set the subnet mask to 255.255.255.0, it appears as a Class C address. Table 9.2 illustrates subnet masks and the range of addresses that are possible.

**TABLE 9.2: SUBNET MASKS FOR IPV4 ADDRESS CLASSES**

| Address Class | Subnet Mask | Number of Addresses | Host Address | Network Address |
|---|---|---|---|---|
| A | 255.0.0.0 | 16,777,216 | xxx.xxx.xxx.xxx | xxx |
| B | 255.255.0.0 | 65,536 | xxx.xxx.xxx.xxx | xxx.xxx |
| C | 255.255.255.0 | 256 | xxx | xxx.xxx.xxx.xxx |

In the address space for IPv4, which is the current IP standard, you will find that the five different address classes (A, B, C, D, and E) can have a range of addresses assigned to them. Table 9.3 illustrates available numbers that can be assigned for each byte range (because Classes D and E are reserved for specific uses, they are not included in the table).

**TABLE 9.3: RANGE OF ADDRESS NUMBERS**

| Address Class | Byte 1 | Byte 2 | Byte 3 | Byte 4 |
|---|---|---|---|---|
| A | 0–127 | 1–254 | 1–254 | 1–254 |
| B | 128–191 | Reserved for network address | 1–254 | 1–254 |
| C | 192–223 | Reserved for network address | Reserved for network address | 1–254 |

The Internet is running out of address space. To solve this problem, as well as to add additional security and other functionality, eventually IPv6 will replace the current IPv4 standard. IPv6 uses a simplified header scheme, better authentication and privacy support, address autoconfiguration, and Quality of Service (QoS) functionality. IPv6 increases the IP address from 32 bits to 128 bits and allows through scoping