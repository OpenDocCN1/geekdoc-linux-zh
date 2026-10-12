
## 15.3 UDP ports

Conceptually, UDP ports are almost identical to TCP ports (Module 10.4):

- Specific *well-known port numbers* are allocated by convention to particular services. The server for a particular service listens on the appropriate well-known port. For example, the DNS server listens on port 53, treats any incoming requests on that port as DNS queries, and processes them accordingly. (See the inside front cover for a fuller list of port numbers.)
- The client specifies the *destination port* when it sends a request to the server. By specifying the specific port number, the client is saying what service is required. For example, Bob uses Alice’s DNS server by sending to her UDP port 53.
- The client listens on an ephemeral port, and includes its port number as the *source port* in the request. The server sends its reply (or replies) to this port on the source machine, and the client reads the replies from it.
- In TCP, the combination $(N_1, P_1, N_2, P_2)$ of source and destination IP and port numbers is a unique reference that specifies a TCP connection. UDP is connection-less, so a listening client port isn’t “connected to” a port on a server, and in fact any machine can send to the client’s listening port, just as any client can send to a server’s port. (In fact, there’s no difference between client and server listening ports in UDP. In TCP, what distinguishes client and server is that the client connects to the server, thereby establishing the connection.) Consequently, the client has to make sure that any “replies” on its listening port really are related to the request it sent. This is why DNS uses identifiers (Module 7.8).

The incoming port number is what UDP uses to demultiplex the packets coming in from the IP layer and pass them up to the respective applications in the application layer (upper part of Figure 15.2). This is an important function of the transport layer, because it’s not provided by the network (IP) layer lower down.

To see which ports are being listened to, use the **netstat** command. You can optionally restrict the output to UDP, using the “-u” option (Linux) or “-p udp” option (Windows-NT). As before, “-n” prints addresses as IP numbers, and “-a” shows all active ports; otherwise, servers listening for incoming data are not shown:

```
netstat -n -a -u          Linux
netstat -n -a -p udp      Windows
```

(On Linux, “-p” gives the name of the program that is listening on this port. There’s no similar standard tool for Windows, but see the Notes.)

### Relation between UDP and TCP port numbers

UDP ports are completely separate from the TCP ports. The port numbers in a UDP packet are used only by the UDP part of the stack, and similarly the port numbers in a TCP packet are processed only by TCP. However, if a service can run over UDP and TCP, then the same well-known port number has been chosen for both, purely for convenience. You can see this by looking at your */etc/services* file (Linux) or C:\WINNT\system32\drivers\etc\services file (NT).

The lower part of Figure 15.2 shows diagrammatically how UDP and TCP are separated in the stack. When a transport protocol passes data down to the IP layer to be transmitted, it sets a special IP protocol number field in the header of the IP packet to say which protocol is being used. The protocol number for UDP is 17. When the packet arrives at the destination machine, the IP layer looks at the protocol number, and passes the packet up to the appropriate protocol in the transport layer. This process of taking a single incoming stream (the IP packets from the link layer) and separating it out into its multiple constituent streams to pass up to the transport layer is called demultiplexing.

![](img/a2132b646d336d5f9a21102d6320e537_432_0.png)

**Figure 15.2** IP demultiplexes on IP protocol number and UDP demultiplexes on UDP port number

## 15.4 How the protocols relate to each other

We have introduced several protocols so far. Some (ARP, ICMP for **ping**) we covered quite informally, emphasizing the practical aspects rather than the formal protocol description. Now that we have covered the two important transport protocols, TCP and UDP, we can put all the different protocols into context. Figure 15.3 shows where in the stack the various protocols sit. Figure 15.4 shows how they are related, and how they interact. We have included some protocols that we'll be covering later – NetBIOS for Microsoft Windows Networking (Part 3) and ESP (used in VPNs, Chapter 27). We've also shown the Novell IPX and SPX protocols in the diagram, just to show how they provide equivalent but different functionality to the TCP/IP protocols.

![](img/a2132b646d336d5f9a21102d6320e537_433_0.png)

**Figure 15.3** The protocol stack

To recap what we said about the functions of the various layers:

- The **link layer** (e.g. an Ethernet LAN segment) is responsible for moving packets from one machine to another that is connected directly to it on the same wire – it handles a single hop.
- The **network layer** moves packets from the source machine to the destination machine, via any intermediate routers on the path. All routing is handled at this level.
- This layer also includes ARP and ICMP because they don't really fit anywhere else.
- ARP acts as an intermediary so that IP can obtain the MAC addresses from the link layer. ICMP uses IP so perhaps ICMP ought to be in the layer above IP; on the other hand, ICMP definitely isn't a transport protocol. (It just goes to show that a model is only a model. Use it when it helps you understand what's happening; forget about it if it causes you problems.)

![](img/a2132b646d336d5f9a21102d6320e537_434_0.png)

- The **transport layer** provides end-host to end-host data communication, and isn't involved on the intermediate routers. The Internet transports are UDP and TCP, which provide ports as a way for the application above to interface with the network layer below. In addition, TCP provides a lot of extra functionality, including reliable (guaranteed) delivery, and connection-oriented sessions.

All the above layers are either in the hardware or built into the operating system. The final layer is different:

- The **application layer** is separate from the operating system, and the protocols at this layer are usually included in the application by means of subroutines or libraries. In addition to the code for the network protocols, the applications of course contain the code to do what the user wants – interact with a database, or handle e-mail, or browse Web pages.

## Summary

- Like TCP, UDP is a transport protocol. It connects applications end to end and plays no part in routing, which it leaves to the lower IP (network) layer.
- UDP is a connection-less datagram-oriented protocol. It sends single packets between client and server and does not establish an ongoing connection.
- UDP is “unreliable” (best-effort). Packets can get lost or out of order and UDP won’t notice, won’t try to retransmit, and won’t inform the application. Any error-recovery required has to be implemented by the application itself, usually by means of re-transmitting if it hasn’t received a response after a particular timeout period.
- UDP is a compact, easy-to-implement protocol. It is suitable for applications that have only intermittent, ad-hoc or small data transfers, and applications that need to broadcast, e.g. to locate a particular service. Common applications that use UDP are the DNS, DHCP, Microsoft Windows Networking, Syslog, and NFS file sharing.
- UDP uses port numbers to identify which application the packets are destined for. UDP and TCP port numbers are completely unrelated although if a service is capable of running over both, the same well-known port number is allocated to each (by convention only).

### What’s next?

In the next chapter we look at DHCP – the Dynamic Host Configuration Protocol. This runs over UDP and is used for automatically setting the TCP/IP and related configuration details of your machines.

### Notes and further reading

The specification for UDP is only three pages long:

- RFC-768 August 1980 User Datagram Protocol

As usual, Stevens gives a good description of what UDP does and how it works.

### Applications that use UDP

- *Stevens, UNIX Network Programming Volume 1* (1990, Prentice Hall PTR)

Contains a detailed discussion of when UDP might be used instead of TCP, and the programming consequences of doing so. In particular see Module 20.4 When to use UDP instead of TCP and Module 20.5 Adding Reliability to a UDP Application.

The RADIUS dial-up authentication service uses UDP instead of TCP; the reasons for this are discussed explicitly in Module 2.3 of:

- RFC-2058 January 1997 Remote Authentication Dial-in User Service (RADIUS)
