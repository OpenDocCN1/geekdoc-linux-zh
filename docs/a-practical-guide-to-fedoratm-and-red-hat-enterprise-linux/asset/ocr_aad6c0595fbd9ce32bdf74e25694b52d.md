![](bbox=[0.15, 0.09, 0.85, 0.4])

# ## CONNECTING THE COMPUTERS

Computers are connected to a network using cables (wired; page 285) or radio waves (wireless or Wi-Fi, page 287). The cables can connect to a variety of devices, some of which are described in this section. See “LAN: Local Area Network” on page 284 for an explanation of cables and definitions of *hub*, *switch*, and *router*.

In the simple star network shown in Figure 16-1, four computers are connected to a single hub or switch. Assume computers 1 and 2 are communicating at the same time as computers 3 and 4. With a hub (page 285), each conversation is limited to a maximum of half the network bandwidth. With a switch (page 285), each conversation can theoretically use the full network bandwidth.

+   * **WAP (wireless access point)** A WAP (wireless access point) connects a wireless network to a wired one. Typically a WAP acts as a transparent bridge, forwarding packets between the two networks as if they were one. If you connect multiple WAPs in different locations to the same wired network, wireless clients can roam transparently between the WAPs.

Wireless networks do not require a hub or switch, although a WAP can optionally fill the role of a switch. In a wireless network, the bandwidth is shared among all nodes within range of one another; the maximum speed is limited by the slowest node.

# ## ROUTERS

A router (page 287) connects a LAN to another network, such as the Internet. A router can perform additional functions, the most common of which is allowing several systems to share a single Internet connection and IP address (NAT; page 910). With NAT, the packets from all systems on the LAN appear to come from a single IP address; the router passes return packets to the correct system. A router can also provide firewall services.