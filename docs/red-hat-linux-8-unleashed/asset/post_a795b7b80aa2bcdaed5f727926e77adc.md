
# Networking with TCP/IP

The first octet usually determines what class the network belongs to. There are three classes of networks. The classes are

- Class A—Consists of networks with the first octet ranging from 1 to 126. There are only 126 Class A networks—each composed of 16,777,214 hosts. (If you're doing the math, there are potentially 16,777,216 addresses, but no portion of an address can be all zeros or 255s). The “10.” network is reserved for local network use, and the “127.” network is reserved for the loopback address of 127.0.0.1. Loopback addressing is used by TCP/IP to allow Linux-related client and server programs to communicate on the same host. This will not appear and is not accessible on your LAN.

NOTE

Notice that zero is not included in Class A. The zero address is used for network-to-network broadcasts. Note that there are two other classes of networks, Class D and E. Class D networks are reserved for multicast addresses and not for use by network hosts. Class E addresses are deemed experimental, and thus are not open for public addressing.

- Class B—Consists of networks defined by the first two octets with the first ranging from 128 to 191. The “128.” network is also reserved for local network use. There are 16,382 Class B networks—each with 65,534 possible hosts.

- Class C—Consists of a network defined by the first three octets with the first ranging from 192 to 223. The “192.” network is another that is reserved for local network use. There are a possible 2,097,150 Class C networks of up to 254 hosts.

No host portion of an IP address can be all zeros or 255s. These addresses are reserved for broadcast addresses. IP addresses with all zeros in the host portion are reserved for network-to-network addresses. IP addresses with all 255s in the host portion are reserved for local network broadcasts. Broadcast messages are not typically seen by users.

These classes are the standard, but a netmask determines what class your network is. The netmask determines what part of an IP address represents the network and what part represents the host. Common netmasks for the different classes are

- Class A—255.0.0.0
- Class B—255.255.0.0
- Class C—255.255.255.0

Because of the allocation of IP addresses for Internet hosts, it is now impossible to get a Class A network. It is also nearly impossible to get a Class B network (all the addresses have been given out, but some companies are said to be selling them), and Class C network availability is dropping rapidly with the current growth of Internet use-wide. See the following sidebar.

![](img/446debe023486a07fde575245cf7a3ff_426_0.png)

# Limits of IP Addressing

The current ipv4 address scheme is based on 32-bit numbering and limits the number of available IP addresses to about 4.1 billion. Many companies and organizations (particularly in the United States) were assigned large blocks of IP addresses in the early stages of the growth of the Internet, which has a shortage of "open" addresses. Even with careful allocation of Internet-connected host addresses and the use of Network Address Translation (to provide communication to and from machines behind an Internet-connected computer), the Internet might run out of available addresses.

Red Hat Linux supports the use of ipv6 and many of networking tools conforming to ipv6 addressing. These tools include ipv6-based packet-filtering, ping, traceroute, and others. Migration to ipv6 is slow in coming, however, because the majority of computer operating systems, software, hardware, and users are still in the ipv4 mindset. Supporting ipv6 will require rewrites to many networking utilities, operations of operating systems currently in use, and firmware in routing and firewall hardware.

# Using IP Masquerading in Red Hat Linux

Three blocks of IP addresses are reserved for use on internal networks and hosts not directly connected to the Internet. The address ranges are 10.0.0.0 to 10.255.255.255, or 1 class A network; 172.16.0.0 to 172.31.255.255, or 16 class B networks; and 192.168.0.0 to 192.168.255.255, or 256 class C networks. Use these addresses when building a Local Area Network (LAN) for your business or home. Which class you choose can depend on the number of hosts on your network.

Internet access for your internal network can be provided by a PC running Red Hat Linux. The Red host is connected to the Internet and used as an Internet gateway to forward information to and from your LAN. The host should also be used as a firewall to protect your network from malicious data and users while functioning as an Internet gateway. The computer will typically have at least two network connections. One is connected to the Internet with the other connected to the computers on the LAN (via a hub or switch). Data is then passed between the LAN and the Internet using Network Address Translation, or NAT, better known in Linux circles as IP Masquerading. See the section "Security" later in this chapter.

# Ports

Most servers on an IP have more than one. For example, servers can use different ports for:

| Service | Port |
| :--- | :--- |
| FTP | 21 |
| HTTP | 80 |
| POP3 | 110 |
| SMTP | 25 |
| SSH | 22 |

These ports are used to identify different services on a host. For example, a web server listens on port 80, while a mail server listens on port 25. Ports are numbered from 0 to 65535. The first 1024 are called well-known ports, and the 1024-49151 are called registered ports. The 49152-65535 are dynamic or ephemeral ports.
