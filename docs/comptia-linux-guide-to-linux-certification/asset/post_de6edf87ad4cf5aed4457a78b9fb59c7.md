
- d. Use the cpio utility to back up all files in the /var directory (which contains symbolically linked files) to the first rewinding IDE tape device that has a block size of 5KB.
- e. Perform a full filesystem backup of the /var filesystem using the dump utility and record the event in the /etc/dumpdates file.
- f. View the contents of the archives created in Exercises 3a, c, d, and e.
- g. Extract the contents of the archives created in Exercises 3a and c to the /root directory.
- h. Extract the contents of the archives created in Exercises 3d and e to their original locations.
- 4. Use the Internet, the library, or other resources to research two other package managers available for Linux systems other than RPM and DPM. For each package manager, list the command and options required to install, query, and remove packages. Also list the benefits that the package manager offers to Linux users and from where it can be downloaded on the Internet.

## Chapter 12
## Network Configuration

After completing this chapter, you will be able to:

- Describe the purpose and types of networks, protocols, and media access methods
- Explain the basic configuration of TCP/IP
- Configure a network interface to use TCP/IP
- Configure a modem, ISDN, and DSL interface
- Describe the purpose of host names and how they are resolved to IP addresses
- Configure TCP/IP routing
- Identify common network services
- Use command-line and graphical utilities to perform remote administration

Throughout this book, you have examined the installation and administration of local Linux services. This chapter focuses on configuring Linux to participate on a network. First, you become acquainted with some common network terminology, then you learn about TCP/IP and the procedure for configuring a network interface. Next, you learn about the Domain Name Space and the processes by which host names are resolved to IP addresses. Finally, you learn how to configure TCP/IP routing as well as how to set up and use various utilities to perform remote administration of a Linux system.

### Networks

Most functions that computers perform today involve the sharing of information between computers. Information is usually transmitted from computer to computer via media such as fiber optic, telephone, coaxial, or unshielded twisted pair (UTP) cable, but it can also be transmitted via wire-less media such as radio, micro, or infrared waves. These media typically interact directly with a peripheral card on the computer, such as a network interface card (NIC) or modem device.

Two or more computers connected via media that can exchange information are called a network. Networks that connect computers within close proximity are called local area networks (LANs), whereas networks that connect computers separated by large distances are called wide area networks (WANs).

Many companies use LANs to allow employees to connect to databases and other shared resources such as printers. Home users can also use LANs to connect several home computers together. Alternatively, home users can use a WAN to connect home computers to an Internet service provider (ISP) to gain access to resources such as Web sites on the worldwide public network called the Internet.

![](img/c27875544958897d817484d558c208c8_555_0.png)

The Internet (the name is short for “inter-network”) is merely several interconnected public networks. Both home and company networks can be part of the Internet. Special computers called routers transfer information from one network to another.

Network media serve as the conduit for information as it travels across a network. But simply sending information through this conduit is not enough. In order for the devices on the network to make sense of this information, it must be organized according to a set of rules, or protocols. A network protocol breaks information down into packets that can be recognized by workstations, routers, and other devices on a network.

You can configure many different network protocols in Linux, including but not limited to the following:

- TCP/IP (Transmission Control Protocol/Internet Protocol)
- UDP/IP (User Datagram Protocol/Internet Protocol)
- IPX/SPX (Internetwork Packet Exchange/Sequenced Packet Exchange)
- AppleTalk
- DLC (Data Link Control)
- DECnet (Digital Equipment Corporation network)

**NOTE**

![](img/c27875544958897d817484d558c208c8_556_0.png)

The most common LAN protocol used today is TCP/IP. It is the standard protocol used to transmit information across the Internet and the one discussed in this chapter.

**NOTE**

![](img/c27875544958897d817484d558c208c8_556_1.png)

When transmitting information across a WAN, you might use a WAN protocol in addition to a specific LAN protocol to format packets for safer transmission. The two most common WAN protocols are Serial Line Internet Protocol (SLIP) and Point-to-Point Protocol (PPP).

