# **10.1 Why we need TCP and transport protocols**

Up to now we have dealt only with the “IP” part of “TCP/IP”. As we saw throughout Part 1, IP is the protocol that moves the packets from the source machine to the destination machine, over the intervening networks via routers. That’s why the IP layer of the stack is also called the internet or network layer (Figure 10.1). From here on we deal with the upper layers in the TCP/IP stack – the *transport* (or *host-to-host*) layer and the *application* layer, both of which perform functions that applications need but that are not provided by the raw IP (network) or link layers. In this chapter we concentrate on TCP, the Transmission Control Protocol. This is the transport layer protocol used by the World Wide Web, e-mail, FTP, and other applications that account for most of the traffic on the Internet. The other widely used transport is UDP, which we cover in Chapter 15.

![](bbox=[0.42, 0.33, 0.64, 0.55])

Figure 10.1 **The TCP/IP protocol stack**

Why do we need these higher-level transport protocols at all and not just use raw IP packets for everything? TCP gives us three major benefits over IP:

+   1. IP is an *unreliable* (or *best-effort*) protocol. It does its best to deliver the data but packets can get lost, e.g. if a router fails or a connection breaks, or if the underlying Ethernet network, which is also only best-effort, fails to deliver a packet. If IP drops a packet like this, the packet is lost, silently – no error message is generated anywhere. For many applications this isn't acceptable, and that’s where TCP comes in. TCP is a *reliable* network protocol: it goes to great lengths to guarantee to deliver all your data, and in the order you sent it, so I know that you receive exactly what I sent. For this reason applications that need to exchange large volumes of data usually use TCP.
+      We explain how TCP provides a reliable connection over unreliable IP in the next module. (By contrast, UDP is not reliable – it’s only best-effort, as we’ll see in Chapter 15.)

+   2. the IP layer routes packets only to the level of a machine. Once the packets arrive at this machine, IP doesn’t have a mechanism for distinguishing packets for different applications on this machine, or for discriminating between multiple connections