
## Remote Login, File Transfer, and Troubleshooting Protocols

Internet Message Access Protocol (IMAP) are used to retrieve e-mail from a mail server.

- **Remote login** is supported through telnet and Secure Shell (SSH). Telnet is a standard terminal emulation protocol used by clients to connect to remote telnet servers. Telnet allows users to remotely connect and issue commands. SSH allows connection to remote servers, but, unlike telnet, provides for encrypted sessions, allowing secure transmissions.
- **File Transfer** is provided through File Transfer Protocol (FTP) and Trivial File Transfer Protocol (TFTP). FTP is a reliable connection-oriented protocol for transferring files between networked systems. TFTP is a connectionless, unreliable protocol for transferring files between networked systems.
- **Troubleshooting** protocols include Packet Internet Groper (Ping) and Traceroute. Ping is used to determine whether a computer is connected to the network. Traceroute traces the path a packet takes to the remote host.

These protocols are divided into two protocol groups, Transmission Control Protocol (TCP) and User Datagram Protocol (UDP). **TCP** is a connection-oriented, reliable protocol. TCP establishes a virtual circuit between two hosts and ensures that information sent between the two is reliable. TCP guarantees delivery of segments. **UDP** is a connectionless and unreliable transport protocol. UDP is responsible for sending information between two hosts, but does not guarantee that the information will arrive at the destination. The advantage of UDP is speed. Because UDP does not guarantee delivery the message is much smaller and its delivery faster.

Consider the types of data that are transferred over a network. If you are copying a file (FTP) from one computer to another, the connection needs to be reliable. If you are requesting the IP address of a host on the Internet (DNS) and you don’t receive the address, you can just request again, because this information is not critical. Therefore, FTP is a TCP protocol and DNS is a UDP protocol.

## Ports

Your computer may be browsing the Web, reading e-mail, and transferring files, all at the same time. With all the different connections occurring there must be a way to track the conversations. TCP and UDP protocols use ports (or sockets) to keep track of the different sessions that are occurring on the network connections. Ports are assigned numbers to identify what they are for and which user is connected.

> **NOTE**
> RFC 1700 identifies port numbers and their assigned uses. See http://www.ietf.org/rfc/rfc1700.txt?number=1700.

Port numbers are divided into three different values. Port numbers from **0 to 255** are called well-known port numbers. These ports are assigned to standard protocols of the TCP/IP suite. For example, DNS is assigned the port number 53. Port numbers from **256 to 1023** are assigned to companies for marketable applications. For example, LDAP (Lightweight Directory Access Protocol, a protocol used to access a LDAP directory) is assigned the port number 389. Port numbers **above 1023** are unregulated. Look in the /etc/services file for a list of well-known ports and possible locally assigned ports.

End systems use port numbers to select the correct application, but the originating source port numbers are usually dynamically assigned values greater than 1023. The port number is part of the packet information and sent between the computers.

Commonly used ports are shown in Table 7–2.

### Table 7–2 Commonly used ports.

| Decimal Port Number | Common Name | Description |
| :--- | :--- | :--- |
| 5 | RJE | Remote Job Entry |
| 7 | ECHO | Echo |
| 15 | NETSTAT | Who is or NETSTAT |
| 20 | FTP-DATA | File Transfer Protocol data |
| 21 | FTP | File Transfer Protocol control |
| 22 | SSH | Secure Shell |
| 23 | Telnet | Terminal Connection |
| 25 | SMTP | Simple Mail Transfer Protocol |
| 53 | DOMAIN | Domain Name System |
| 63 | WHOIS | Whois ++ |
| 68 | DHCP | Domain Host Configuration Protocol |
| 69 | TFTP | Trivial File Transfer Protocol |
| 70 | GOPHER | GOPHER Distributed document search and retrieval |
| 79 | FINGER | Finger |
| 80 | HTTP | Hypertext Transfer Protocol |
| 98 | LINUXCONF | Linux configure |
| 110 | POP3 | Post Office Protocol version 3 |
| 115 | SFTP | Secure File Transfer Protocol |
| 119 | NNTP | Network News Transfer Protocol |
| 123 | NTP | Network Time Protocol |
| 143 | IMAP | Internet Mail Access Protocol |
| 161 | SNMP | Simple Network Management Protocol |

![](img/37f079cee226b270f2e09b37a2e4a05d_180_0.png)

## Network Addresses

Simply connecting machines together does not automatically enable them to talk to each other. Hosts on a network must have an address to allow communication. Various addressing schemes are available depending on the protocol used. Most use TCP/IP, but some will use AppleTalk or IPX, which are completely different from TCP/IP.