Another important part of the puzzle, the media access method, is a set of rules that govern how the various devices on the network share the network media. The media access method is usually contained within the hardware on the NIC or modem. Although many media access methods are available, the one most commonly used to send TCP/IP packets onto network media is Ethernet. It ensures that any TCP/IP packets are retransmitted onto the network if a network error occurs. Another media access method, Token Ring, controls which computer has the ability to transmit information by passing a special packet of information, called a token, around the network. Only the computer that currently has the token can transmit information.

**NOTE**

![](img/c27875544958897d817484d558c208c8_556_2.png)

Wireless-Fidelity (Wi-Fi) LANs also use Ethernet to place packets onto the network medium (in this case, the air).

### The TCP/IP Protocol

The TCP/IP protocol is actually a set, or suite, of protocols with two core components: TCP and IP. Together, these two protocols ensure that information packets travel across a network as quickly as possible, without getting lost or mislabeled.

When you transfer information across a network such as the Internet, that information is often divided into many thousands of small packets. Each of these packets may take a different physical route when reaching its destination since routers can transfer information to multiple interconnected networks. TCP ensures that packets can be assembled in the correct order at their destination regardless of the order in which they arrive. Additionally, TCP ensures that any lost packets are retransmitted.

IP is responsible for labeling each packet with the destination address. As a result, each computer that participates on a TCP/IP network must have a valid Internet Protocol (IP) address that identifies itself to the IP protocol. Nearly all computers on the Internet use a version of the IP protocol called IP version 4 (IPv4). However, a small number of computers use a next-generation IP protocol called IP version 6 (IPv6). We will examine the structure and configuration of IPv4 and IPv6 in this chapter.

### The IPv4 Protocol

To participate on an IPv4 network, your computer must have a valid IP address as well as a subnet mask. Optionally, you can configure a default gateway to participate on larger networks such as the Internet.

#### IPv4 Addresses

An IP address is a unique number assigned to the computer that identifies itself on the network, similar to a unique postal address that identifies your location in the world. If any two computers on the same network have the same IP address, it is impossible for information to be correctly delivered to them. Directed communication from one computer to another single computer using TCP/IP is referred to as a **unicast**.

The most common format for IPv4 addresses is four numbers called **octets** that are separated by periods. Each octet represents an 8-bit binary number (0=255). An example of an IP address in this notation is 192.168.5.69.

You can convert between decimal and binary by recognizing that an 8-bit binary number represents the decimal binary powers of two in the following order:

| Bit | Value |
| :--- | :--- |
| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |

Thus, the number 255 is 11111111 (128+64+32+16+8+4+2+1) in binary, and the number 69 is 01000101 (64+4+1) in binary. When the computer looks at an IP address, the numbers are converted to binary. To learn more about binary/decimal number conversion, visit www.wikitow.com/Convert-from-Decimal-to-Binary.

All IPv4 addresses are composed of two parts: the network ID and the host ID. The **network ID** represents the network on which the computer is located, whereas the **host ID** represents a single computer on that network. No two computers on the same network can have the same host ID; however, two computers on different networks can have the same host ID.

The network ID and the host ID are similar to postal mailing addresses, which are made up of a street name and a house number. The street name is similar to a network ID. No two streets can have the same name, just as no two networks can have the same network ID. The host ID is like the house number. Two houses can have the same house number as long as they are on different streets, just as two computers can have the same host ID as long as they are on different networks.

Only computers with the same network ID can communicate with each other without the use of a router. This allows administrators to logically separate computers on a network; computers in the Accounting Department could use one network ID, whereas computers in the Sales Department could use a different network number. If the two departments are connected by a router, computers in the Accounting Department can communicate with computers in the Sales Department and vice versa.

![](img/c27875544958897d817484d558c208c8_557_0.png)

> If your TCP/IP network is not connected to the Internet, the choice of IP address is entirely up to you. However, if your network is connected to the Internet, you might need to use preselected IP addresses for the computers on your network. IP addresses that can be used on the Internet are assigned by your Internet service provider.

![](img/c27875544958897d817484d558c208c8_557_1.png)

The IP address 127.0.0.1 is called the **loopback IP address**. It always refers to the local computer. In other words, on your computer, 127.0.0.1 refers to your computer. On your coworker's computer, 127.0.0.1 refers to your coworker's computer.
