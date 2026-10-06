# 12.2.1 Properties of Transparent Bridges

In accord with the definition in Section 12.2, a Linux system can be used to implement a local transparent translation¹ bridge, which can interconnect different 802.x LANs. Figure 12–1 shows an example in which the Linux computer acts as a bridge, connecting three LANs of different types: one Ethernet (IEEE 802.3), one Fast Ethernet (IEEE 802.3u), and one wireless LAN (IEEE 802.11).

When we use a translation bridge to link different 802.x LANs, the properties of the different sets of protocols have to be adapted. For example, the bridge should consider the different access methods of the interconnected LANs; it should also consider and convert different packet formats. In addition, we have to consider that properties could be lost during the translation from one LAN to another type. Examples include priorities or acknowledgments in 802.5 networks, because the latter dont have anything comparable. Linux currently supports only the connection of local area networks that use an Ethernet-compatible format on MAC level.

The transparent bridge in Figure 12–1 is responsible for switching data packets between the three networks used to communicate. Data packets (which are also called frames on layer 2) allow the stations in these three networks to communicate, and with their destination within one local area network are not transported to the other two LANs—internet and intranet traffic is separate.

The bridge need forward only those data packets intended for another LAN. This translates into a considerable reduction of the network load, because internal traffic remain within the LANs and parallel communication is possible internally in each of these LANs. If a computer in one LAN wants to send data to another LAN, then only those LANs required for the transport are used. In addition, the bridge ensures that faulty data packets are filtered and prevented from being transported to the other networks. The filtering concept supported by bridges will be described in Section 12.2.2.

Transparent bridges are characterized mainly by the fact that they are hidden from the stations in the network. In addition, they forward frames from one LAN into another LAN independently. To both the inside and the outside, it seems like there is one large IEEE-802.2-compatible network. The bridge does not consider protocols used on the network layer; you can select arbitrary protocols.

To achieve transparency, each bridge maintains a table (forwarding database) that stores the output line used to reach a station for each layer-2 address. We will see in Section 12.4.2 how this forwarding table is implemented in Linux.

The properties of how a Linux bridge introduced above will be discussed in more detail in the next sections.

> however, with the limitation that the 802.x networks are compatible, mainly with regard to their maximum frame lengths. For example, 802.3 and 802.11 can easily be combined, but problems could arise when they use 802.5 LANs.