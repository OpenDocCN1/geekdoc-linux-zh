# LISTING 21.1 Continued

```
gif0: flags=8010<POINTTOPOINT,MULTICAST> mtu 1280
gif1: flags=8010<POINTTOPOINT,MULTICAST> mtu 1280
gif2: flags=8010<POINTTOPOINT,MULTICAST> mtu 1280
gif3: flags=8010<POINTTOPOINT,MULTICAST> mtu 1280
lo0: flags=8049<UP,LOOPBACK,RUNNING,MULTICAST> mtu 16384
	inet6 fe80::1%lo0 prefixlen 64 scopeid 0x7
	inet6 ::1 prefixlen 128
	inet 127.0.0.1 netmask 0xff000000
ppp0: flags=8010<POINTTOPOINT,MULTICAST> mtu 1500
sl0: flags=c010<POINTTOPOINT,LINK2,MULTICAST> mtu 552
faith0: flags=8000<MULTICAST> mtu 1500
```

# IP Version 6 (IPv6)

Various groups, such as the KAME project (http://www.kame.net), have been working recently on incorporating support for the next generation of IP (version 6, or IPv6) into FreeBSD. IPv6 provides a 128-bit address space, with addresses effectively four times the size in IPv4 (the current version). The result is address space for 3.4x10^38 hosts—a number that we're unlikely to reach anytime soon, to say the least. Also included in IPv6 are a number of other enhancements, such as built-in encryption and authentication, connection differentiation (with flow labels), complete auto-configurability of hosts, and the abandonment of several outdated parts of IPv4 that are no longer used.

IPv6 is catching on very, very slowly. Networks are expensive to build, and retrofitting them to be IPv6 compliant generally means replacing all existing equipment with newer, more expensive, less-mature hardware. Very few companies are willing to take that plunge just yet. But in the meantime, FreeBSD has full support for IPv6 and can take advantage of the various network resources currently available for IPv6.

# Networking at the Ethernet Level

The Address Resolution Protocol (ARP) and the MAC (or Ethernet) address provide the way in which Ethernet cards communicate on a LAN. ARP forms the basis for Internet routing, allowing routers to behave as destinations for LAN traffic, and then manipulate the Ethernet headers to make them compatible with the destination network.

Although IP addresses are fairly visible to us as users because we can specify them directly in our networking applications, such as Web and FTP programs, they are really just artificial constructs; they're bound to their hosts' Ethernet interfaces at the operating system level and can be changed at any time. At the bottom level of the TCP/IP stack, the data link layer, the IP address has no meaning—an Ethernet card knows nothing about what IP address the operating system has assigned to it or its hardware. Device drivers exist at a higher level than the one at which the device communicates with the network.