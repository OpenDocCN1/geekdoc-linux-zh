# 360 Linux Administration: A Beginner’s Guide

![](bbox=[0.33, 0.09, 0.66, 0.18])

From: 200.2.2.2:1025
To: 192.168.1.5:80

Eth0: 192.168.1.1

![](bbox=[0.47, 0.25, 0.56, 0.285])

Eth1: 100.1.1.1

From: 200.2.2.2:1025
To: 100.1.1.1:80

![](bbox=[0.43, 0.35, 0.63, 0.41])

**Figure 13-2** Using DNAT on a connection

server sends a packet back, the NAT engine does the reverse, so the client thinks that it is talking to 100.1.1.1. (Note that this particular form of NAT is also referred to as port address translation, or PAT).

# **Connection Tracking and NAT**

Although the surface NAT appears to be a great way to provide security, unfortunately it is not enough. The problem with NAT is that it doesn’t understand the contents of the flows and whether a packet should be blocked because it is in violation of the protocol. For example, if we have a network set up, as in Figure 13-2. When a new connection arrives for the server, we know that it must be a TCP SYN packet. With a blind NAT, however, the packet will be forwarded, regardless of its purpose of establishing a new connection. Whether or not it is a TCP SYN packet.

To make NAT useful, Linux offers *stateful connection tracking*. This feature allows NAT to examine a packet’s header intelligently and determine whether it makes sense from a TCP protocol level. Thus, if a packet arrives for a new TCP connection that is not a TCP SYN, connection tracking will reject the packet without putting the server at risk. Even better, if a valid connection is established and a malicious person tries to spoof a random packet into the flow, stateful connection tracking will drop the packet unless it matches all of the criteria to be a valid packet between the two endpoints (a difficult feat, the attacker is able to sniff the traffic ahead of time).

As we discuss NAT throughout the remainder of this chapter, keep in mind that NAT NAT can occur, state connection tracking can occur.