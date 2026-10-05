# Tricks and tools for subnet arithmetic

# Exhibit C Netmask base conversion

| IP address | 128 | 138 | 243 | 0 |
|---|---|---|---|--|
| Decimal netmask | 255 | 255 | 255 | 192 |
| Hex netmask | f f | f f | f f | c 0 |
| Binary netmask | 1111 1111 | 1111 1111 | 1111 1111 | 1100 0000 |

/26 network has 6 bits (32 - 26 = 6) to number hosts. 2^6 is 64, so the network has 64 potential host addresses. However, it can only accommodate 62 actual hosts because the all-0 and all-1 host addresses are reserved (they are the network and broadcast addresses, respectively).

In our 128.138.243.0/26, the extra two bits of network address obtained by subnetting can take on the values 00, 01, 10, and 11. The 128.138.243.0/24 network has been divided into four /26 networks:

+   * 128.138.243.0/26 (0 in decimal is 00000000 in binary)
* 128.138.243.64/26 (64 in decimal is 01000000 in binary)
* 128.138.243.128/26 (128 in decimal is 10000000 in binary)
* 128.138.243.192/26 (192 in decimal is 11000000 in binary)

The bolded faces of the last byte of each address are the bits that belong to the network portion of that byte.

# Tricks and tools for subnet arithmetic

It's confusing to do all bit twiddling, but some tricks can make it simpler. The number of hosts per network and the value of the last byte in the netmask always adds up to 256:

+   * netmask byte = 256 - net size

For example, 256 - 64 = 192, which is the final byte of the netmask of the preceding example. Another arithmetic fact is that the last byte of an network address (as to netmask) must be evenly divisible by the number of hosts per network. We see this in action in the 128.138.243.0/26, where the last bytes of the networks are 0, 64, 128, and 192—all divisible by 64.7.

Given an IP address (say, 128.138.243.100), we cannot tell without the associated netmask what the network address and broadcast address would be. Table 14.3 on the next page shows the possibilities for /16 (the default for a class B), /24 (a plausible value), and /26 (a reasonable value for a small network).

The network address and broadcast address steal two hosts from each network, so it would seem that the smallest meaningful network would have four possible

+   7. Of course, 0 counts as being divisible by any number...