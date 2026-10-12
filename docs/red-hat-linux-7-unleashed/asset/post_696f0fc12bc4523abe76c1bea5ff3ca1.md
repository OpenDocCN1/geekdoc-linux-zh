
as 192.168.8.0/22. To correctly write out this particular range, you must specify two networks: 192.168.10.0/23 and 192.168.12.0/23. Here’s the general rule that lets you know whether the continuous base addresses may be grouped together: For the number X of continuous base addresses to have a common prefix (network number), X must be a power of two, and the last octet containing the network number must be evenly divisible by X.

With that rule in mind, revisit the 192.168.8.0/22 network. To apply the bit count (netmask) against the network prefix (network number), you can write out their binary values and visualize which ranges fall into the mask.

```text
1 10000001 01010100 00001000 00000000 (192.168.8.0)
1 11111111 11111111 11111100 00000000 (255.255.252.0 or 22-bits)
=====================================================
1 10000001 01010100 00000111 00000000 (192.168.7.0 is masked out)
1 10000001 01010100 00001000 00000000 (192.168.8.0 obviously is in)
1 10000001 01010100 00001001 00000000 (192.168.9.0 is in)
1 10000001 01010100 00001010 00000000 (192.168.10.0 is in)
1 10000001 01010100 00001011 00000000 (192.168.11.0 is in)
1 10000001 01010100 00001100 00000000 (192.168.12.0 is masked out)
```

In this example, X=4, because we’re combining four continuous base addresses—4 is a power of two, and 8 (the last octet of the base address) is evenly divisible by 4.

## Reserved Network Numbers

There is also a standard reserved block of addresses, defined in RFC-1918, for use in *private networks*. These are networks that will never be connected directly to any public network (specifically the Internet). The private-network addressing standard is shown in Table 20.2.

**TABLE 20.2 Private Network Addresses According to RFC-1918**

| Address Range | Network Class |
| --- | --- |
| 10.0.0.0–10.255.255.255 | A (1 class A network) |
| 172.16.0.0–172.31.255.255 | B (16 class B networks) |
| 192.168.0.0–192.168.255.255 | C (256 class C networks) |

There is another reserved class A network, with addresses in the range of 127.0.0.0–127.255.255.255. This is known as the *loopback* network. It is a virtual network that points to the same host where the packet originates. The usual loopback address in any system is 127.0.0.1. If you want a program to connect to the localhost (the same system) it’s running on, you can open a connection to 127.0.0.1. This is useful, for example, when running networking software in a system that isn’t connected to a network, or for testing daemons on the local system.

**Note**

The Class C IP address ranges are intended as private-network addresses for use on internal LANs, especially since the terminals or workstations are not directly connected to the Internet. Most Red Hat Linux users will set up a gateway computer that then forwards or retrieves information for the LAN--this is known as IP masquerading.

## Routing

Networks are connected by means of routers. A *router* is a device that has connections to two or more networks and takes care of moving packets between them. When a host sends out a packet whose destination lies in the same network, it sends it directly to the destination host. However, if the packet’s destination lies in a different network, it sends the packet to a router so that the router will send it to the correct network. This is why it’s so important to set a host’s netmask correctly--it’s the parameter that tells the host whether to send the packet directly to the destination host or to the router (see Figure 20.2).

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_691_0.png)

A network usually has a *default router*, which connects it to other networks. In such a setup, all traffic whose destination is outside the local network gets sent to the default router. There may be several routers in a network; for example, one to the Internet and another one to other internal networks. In this case, it may be necessary to use a *static route* to tell the host to send packets destined for specific subnets to a specific router, or use *dynamic routing* by means of a routing daemon (such as *lgprd* or *routed*). These daemons are discussed in the "Network Daemons" section later in this chapter.

## The TCP/IP Protocol Suite

TCP/IP is actually not just one protocol, but a protocol suite. At the low level, it’s composed of the following protocols:

- IP
- TCP
- UDP

