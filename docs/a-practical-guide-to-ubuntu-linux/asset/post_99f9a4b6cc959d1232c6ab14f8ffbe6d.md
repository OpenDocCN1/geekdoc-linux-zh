
You can use an extranet (also called a partner net) or a virtual private network (VPN) to improve security. These terms describe ways to connect remote sites securely to a local site, typically by using the public Internet as a carrier and employing encryption as a means of protecting data in transit.

Following are some terms you may want to become familiar with before you read the rest of this chapter:

- ASP (page 1135) hub (page 1152) packet (page 1164)
- bridge (page 1138) internet (page 1154) router (page 1170)
- extranet (page 1147) Internet (page 1154) sneakernet (page 1172)
- firewall (page 1148) intranet (page 1154) switch (page 1175)
- gateway (page 1149) ISP (page 1155) VPN (page 1180)

# TYPES OF NETWORKS AND HOW THEY WORK

Computers communicate over networks using addresses assigned by software. A computer message, called a packet, frame, or datagram, includes the address of the destination computer and the sender's return address. The most common types of networks are broadcast, point-to-point, and switched. One popular, token-based networks (such as FDDI and token ring) are rarely seen anymore.

Speed is critical to the functioning of the Internet. Newer specifications (cat 6 and 7) are being standardized for 1000BaseT (1 gigabit per second, gigabit Ethernet, or Gig-E) and faster networking. Some of the networks that have the backbone of the Internet run at almost 40 gigabits per second (OC768) to accommodate the ever-increasing demand for network services. Table 10-1 lists some of the specifications in use today.

| Specification | Speed |
| --- | --- |
| DSO | 64 kilobits per second |
| ISDN | Two DSO lines plus signaling (16 kilobits per second) or 128 kilobits per second |
| T-1 | 1.544 megabits per second (24 DSO lines) |
| T-3 | 43.232 megabits per second (28 T-1s) |
| OC3 | 155 megabits per second (100 T-1s) |
| OC12 | 622 megabits per second (4 OC3s) |
| OC48 | 2.5 gigabits per second (4 OC12s) |
| OC192 | 9.6 gigabits per second (4 OC48s) |
| OC768 | 38.4 gigabits per second (4 OC192s) |

# BROADCAST NETWORKS

On a broadcast network, as Ethernet, any of the many systems attached to the network cable can send a message at any time; each system examines the address in each message and responds only to messages addressed to it. A problem occurs in a broadcast network when multiple systems send data at the same time, resulting in a collision of the messages on the cable. When messages collide, they become garbled. The sending system notices the garbled message and resends it after waiting a short but random amount of time. Waiting a random amount of time prevents those systems from resending the data at the same moment and experiencing another collision. The extra traffic that from collisions can strain the network; if the collision rate gets too high, retransmissions may result in more collisions. Ultimately the network may become unusable.

# POINT-TO-POINT NETWORKS

A point-to-point link does not seem like much of a network because only two endpoints are involved. However, most connections to WANs (wide area networks) go through point-to-point links, using wire cable, radio, or satellite links. The advantage of a point-to-point link is its simplicity: because only two systems are involved, the traffic on the link is limited and well understood. A disadvantage is that each system can typically be equipped for only a small number of such links; it is impractical and costly to establish point-to-point links that connect every computer to all others. Point-to-point links often use serial lines and modems. The combination of modem with point-to-point link allows an isolated system to connect to a larger network. The most common types of point-to-point links are the ones used to connect to the Internet. When you use DSL (digital subscriber line), you are using a point-to-point link to connect to the Internet. Serial lines, such as T-1, T-3, ATM, and ISDN, are all point-to-point. Although it might seem like a point-to-point link, a cable is based on broadcast technology and is similar to Ethernet.

# SWITCHED NETWORKS

A switch is a device that establishes a virtual path between source and destination hosts in such a way that each path appears to be point-to-point. The switch creates and tears down virtual paths as hosts seek to communicate with each other. Contrast this approach with a broadcast network, where each host also sees traffic for other hosts. The advantage of switched network over point-to-point network is that each requires only one connection. Scalability is provided by further linking. The term DSL incorporates a suite of technologies, which includes ADSL, SDSL, and HDSL.

# LAN: LOCAL AREA NETWORK

