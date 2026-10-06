The first task is solved by the Internet Group Management Protocol (IGMP), which has to be supported by each multicast-capable Internet computer. Section 17.3 introduces IGMP and its implementation in Linux systems. For the second task, we have to distinguish between end system and forwarding systems. Section 17.4 will discuss how both types are supported in Linux. As with Internet routing, group communication also separates clearly between forwarding and routing. There are different multicast routing algorithms, including the Distance Vector Routing Protocol (DVMRP), which which will be introduced in Section 17.5.2 as a representative example for these algorithms, using the routed daemon.

# GROUP COMMUNICATION

Before we introduce the details of IP multicast in Linux, the following sections give a brief summary of the three communication forms: unicast, broadcast, and multicast.

# Unicast

Unicast is the classic form of communication between two partners—point to point. In the context of this book, this means that two computers communicate with each other only. When a unicast communication service is used to transmit data to several receivers, this has to be done independently of one another in several processes. This means that the cost for the data transport increases in proportion to the number of receivers, as shown in Figure 17–1.

Naturally, if there is a large number of receivers, this cost leads to an extreme load on the network, and so this technique is unsuitable for the distribution of large data volumes, such as multimedia data. Broadcast communication represents a better solution in some cases.

![](bbox=[0.153, 0.613, 0.883, 0.876])

FIGURE 17–1 In unicast communication, the packet is sent to each receiver separately.