
capability to expand its usefulness beyond what the user can buy off the shelf and install from CD, instantly and without any physical media being introduced. The advent of networking and what it means for business and recreation is what has fueled the computer revolution that is very likely behind your decision to use FreeBSD.

The de facto standard protocol suite that runs almost all active networks these days is the Transmission Control Protocol/Internet Protocol (TCP/IP). Networking—especially FreeBSD networking—has become nearly synonymous with TCP/IP in recent years. TCP/IP, whose fundamental structure we will be examining in some detail later in this chapter, has enjoyed some thirty years of development and maturity, and its extensibility and modularity are part of what has contributed to its success. Although the first recognized computer network—the United States Department of Defense-funded ARPAnet—dates back to 1969, when its first four nodes were brought online at four universities in the western US, TCP/IP itself has its roots in a 1974 paper by Internet design pioneers Vint Cerf and Bob Kahn titled “A Protocol for Packet Network Interconnection.” The Transmission Control Program, later to become split into TCP (Transmission Control Protocol) and IP (Internet Protocol), demonstrated a way that data could be sent reliably over the packet-switching networks that were then still newly discovering their usefulness. UNIX systems from Bell Labs, first released in 1977, helped to popularize the new protocol suite and some of the variants that fell into its layered structure, including UDP and ICMP. Thus, the foundations of FreeBSD’s TCP/IP heritage were laid. Today, the TCP/IP suite implemented by FreeBSD is known as the reference implementation. Other software vendors use FreeBSD’s model for determining how TCP/IP should correctly work. This is a result of FreeBSD’s Unix roots and the original Bell Labs and Berkeley code that still forms the core of its networking subsystem.

The TCP/IP suite forms the backbone for the Internet and all its trappings. It’s just about the only game in town for network traffic over wide area network (WAN) links, such as the telecommunications links between geographical regions. TCP/IP also is quite prevalent in local area networks (LANs). Most LANs are high-speed corporate, enterprise, or university networks connected directly through Ethernet or similar physical-link protocols.

A standardized model for the networking “stack,” known as Open Systems Interconnection (OSI), establishes the general structure of TCP/IP. OSI dictates as many as seven “layers” of implementation for a computer network, each of which has its own measure of specificity and its own functional applicability to the user, the software, the operating system, and the networking hardware. The conceptual arrangement of the OSI model, as exemplified in the Internet’s typical usage, is shown in Figure 21.1.

![](img/48eec858cce7dfb89da36a4d40b7daf3_510_0.png)

**FIGURE 21.1** OSI stack layering diagram, as it is used in TCP/IP.

In an OSI stack, data travels from the highest level (the user-interface level, where it is in its most specialized form, allowing the user to interact with it using a variety of interface metaphors, such as command lines and windowing systems) progressively down to its lowest level, where it is at its most generic and abstract form—a form that can be handled by very simple hardware and software protocols. This is achieved by each layer of the stack wrapping the data in “headers,” or abstraction layers that allow the data to be decoded later by another TCP/IP stack, when the data reaches that layer on the way down. At the very bottom, the data is not “Web pages” or “e-mail.” Instead, it’s just ones and zeroes that the Ethernet card knows to send to another Ethernet card. All the packaging tells the remote Ethernet card what to do with the data—whether it is destined for that card’s machine (in which case it should pass the data further on up the stack for decoding and delivery) or for another computer elsewhere on the network—or even on another network, in which case the data is forwarded on.

The different layers of the stack define different levels of addressing and routing specificity. The IP layer, the component that corresponds to the “network” layer of the stack, knows how to send packets of data to other computers on the Internet, as defined by their IP addresses. TCP and UDP, which you will learn about later, are protocols that exist higher up the stack, in the “transport” layer. These rely on the network layer’s ability to deliver packets, but they add their own specific methods of delivery. Below IP, the “data link” layer knows nothing about IP addresses—all it knows about is the hardware addresses on other Ethernet cards on the network. However, because IP information is embedded in any packet that the data link layer receives to transmit, the receiver will know where on the Internet it's supposed to go.

Many other protocols exist at the various levels of the OSI stack, and they each play a part in routing traffic to its destination and ensuring its integrity. This chapter discusses how all these protocols fit into the TCP/IP structure and how FreeBSD deals with them.

## Network Topologies

Your FreeBSD machine might be installed on a university network, in a professional co-location facility, within a corporate enterprise network, or on a home dial-up network (or dialed-up directly). These are just the most common types of settings. Different network topologies, or logical layouts of devices and data link mechanisms, are as numerous as the individual networks in the world—no two are exactly the same. However, virtually all networks share a common basic topology and a few fundamental components.

In Figure 21.2, you can see the type of topology that would be found in a typical home network. The topology shown here is also serviceable as a simplified diagram of an enterprise or university network.

![](img/48eec858cce7dfb89da36a4d40b7daf3_511_0.png)

**FIGURE 21.2** A basic network topology, showing a WAN and a LAN, separated by a router and comprising a number of different types of computers.

Most basic network topologies involve a WAN, a relatively low-speed serial link to the Internet, such as a T1, T3, DSL, or cable modem connection. These link types are often referred to generically as “broadband,” although the mechanisms for each are widely different, and a WAN does not have to be “broadband,” as the term is popularly defined. The bandwidth (or speed) of WAN links can range from the kilobits per second, in the case of 33–56Kbps modems, up through the massively infrastructural OC-3, OC-12, OC-48, and OC-192 links used between major telecommunications operators. Table 21.1 shows the equivalent speeds of most of the common WAN link types.

**TABLE 21.1** Serial WAN Link Types and Corresponding Transfer Speeds

| Link Type | Speed | Equivalency |
|---|---|---|
| Modem | Up to 56Kbps | |
| ISDN | 56-128Kbps | |
| DSL | 192Kbps-1.5Mbps | |
| Cable modem | 1Mbps-5Mbps | |
| T1 | 1.5Mbps | 24 D50 lines |
| T3 | 43.2Mbps | 28 T1 lines |
| OC-3 | 155Mbps | 100 T1 lines |
| OC-12 | 622Mbps | 4 OC-3 lines |
| OC-48 | 2.5Gbps | 4 OC-12 lines |
| OC-192 | 9.6Gbps | 4 OC-48 lines |

These WAN link types are designed to run over very long distances. Because of their serial nature, they can carry traffic over telephone copper, fiber-optic lines, and any other infra-structure that carries standard telephone network “trunk” traffic. In fact, data traffic over these lines is indistinguishable from voice traffic; it’s treated exactly the same way by phone switching equipment and travels from one geographical location to another the same way a phone call would.

> **NOTE**  
> Actually, digital switching equipment is becoming more prevalent with time; whereas analog signals are opaque to any switching equipment beyond a very rudimentary level, digital signals can be differentiated easily by the right kinds of equipment. For the most part, though, WAN lines carry data and voice traffic the same way.

Another type of network topology is the Internet Service Provider (ISP) model, which involves a primary network like the one shown in Figure 21.2. This architecture also includes a secondary WAN that connects the network to a large number of home users dialing up via modems and phone lines. This is illustrated in Figure 21.3.