Local area networks (LANs) are confined to a relatively small area—a single facility, building, or campus. Today LANs run over copper or fiber optic (glass or plastic) cable, but other wireless technologies, such as infrared (similar to television remote control devices) and radio wave (wireless, or Wi-Fi), are becoming popular. If its destination address is not on the local network, a packet must be passed to another network by a router. A router may be a general-purpose computer or special-purpose device attached to multiple networks to act as a gateway between them.

# ETHERNET

A system connected to a LAN usually connects to a network using Ethernet. A typical Ethernet connection can support data transfer rates from 10 megabits per second to 1 gigabit per second, with further speed enhancements planned for the future. As a result of computer load, competing traffic and network overhead, transfer rates on an Ethernet are always slower than the maximum theoretical transfer rate. An Ethernet network transfers data using copper or fiber optic cable or wireless transmitters and receivers. Originally, each computer was attached to a thick coaxial cable (called thnet) at tap points spaced at sixfoot intervals. The thick cable was awkward to deal with, so other solutions, including a thinner coaxial cable called 10Base2 developed. Most Ethernet connections are either wireless or made of unshielded twisted pair (referred to as UTP, Category 5 [cat 5], Category 5e [cat 5e], Category 6 [cat 6], 10BaseT, or 100BaseT)—similar to the type of wire used for telephone lines and serial communications.

- Segment A network segment is a part of a network in which all systems communicate using the same physical layer (layer 1) of the IP and OSI models (page 380).
- Duplex In half-duplex mode, packets travel in one direction at a time over the cable. In duplex mode, packets travel in both directions.
- Hub A hub (sometimes called a concentrator) is a device that connects systems so they are all of one network segment and share the network bandwidth. Hubs work at the physical layer of the IP and OSI models (layer 1, page 380).
- Switch A switch connects network segments. A switch identifies which devices are connected to which of its ports. The switch sends each packet only to the device it is intended for. Because a switch sends packets only to their destination devices, it can conserve network bandwidth and perform better than a hub. A switch may have buffers for holding and queuing packets. Switches work at the data link layer of the IP and OSI models (layer 2, page 380).
- 2. Versions of Ethernet are classified as BaseY, where X is the data rate in megabits per second, Base baseband (as opposed to radio frequency), and Y is the category of cabling.

Some Ethernet switches have enough bandwidth to communicate simultaneously, in full-duplex mode, with all connected devices. A nonswitched (hub-based) broadcast network can run in only half-duplex mode. Full-duplex Ethernet improves performance by eliminating collisions. Theoretically, each host on a switched network can transmit and receive simultaneously at the speed of the network (e.g., 100 megabits per second) for an effective bandwidth between hosts of twice the speed of the network (e.g., 200 megabits per second), depending on the capacity of the switch.

A router connects networks. For example, a router can connect a LAN to a WAN (as the Internet). A router determines which paths should take travel to a different network and forwards the packets. Routers work at the network layer of the IP and OSI models (layer 3, page 380). The next page covers routers in more depth.

# WIRELESS

Wireless networks are becoming increasingly common. They are found in offices, homes, and public places, such as universities, coffee shops, and airports. Wireless access points provide functionality similar to an Ethernet hub. They allow multiple users to interact via a common radio frequency. A wireless, point-to-point connection allows you to wander about your home or office with a laptop, using an antenna to link to a LAN or to the Internet via a base station. A wireless access point, or base station, connects a wireless network to a wired network so that no special protocol is required for a wireless connection. Refer to the Linux Wireless HOWTO at [URL].

# WAN: Wide Area Network

A wide area network (WAN) covers a large geographic area. In contrast, the technologies (such as Ethernet) used for LANs were designed to work over limited distances and for a certain number of host connections. A WAN may span long distances over dedicated data lines (leased from a telephone company) or radio or satellite links. These networks are often used to interconnect LANs. Major Internet providers rely on WANs to connect to their customers within a country and around the globe.

Some networks do not fit into either the LAN or the WAN designation. A metropolitan area network (MAN) is a network that is contained in a smaller geographic area, such as a city. Like WANs, MANs are typically used to interconnect LANs.

# Internetworking Through Gateways and Routers

A LAN connects to a WAN through a gateway, a generic term for a computer or special device with multiple network connections that passes data from one network to another. A gateway converts the data traffic from the format used on the LAN to that used on the WAN. Data crosses the country from one Ethernet to another over a WAN, for example, is repackaged from the Ethernet format to a different format that can be processed by the communications equipment that.
