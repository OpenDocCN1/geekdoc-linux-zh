gateway to the Internet or, for example, a campus intranet. Figure 15-4 depicts a point-to-point wireless LAN.

![](bbox=[0.25, 0.14, 0.8, 0.32])

Figure 15-4: Wireless communication can go through an access point.

+   - **Multiple wireless access points and roaming** — Each wireless network can be configured as a separate cell. Multiple cells can be joined together in what is called a *Managed Wireless LAN*. In this arrangement, each cell’s access point acts as a bridge (in fact, its actions are referred to as *bridging* by passing all data from the cell to other cells without changing any node’s MAC address. In other words, the managed wireless LAN masks the fact that there are multiple wireless cells invisible to the clients on those cells. This arrangement allows users to roam among cells as they come in and out of range without losing continuity of communication.

> **NOTE:** Although Linux does not support any wireless LAN cards that can act as a bridging wireless access point, you can have the Linux system act as a client to a bridging access point. Set your card to Managed mode and identify the MAC address for your wireless LAN’s access point.

For our purposes, we focus on star (wired) and peer-to-peer (wireless) topologies. Common to both of these topologies is the protocol used to send data over those wired and wireless media — the Ethernet protocol.

# LAN equipment

The equipment that you need to connect your LAN can include some or all of the following:

> **CROSS-REFERENCE:** For a complete description of wireless hardware, see the “Choosing wireless hardware” section later in this chapter.

+   - **Network Interface Card (NIC)** — Typically, one of these cards goes into a slot in each computer. For wired Ethernet networks, the cards can transmit data at 10 Mbps or 100 Mbps. Gigabit (1000 Mbps) NICs are also now available, but are quite a bit more expensive. An 802.11b wireless NIC card can operate at speeds of up to 11 Mbps, but is