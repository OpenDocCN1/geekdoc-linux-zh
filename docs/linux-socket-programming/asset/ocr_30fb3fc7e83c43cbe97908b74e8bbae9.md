| Negotiated window size | Fixed window (determined by program) |
| Record oriented | Packet oriented |
| Built on Networking layer | Built on IP |

UDP adds one primary feature of the Transport layer: virtual networks with ports. As described in Chapter 4, "Sending Messages Between Peers," this particular feature abstracts the network and lets your network program act like it solely owns the connection. All other features are like the IP layer. If properly positioned, UDP straddles the Network and Transport layers, leaning more on the Network side.

# Layer 3: Host Streams (TCP)

The TCP layer matches the OSI Transport layer very well. Both provide the reliability, streaming, ordering, and error management needed for building sessions. It is important to emphasize that TCP does not rest on UDP. It has its own header and own path in the network subsystem. For a side-by-side comparison, see Table 5.3.

| **Table 5.3, Transport Layer Versus TCP** |  |
| **Transport Layer** | **UDP** |
| Reliable data | Reliable data (checksums) |
| Reliable delivery | Guaranteed delivery |
| Negotiated window size | Sliding window |
| Record oriented | Stream oriented |
| Built on Network layer | Built on IP |

# Layer 4: Application Layer

This is where the TCP/IP model stops. According to the model, the Application layer comprises OSI's Session (5), Presentation (6), and Application (7) layers. The TCP/IP model has a few applications that fill these roles. Some examples of this layer are Web browsers, gateways, Telnet, and FTP (File Transfer Protocol). Remote Procedure Calls (RPCs) best align with the Presentation layer. Network File System (NFS) depends on RPCs and appears to fit the Application layer. Still, these applications blur the boundaries so that assigning them to any particular layer is difficult.

The Application layer rests on top of the Host Streams layer (UDP and TCP). However, it may accept messages directly from ICMP.

# Fundamental Differences Between OSI and IP

Both the OSI and IP models use layering to define the roles of each protocol stack. They also move from the hardware-dependent code to the abstract application. But you may have noticed some differences.

OSI layers the data as well as the protocol. Referring back to Figure 5.1, each layer of the stack has its own header information. As the data moves down the stack toward the Physical layer, each layer encapsulates the message inside its own packet.

For example, if you send a Session layer message, the Physical layer sees a list of headers in reverse order: datalink, network, transport, and session. The message itself follows all these headers at the end of the data. Each layer uses this process, including the Physical layer. Eventually, you may have up to seven headers on a single packet.