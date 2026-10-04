this is usually the primary factor in picking one. These are all free or open-source applications except for AiroPeek, which is listed because of its popularity and relative low price compared to other commercial wireless network analyzers.

# # NetStumbler

NetStumbler (www.netstumbler.com) is a freeware-driving tool that will give you a list of discovered networks with the MAC, SSID, channel, WEP status, and other management information. It supports most GPS devices and exports to a plain text and wi-scan formatted output in addition to its own proprietary format. It works with Hermes (Lucent)-based cards in Windows 2000, but in Windows XP via the NDIS 5.1 it can support some other cards such as a Cisco 350 or Prism 2 chipset interface to discover networks; sends out a request on each channel looking for an access point configured to respond. Most APs are set to respond probe by default but have a configuration option to disable. When this is disabled, NetStumbler is unable to see the network, and you will have to go to an application that uses monitor-mode to see beacons and association packets to enumerate the network. NetStumbler is the most widely used WLAN discovery tool, despite its shortcoming that it relies on broadcast responses only. Refer to Figure 15.5 for a look at the NetStumbler interface; it will list each discovered network with the MAC address of the access point with a color to indicate signal strength.

# ## Figure 15.5 The NetStumbler Interface

![](bbox=[0.258, 0.613, 0.715, 0.778])

# # AiroPeek NX

AiroPeek NX (www.wildpackets.com) is a full-function commercial 802.11 network analysis tool. Although its capabilities are intended for network troubleshooting, they can also be easily adapted for WLAN discovery. To use AiroPeek for discovery, complete the following steps: