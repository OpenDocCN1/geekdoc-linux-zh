
forms the basis of the Internet; without it the Internet would be a very different place indeed, if it even existed!

On the other hand, UDP is a connectionless protocol. Applications using this protocol just choose their destination and start sending. UDP is normally used for small amounts of data or on fast and reliable networks. If you are interested in the internals of TCP/IP, see the “Reference” section at the end of this chapter for places to look for more information.

## Ubuntu and Networking

Chances are that your network card was configured during the installation of Ubuntu. You can however, use the ifconfig command at the shell prompt or Ubuntu’s graphical network configuration tools, such as network-admin, to edit your system’s network device information or to add or remove network devices on your system. Hundreds of networking commands and utilities are included with Ubuntu—far too many to cover in this chapter and more than enough for coverage in two or three volumes.

Nearly all Ethernet cards can be used with Linux, along with many PCMCIA wired and wireless network cards. The great news is that many USB wireless network devices also work just fine with Linux, and more will be supported with upcoming versions of the Linux kernel. Check the Linux USB Project at http://www.linux-usb.org/ for the latest developments or to verify support for your device.

After reading this chapter, you might want to learn more about other graphical network clients for use with Linux. The GNOME Ethereal client, for example, can be used to monitor all traffic on your LAN or specific types of traffic. Another client, NmapFE, can be used to scan a specific host for open ports and other running services.

## TCP/IP Addressing

To understand networking with Linux, you need to know the basics of TCP/IP addressing. Internet IP addresses (also known as public IP addresses) are different from those used internally on a local area network, or LAN. Internet IP addresses are assigned (for the United States and some other hosts) by the American Registry for Internet Numbers, available at http://www.arin.net/. Entities that need an Internet address apply to this agency to be assigned an address. The agency assigns Internet service providers (ISPs) one or more blocks of IP addresses, which the ISPs can then assign to their subscribers.

You will quickly recognize the current form of TCP/IP addressing, known as IPv4 (IP version 4). In this method, a TCP/IP address is expressed as a series of four decimal numbers—a 32-bit value expressed in a format known as dotted decimal format, such as 192.168.120.135. Each set of numbers is known as an octet (eight ones and zeros, such as 10000000 to represent 128) and ranges from zero to 255.

The first octet usually determines what class the network belongs to. There are three classes of networks. The classes are:

Class A—Consists of networks with the first octet ranging from 1 to 126. There are only 126 Class A networks—each composed of up to 16,777,214 hosts. (If you are doing the math, there are potentially 16,777,216 addresses, but no host portion of an address can be all zeros or 255s.) The "10." network is reserved for local network use, and the "127." network is reserved for the loopback address of 127.0.0.1. Loopback addressing is used by TCP/IP to enable Linux network-related client and server programs to communicate on the same host. This address will not appear and is not accessible on your LAN.

## NOTE

Notice that zero is not included in Class A. The zero address is used for network-to-network broadcasts. Also, note that there are two other classes of networks, Classes D and E. Class D networks are reserved for multicast addresses and not for use by network hosts. Class E addresses are deemed experimental, and thus are not open for public addressing.

Class B—Consists of networks defined by the first two octets with the first ranging from 128 to 191. The "128." network is also reserved for local network use. There are 16,382 Class B networks—each with 65,534 possible hosts.

Class C—Consists of a network defined by the first three octets with the first ranging from 192 to 223. The "192." network is another that is reserved for local network use. There are a possible 2,097,150 Class C networks of up to 254 hosts each.

No host portion of an IP address can be all zeros or 255s. These addresses are reserved for broadcast addresses. IP addresses with all zeros in the host portion are reserved for network-to-network broadcast addresses. IP addresses with all 255s in the host portion are reserved for local network broadcasts. Broadcast messages are not typically seen by users.

These classes are the standard, but a netmask also determines what class your network is in. The netmask determines what part of an IP address represents the network and what part represents the host. Common netmasks for the different classes are:

- Class A—255.0.0.0
- Class B—255.255.0.0
- Class C—255.255.255.0

Because of the allocation of IP addresses for Internet hosts, it is now impossible to get a Class A network. It is also nearly impossible to get a Class B network (all the addresses have been given out, but some companies are said to be willing to sell theirs), and Class C network availability is dropping rapidly with the current growth of Internet use worldwide. See the following sidebar.
