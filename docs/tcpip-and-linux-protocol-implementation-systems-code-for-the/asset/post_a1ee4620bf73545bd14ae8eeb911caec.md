
these protocols also have self-organizing-repair server mechanisms. These will alter the traffic patterns again.

Similar evolution is occurring in the streamed multimedia traffic flows that emanate from Internet radio and TV sites, with TCP-like adaptation being the apparent goal for RealAudio and Video, the most commonly used products for such services in the Internet.

## 7.5 Management

The following commands on Linux can be used to monitor the transport layer.

- Netstat—can display active connections; for example netstat -a will display all active and listening connections.
- Tcpdump—can trace packets on wire by putting system into promiscuous mode at driver level (says "recognize all frames as me") and passing up through a filter to an application that can further process or dump to a screen.
- ethereal (www.ethereal.com)—will provide a graphical display of network traffic.

## 7.6 TCP vs. UDP

As we have, TCP covers many of the problems with UDP, but at what cost? TCP is a much more heavyweight protocol than UDP. Indeed, it can be seen simply from the number of pages of this book how much effort is needed in its description and implementation. However there are some circumstances where UDP is the better transport mechanism. These include situations where memory and resources are limited, such as initial boot-off-network operations on diskless workstations where a TFTP (Trivial File Transfer Protocol) implementation, which runs over UDP, can be implemented in a few bytes of ROM code and minimal RAM requirements. Other times when use of UDP may benefit an advantage. When the lightweight nature can provide a performance advantage. An example here is DNS over a LAN, when a quick name resolution is required, and in a LAN environment there are often enough resources to be relatively assured of a successful communication. UDP can also be used when another mechanism is responsible for portioning the bandwidth, for example communication over RSVP-established sessions. The Real-Time Protocol (RTP) is a protocol designed to carry real-time traffic, such as video and audio, over the Internet. It uses UDP as its transport mechanism.

## 7.7 RTP–Real-Time Protocol

The RTP-time protocol is designed to carry multimedia flows over the Internet. Whether RTP is a transport layer protocol or an application layer protocol is a commonly debated point. For the argument that RTP is an application layer protocol are the facts that RTP data packets are carried in UDP segments (a transport layer service), and RTP is usually implemented in user space. For the contrary argument is the fact that RTP provides a number of additional services to application layer layer these are synchronization and framing. RFC 1889 describes RTP and a number of other RFCs describe different payload formats for particular media types. RTP is generally implemented as a user library and not in the kernel, so is is beyond the scope of this work.

## 7.8 Writing a New Transport Layer

If you are developing a new transport layer that uses IP as its networking layer and sockets as the application API, then linking it with the existing protocol suites becomes simply a matter of writing the appropriate linkage functions and filling in the function holding structures (see Section 7.3.4).

## 7.9 Summary

This chapter examined transport protocols and their implementation. The facilities provided by the transport layer, that is, multiplexing, reliability, flow and congestion control, synchronization, and framing, each have been examined and their implementations detailed. A comparison of popular transport protocols TCP, UDP, and RTP, has been made and instructions on writing your own transport layer given.

![](img/06c11ba8be5c1c24aa633e12618e2ebd_596_0.png)

> “I'm not sure that the ability to create routing diagrams similar to pretzels with Mad Cow disease is actually a marketable skill.”
—Steve Levin

## 8.1 Roadmap

This chapter is about Internet plumbing and path finding. Here we discuss how we interconnect links of different types, and having done so, how we find our way from A to B across a complex topology. Linux supports a variety of routing protocols; and Linux systems, running on PCs or other hardware platforms, are in widespread use as low-cost solutions for low- to medium-performance routers (though not entirely modest—up to 100 BaseT and OC3 wide area links are easily supported, and there are no obvious reasons not to build up to a Gbps router).

There are two main components to a router: forwarding and routing. The forwarding task is carried out on each and every packet and involves looking up the destination (and possibly other data from the packet) in a forwarding table, and using the result to decide which interface to transmit the packet on. This is a kernel procedure. The routing task involves the business of building and maintaining the forwarding table, and is carried out asynchronously, usually by a user space process. There are a variety of routing protocols that are used in the Internet, but the basic tasks are the same.

In this chapter, we review the components of the routing system, and then look at Linux kernel support for the forwarding information base and of it from routing protocols in user space.

## 8.2 Introduction

An routing system takes the work of finding a path away from end systems. As with the postal service, end users and systems only know the location (address) of a recipient to get information there. An end system discovers an address by being given it. Typically, an end user uses a DNS name, which is looked up in the name server system, and results in the application software being given an IP address. The end software then uses this address as the handle for communication with the far end. The infrastructure of the Internet protocol layer, in end routers and links, conspires to deliver the packets to the right place, based on the destination in IP packets. The routing system may optionally consult other fields in the IP header to provide enhanced services. The maps have to be constructed somehow, and there are a variety of approaches to doing this.

**Forwarding decision frequency.** The forwarding decision is taken most often. We can decide which route will take separately for each packet, or we fix our decision for a number of packets in a row, or even for a number of packets for a given user, perhaps for some configured amount of time. Whoever a forwarding system works, it seems that we do not want to carry out any complex calculation, and we especially want to avoid any exchange of information with any other routers just so as to be forward one packet.

Information about the world could be distributed infinitely quickly. In a physical transport system (e.g., the postal service, or a freeway system for cars) where information can be sent about remote conditions by radio in a communications network, the state of a link some ways can only be learned as the users' own data can travel. In other words, our information about the rest of the world is out of date. This means that it does not make sense to change what route we use too often. At one extreme, we can fix the route taken by packets manually, via some configuration tool or through network management. In fact, it is quite common to do this effectively in parts of the network where there are no choices anyway—this is called setting up a default route. As one looks further into the network, this does not make sense, since there are alternative possible paths through the network, and it would seem a shame not to be able to use them if our (default) choice link or path fails. Thus it is usual to configure fixed, or even default routes only on end systems or non-multihomed site access routers.

**Routing calculation frequency.** We could recalculate routes every time there was a new flow (e.g., a new TCP session or a new Web download). This might make sense if flows lasted a long time, since we might also be able to carry out some clever load balancing, provided we were able to tell the rest of the world about our new flow and which paths we were considering for it. In practice, on the Internet, flows are short lived, so most current routing protocols do not consider recalculating routes based on short-term information. It is more common to carry out a routing calculation based on one of two factors:

- data into the route computation; currently, this is regarded as somewhat of a black art.

It is also useful to have periodic refreshes (soft state refreshes) to make sure that everyone has a consistent view of the world.

**Routing update data sources.** The input data for a routing calculation can be delivered from a central monitoring system to each router, or from the router's neighbors, hop-by-hop, or distributed by each router flooding information to all the other routers in an area. Each approach has its advantages. Central systems may fail, depriving the routers of updates, but a centralized system takes load off the routers. A hop-by-hop advertisement is simple, but leads to potential inconsistency. A flooding approach can lead to a consistent view, but requires some traffic control for the route updates.

**Routing update data distribution.** The way the routing data is distributed is partly a consequence of the sources for routing calculation. However, in general, routing data is high priority; without it, user data is unlikely to be delivered to the right place, or via the right path. Routing data may flow over different channels than the users' data. If so, it is important for a routing protocol to maintain status information about the users' actual data path, since it is no longer implicit in the reception of routing update data over a link that the users' data will travel so easily.

If a flooding approach is used to distribute routing data, from or to a management node, or from each router to all in an area, the flood must be constrained not to loop. This may entail a simplified baseline routing computation (e.g., building a spanning tree amongst all the (routers) first.
