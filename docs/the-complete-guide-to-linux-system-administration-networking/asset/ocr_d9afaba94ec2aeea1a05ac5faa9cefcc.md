# Understanding Networking

In Chapter 7, "Using Network Clients," you learned basic information about networking. This section provides more details on networking concepts. If your system administrator has set up a DHCP server on your network, however, configuring networking when you install Linux is easy: you just specify an option such as "Use DHCP" or "Use Dynamic Configuration."

If you do not have a DHCP server on your network and you plan on using Linux on a network, you need to define basic networking parameters when you install Linux. Even if you are using DHCP for your first installation, a basic knowledge of networking concepts is critical for your work as a Linux system administrator.

To communicate with each other effectively, computer systems use networking protocols. A protocol is an organized pattern of signals or words. Linux networking involves many different protocols, some of which you saw in Chapter 7. One protocol provides basic communication between network adapters (hardware in the computer that provides an interface between the computer and the network). Another lets Web browsers communicate with Web servers. Altogether, Linux supports dozens of networking protocols, each one designed for a different purpose. Some of the most important protocols are discussed in the following sections.

# IP Networking

Recall that to configure networking, each computer must have a unique IP address, either assigned explicitly or from a DHCP server. IP addresses are used all over the world, but if any two users have identical IP addresses, their networks can malfunction. To avoid these problems, you must only use an IP address that has been assigned to the computer on which you install Linux. Typically, if you are not relying on DHCP, your instructor or your Internet service provider (ISP) assigns you an IP address from a range of addresses that they have been assigned.

> NOTE
> A newer version of IP called IPv6 (for version 6), or IPng (for Next Generation) is also available, though it is not widely used yet. IPv6 addresses are four times as large as regular IP addresses (which are sometimes called IPv4, for version 4). Having larger addresses means that IPv6 can support many more networked devices. IPv6 also has many other advanced features to improve the Internet. IPv6 is an advanced topic that is not discussed in this book, but Linux fully supports IPv6 networking. You can learn more about it by visiting www.6bone.net.

All of the IP addresses on a single network are related; for example, their first three numbers may be the same. Several special IP addresses are associated with setting up Linux networking so that packets can be passed around the network. These special IP addresses are: