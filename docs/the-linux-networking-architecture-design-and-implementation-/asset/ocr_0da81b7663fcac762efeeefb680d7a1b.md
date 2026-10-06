# 574 Appendix C Tools and Commands for Network Operation

The following list describes the parameters of the ifconfig command (with the names of the relevant flags in brackets). Some of these parameters enable certain modes of the network device (e.g., the ARP capability). These modes can be disabled by a leading minus (–) sign.

+   up activates a network device. When you use this command to state an address, then up is taken as the default option. If up called without additional parameters, ifconfig initializes the network adapter to the default values (e.g., the IP address to 0.0.0.0, which won't make sense). The up option sets the flags UP and RUNNING.

+   down activates a network device. However, this device remains in the list of registered devices, so that it can be reactivated. At the same time, all routes in which this network device participated were removed from the routing table. netmask assigns a subnet mask to the network device.

+   pointpoint address is used for a point-to-point connection that directly connects two computers. Examples include SLIP and PLIP network connections. This parameter is used to set the IP address of the peer system, ifconfig shows the presence of a point-to-point peer by the flag POINTPOINT.

+   broadcast address sets the broadcast address of the network device. It is normally built from the network address and the appropriate address class all the host part are set to one. However, the broadcast address can also be set explicitly. The presence of a broadcast address is shown by the flag BROADCAST.

+   mtu sets the Maximum Transfer Unit (MTU) (i.e., the maximum size of a MAC frame) to the specified size. The default value is 1500 bytes for Ethernet adapters, 296 bytes for SLIP connections.

+   arp enables the Address Resolution Protocol for network devices that use broadcast technologies (Ethernet, token ring, etc.) to allocate logical layer-3 addresses to MAC addresses. This option is set by default for broadcast networks. ifconfig shows the flag NOARP if ARP was deactivated.

+   -arp disables the use of the Address Resolution Protocol and sets the NOARP prom moves the network adapter into the promiscuous mode. For broadcast networks, this mode causes all packets to be received by the network interface and to be forwarded to the higher layers, regardless of whether they are addressed to this computer. This allows us to monitor network traffic in a local area network. Of course, this mode should be used for analysis purposes only, which is often extremely useful. The tcpdump tool uses the promiscuous mode to analyze the traffic in a local area network. -promiscuous mode is shown by the flag PROMISC.

+   -multicast enables the receipt of multicast packets addressed to groups at which the computer is registered as a member.
-multicast enables the receipt of multicast packets.

+   allmult enables the receipt of all multicast packets, including multicast packets from groups of which the computer is not a member. This mode is used by multi-routers, among others.