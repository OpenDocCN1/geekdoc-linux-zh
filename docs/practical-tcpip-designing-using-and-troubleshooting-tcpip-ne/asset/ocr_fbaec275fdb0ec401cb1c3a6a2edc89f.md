# ## 4.5 Specifying different sizes of network range

The netmasks we’ve used so far give us particular sizes of networks (or address ranges):

| Netmask | Number of IP addresses in range |
| :--- | :--- |
| 255.255.255.0 | 256 |
| 255.255.0.0 | 65,536 |
| 255.0.0.0 | 16,777,216 |

The netmasks above are the defaults for the A, B, and C address classes that were invented when the Internet was very small. Nowadays, the Internet is used so widely that IP address space is very scarce. Everyone can’t have even a full class-C, and organizations have to make do with much smaller networks, often a partial class-C with just 4, 8, or 16 addresses in the range. Our range specification mechanism must be able to handle these very small ranges. If we want to specify one of these smaller networks, or an intermediate-sized network with 1,800 or 10,000 machines, how do we do that using a netmask?

The solution is to use not one whole byte for the host part (mask 255.255.255.0) or two whole bytes (mask 255.255.0.0) but something like 3/4 byte, or 1 7/8 of a byte. From the examples in earlier modules, you’ll have seen that the number of addresses in the range is determined by the number of bits in the host part of the address. It follows that the network size is always a power of two: a 1-bit host part gives two addresses (2¹), 2 bits gives 2²=4 addresses, 3 bits gives 2³=8 addresses and so on. For example, netmask 255.255.0.0 has a two-byte (16-bit) host part, which gives a range size of 2¹⁶= 65,536 addresses. To accommodate the range size we want, we work out how many bits we need in the host part, which in turn automatically determines the netmask. For example:

We want a network with 25 machines – a range containing 25 addresses. A 4-bit host part gives 16 addresses (which isn’t enough) and a host part of 5 bits gives 2⁵=32 addresses, which is OK. This implies a network part with (32 – 5) = 27 bits. Therefore the netmask consists of 27 1-bits on the left, followed by 5 0-bits on the right (Figure 4.4(a)). Converting that to decimal (using the decimal/binary conversion table inside the back cover) gives us the netmask shown in Figure 4.4(b).

![](bbox=[0.13, 0.78, 0.91, 0.89])