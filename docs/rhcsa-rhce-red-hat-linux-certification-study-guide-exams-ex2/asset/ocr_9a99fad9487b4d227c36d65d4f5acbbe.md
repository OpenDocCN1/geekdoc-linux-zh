TABLE 3-4
ifconfig Switches

| Parameter | Description |
|---|---|
| up | Activates the specified adapter. |
| down | Deactivates the specified adapter. |
| netmask address | Assigns the address subnet mask. |
| broadcast address | Assigns the address as the broadcast address. Rarely required, since the default broadcast address is standard for most current networks. |
| metric N | Allows you to set a metric value of N for the routing table associated with the network adapter. |
| mtu N | Sets the maximum transmission unit as N, in bytes. |
| -arp | Deactivates the Address Resolution Protocol (ARP), which collects network adapter hardware addresses. |
| promisc | Activates promiscuous mode. This allows the network adapter to read all packets to all hosts on the LAN. Can be used to analyze the network for problems or to try to decipher messages between other users. |
| -promisc | Deactivates promiscuous mode. |

However, a couple of more intuitive scripts are designed to control network adapters: ifup and ifdown. Unlike the ifconfig command, they call appropriate configuration files and scripts in the /etc/sysconfig/network-scripts directory, for details on how a network adapter is to be activated and deactivated.

For example, the ifup eth0 command brings up the first Ethernet network adapter based on the ifcfg-eth0 configuration file and the ifcfg-eth script in the /etc/sysconfig/network-scripts directory. If you've configured the network adapter with the Network Connections tool described later in this chapter, the filename in the /etc/sysconfig/network-scripts directory may be something like ifcfg-System_eth0.

# arp as a Diagnostic Tool

The ARP protocol associates the hardware address of a network adapter with an IP address. The arp command displays a table of hardware and IP addresses on the local computer. The arp command can help detect problems such as duplicate addresses on the network. Such problems may happen with improperly cloned systems. If needed, the arp command can be used to set or modify hardware routing tables. As hardware addresses are not routable, an arp table should be limited to the local network. Here's a sample arp command, showing all arp entries in the local database: