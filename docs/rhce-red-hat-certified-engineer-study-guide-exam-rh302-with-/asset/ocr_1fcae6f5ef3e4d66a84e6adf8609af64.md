TCP/IP Model 87

FIGURE 4.1 The TCP/IP protocol layers

![](bbox=[0.331, 0.153, 0.893, 0.381])

# Network Access Protocols

The bottommost layer of protocols, the network access protocols, includes all functions necessary to access the physical network medium and transmit data to hosts on the local network. Commonly, TCP/IP is used in conjunction with Ethernet, a protocol that provides these functions.
Network access protocols tend to be implemented in hardware. For example, typical network adapter cards understand the Ethernet protocol. Consequently, the network access layer is seldom a major concern of the Linux systems administrator.

# Internet Protocols

The Internet protocols layer establishes IP addresses as the standard means of addressing TCP/IP hosts. This layer also handles the routing of messages that are destined for hosts outside of the local network.
A host can send data to another host on the local network by directing the data to the IP address of the destination host. Alternatively, a network host can send a broadcast message that reaches every host on the local network.
A host that is connected to more than one network can be configured to pass data from one network to the other. Such a host is known as a router.

Copyright ©2000 SYBEX, Inc., Alameda, CA    www.syex.com