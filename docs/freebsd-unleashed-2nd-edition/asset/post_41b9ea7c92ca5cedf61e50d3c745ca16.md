
a type of switch that links different networks so that traffic from hosts on one network can travel to another network directly without having to go to a router in the interim. Think of a bridge as a type of switch that spans different networks, linking them together above the *data link* layer of the stack so that traffic from hosts on one network destined for another network can travel there directly without having to go to a router in the interim. This is useful for allowing traffic to pass from an Ethernet network to a Token Ring network, which is another style of LAN that is rapidly on the way out, so we won't bother discussing it.

## Routers

A router is the most complex (and expensive) of all networking devices. Routers have full operating systems and maintain tables that keep track of where entire networks can be found. Most small networks have only one router, at the "edge" of the network (the boundary between the LAN and the WAN that connects it to the Internet), specifying which network numbers indicate the LAN and which ones should be forwarded upstream into the WAN. You can have any number of routers in your network, though, each one managing a subnetwork and subsubnet to the topmost router.

What's more, routers use a variety of protocols to communicate with each other and plot out what's the best way for a packet to get from one place to another. When you send out a packet, it travels upstream from router to router, until it reaches a router that knows where downstream to find your packet's destination network. That router sends your packet through the downstream route until it reaches the destination LAN and, ultimately, the destination host. Routing is the backbone of the Internet and possibly the most complex part of the way TCP/IP networking operates. You'll learn more about routing in Chapter 27, "Configuring an Internet Gateway."

> **TIP**
> You can see Internet routing in action by performing a *traceroute*; simply type **traceroute *<hostname>*** to get a listing of all the routers between you and your specified host as well as a reading of how fast that router responds. This is also useful for seeing how well the routers are performing between you and your destination host. Here's an example:

```
# traceroute freebsd.org
traceroute to freebsd.org (216.136.204.21), 64 hops max, 40 byte packets
  1 dot7.rrc1.pf.somehere.com (203.152.186.253) 3.200 ms  0.632 ms  3.910 ms
  2 pos1-0-0.orc5.pf.somehere.com (192.7.4.162) 1.055 ms  0.634 ms  0.572 ms
  3 gr-2-0-0-1.orpa8.pf.somehere.com (192.7.4.164) 1.862 ms  1.390 ms  1.426 ms
  4 so-1-0-0.orpa7.pf.somehere.com (192.7.4.230) 1.366 ms  1.003 ms  3.606 ms
  5 bas1-m.pao.yahoo.com (198.32.176.135) 1.211 ms 1.310 ms 1.378 ms
  6 ge-0-2-0.msr1.sc5.yahoo.com (216.115.100.233) 2.456 ms 2.413 ms ge-1-2-0.msr2.sc5.yahoo.com (216.115.101.230) 4.885 ms
  7 v144.bas2-m.sc5.yahoo.com (66.163.160.222) 1.925 ms 2.295 ms 2.389 ms
  8 freefall.FreeBSD.org (216.136.204.21) 4.577 ms 2.107 ms 3.137 ms
```

Most routers have either one or two LAN-side ports, either RJ-45 jacks or AUI ports that require transceivers—devices that translate the signal from one physical format to another—to convert the interface to twisted pair. On the other side of the router is a serial cable that connects to the DSU/CSU or other such high-speed serial converter, beyond which you have WAN traffic. Routers vary greatly in size, complexity, number, and type of ports, manageability, and price. Understanding how they work is one of the most important things you can learn in the networking world.

## Network Protocols

We've mentioned that most Internet traffic—HTTP, e-mail, FTP, and so on—uses TCP/IP as its transport protocol. TCP/IP itself refers to the combination of the most common “network” and “transport” protocols in use on the Internet. IP, the Internet Protocol, is the backbone of the vast majority of Internet traffic—the “network” layer of the TCP/IP stack. TCP, however, isn't the only commonly used “transport” layer protocol. There's also UDP, the User Datagram Protocol, which differs from TCP in a few key ways. IP also isn't the only means of carrying traffic at the “network” level; it has a number of contemporaries, too, but they're mostly useful on LANs. These include AppleTalk, IPX, NetBIOS, and so on. Then there's ICMP, which exists partly on the “network” layer and partly on the “transport” layer; it's the mechanism by which the `ping` and `traceroute` utilities work. We'll talk about each of these protocols in some detail next.

### The Transmission Control Protocol (TCP)

TCP is a two-way transmission protocol that's designed to be *reliable*, unlike UDP. TCP has lots of built-in features to make sure the traffic it carries arrives properly at its destination. It also has features to divide large packets into appropriately sized fragments so as to transmit more efficiently.

TCP uses *retransmission* to provide reliability. Here's how a simplified version of retransmission works: When a TCP packet is sent over the network, a timeout is set by the sender, which then waits for an acknowledgment (ACK) packet to come back from the other side. When it receives the ACK, the sender then proceeds to send the next packet. If the sender doesn’t get the ACK within the specified timeout, it knows that either its own packet didn’t make it or the acknowledgment packet got lost on the way back. The sender resends the packet and again waits for the ACK. This is a retransmission, and although it does provide reliability, it also decreases network efficiency. Each time a packet is retransmitted, it creates doubled traffic in the infrastructure, which can lead to congestion, especially considering that each packet has a certain amount of overhead in the size of the TCP/IP headers that must accompany it. This overhead uses up a certain amount of bandwidth, regardless of what other content makes up the packets.

A TCP connection involves an active setup procedure in which both hosts at the endpoints of the connection exchange startup tokens; disconnection at the end of a flow involves a similar exchange. This means that, unlike UDP flows, TCP flows can be accurately tracked by the system and their state can be viewed using tools such as netstat. TCP connections are also full-duplex, meaning that data can be sent and received at the same time, using the same packets. It’s not uncommon for there to be a data payload on the ACK packets, for example. TCP has a number of other interesting features, such as a checksum that ensures the integrity of the data in the packet, automatic packet fragmentation and reconstruction, and out-of-order resequencing at the receiver level. These are all things that UDP doesn’t do—or at least isn’t required to do.

TCP is used in protocols in which data integrity is important and a connection can be ensured, such as Web surfing, e-mail, FTP, and the vast majority of other network applications.

### The User Datagram Protocol (UDP)

UDP is a similar “transport” protocol to TCP, existing at the same layer in the OSI stack model; however, it differs from TCP in a number of key ways. The big thing to remember about UDP is that it’s unreliable. There is no acknowledgment mechanism, no retransmission mechanism, and no true “connection” concept. UDP packets can be broadcast to anyone on the network, if so chosen, or a selected set of recipients, regardless of whether they’re expecting to hear anything.

UDP packets can get lost along the way from the sender to the receiver, and neither can have any way of knowing that it missed any packets. There are no sequence numbers in UDP as there are in TCP. A sender simply spews out the traffic, and the specified recipients can receive it or not—it’s up to them and the network. Any reliability in a UDP flow must be added by the application using it; an example of this is the Network Filesystem (NFS) protocol, which is described in detail in Chapter 32, “The Network Filesystem (NFS).”

> **NOTE**
> Why would a file-management and transfer protocol such as NFS, with its need for secure data integrity, use UDP? The reason is that with NFS, many hosts on the network can be using an NFS resource, and any of them can drop off the network without warning. Rather than maintaining
