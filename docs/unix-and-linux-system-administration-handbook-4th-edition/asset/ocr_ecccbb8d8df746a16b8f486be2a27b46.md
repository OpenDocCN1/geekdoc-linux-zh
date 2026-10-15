# Table 14.3 Example IPv4 address decodings

| IP address | Netmask | Network | Broadcast |
|---|---|---|---|
| 128.138.243.100/16 | 255.255.0.0 | 128.138.0.0 | 128.138.255.255 |
| 128.138.243.100/24 | 255.255.255.0 | 128.138.243.0 | 128.138.243.255 |
| 128.138.243.100/26 | 255.255.255.192 | 128.138.243.64 | 128.138.243.127 |

hosts: two real hosts—usually at either end of a point-to-point link—and the network and broadcast addresses. To have four values for hosts requires two bits in the host portion, so such a network would be a /30 network with netmask 255.255.255.252 or 0xFFFFFFFC. However, a /31 network is in fact treated as a special case (see RFC3021) and has no network or broadcast address; both of its two addresses are used for hosts, and its netmask is 255.255.255.254.

A handy web site called the IP Calculator by Krischan Jodies (it's available at jodies.de/ipcalc) helps with binary/hex/mask arithmetic. IP Calculator displays everything you might need to know about a network address and its netmask, broadcast address, hosts, etc. A tarball for a command-line version of the tool, ipcalc, is also available.

On Ubuntu you can install ipcalc through apt-get.

Here's some sample IP Calculator output, munged a bit to help with formatting:
Address: 24.8.175.69 00001100.00001000.10101111.01000101
Netmask: 255.255.255.0 = 24 11111111.11111111.11111111.00000000
Wildcard: 0.0.0.255 00000000.00000000.00000000.11111111
=>
Network: 24.8.175.0/24 00001100.00001000.10101111.00000000 (Class A)
Broadcast: 24.8.175.255 00001100.00001000.10101111.11111111
HostMin: 24.8.175.1 00001100.00001000.10101111.00000001
HostMax: 24.8.175.254 00001100.00001000.10101111.11111110

The output provides both easy-to-understand versions of the addresses and "cut and paste" versions. Very useful.

Red Hat includes a similar but unrelated program that's also called ipcalc. However, it's relatively useless because it only understands default IP address classes.

If a dedicated IP calculator isn't available, the standard utility bc makes a good backup utility since it can do arithmetic in any base. Set the input and output bases with the ibase and obase directives. Set the obase first; otherwise, it's interpreted relative to the new ibase.

# CIDR: Classless Inter-Domain Routing

Like subnetting, of which it is a direct extension, CIDR relies on an explicit netmask to define the boundary between the network and host parts of an address. But unlike subnetting, CIDR allows the network portion to be made smaller than would be implied by an address's implicit class. A short CIDR mask may have the

> CIDR is defined in RFC1519.