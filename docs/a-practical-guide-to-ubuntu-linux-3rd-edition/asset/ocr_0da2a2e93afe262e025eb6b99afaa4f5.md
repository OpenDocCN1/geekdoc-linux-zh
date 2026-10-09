![](bbox=[0.29, 0.09, 0.84, 0.34])

**Figure 17-1** A simple network

+   * You can set up an Ubuntu system as a router. The Linux kernel can use **gufw** (page 876) or **iptables** (page 880) to implement a firewall to help protect a system.

+   * You can use a special-purpose distribution/operating system tailored for use as a router. For example, SmoothWall (www.smoothwall.org), pfSense (www.pfsense.com), and m0n0wall (m0n0.ch/wall) provide browser-based configurations in the style of a hardware router.

# NIC: NETWORK INTERFACE CARD

Each system’s NIC may be a separate Ethernet card (wired or wireless) or the NIC may be built into the motherboard.

| **Supported NICs** | Linux supports most wired and many wireless Ethernet NICs. |
|---|---|
| **Unsupported wireless NICs** | If a wireless network card is not supported under Linux directly, you may be able to get it to work with NdisWrapper (sourceforge.net/projects/ndiswrapper), **ndiswrapper-common**, **ndiswrapper-utils-1.9**, and **ndisgtk** packages, which uses Win32 drivers. NdisWrapper is a kernel module that provides a subset of the Windows network driver API. See help.ubuntu.com/community/WifiDocs/Driver/Ndiswrapper for instructions on installing a Windows driver. |
| **Wireless bridge** | An alternative to a wireless NIC is a wireless bridge. A wireless bridge forwards packets between wired and wireless interfaces, eliminating the need for wireless drivers. This simple device has an Ethernet port that plugs into a NIC and an 802.11 (wireless) controller. While carrying a bridge around is usually not feasible for mobile users, a wireless bridge is an easy way to migrate a desktop computer to a wireless configuration. |