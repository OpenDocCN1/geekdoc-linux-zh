| 192.0.2.0~192.0.2.255 | 1 × class-C network/range |

![](bbox=[0.16, 0.12, 0.74, 0.36])

**Figure 4.7** Private 10.x.x.x addresses used with network address translation

The idea behind this is that 10 or 15 years ago, most TCP/IP networks were not connected to the Internet. People often used addresses listed in the examples in manufacturers' manuals when setting up their networks. The world was full of private networks using Sun Microsystems' addresses. When these sites finally connected to the Internet, they had to renumber all their machines.

# IP numbers for small self-configured networks

DHCP (Chapter 16) is a dynamic host configuration system that lets client machines obtain all their IP configuration settings at boot time from a central DHCP server. The big advantages are central administration of IP numbers and clients don't have to be individually configured.

However, if a client machine boots and can't find a DHCP server, what does it do? It could just fail to boot, but another option is for it to use a number from a specially allocated range:

| 169.254.0.0~169.254.255.255 | 1 × class-B network/range |

so that it can start and work on the local network at least. This is especially useful for home machines or small organizations where there is no trained network administrator. Some versions of Windows (including Win-9x) make use of this (see Notes).