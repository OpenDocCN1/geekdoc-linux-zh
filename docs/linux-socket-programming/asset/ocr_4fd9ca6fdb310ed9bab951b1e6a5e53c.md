# ## Solving the Dwindling IPv4 Address Space

The IAB has taken some measures to solve the dwindling address problem. The cost of owning real IP addresses has risen, so companies now use masquerading and DHCP to limit the number of allocated addresses.

Additionally, the Internet could adopt a wider addressing scheme than merely 32 bits. IPv6 [RFC2460] answers that exact request. The IPv6 is 128-bits long (or 16-bytes wide). This opens the possibilities well into the next century—at least. The effective number of addresses in IPv4 is about two billion network nodes (taking out the special addresses). The effective address space for IPv6 is 110381.

# ## What Does IPv6 Look Like?

An IPv6 address looks a little different from IPv4 because of the large number of digits a programmer now has to manage. Each address is eight hexadecimal numbers separated with colons. For example, one legal address is `2FFF:80:0:0:0:94:1`. For shorthand, you can replace the repeating zeros with two colons (`2FFF:80::94:1`).

Ports can still be tacked on to the end of the address using a period and port number in decimal. For example, port 80 for the previous address would be `2FFF:80::94:1.80`. You can't use the colon separator because it makes the shorthand ambiguous.

The IPv6 address space (like that of IPv4) has already been divided up into specific regions or groups [RFC1897, RFC2471]. The groups attempt to merge different addresses (like IPX). As of the writing of this book, the definition is still in flux, many groupings remaining undefined.

Of the different groupings, the numeric address value that starts with `001` as the first three bits specifically replaces the IPv4 addressing. Figure 19.1 shows with this address.

![](bbox=[0.1, 0.59, 0.9, 0.62])

![](bbox=[0.18, 0.63, 0.81, 0.71])

Figure 19.1 has five parts: allocation ID, TLA ID, NLA ID, SLA ID, and interface ID. Table 19.1 defines the purpose of each part.

Table 19.1. IPv6 Address Parts
| Field | Description |
| --- | --- |
| Allocation ID | This is the 3-bit flag (001) that indicates that this is a public Internet address. (3 bits) |
| TLA ID | Top-Level Aggregation. This represents the highest level of the world-wide Internet. (13 bits) |
| NLA ID | Next-Level Aggregation. Subdivided group within the TLA. (32 bits) |
| SLA ID | Site-Level Aggregation. This could be a large corporation or conglomerate. (16 bits) |
| Interface ID | The specific machine ID. (64 bits) |

One of the problems networks had to solve was the "everybody knows everybody" problem first discussed in Chapter 2. This problem forces all the routers to know every address available so that it routes a message correctly. That is why machines could not use the MAC addresses.