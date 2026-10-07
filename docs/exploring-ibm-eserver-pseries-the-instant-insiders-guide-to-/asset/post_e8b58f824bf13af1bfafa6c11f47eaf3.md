
# pSeries Communications 251

Each the overall productivity of the users participating in it. Slow communications can translate to slow response time, leading to frustration and reduced concentration.

The price one for the high-speed communications available with LANs is limited distance, as the term “local” in “local area network” indicates. Because of electrical limitations, LANs cannot be used as a direct communications link between distant computers (e.g., computers across town from one another). However, multiple LANs can be linked together over more traditional communications links (e.g., WANs–wide area networks).

Each computer that participates in a LAN is a node in the network. A pSeries system can act as either a client node or a server node. A client node can operate as any normal standalone pSeries system and can also participate in LAN communications. Any shared resources on the network are accessible by a client node, but the client node itself offers no resource for other nodes to do and can also offer resources, such as disk storage or a printer, for use by the other nodes in the network. pSeries users participating in a LAN have three basic advantages over similar users not connected by a LAN:

- Data sharing
- Program sharing
- Equipment sharing

Today, data sharing is often the major reason to connect computers via a LAN. It is typical for many users to need access to the same body of information (e.g., design standards, image libraries, telephone directories, inventory information, etc.). With a LAN and the proper application programs, multiple users can simultaneously access to a single body of information. Further, that information can be located on any computer (or even many computers) in the LAN.

Because programs are stored in files, just like data, application programs available on one pSeries system can be loaded and executed by another pSeries in the network, subject to the applicable software licensing terms. An even more powerful use of program sharing is when one application program on a client (a client application) communicates directly with an application program on a server (a server application).

## 252 Exploring IBM@server pSeries

This direct program-to-program interaction allows for the development of very powerful systems of application programs that run on different computers in a LAN and work together. In such an environment, information located anywhere in the network is at the fingertips of any authorized user on the network. Also, specific server applications can be located on the computer system best suited for the task they provide services to all network users.

Equipment sharing is another reason to connect computers via a LAN. Equipment sharing allows server nodes participating in a LAN to share their disk space, printers, communications equipment, and so forth with other nodes in the LAN. This equipment-sharing function allows for more efficient use of the computing environment participating in the LAN.

With this understanding of LANs, we will now examine two LANs commonly used with pSeries systems: Ethernet and Token-Ring. It should be understood that many variations and combinations of the simple examples that follow are also possible.

## pSeries and the Ethernet LAN

Ethernet is a type of LAN commonly used in the open-system arena. The Ethernet LAN is widely supported by many different computer manufacturers, which is why it is commonly found in open-system environments. Ethernet LANs often consist of a mixture of different types and bands of computers.

Figure 4.5 shows the basic structure of an Ethernet LAN using the Carrier Sense Multiple Access/Collision Detect (CSMA/CD) protocol described in Chapter 2. Since each computer is attached as a tap-off from a common access or information bus, this type of Ethernet is called a bus-wired network. As pointed out in Chapter 2, most Ethernet systems use hubs to which each node is attached rather than the bus shown in the figure, eliminating the need for each node to handle collisions. Instead, the Ethernet handles the contention among the nodes. Today's Ethernet networks can transfer information at rates of 10 million bits per second (10 Mbps), 100 million bits per second (100 Mbps), or 1 billion bits per second (1 Gbps).

The Ethernet is probably the most commonly supported LAN technology, available with almost every type of computer and every operating system. An Ethernet LAN can, for example, consist of pSeries systems, personal computers running Microsoft Windows, shared printers, or any open-system computer, as long as TCP/IP communication is supported over an Ethernet LAN.

## pSeries Communications 253

![](img/29c52a1767a1e621ce6343faa9399737_279_0.png)

**Figure 4.5.** The basic structure of an Ethernet local area network.

There are many Ethernet attachment options available for pSeries systems. In Chapter 2, eight Ethernet adapters are described (see Figure 2.13) in addition to the integrated Ethernet ports for pSeries systems.