IP is the lowest common denominator of TCP/IP. Every protocol at a higher level must eventually be translated into IP packets. An IP packet is self-contained in the sense that it contains within itself the addresses of its source and destination. However, it may be part of a larger conversation.

TCP is a *connection-based* or *stream-oriented* protocol on top of IP. This means that an application that communicates with another using TCP sends and receives data as a stream of bytes, and the TCP/IP stack takes care of splitting the data into packets and putting the packets back together again in the receiving end. It also ensures that the packets arrive in order and retransmission of missing or corrupt packets.

On the other hand, the UDP protocol is a *datagram-based* or *packet-oriented* protocol. It is a connectionless protocol. This protocol does not have built-in checking to ensure that the packets arrive in order, or to check for missing packets. However, due to this missing protocol overhead, UDP can be quite efficient for use with applications that send small amounts of information, or on a network that is fast and reliable, such as Ethernet on a private LAN.

Application-specific protocols work on top of TCP and UDP. Some of these follow:

- SMTP (Simple Mail Transfer Protocol)
- HTTP (HyperText Transfer Protocol)
- FTP (File Transfer Protocol)
- SNMP (Simple Network Management Protocol)
- NFS (Network Filesystem)

Each has different characteristics, depending on its intended use. Figure 20.3 shows the layers of the TCP/IP suite and the corresponding layers in the OSI reference model. The OSI model was never widely adopted. It consisted of seven layers: application, presentation, session, transport, network, (data) link, and physical.

## Ports

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_693_0.png)

A single computer may host several services. To distinguish one service from the next, something more is needed than just the host’s IP address. You use different ports on the computer to respond to specified services (see Figure 20.4). *Ports* are analogous to the jacks in an old-fashioned manual switchboard.

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_693_1.png)

A server daemon can be configured to listen on any port. However, things would be very complicated if this decision were entirely arbitrary, because there would be no easy way of finding out what port a given service was listening on. To help, some *well-known ports* have been defined in RFC-1700. Some of these well-known ports are listed in Table 20.3.

**TABLE 20.3 Some Well-Known Port Numbers**

| Port/Protocol | Name | Use |
|---|---|---|
| 7/tcp | echo | Echoes everything it receives |
| 13/tcp | daytime | Sends back the current date and time |
| 22/tcp | ssh | Secure Shell |
| 23/tcp | telnet | Remote terminal emulation |
| 25/tcp | smtp | Email transfer |
| 53/udp | domain | Domain Name System |
| 80/tcp | www | World Wide Web traffic |
| 110/tcp | pop3 | Post Office Protocol, version 3 |
| 443/tcp | https | Secure Web traffic |

## Sockets

In network parlance, a *socket* is a network connection between two processes, which may be running on the same or different computers. Technically, an *open socket* has four parts: source host, source port, destination host, destination port. A *closed socket* has only the source port and source host.

Note that a socket has ports on both sides of the connection. When a client tries to connect to a server, it first asks the system for a *free port* (one that isn't being used by any other program). It then asks the system to connect to a destination host and port using that source port. That is why there can be several programs connected between the same two hosts; for example, a browser can have two or more windows open to the same host. The system keeps track of both the source and the destination port, and has different sockets for each connection.

## Configuring the Network

In Red Hat, basic network configuration is generally done at installation time, when configuring the base system, but network interfaces may be added or deleted at any time. As with other UNIX systems, all configuration data is stored in text files in the */*etc tree.

An important thing to consider is that Linux, like other UNIX systems, can be reconfigured on-the-fly. In other words, almost any parameter can be changed while the system is operating, without rebooting. This makes it easy to experiment and correct configuration problems. However, if you are new to making permanent configuration changes, it is recommended that you reboot after making any important configuration changes, to ensure the correct configuration will be used when the system reboots.

If you are new to Red Hat Linux and simply want to configure your network to get your system running or to make basic changes to an existing configuration, then the following section is for you. It will quickly outline how to make changes to your network
