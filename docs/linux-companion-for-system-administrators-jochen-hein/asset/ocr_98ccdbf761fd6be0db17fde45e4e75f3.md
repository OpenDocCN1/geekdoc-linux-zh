```
ip      0      IP      # internet protocol, pseudo number
icmp    1      ICMP   # internet control message protocol
igmp    2      IGMP   # internet group multicast protocol
gggp     3      GGP     # gateway-gateway protocol
tcp     6      TCP     # transmission control protocol
pup     12     PUP     # PARC universal packet protocol
udp     17     UDP    # user datagram protocol
idp    22     IDP    # WhatisThis?
raw     255    RAW     # RAW IP interface
```

# Listing 14.1 Internet protocols (/etc/protocols).

+   * IP, the Internet Protocol, serves as a basis for TCP and UDP. It is a connectionless protocol which does not contain any mechanisms for guaranteeing data transfer. The only thing required from the implementation is a 'best effort' when forwarding the packets. Furthermore, the quality of a connection can be improved by means of ICMP. The protocol is defined in [rfc0791].

+   * ICMP, the Internet Control Message Protocol, is used for the exchange of messages between computers on a very low level. This protocol is often implemented in the kernel itself. The individual message types of ICMP are defined in [rfc0792]; the most important ones are ICMP echo (using ping), ICMP redirect (changing of routes), and ICMP messages that signal refusal to establish a connection ('connection refused').
nYou can use the icmpinfo program to display and control ICMP packets. Particularly on computers in very active networks, lots of messages are output, with the 'unimportant' ones only being displayed upon request. More details about this program can be found in Chapter 26.

+   * TCP (Transmission Control Protocol), [rfc0793], is a connection-oriented, reliable protocol which is, however, slower. Application programs can rely on the fact that all packets will be transmitted in the correct order. The kernel ensures completeness of data by means of retransmissions, acknowledgments, and timeouts.

+   * UDP (User Datagram Protocol). [rfc0768], a connectionless, unreliable protocol which is faster than TCP. The speed advantage results from being no requirement for a connection to be established, which takes three steps in TCP. On the basis of this protocol, applications can, however, implement reliable protocols, although the network layer cannot guarantee completeness of transmission.