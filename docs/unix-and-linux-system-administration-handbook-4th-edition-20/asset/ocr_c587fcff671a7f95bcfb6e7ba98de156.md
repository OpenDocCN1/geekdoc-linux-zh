# IPv4 and IPv6

# Exhibit A TCP/IP layering model

| APPLICATION LAYER | arp | SSH, FTP, HTTP | DNS, Halo 3 | tracerroute |
| TRANSPORT LAYER | TCP | UDP |
| NETWORK LAYER | IP | ICMP |
| LINK LAYER | ARP, device drivers |
| PHYSICAL LAYER | Copper, optical fiber, radio waves

# IPv4 and IPv6

The version of TCP/IP that has been in widespread use for three decades is protocol version 4, aka IPv4. It uses four-byte IP addresses. A modernized version, IPv6, expands the IP address space to 16 bytes and incorporates several others learned from the use of IPv4. It removes several features of IP that experience has shown to be of little value, making the protocol potentially faster and easier to implement. IPv6 also integrates security and authentication into the ba-protocol.

All modern operating systems and many network devices already support IPv6. However, active use of IPv6 remains essentially zero in the real world. Experience suggests that it's probably best for administrators to defer production of IPv6 to the extent that this is possible. Everyone will eventually be forced to switch to IPv6, but as of 2010 that is still years away. The transition is not so far in the future that you can ignore it when purchasing new devices. In IPv6 compatibility for new acquisitions.

The development of IPv6 was to a extent motivated by the concern that we are running out of 4-byte IPv4 address space. And indeed we: projections indicate the current IPv4 allocation system will collapse some time after 2011. (See ipv4.potaroo.net for a daily update.) Even so, mainstream adoption of IPv6 throughout the Internet is probably still not in the cards soon.

More likely, another round of stopgap measures on the part of ISPs and ICANN (or more specifically, its subsidiary IANA, the Internet Numbers Authority) will extend the dominance of IPv4 for another few years. We see wider use of IPv6 on the Internet backbone, but outside of large ISPs, academic sites involved in Internet research, and universal providers such as Google, our

+   3. A Google study presented at RIPE 57 in October 2008 indicated that overall IPv6 penetration (actual use, not capability) was 0.24%. No country had IPv6 penetration greater than 0.76%.