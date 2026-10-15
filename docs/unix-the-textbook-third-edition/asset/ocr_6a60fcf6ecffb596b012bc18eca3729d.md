various applications. Most of the first layer is handled by hardware (type of communication medium used, attachments of hosts to the medium, etc.). The network interface card (NIC) in a host handles the rest of the first layer and the second layer. Layer 2 consists of medium access control (MAC) addresses, network cards, drivers, and switches. Layers 3 and 4 are fully implemented in the operating system kernel on most existing systems. The first two layers are network hardware specific, whereas the remaining layers work independently of the physical network. On newer gigabit Ethernet interfaces where the processing overhead of the network stack becomes significant, the TCP offload engine (TOE) technology is used in the NIC to offload processing of the TCP/IP stack to the network controller.

# EXERCISE 11.1

Ask your system administrator: How many hosts are connected on your LAN? What type of computers are they (PCs or workstations)?

# EXERCISE 11.2

What is the physical medium for your network (coaxial cable, twisted pair, or glass fiber)? Ask your instructor or system administrator about the topology of your network (bus, ring, etc.).

# EXERCISE 11.3

Ethernet is the most commonly used link-level protocol for LANs. Does your LAN use Ethernet? If not, what does it use?

# 11.5 THE TCP/IP SUITE

Several protocols are associated with various layers in the TCP/IP model. These protocols result in what is commonly known as the TCP/IP suite, which is illustrated in Figure 11.3.

The description of most of the protocols in the suite is beyond the scope of this textbook, but we briefly describe the purpose of those that are most relevant to our discussion. As a user, you see the application layer in the form of applications and utilities that can be executed to invoke various Internet services. Some of the commonly used applications are for electronic mail, Web browsing, file transfer, and remote login. We discuss some of the most useful applications in Section 11.8.

# 11.5.1 TCP and UDP

The purpose of the transport layer is to transport application data from your machine to a remote machine and vice versa. This delivery service can be a simple, best-effort service that does not guarantee reliable delivery of the application data or one that guarantees reliable and in-sequence delivery of the application data. The User Datagram Protocol (UDP) provides a best-effort delivery service and the Transmission Control Protocol (TCP) offers completely reliable, in-sequence delivery. The UDP is a connectionless protocol; that is, it simply sends the application data to the destination without establishing a virtual