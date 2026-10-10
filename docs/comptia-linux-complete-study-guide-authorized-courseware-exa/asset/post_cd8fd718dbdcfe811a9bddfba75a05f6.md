
IPv4 addresses are usually expressed as four base-10 numbers (0~255) separated by periods, as in 192.168.29.39. If your Linux system's protocol stack is already up and running, you can discover its IP address by using ifconfig, as described earlier. The output includes a line like the following, which identifies the IP address (inet addr):

`inet addr:192.168.29.39 Bcast:192.168.29.255 Mask:255.255.255.0`

Although it isn't obvious from the IP address alone, this address is broken into two components: a network address and a computer address. The network address identifies a block of IP addresses that are used by one physical network, and the computer address identifies one computer within that network. The reason for this breakdown is to make the job of routers easier—rather than record how to direct packets destined for each of the 4 billion IP addresses, routers can be programmed to direct traffic based on packets' network addresses, which is a much simpler job. Ordinarily, a computer can directly communicate only with computers on its local network segment; to communicate outside of this set of computers, a router must be involved.

IPv6 addresses work in a similar way, except that they're larger. Specifically, IPv6 addresses consist of eight groups of four-digit hexadecimal numbers separated by colons, as in fed1:0db8:85a3:08d3:1319:8a2e:0370:7334. If one or more groups of four digits is 0000, that group or those groups may be omitted, leaving two colons. Only one such group of zeroes can be compressed in this way, because if you removed two groups, there would be no way of telling how many sets of zeroes would have to be replaced in each group.

The network mask (also known as the subnet mask or netmask) is a number that identifies the portion of the IP address that's a network address and the part that's a computer address. It's helpful to think of this in binary (base 2) because the netmask uses binary 1 values to represent the network portion of an address and binary 0 values to represent the computer address. The network portion ordinarily leads the computer portion. Expressed in base 10, these addresses usually consist of 255 or 0 values, 255 being a network byte and 0 being a computer byte. If a byte is part network and part computer address, it will have some other value. Another way of expressing a netmask is as a single number representing the number of network bits in the address. This number usually follows the IP address and a slash. For instance, 192.168.29.39/24 is equivalent to 192.168.29.39 with a netmask of 255.255.255.0—the last number shows the network portion to be three solid 8-bit bytes, hence 24 bits. The longer notation showing all 4 bytes of the netmask is referred to as dotted quad notation. IPv6 netmasks work just like IPv4 netmasks, except that larger numbers are involved, and IPv6 favors hexadecimal to decimal notation.

