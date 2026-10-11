**TABLE 5.3** *Continued*

| **Transport Layer** | **UDP** |
| :--- | :--- |
| Negotiated window size | Sliding window |
| Record oriented | Stream oriented |
| Built on Network layer | Built on IP |

# Layer 4: Application Layer

This is where the TCP/IP model stops. According to the model, the *Application* layer com- prise OSi's *Session* (5), *Presentation* (6), and *Application* (7) layers. The TCP/IP model has a few applications that fill these roles. Some examples of this layer are Web browsers, gateways, Telnet, and FTP (File Transfer Protocol). Remote Procedure Calls (RPCs) best align with the Presentation layer. Network File System (NFS) depends on RPCs and appears to fit the *Application* layer. Still, these applications blur the boundaries so that assigning them to any particular layer is difficult.

The *Application* layer rests on top of the *Host Streams* layer (UDP and TCP). However, it may accept messages directly from ICMP.

# Fundamental Differences Between OSI and IP

Both the OSI and IP models use layering to define the roles of each protocol stack. They also move from the hardware-dependent code to the abstract application. But you may have noticed some differences.

OSI layers the data as well as the protocol. Referring back to Figure 5.1, each layer of the stack has its own header information. As the data moves down the stack toward the Physical layer, each layer encapsulates the message inside its own packet.

For example, if you send a *Session* layer message, the Physical layer sees a list of headers in reverse order: *datalink, network, transport,* and *session*. The message itself follows all these headers at the end of the data. Each layer uses this process, including the Physical layer. Eventually, you may have up to seven headers on a single packet.

The receiver reverses the process. It uses the encapsulated data to determine whether to pass your message up to the next layer. In the previous example, your message arrives at the Physical layer. Each layer peals off its header. If it sees another header, it passes the message up to the next layer. Eventually, the message stops at the *Session* layer.

The IP model operates differently. Attaching a header for every layer can make your message header heavy, reducing throughput. Instead, the IP model places the protocol type in the IP