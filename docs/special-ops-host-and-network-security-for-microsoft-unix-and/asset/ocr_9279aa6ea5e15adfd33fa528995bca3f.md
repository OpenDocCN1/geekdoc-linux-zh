maximum speed of 54 Mbps and is not compatible with 802.11, 11b, or 11g hardware.

+   **802.11b** This standard runs in the 2.4 GHz frequency range at 11 Mbps. It is the most widely deployed standard at this point and the focus of this chapter. Most of the available wireless LAN tools use this standard, as well as non-802.11 devices, such as Bluetooth wireless systems, X10 home automation gear, and cordless phones.

+   **802.11g** This is a 54Mbps standard that operates in the 2.4 GHz range and is backward-compatible with 802.11 and 802.11b equipment.

# Components of a Wireless Network

Wireless networks require a different set of hardware than the normal Ethernet hubs and switches. Access points connect the wireless network to the wired one and require wireless NICs to connect to them. In this section, we introduce the basic components of a wireless network.

# Bridging the Air Gap: Access Points and Bridges

In the traditional networking sense, all 802.11 access points are network bridges. They connect the wired and wireless networks at Layer 2 and will forward any packets on that segment like a regular Ethernet bridge. 802.11 devices can be wireless access points or wireless bridges depending on their configuration. Vendors will refer to an 802.11 device that is meant to join two wired network segments as a bridge and a wireless device that access client connections is referred to as an access point (see Figure 15.1). Sometimes a device can be both at once, but usually they are deployed as one or the other role. Since both are Layer 2 bridges to the Ethernet network they are connected to, you should realize that if you plug the access point into an Ethernet hub, each 802.11 client will see all the traffic on the hub. Plugged into a switch, the access point client will see only the packets destined for clients on the wireless network directed towards the AP’s Media Access Control (MAC).

In Ethernet terminology, clients associated with a wireless access point resemble a switch, where the only packets they see are broadcast and those destined for their MAC. This means that to sniff on a network in-band, you would need to use an Address Resolution Protocol (ARP)-spoofing tool such as Ettercap. Although you could watch traffic on the Net using a wireless sniffer, you would be in a receive-only mode and not able to inject traffic directly.