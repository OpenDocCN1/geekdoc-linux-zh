# Setting Up Network Connections and LANs

Although Linux does not support any wireless LAN cards that can act as a bridging wireless access point, you can have the Linux system act as a client to a bridging access point. Set your card to *Managed* mode, and identify the MAC address for your wireless LAN’s access point. For information on the current state of wireless Ethernet bridging, refer to the Bridging page at the OSDL web site (http://linux-net.osdl.org/index.php/Bridge).

For our purposes, we focus on star (wired) and peer-to-peer (wireless) topologies. Common to both of these topologies is the protocol used to send data over those wired and wireless media — the Ethernet protocol.

# LAN Equipment

The equipment that you need to connect your LAN can include some or all of the following:

For a complete description of wireless hardware, see the “Choosing Wireless Hardware” section later in this chapter.

+   - **Network Interface Card (NIC)** — Typically, one of these cards goes into a slot in each computer. For wired Ethernet networks, the cards can transmit data at 10 Mbps (megabits per second) or 100 Mbps. Gigabit (1,000 Mbps) NICs are also available and have recently dropped quite a bit in price. An 802.11b wireless NIC card can operate at speeds of up to 11 Mbps but is more expensive than a wired NIC card. Recently, 802.11g cards have become much more popular, as well as coming down drastically in price.

+   - **Cables** — For star topologies, cables are referred to as *twisted-pair*. Category 5e wiring, which contains four twisted-pair sets per wire, is the most common type of wiring used for LANs today. A connector at each end of the cable is an RJ-45 plug, similar to those used on telephone cables. Ethernet interfaces are either 10Base-T (10-Mbps speeds) or 100Base-TX (100-Mbps speeds). These cables plug into the computer’s NIC at one end and the hub at the other.
+   
+     Figure 14-6 shows an example of a twisted-pair cable with an RJ-45 connector used for star topologies.

+   - **Hubs** — With the star topology, hubs were once the most popular way to connect computers. With low-cost network switches becoming more popular, however, hubs are now less often used. Sometimes hubs are also referred to as *repeaters* because they receive signals from the nodes connected to them and send the signals on to other nodes.

+   - **Switches** — Switches are now more commonly used than hubs. Switches let you divide a LAN that is getting too large into segments that are more manageable. A switch can reduce network traffic by directing messages intended for a specific computer directly to that computer. This is as opposed to a hub, which broadcasts all data to all nodes. Because switches have come down so much in price, in most cases, you should just pay a few extra dollars and get a switch instead of a hub. Besides the common 10/100-Mbps switches, Gigabit switches (1,000 Mbps) are now available for economical prices.