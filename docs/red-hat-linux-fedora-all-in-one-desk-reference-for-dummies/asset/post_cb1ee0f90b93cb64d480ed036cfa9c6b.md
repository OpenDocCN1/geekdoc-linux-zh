
As you can see, the format of entries are the same for both `chap-secrets` and `pap-secrets`. There are four fields in each line, in the following order:

- 1. `client` — This field contains the name to be used during authentication. This is the username that you get from the ISP.
- 2. `server` — This field contains the name of the remote system to which you are authenticating the local system. If you don't know the server's name, put an asterisk to indicate any server.
- 3. `secret` — This is the secret that your system's PPP server has to send to the remote system to authenticate itself. This is the password you received from the ISP.
- 4. `IP addresses` — This optional field can contain a list of the IP addresses that the local system may use when connecting to the specified server. Typically, this field is left blank because the local system usually gets a dynamic IP address from the server and (therefore) doesn't know what IP address it would use.

## Chapter 2: Setting Up a Local Area Network

### In This Chapter

- Understanding TCP/IP networks
- Setting up an Ethernet LAN
- Configuring TCP/IP networking
- Connecting your LAN to the Internet

Red Hat Linux comes with built-in support for TCP/IP (Transmission Control Protocol/Internet Protocol) networking, as do most modern operating systems from Windows to Mac OS. You can have TCP/IP networking over many different physical interfaces, such as Ethernet cards, serial ports, and parallel ports.

Typically, you use an Ethernet network for your local area network (LAN) — at your office or even your home (if you happen to have several systems at home). To connect to remote systems over a modem, you use TCP/IP networking over Point-to-Point Protocol (PPP).

This chapter describes how to set up an Ethernet network. Even if you have a single PC, you may need to set up an Ethernet network interface so you can connect your PC to high-speed Internet access that uses DSL or cable modem. (I cover DSL and cable modem in Chapter 1 of this mini-book.)

### Understanding TCP/IP

You can understand TCP/IP networking best if you think in terms of a layered model with four layers. Think of each layer as responsible for performing a particular task. The layered model describes the flow of data between the physical connection to the network and the end-user application. Figure 2-1 shows the four-layer network model for TCP/IP.

In this four-layer model, information always moves from one layer to the next. For example, when an application sends data to another application, the data goes through the layers in this order: Application→Transport→Network→Physical. At the receiving end, the data goes up from Physical→Network→Transport→Application.

Figure 2-1:
You can understand TCP/IP using the four-layer network model.

|   | Layer | Protocols / Notes |
|---|-------|-------------------|
| 4 | Application | Mail, file transfer, TELNET |
| 3 | Transport | TCP (Transmission Control Protocol)<br>UDP (User Datagram Protocol) |
| 2 | Network | IP (Internet Protocol) |
| 1 | Physical | Ethernet |

![](img/a7eec43a54473e95dc5ea333fecf1bd7_337_0.png)

Each layer has its own set of protocols — conventions — for handling and formatting the data. If you think of sending data as something akin to sending letters through the postal service, then a typical protocol would be a preferred sequence of actions for a task such as addressing an envelope (first the name, then the street address, and then city, state, and Zip or other postal code).

Here's what each of the four layers does, top to bottom:

- **Application layer:** Runs the applications that users use, such as e-mail readers, file transfers, and Web browsers. There are application-level protocols such as Simple Mail Transfer Protocol (SMTP) and Post Office Protocol (POP) for e-mail, Hyper Text Transfer Protocol (HTTP) for the Web, and File Transfer Protocol (FTP) for file transfers. Application-level protocols also have a *port number* that you can think of as an identifier for a specific application. For example, port 80 is associated with HTTP or the Web server.
- **Transport layer:** Sends data from one application to another. The two most important protocols in this layer are *Transmission Control Protocol* (TCP) and *User Datagram Protocol* (UDP). TCP guarantees delivery of data; UDP just sends the data without ensuring that it actually reaches the destination.
- **Network layer:** This layer is responsible for getting data packets from one *network* to another. If the networks are far apart, the data packets are routed from one network to the next until they reach their destination. The primary protocol in this layer is the Internet Protocol (IP).
- **Physical layer:** Refers to the physical networking hardware (such as an Ethernet card or Token Ring card) that carries the data packets in a network.

