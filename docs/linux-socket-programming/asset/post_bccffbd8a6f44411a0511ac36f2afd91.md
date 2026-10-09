
## Layer 7: Application

The last layer, the Application layer, provides network services such as file transfer, terminal emulation, messaging, and network management. Essentially, most applications use this layer, since it provides the Application Programming Interface (API). However, it is not the actual user application; it is the set of library calls and services to help the applications work with the network. Network File System (NFS) is an example of this layer that hooks into the operating system's virtual file system architecture. It builds on top of the RPC tools to provide the function interfaces.

## Internet Protocol Suite

Linux (like most other UNIX operating systems) does not use the OSI network model directly. However, the model is a starting point to understanding the IP Stack. Linux uses the Internet Protocol suite to manage its native network interface.

### NOTE

The IP protocol sprang from the ARPAnet (Advanced Research Projects Agency Network) funded by DARPA (Defense Advanced Research Projects Agency) in 1972. BBN Corporation implemented the first vestiges of the network. Later, UNIX, a free operating system offered by Bell Labs, adopted the model as well. The universities involved used UNIX to test out a concept of linking several computers together throughout the United States. The Sockets API originated with BSD 4.2 in 1983.

The Internet Protocol suite has four layers that map closely to the OSI model. The highest layer is called the Application layer. The IP suite's Application layer encompasses OSI's layers 5–7 (see Figure 5.2). Refer to Figure 5.1 for a comparison.

> Figure 5.2. The DoD or Internet Protocol Stack compares closely to the OSI model. The Socket API stops at OSI's Transport (4) layer. The protocol leaves the remaining layers to high-level programs like Telnet, FTP, and Lynx.

![](img/03334662da8fdfb8d95a02f270c522f6_86_0.png)

## Layer 1: Network Access Layer

IP's first network layer most closely matches OSI's Physical and Datalink layers. Because the hardware and drivers are so closely tied together and the hardware support varies so widely, you cannot isolate one from the other.

The characteristics are similar: The driver works closely with the hardware interfaces to provide a common set of functionality to the kernel. The kernel, in exchange, gives the driver direct access to the ports and interrupts. If an interface is lacking in any features that the kernel needs, the drivers take up the slack.

Linux adds another feature that complicates this layer: hot swapping network adapters. This is found in PCMCIA support. When you insert a PC card, the PC card manager recognizes it, allocates the appropriate ports and interrupts, inserts the defined kernel modules, and configures your network. Likewise, when you remove the card, the manager disables the network and removes the kernel module.

## Layer 2: Internetwork Layer (IP)

The IP layers (both IPv4 and IPv6) depend on the device drivers to provide a common interface and functionality. Both versions are different in this layer. They compose different protocol stacks that translate to and from IPv4 and IPv6, as needed, to ensure compatibility.

The IP layer best aligns with the OSI Network layer. It provides the logical addressing and routing functions of that layer. The one part that the IP layer lacks is the error messaging of the Network layer.

### Layer 2: Control/Error Messaging Extensions (ICMP)

ICMP (Internet Control Message Protocol) adds the missing error messaging of the OSI Network layer. ICMP provides the message protocols for errors and exceptions in the routing and forwarding of messages. Typical exceptions include `network not reachable` and `host not found`.

This protocol works with other systems to perform various functions. For example, it works with the routing tables (ARP) when hosts become unreachable. Additionally, it works with TCP to speed up or slow down the communication and change the sliding window. IPv6 has even added control for multicast group management.

What's interesting about ICMP is that it stands alone. Neither UDP nor TCP uses its layer. They do accept its messages for their own processing.

## Layer 3: Host to Host (UDP)

Contrary to popular opinion, UDP (User Datagram Protocol) does *not* match perfectly with the OSI Transport layer (see *Figure 5.3*). The Transport layer guarantees delivery, in-order packets, error-free packets, and stream-like functions. UDP does not; see *Table 5.2*.

![](img/03334662da8fdfb8d95a02f270c522f6_87_0.png)

![](img/03334662da8fdfb8d95a02f270c522f6_87_1.png)

**Table 5.2**, Transport Layer Versus UDP

| *Transport Layer* | *UDP* |
|---|---|
| Reliable data | Reliable data (checksums) |
| Reliable delivery | No guaranteed delivery |
| Negotiated window size | Fixed window (determined by program) |
| Record oriented | Packet oriented |
| Built on Networking layer | Built on IP |

UDP adds one primary feature of the Transport layer: virtual networks with ports. As described in Chapter 4, "Sending Messages Between Peers," this particular feature abstracts the network and lets your network program act like it solely owns the connection. All other features are like the IP layer. If properly positioned, UDP straddles the Network and Transport layers, leaning more on the Network side.

