
The sharing of information drove the expansion of the Internet to exponential proportions with Request for Comment documents (RFCs). RFCs solicited feedback on proposed standards and then, once they were integrated, formed the basis of standards for Internet technologies. These are still used to this day to feel out to peers new enhancements to protocols and new technology that helps make the Internet what it is today.

> you are interested in reading the RFCs that formed the basis of the Internet as we know it today (and many newer ones), search www.rfc-editor.org and www.rfc.net.

The Internet is a place for pioneers to shape society in one form or another; it has provided users with something that has truly revolutionized the way we communicate and work.

## TCP/IP

In the previous section, we discussed how TCP/IP was designed as a resilient network protocol and about how moving data from one part of the world to another is seamless. This is no easy task, and TCP/IP is able to do this for two fundamental reasons—it is simple in its design, and it is open.

A protocol is classified as open when every single person in the world is able to see how it works, right down to the wire.

TCP/IP is based on a layered architecture, as are many network protocols. These layers form the basis of network abstraction. By abstracting layers from each other, you can make sure the technology grows to meet the demands placed upon it.

Imagine that the TCP/IP protocol was designed and implemented over 20 years ago. With most things in computing, a change in 10 to 20 years, but TCP/IP has managed to keep up with trends in computing and networking. This is because network speeds get faster, the protocol's abstractive nature has managed not to be tied to a technology that is 20 years old.

## The ISO OSI Model

Every abstracted network protocol adheres to, either loosely or strictly, the International Organization for Standardization (ISO) standard seven-layer Open Systems Interconnect (OSI) model (see Figure 6-1). It provides a generalized architecture that defines a way to design a network protocol.

Figure 6-1: The ISO OSI seven-layer model

| |
| :--- |
| Application |
| Presentation |
| Session |
| Transport |
| Network |
| Data Link |
| Physical |

From the bottom up, you find the following layers:

- **Physical layer** — Deals with how information is transmitted over a medium, whether it is copper or fiber Ethernet, wireless networking, or satellite transmission. This layer has no concept of the upper layers and does not need to have, as it is concerned only about getting information safely from one place to another a medium.

- **Data link layer** — Concerned with the encapsulation of data from the upper layers in preparation for moving to the wire. Protocols in this layer could be Ethernet or token ring.

- **Network layer** — The network layer is used to define addressing schemes for nodes and networks. It is not concerned with the accuracy of the data it is encapsulating or what format the data is. Its only concern is that the data is able to get from A to B.

- **Transport layer** — Concerned about how data is moved from A to B. Protocols in this layer could be TCP or User Datagram Protocol (UDP); it also deals with the integrity and retransmission of data in the event of a failure.

- **Session layer** — Concerned with making, you guessed it, a session between two machines, to be ready for sending data that is passed to it by upper layers using lower layers to transport this data to its destination.

- **Presentation layer** — Concerned with how data is represented. For example, HTML, JPEG, or MP3 formats would reside here.

- **Application layer** — Concerned with applications that use the network protocol. Applications could be SMTP, Hypertext Transfer Protocol (HTTP), and FTP.

It may be unclear how this model helps abstraction and further the protocol. I hope that the following example will help you understand.

Suppose I am sitting in my garden on a sunny day in London (amazing, but we do get here!) writing this chapter. I am running a wireless network in my house, so I can check my email, surf the web, and listen to some music on my laptop. None of this would be possible without a layered architecture because I am using so many different protocols running over a wireless connection, which is then connected to an asymmetric digital subscriber line (ADSL) router, further connected to a firewall.

I am in my garden, and need to send a chapter to my editor at Wiley. To do this, I need to open an FTP connection to the Wiley server. Here is what happens.

I initiate an FTP connection, with the IP address of the server I want to connect to. My machine sees that the server I want to communicate with is not on its local network and sends the request over to my router, which needs to get to Wiley. My router also does not specifically understand where the FTP server I need to talk to, so it sends the packet to its default router, and so on. It will carry on, with each router getting closer and closer to the destination. When the packet hits Wiley's FTP server, TCP/IP creates a network so that the FTP server knows that specific connection is coming from my IP address.

When this connection is established, I have a virtual connection to the FTP server — that, according to my laptop I have a connection to Wiley, regardless that it is not a physical connection, but rather traversing many routers, the Atlantic, and many firewalls. This is transparent not only to the user, but also to the client machine. My FTP client does not care how a connection is made to Wiley; it is only concerned that my connection can be.

## Connection Versus Connectionless Protocols

The transport layer has two protocols used to transport data from A to B—TCP and UDP, which are connection- and connectionless-based protocols, respectively. Most TCP/IP application services use the reliable TCP protocols to transport data. TCP maintains a connection as long as is needed to fulfill a request. During this time, if a checksum error is found in a packet, the TCP protocol requests a retransmission. To the upper layers, this is transparent and guarantees data consistency. Short bursts are needed, or where the upper layers take loss or error, UDP can be used to reduce overhead, at the cost of data consistency. UDP is commonly used for Domain Name System (DNS) lookups (small packet size, the upper layer is capable of requesting data in the event of failure) and also for streaming Moving Picture Group (MPEG) streams. The MPEG protocol is able to deal with quite a high amount of data loss and errors itself.

When the FTP connection is established, I need then to upload a text document that is in a certain format (Word). I use FTP commands to create a new directory and to upload my document to the server. Again, using FTP commands, I close the connection to the FTP server, which closes my TCP/IP connection, and the transfer is over.

We used pretty much of the OSI layers in this transaction. Table 6-1 comparatively shows the correlation between an action in the example and the layer used.

### Table 6-1: OSI Layers and Their Uses

| Layer | Action |
| --- | --- |
| Application | The FTP protocol is an application layer protocol. |
| Presentation | The transfer of my Word document in a format that is understandable by both servers, and the way a Word document is constructed internally is a presentation layer protocol. |
| Session | When my laptop initially communicates with the FTP server, it has to create a TCP/IP session. It has no bearing on the FTP protocol because FTP works "on top" of a TCP/IP session. |
| Transport | The TCP/IP connection established in the OSI layer will be a connection-based protocol that lasts for the time of the FTP connection. Transporting packets is handled by the transport layer, which encapsulates the data from upper layers into manageable chunks. It also deals with the integrity of the data and retransmission of lost packets. |
| Network | When I specify an IP address to connect, the network layer deals with establishing a route through my firewall, across the Atlantic, and to the FTP server. This involves addressing schemes and routing. |
| Data link layer | After packets have been encapsulated by the upper layers, they are prepared by the data link layer to be transported over a wireless connection from my laptop to the base station. This involves packaging data from the upper layers into 802.11 protocol packets and also with any encryption scheme that I have between my and the base station. |
| Physical layer | This would deal with frequencies, signal strength, and so on of my wireless connection, as well as timing for sending packets over a wireless network. |

We talk all about encapsulation in Table 6-1, and this is an important part of a layered network model. *Encapsulation* is a means to wrap data packets inside