The beauty of the layered model is that each layer only takes care of its specific task, leaving the rest to the other layers. The layers can mix and match — you can have a TCP/IP network over any type of physical network medium, from Ethernet to radio waves (in a wireless network). The software is modular as well because each layer can be implemented in different modules. For example, typically the Transport and Internet layers already exist as part of the operating system; any application can make use of these layers.

### TCP/IP and the Internet

TCP/IP has become the protocol of choice on the Internet — the "network of networks" that evolved from ARPAnet. The U.S. Government's Advanced Research Projects Agency (ARPA) initiated research in the 1970s on a new way of sending information, using packets of data sent over a network. The result was ARPAnet: a national network of linked computers. Subsequently, ARPA acquired a Defense prefix and became DARPA. Under the auspices of DARPA, the TCP/IP protocols emerged as a popular collection of protocols for internetworking — communication among networks.

TCP/IP has flourished because the protocol is open. That means the technical descriptions of the protocol appear in public documents, so anyone can implement TCP/IP on specific hardware and software.

TCP/IP also made great inroads because stable, working software was available. Instead of a paper description of network architecture and protocols, the TCP/IP protocols started out as working software — and who can argue with what's already working? These days (as a result), TCP/IP rules the Internet.

### IP addresses

When you have many computers on a network, you need a way to identify each one uniquely. In TCP/IP networking, the address of a computer is the IP address. Because TCP/IP deals with internetworking, the address is based on the concepts of a network address and a host address. You may think of the idea of a network address and a host address as having to provide two addresses to identify a computer uniquely:

- Network address indicates the network on which the computer is located.
- Host address indicates a specific computer on that network.

### Next-generation IP (IPv6)

When the 4-byte IP address was created, the number of available addresses seemed adequate. Now, however, the 4-byte addresses are running out. The Internet Engineering Task Force (IETF) recognized the potential for running out of IP addresses in 1991 and began work on the next-generation IP addressing scheme. They called it IPng (for Internet Protocol Next Generation) and intended that it will eventually replace the old 4-byte addressing scheme (called IPv4, for IP Version 4).

IPv6 is designed to be an evolutionary step from IPv4. The proposed standard provides direct interoperability between hosts using the older IPv4 addresses and any new IPv6 hosts. The idea is that users can upgrade their systems to use IPv6 when they want and that network operators are free to upgrade their network hardware to use IPv6 without affecting current users of IPv4. Sample implementations of IPv6 are being developed for many operating systems, including Linux. For more information about IPv6 in Linux, consult the Linux IPv6 FAQ/HOWTO at www.linuxhq.com/IPv6/.

Several alternative addressing schemes for IPng were proposed and debated. The final contender, with a 128-bit (16-byte) address, was dubbed IPv6 (for IP Version 6). On September 18, 1995, the IETF declared the core set of IPv6 addressing protocols to be an IETF Proposed Standard.

The IPv6 128-bit addressing scheme allows for 170,141,183,460,469,232,000,000,000,000,000,000 unique hosts! That should last us for a while!

The network and host addresses together constitute an IP address and it's a 4-byte (32-bit) value. The convention is to write each byte as a decimal value and to put a dot (.) after each number. Thus you see network addresses such as 132.250.112.52. This way of writing IP addresses is known as dotted-decimal or dotted-quad notation.

In decimal notation, a byte (which has 8 bits) can have a value between 0 and 255. Thus a valid IP addresses can use only the numbers between 0 and 255 in the dotted-decimal notation.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_339_0.png)

### Internet services and port numbers

The TCP/IP protocol suite has become the lingua franca of the Internet because many standard services are available on any system that supports TCP/IP. These services make the Internet tick by facilitating the transfer of mail, news, and Web pages. These services go by well-known names such as the following:

- DHCP (Dynamic Host Configuration Protocol) is for dynamically configuring TCP/IP network parameters on a computer. DHCP is primarily