## Layer 3: Host Streams (TCP)

The TCP layer matches the OSI Transport layer very well. Both provide the reliability, streaming, ordering, and error management needed for building sessions. It is important to emphasize that TCP does not rest on UDP. It has its own header and own path in the network subsystem. For a side-by-side comparison, see Table 5.3.

| **Transport Layer** | **TCP** |
|---|---|
| Reliable data | Reliable data (checksums) |
| Reliable delivery | Guaranteed delivery |
| Negotiated window size | Sliding window |
| Record oriented | Stream oriented |
| Built on Network layer | Built on IP |

## Layer 4: Application Layer

This is where the TCP/IP model stops. According to the model, the Application layer comprises OSI's Session (5), Presentation (6), and Application (7) layers. The TCP/IP model has a few applications that fill these roles. Some examples of this layer are Web browsers, gateways, Telnet, and FTP (File Transfer Protocol). Remote Procedure Calls (RPCs) best align with the Presentation layer. Network File System (NFS) depends on RPCs and appears to fit the Application layer. Still, these applications blur the boundaries so that assigning them to any particular layer is difficult.

The Application layer rests on top of the Host Streams layer (UDP and TCP). However, it may accept messages directly from ICMP.

## Fundamental Differences Between OSI and IP

Both the OSI and IP models use layering to define the roles of each protocol stack. They also move from the hardware-dependent code to the abstract application. But you may have noticed some differences.

OSI layers the data as well as the protocol. Referring back to Figure 5.1, each layer of the stack has its own header information. As the data moves down the stack toward the Physical layer, each layer encapsulates the message inside its own packet.

For example, if you send a Session layer message, the Physical layer sees a list of headers in reverse order: datalink, network, transport, and session. The message itself follows all these headers at the end of the data. Each layer uses this process, including the Physical layer. Eventually, you may have up to seven headers on a single packet.

The receiver reverses the process. It uses the encapsulated data to determine whether to pass your message up to the next layer. In the previous example, your message arrives at the Physical layer. Each layer peels off its header. If it sees another header, it passes the message up to the next layer. Eventually, the message stops at the Session layer.

The IP model operates differently. Attaching a header for every layer can make your message header heavy, reducing throughput. Instead, the IP model places the protocol type in the IP header. When IP gets the message, it checks that field and routes the message directly to the protocol you chose, after removing its own header.

Also, as indicated at the end of Chapter 3, each of IP's protocols fills a specific role. Unlike the OSI model, where each layer rests squarely on the back of the lower layers, all protocols rest on IP raw protocol.

Again, the IP model uses a protocol to address a particular need. ICMP is for error messaging, UDP is for directed messages and connectionless communications, and TCP is for streaming. The raw IP is for developing new protocols.

## What Services What?

The next step is how to use the DoD Network model. If you want to access all the different layers of the IP Stack, use the `socket()` system call.

**Table 5.4. DoD Layer Summary**

| **DoD Layer** | **Programmer/User Access** |
|---|---|
| 4-Application | FTP, Gopher, Lynx, Netscape, IRC |
| 3-Host to Host (TCP) | `socket(PF_INET, SOCK_STREAM, 0);` |
| 3-Host to Host (UDP) | `socket(PF_INET, SOCK_DGRAM, 0);` |
| 2-Internetwork (ICMP) | `socket(PF_INET, SOCK_RAW, IPPROTO_ICMP);` |
| 2-Internetwork (IP) | `socket(PF_INET, SOCK_RAW, protocol);` |
| 1-Network Access | `socket(PF_INET, SOCK_PACKET, filter);` |

This interface may differ from your expectations. Linux allows read access to the low-level driver messages using `SOCK_PACKET`. This Linux-specific feature gives you access to any and all messages on the network. You used this feature to build your own network snooper in Chapter 3.

## Summary: From Theory to Application

This chapter examines the interface between the different network elements that need to work in harmony. The network challenge includes computer hardware interfacing, network connection issues, operating system linking, and application interfacing. Each has specific problems that get in the way of giving your program access to other computers. Networking addresses these problems using carefully designed models to help you program in a consistent way.

Two networking models, OSI and IP (or DoD), separate the solutions into layers. The layers rest on top of each other like layers of a cake. The support that the lower layers provide increases the data reliability and interfacing of higher layers. The layers also offer you a wide selection of speed versus reliability.

The first layer addresses the physical interfacing between computers. In succession, each layer strengthens message reliability, arrival, and flow. When you use interfaces from the middle layers of the protocol stack, you can expect that the data will arrive correctly.