With the availability of gigabit Ethernet adapters for fiber-optic connection and 100/100/1000 Mbps Ethernet adapters for UTP (copper) links, Ethernet is the primary technology for high-speed links among servers. Integrated 100/100/1000 Mbps Ethernet controllers, as available on the p65, will probably become standard in future pSeries designs, and there are dual-port Ethernet adapters that operate at gigabit speeds. The Ethernet options for pSeries servers enable many high-speed Ethernet connections with minimal use of I/O slots. To build complex, long-distance networks, these adapters must be integrated with networking products like hubs, switches, and routers. These are available from third-party suppliers such as Cisco Systems, whom IBM has recently announced an alliance to integrate IBM's system products and services with Cisco's leadership networking products for the Internet.

Figure 4.6 shows one possible wiring arrangement on a company's premises. This diagram could represent, for example, the intranet connections either the company or the supplier building of Figure 4.4. In Figure 4.6, various employees' PC workstations are connected to Ethernet hubs located in a wiring closet or communications room. We have shown some hubs supporting 10 Mbps on the input side and others supporting 100 Mbps input. It is possible, of course, for each PC

![](img/29c52a1767a1e621ce6343faa9399737_280_0.png)

There are many hubs, switches, and routers on the market, along with all the supporting hardware and software. With a variety of Ethernet adapters to choose from and the availability of the necessary software interfaces for AIX 5L or Linux, pSeries servers provide all the tools required for integration into Ethernet LAN networks.

## pSeries and the Token-Ring Network

The Token-Ring LAN technology, developed by IBM, is less pervasive in the industry than Ethernet. Although pSeries systems and AIX still support Token-Ring, it is not widely used. Figure 4.7 shows the basic structure of Token-Ring. The nodes of the network are arranged in a ring pattern, thus giving the network its name. Information is transferred over the network at either 4 or 16 million bits per second using the token-passing protocol.

![](img/29c52a1767a1e621ce6343faa9399737_281_0.png)

**Figure 4.7.** The basic structure of a Token-Ring network.

## 282 Exploring IBM@serverSeries

ring from node to node in a continuous circle. The token is the “mailbag” of the network. It carries the network messages (one at a time) from the transmitting node to all other nodes in the network until the recipient is reached and the message is delivered. When a node receives a frame, it looks to see if it is a message or a token frame. If it is a token frame, it means the network is idle and that node can send a message. If it is a message frame, the node will examine the address contained in the token to see if the message is intended for that node. If not, the frame will be passed unchanged to the next node.

Although IBM offers 100/16/4 Mbps Token-Ring for some servers and personal computers, the pSeries emphasis is on Ethernet and only a 16/4 Mbps Token-Ring adapter (#4959) is available for pSeries servers.

## ASCII Terminal Networks

Although the use of ASCII terminals attached to pSeries systems is almost a thing of the past, it should be noted that pSeries provides support for users at ASCII terminals. Local terminals and printers are attached via industry-standard EIA-232 async communications ports (one port per terminal or printer). pSeries systems can stand with two or more ports. The 8-Port async Adapter EIA-232 (#2943) will provide the additional ports needed in our example configuration, for a total of 10 EIA-232 ports. The AIX operating system comes with the necessary support for the EIA-232 ports and the async protocols they use.

If it is necessary to attach a remote terminal to the pSeries system, a modem must be attached to a telephone line at each end (server and remote terminal). “Modem” stands for “modulator-demodulator” and is a device for modulating or translating digital signals into analog telephone-line signals for transmission, and versa (modulating) for receiving signals from other systems. IBM does not sell modems, but many industry-standard modems are available. With dialup telephone lines, 56 KBps modems are commonly used, and higher-speed modems are available for use on leased telephone circuits.

## Clustering for High Availability

We have already seen that pSeries systems can communicate with another over various types of LANs to implement data sharing, pro-
