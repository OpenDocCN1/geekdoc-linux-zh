**Table 4.3** ifconfig options and keywords

| Option | Description |
| :--- | :--- |
| -a | Applies to all interfaces presently installed on the system |
| arp<br>-arp | Enables the use of the Address Resolution Protocol (ARP) on this interface; disables the use of ARP with the -arp option |
| promisc<br>-promisc | Enables promiscuous (i.e., listen for all traffic) mode on this interface. The -promisc option disables it |
| allmulti<br>-allmulti | Enables all multicast traffic to be received by the interface. The -allmulti option will disable the reception of multicast packets |
| broadcast<br>-broadcast | With the argument given, sets or clears the broadcast address for this interface. This is a network-layer broadcast address |
| pointtopoint<br>-pointtopoint | Enables a point-to-point mode for this interface. The basic assumption is that this is a dedicated link between two devices. If the address argument is provided, it sets the protocol address for the other side of the link. Disables the point-to-point mode with the **pointtopoint** keyword |
| up | Causes the interface to be brought up or activated |
| down | Causes the interface to be shut down or deactivated |
| netmask | Sets the IP network mask for this interface. The specified argument can be in the form **255.0.0.0** (dotted decimal) or **0xffffff00** (hexadecimal) |
| broadcast | Sets the IP broadcast for this interface. The specified argument can be expressed in the same format as the **netmask** keyword |
| address | Sets the IP address for this interface. This must be a unique IP address not previously assigned to another system |