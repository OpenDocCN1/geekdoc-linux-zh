
![](img/1744bde8c889adfab3fc911e1687fecf_622_0.png)

Figure 15-4 Wireless communication can go through an access point.

- Multiple wireless access points and roaming — Each wireless network can be configured as a separate cell. Multiple cells can be joined together in what is called a Managed Wireless LAN. In this arrangement, each cell’s access point acts as a bridge (in fact, its actions are referred to as bridging) by passing all data from the cell to other cells without changing any node’s MAC address. In other words, the managed wireless LAN makes the fact that there are multiple wireless cells invisible to the clients on those cells. This arrangement allows users to roam among cells as they come in and out of range without losing continuity of communication.

> NOTE: Although Linux does not support any wireless LAN cards that can act as a bridging wireless access point, you can have the Linux system act as a client to a bridging access point. Set your card to Managed mode and identify the MAC address for your wireless LAN’s access point.

For our purposes, we focus on star, bus, and wireless topologies. Common to all of these topologies is the protocol used to send data over those wired and wireless media — the Ethernet protocol.

## 604 Part IV: Red Hat Linux Network and Server Setup

### LAN equipment

The equipment that you need to connect your LAN can include some or all of the following:

> CROSS-REFERENCE: For a complete description of wireless hardware, see the “Choosing wireless hardware” section later in this chapter.

- Network Interface Card (NIC) — Typically, one of these cards goes into a slot in each computer. For wired Ethernet networks, the cards can transmit data at 10 Mbps or 100 Mbps. Gigabit (1000 Mbps) NICs are also now available, but are quite a bit more expensive. An 802.11B wireless NIC card can operate at speeds of up to 11 Mbps, but will be more expensive than a wired NIC card.

> **TIP:** If you are looking to upgrade your network in the near future, but still have a lot of computers around that run at 10 Mbps, you may want to consider buying new NICs that run at both 10 Mbps and 100 Mbps. When you switch over to 100 Mbps, you will have fewer cards to replace.

- Cables — Star and bus topologies require different cabling. Wireless LANs, as you might guess, require no cables, but may require additional antennas depending on the distances and obstacles (see the section “Setting Up a Wireless LAN” for details).

For star topologies, cables are referred to as *twisted-pair*. Category 5 wiring, which contains four twisted-pair sets per wire, is the most common type of wiring used for LANs today. A connector at each end of the cable is an RJ-45 plug, similar to those used on telephone cables. Ethernet interfaces are either 10Base-T (10 Mbps speeds) or 100Base-TX (100 Mbps speeds). These cables plug into the computer’s NIC at one end and the hub at the other.

For bus topologies, coaxial cables are used. These cables are also referred to as thin Ethernet cables, or *thin net*. (There are also thick net cables, which are more expensive and more cumbersome to deal with. These are rarely used and are primarily for network backbones.)

The connector on coaxial cables is a barrel connector (BNC). A “T” connector attaches to the BNC port on the NIC. In the middle of the daisy chain, each computer connects to two adjacent computers using the T connector. At the two ends of the chain, the computer connects to one adjacent computer, then uses a terminator at the other end of the T to end the chain.

Figure 15-5 shows an example of a twisted-pair cable with an RJ-45 connector used for star topologies. Figure 15-6 shows a coaxial (thin net) cable with a BNC connector and a T connector used for bus topologies. A terminator at the end of the T connector shows that this is the end of a chain. If it were in the middle of the chain, the other side of the T would be connected to the next computer in the chain.

![](img/1744bde8c889adfab3fc911e1687fecf_623_0.png)

Figure 15-5: A star topology’s twisted-pair cables have RJ-45 connectors (similar to telephone-cable connectors).

![](img/1744bde8c889adfab3fc911e1687fecf_624_0.png)

**Figure 15-6:** A bus topology has coaxial cables that must be terminated (as shown) or continued from the T.

- Hubs — With the star topology, a hub is typically used to connect the computers. For the bus topology a hub can be used, but is not necessary. Sometimes hubs are also referred to as repeaters or concentrators because they receive signals from the nodes connected to them and send the signals on to other nodes. Intel and 3Com make popular, inexpensive hubs for small offices.

The questions you need to answer when choosing a hub are how many ports you need and how fast you want your network to go. If you need to expand in the future, hubs can be connected together. Choice of speeds is 10 Mbps or 100 Mbps. The higher speed means more expensive cards and a more expensive hub, but significantly better performance. Some 10 Mbps hubs offer one or more coaxial connectors.

- Switches — A switch lets you divide subnetworks that are getting too large into segments that are more manageable. A switch can reduce network traffic by directing messages intended for a specific computer directly to that computer. This is as opposed to a hub, which broadcasts all data to all nodes.

One piece of equipment that I won’t go into yet is a router. A router is used to direct information from the LAN to other LANs or the Internet.

> **CROSS-REFERENCE:** Machines that carry out routing functions are described in Chapter 16.

## Choosing peer-to-peer versus client/server models

Although the Ethernet hub sees all computers on the network as equal, the computers on that hub can actually play different roles. The models used to describe the two general types of computing environments are client/server and peer-to-peer. Red Hat Linux is usually described as a server computer. However, Red Hat Linux can also function quite happily as a client machine or in a peer-to-peer network.

### Client/server model

In a client/server model, one or more server computers manage most network services. The server acts as a focal point for administration and security of the network. It may also control printers, databases of information, backup media, and other resources that need to be made available to client computers on the network. The client is the person (or more correctly, the software program) that requests services from the network.

A server computer can act as a server for some or all of these services:

- Print Server — This maintains and manages one or more printers.
- File Server — A central repository for documents and databases of information.
- Mail Server — This gathers e-mail intended for clients on the network and makes it accessible to those clients.
- FTP Server — This is used to make files available to users who log in to the server over the network. (Anonymous FTP is a way of making files available to strangers.)
- Web Server — This makes Web pages (HTML) and related content available to users on the network.
- News Server — This gathers messages from Usenet newsgroups, allowing users to read and respond to topics of interest.

Red Hat Linux can act as any of the server types described above. However, with a growing number of productivity applications becoming available for Linux and friendly X-based desktops (such as KDE and Gnome), Red Hat Linux is beginning to make a better case for becoming a client system as well.

Because Red Hat Linux can run applications as well as offer services, a purer example of a network server is NetWare (from Novell, Inc.). A NetWare server has no way of running applications. It is tuned to store and secure files efficiently, as well as manage groups of printers.

> **CROSS-REFERENCE:** Chapters 17 through 25 describe how to set up different kinds of servers in Red Hat Linux.

### Peer-to-peer model

In a peer-to-peer network, computers generally behave as equals. Each computer has most of what it needs to operate on its own. Any computer on the network may offer services to other computers. One computer may share the contents of a file system, whereas another may offer its printer for use by others.

A typical peer-to-peer network is one where several employees in a business each have a computer at their desk. A shared printer may be connected to one person’s computer, whereas a tape backup system may be connected to another.

The drawback with peer-to-peer networks is that if there is a big demand for your printer or other device, your computer’s performance may suffer (and so may your work). That’s why larger networks tend to offload shared services to a server.
