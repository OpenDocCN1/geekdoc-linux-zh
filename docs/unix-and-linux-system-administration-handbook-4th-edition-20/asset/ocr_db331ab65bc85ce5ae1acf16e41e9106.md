# Chapter 14 TCP/IP Networking

# DHCP software

ISC, the Internet Systems Consortium, maintains a very nice open reference implementation of DHCP. Major versions 2, 3, and 4 of ISC's software are all in common use, and all of these versions work fine for basic service. Version 3 supports backup DHCP servers, and version 4 supports IPv6. Server, client, and relay agents are all available from isc.org.

Major Linux distributions use some version of the ISC software, although you may have to install the server portion explicitly. The server package is called dhcp on Red Hat, dhcp3-server on Ubuntu, and dhcp-server on SUSE.

Non-Unix systems have their own home-grown DHCP implementations, and unfortunately our example UNIX systems all fall into this category.

It's best not to tamper with the client side of DHCP, since that part of the code is relatively simple and preconfigured and ready to use. Changing the client side of DHCP is not trivial.

However, if you need to run a DHCP server, we recommend the ISC package over vendor-specific implementations. In a typical heterogeneous network environment, administration is greatly simplified by standardization on a single implementation. The ISC software provides a reliable, open source solution that builds without incident on most versions of UNIX.

In the next few sections, we briefly discuss the DHCP protocol, explain how to set up the ISC server that implements it, and review some configuration issues.

# How DHCP works

DHCP is a backward-compatible extension of BOOT, a protocol originally designed to help disk UNIX workstations. DHCP generalizes the parameters that can be supplied and adds the concept of a lease period for assigned values.

A DHCP client begins its interaction with a DHCP server by broadcasting a "Hello! Who am I?" message.¹⁵ If a DHCP server is present on the local network, it negotiates with the client to provide an IP address and other networking parameters. If there is no DHCP server on the local net, servers on different subnets receive the initial broadcast message through a separate piece of DHCP software that acts as a relay agent.

When the client's lease time is half over, it attempts to renew its lease. The server is obliged to keep track of the addresses it has handed out, and this information must persist across reboots. Clients are supposed to keep their lease state across reboots too, although many do not. The goal is to maximize stability in network configuration. In theory, all software should be prepared for network changes at a moment's notice, but a lot of still makes unwarranted assumptions about the continuity of the network.

+   15. The clients initiate conversations with the DHCP server by using the generic all-ones broadcast address. The clients don't know their subnet masks and therefore can't use the subnet broadcast address.