On modern IPv4 networks, netmasks are often described in Classless Inter-Domain Routing (CIDR) form. Such network masks can be broken at any bit boundary for any address. For instance, 192.168.1.7 could have a netmask of 255.255.0.0, 255.255.255.0, 255.255.255.128, or various other values. (Keeping each byte at 0 or 255 reduces the odds of human error causing problems but sometimes isn't practical, depending on the required or desired sizes of subnets.) Traditionally, though, IPv4 netmasks have been broken into one of several classes, as summarized in Table 8.1. Classes A, B, and C are for general networking use. Class D addresses are reserved for multicasting—sending data to multiple computers simultaneously. Class E addresses are reserved for future use. There are a few special cases within most of these ranges. For instance, the 127.x.y.z addresses are reserved for use as loop-back (a.k.a. localhost) devices—these addresses refer to the computer on which the address is entered. Addresses in which all the machine bits are set to 1 refer to the network block itself—they're used for broadcasts. The ultimate broadcast address is 255.255.255.255, which sends data to all computers on a network segment. (Routers normally block packets directed to this address. If they didn't, the Internet could easily be brought to its knees by a few people flooding the network with broadcast packets.)

### Table 8.1 IPv4 Network Classes and Private Network Ranges

| Class | Address Range | Reserved Private Addresses |
| :--- | :--- | :--- |
| A | 1.0.0.0–127.255.255.255 | 10.0.0.0–10.255.255.255 |
| B | 128.0.0.0–191.255.255.255 | 172.16.0.0–172.31.255.255 |
| C | 192.0.0.0–223.255.255.255 | 192.168.0.0–192.168.255.255 |
| D | 224.0.0.0–239.255.255.255 | none |
| E | 240.0.0.0–255.255.255.255 | none |

Within each of the three general-use network classes is a range of addresses reserved for private use. Most IP addresses must be assigned to individual computers by a suitable authority, lest two systems on the Internet both try to use a single address. Anybody can use the reserved private address spaces, though. (These address blocks are sometimes referred to as RFC1918 addresses, after the standards document—RFC1918—in which they’re defined.) The caveat is that routers normally drop packets sent to these addresses, effectively isolating them from the Internet as a whole. The idea is that these addresses may be safely used by small private networks. Today, they’re often used behind Network Address Translation (NAT) routers, which enable arbitrary numbers of computers to “hide” behind a single system. The NAT router substitutes its own IP address on outgoing packets and then directs the reply to the correct system. This is very handy if you want to connect more computers to the Internet than you have IP addresses.

I generally use reserved private addresses for examples in this book. Unless otherwise specified, these examples work equally well on conventional assigned (non-private) IP addresses.

IPv6 has its equivalent to private addresses. IPv6 site-local addresses may be routed within a site but not off-site. They begin with the hexadecimal number fec, fee, fdd, or fef.

Link-local addresses are restricted to a single network segment; they shouldn't be routed at all. These addresses begin with the hexadecimal number fe8, fe9, fea, or feb.

IPv4 address classes were designed to simplify routing; but as the Internet evolved, they became restrictive. Thus, today they serve mainly as a way to set default netmasks, such as 255.0.0.0 for Class A addresses or 255.255.255.0 for Class C addresses. Most configuration tools set these netmasks automatically, but you can override the settings if necessary. IP addresses and netmasks are extremely important for network configuration. If your network doesn't use DHCP or a similar protocol to assign IP addresses automatically, you must configure your system's IP address manually. A mistake in this configuration can cause a complete failure of networking or more subtle errors, such as an inability to communicate with just some computers.

![](img/f339a9f48c4b443e61c74acb4c9c3da4_454_0.png)

Non-TCP/IP stacks have their own addressing methods. NetBEUI uses machine names; it has no separate numeric addressing method. AppleTalk uses two 16-bit numbers. These addressing schemes are independent from IP addresses.

## Broadcasting Data

Earlier, I mentioned broadcasts. A broadcast is a type of network transmission that's sent to all the computers on a local network, or occasionally all of the computers on a remote network. Under TCP/IP, a broadcast is done by specifying binary 1 values in all the machine bits of the IP address. The network portion of the IP address may be set to the network's regular value, and this is required for directed broadcasts—that is, those that are sent to a remote network. (Many routers drop directed broadcasts.) In many cases, broadcasts are specified by the use of 255.255.255.255 as an IP address. Packets directed at this address are sent to all the machines on a local network.

Because the broadcast address for a network is determined by the IP address and netmask, you can convert between the broadcast address and netmask, given one of these and a computer's IP address. If the netmask happens to consist of whole-byte values (expressed as 0 or 255 in dotted quad notation), the conversion is easy: Replace IP address components that have 0 values in the dotted quad netmask with 255 values to get the broadcast address. For instance, consider a computer with an IP address of 172.24.21.201 and a netmask of 255.255.0.0. The final two elements of the netmask have 0 values, so you swap in 255 values for these final two elements in the IP address to obtain a broadcast address of 172.24.255.255.

In the case of a CIDR address that has non-255 and non-0 values in the netmask, the situation is more complex because you must resort to binary (base 2) numbers. For instance, consider a computer with an IP address of 172.24.21.201 and a netmask of 255.255.128.0 (that is, 172.24.21.201/17). Expressed in binary, these numbers are

```
10101100 00011000 00010101 11001001
11111111 11111111 10000000 00000000
```
