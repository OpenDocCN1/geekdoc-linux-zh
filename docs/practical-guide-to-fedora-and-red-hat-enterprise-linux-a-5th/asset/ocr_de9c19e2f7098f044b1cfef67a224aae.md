Each computer on a LAN must be connected to the hub. If you are using more than one hub, connect the port labeled **uplink** on one hub to a normal port on another hub.

+   * **Wireless access point (WAP)**
+     A wireless access point (WAP) connects a wireless network to a wired one. Typically a WAP acts as a transparent bridge, forwarding packets between the two networks as if they were one. If you connect multiple WAPs in different locations to the same wired network, wireless clients can roam transparently between the WAPs.
+   
+   * **Wireless networks do not require a hub**, although a WAP can optionally fill a similar role. In a wireless network, the bandwidth is shared among all nodes within range of one another; the maximum speed is limited by the slowest node.

# # GATEWAYS AND ROUTERS

If the LAN you are setting up is connected to another network, such as the Internet, you need a router, sometimes called a gateway. A router can perform several functions, the most common of which is allowing several systems to share a single Internet connection and IP address (NAT; page 820). When a router uses NAT, the packets from each system on the LAN appear to come from a single IP address; return packets are passed back to the correct system.

You have several choices for routers:

+   * A simple hardware router is relatively cheap and does most things required by a small network.
+   * You can set up a Fedora/RHEL system as a router. The Linux kernel can use iptables (page 819) to route packets between network adapters.
+   * You can use a Linux distribution tailored for use as a router. For example, SmoothWall (www.smoothwall.org) provides a browser-based configuration in the style of a hardware router.

# # NIC: NETWORK INTERFACE CARD

Each system's NIC may be a separate Ethernet card (wired or wireless) or the NIC may be built in to the motherboard.

+   * **Supported NICs**
+     Linux supports most wired Ethernet NICs. Fewer wireless NICs are supported. See “More Information” on page 617 for references.
+   * **Unsupported wireless NICs**
+     If a wireless network card is not supported under Linux directly, you may be able to get it to work using NdisWrapper (ndiswrapper.sourceforge.net; also available as an rpm file from the Fedora and RHEL5 repositories at rpmfusion.org), which uses Win32 drivers. NdisWrapper is a kernel module that provides a subset of the Windows network driver API. No Fedora/RHEL package contains this program.
+   * **Wireless bridge**
+     An alternative to a wireless NIC is a wireless bridge. A wireless bridge forwards packets between wired and wireless interfaces, eliminating the need for wireless drivers. This simple device contains an Ethernet port that plugs into a NIC and an 802.11 (wireless) controller. While carrying a bridge around is usually not feasible for mobile users, it is an easy way to migrate a desktop computer to a wireless configuration.