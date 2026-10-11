![](bbox=[0.17, 0.075, 0.24, 0.145])

**EXAM TIP**  Be sure you are very comfortable with Linux networking basics before taking your Linux+/LPIC-1 exam. The exam assumes you have a solid understanding of the Internet Protocol (IP). Be sure you understand how IP addressing works. You should be able to look at any given IP address and identify it as a class A, B, or C address. You should also be able to identify the network and node portions of the address using the subnet mask. You should know what the DNS server and default gateway router addresses are used for when configuring network settings on a Linux system. You should also know how to install a network interface in the system, including an Ethernet card and a modem. You should know how to use the ifconfig command to manage the network interfaces installed in your system. You should also know how to use commands such as ping, netstat, and traceroute to troubleshoot your network configuration.

Let's begin this chapter by reviewing how the IP protocol can be used to enable communications between networked systems.

# # IP Networking Overview

Before you can configure your Linux system to participate on a computer network, you have to first install some kind of network interface and then configure it to work on your particular network. Back in the early days of networking, you could choose from a variety of network interfaces and network protocols. For example, when I first started managing computer networks, I pretty much had three choices for my network infrastructure:

+   - Archnet
+   - Token Ring
+   - Ethernet

For network protocols, you could choose from the Internetwork Packet Exchange (IPX) protocol or the Internet Protocol (IP), as well as some upper-layer protocols such as NetBIOS.

Archnet has been dead and gone for some time. It has completely disappeared from the network scene. I doubt you will ever encounter an Archnet network. Likewise, Token Ring has all but disappeared, although you may still find it deployed on a limited number of networks. By far and away, most of the networks you will work with will be Ethernet networks.

The same holds true with networking protocols. There was a time when many networks ran the IPX protocol. Today, however, IPX has almost disappeared. If you're going to be working with a modern network, you will more than likely be working with the IP protocol.

In light of this situation, the Linux+/LPIC-1 exam is heavily focused on using Ethernet boards configured with the IP protocol in Linux systems. We're going to spend the first part of this chapter learning how to do this.