Two forms of addressing need to be considered, the physical address and the logical address. Physical addresses are used by the data link layer to find hosts that are on the same network segment. Logical addresses are used by the network layer to find hosts anywhere. A physical address is like your social security number. Regardless of where you go, the same number applies. A logical address is like your postal address. When you move to a new location your postal address will change.

### MAC Addresses

Each LAN interface on a host has a unique address burned into its ROM chip. This address is a 48-bit hexadecimal value divided into two parts. The first 24 bits identify the vendor or manufacturer of the device, and the second set of 24 bits identify the individual network interface card (NIC).

To view the MAC address of the Ethernet interface on a Linux-installed computer, use the command **ifconfig ethX** where X is the number of the Ethernet interface (0 for the first interface, 1 for the second, and so on). To view the configuration of the first Ethernet interface (Figure 7–5), type the **ifconfig eth0** command.

Several lines of information are displayed. The MAC address is shown on the line that starts with eth0. The line on Figure 7–5 is:

```
eth0      Link encap:Ethernet  HWaddr 00:90:27:8A:77:86
```

The MAC address for this interface is **00:90:27:8A:77:86**. In other programs or references, the MAC may be written as **0090.278A.7786**.

![](img/37f079cee226b270f2e09b37a2e4a05d_181_0.png)

Before a host directly connected on a LAN can exchange data with another computer, it must have the MAC address of the destination machine. The MAC address is determined through Address Resolution Protocol (ARP). The host transmits an ARP message requesting the MAC of a specific machine. All machines on the network segment will receive the message, but only the machine in question will respond with its MAC address. The host will store the MAC address in its ARP table for a short time to accommodate additional communications.

In Figure 7-6, if host 192.168.0.4 wants to send a message to 192.168.0.5, it will broadcast an ARP request to all machines on its network. The machines that do not match the requested address will discard the request. Machine 192.168.0.5 will send an ARP reply with its MAC address. When 192.168.0.4 receives the ARP reply it will use it in the frames that it generates in the data link layer.

![](img/37f079cee226b270f2e09b37a2e4a05d_181_1.png)

## IP Addresses

The MAC address is used to communicate between machines on the same network segment; however, to communicate with computers on the Internet and other large networks, a more comprehensive addressing scheme is required. The TCP/IP protocol suite requires that each host on the network have an Internet Protocol (IP) address.

When using TCP/IP, each host has a unique 32-bit logical address. The address is expressed in 32-bit dotted-decimal format. **192.168.0.1** represents a valid IP address and its binary equivalent is **11000000.10101000.00000000.00000001**. Each group of eight binary values is called an **octet**.

## Binary Numbers

A TCP/IP address is actually four groups of eight bits (eight bits are called a *byte*). A bit can have a binary value of 0 or 1. So the range of values of eight bits is 00000000 to 11111111, which translates into 0 to 255 in decimal.

With eight binary bits, from left to right, the bits have a decimal value of 128, 64, 32, 16, 8, 4, 2, and 1 (Figure 7–7). With all ones in the eight bits, you get a value of 255 by adding the value of each bit. To convert the binary bits to their decimal equivalent you add the associated values of each bit that has a binary value of one. For example, if you have the eight bits (byte) 11001101, you determine the decimal equivalent by adding the values of all the bits that have the binary value of one. In this case you would add 128 + 64 + 8 + 4 + 1 giving 205.

![](img/37f079cee226b270f2e09b37a2e4a05d_182_0.png)

![](img/37f079cee226b270f2e09b37a2e4a05d_182_1.png)

To convert a decimal number to its binary equivalent you can do the opposite. For example, if you have the decimal value of 205 you would do the sequence shown in Table 7–3.

![](img/37f079cee226b270f2e09b37a2e4a05d_182_2.png)

### Table 7–3 Decimal to Binary Conversion

| Binary Bit | Is the decimal number larger than the binary bit value? If yes, subtract the numbers and use the result on the next line. | Put 1 if the answer was yes and 0 if no |
| :---: | :---: | :---: |
| 128 | Yes: 205 – 128 = 77 | 1 |
| 64 | Yes: 77 – 64 = 13 | 1 |
| 32 | No: 13 – 32 | 0 |
| 16 | No: 13 – 16 | 0 |
| 8 | Yes: 13 – 8 = 5 | 1 |
| 4 | Yes: 5 – 4 = 1 | 1 |
| 2 | No: 1 – 2 | 0 |
| 1 | Yes: 1 – 1 = 0 | 1 |

The binary values are important in IP addresses because the bits are used to represent networks and hosts.

## Networks and Hosts

IP addresses can be divided into network and host components (Figure 7–8). The network portion identifies which network the host is attached to. The host portion identifies the specific device on that network.
