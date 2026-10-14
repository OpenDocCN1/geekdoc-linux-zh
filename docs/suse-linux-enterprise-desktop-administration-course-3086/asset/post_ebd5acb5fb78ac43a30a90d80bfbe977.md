
## Network Connections (Sockets)

In UNIX and some other operating systems, a software object that connects an application to a network protocol is called a socket. This enables two-way communication between programs on a network.

For example, a program can send and receive TCP/IP messages by opening a socket and reading data from and writing data to the socket.

This simplifies program development because the programmer only needs to worry about working with the socket and can rely on the operating system to actually transport messages across the network correctly.

Each socket gets bound to a given port, which lets the Transport-layer protocol (such as TCP or UDP) identify which application to send data to.

For TCP and UDP protocols, a socket on a host is defined as the combination of an IP address and a port number (such as http://192.168.1.1:5801).

![](img/9129877170834ca9d5fdac5319bf5f12_641_0.png)

Another type of socket used by POSIX-compliant systems (called POSIX Local IPC Sockets or simply IPC sockets) facilitates interprocess communication. These connections are from the local computer to itself, and not a connection over a physical network.

![](img/9129877170834ca9d5fdac5319bf5f12_641_1.png)

For details on TCP and UDP protocols, see “Transmission Control Protocol (TCP)” and “User Datagram Protocol (UDP).”

## Network Services

Network services are programs that let users share network resources. On a network, nodes use network services to communicate across transmission media, such as cables.

Network services require resources and processing capabilities to accomplish a task, such as data processing.

Some examples of network services are CUPS (Common UNIX Printing System), DNS (for name resolution), and NFS (for network file services).

## TCP/IP Layer Model

Over the years, the functions of networks have grown in complexity due to different types of networks needing to be connected and the increasing number and requirements of applications.

Because of this increasing complexity, an attempt has been made to combine individual tasks within a network into groups and implement these as packages.

In the network environment, these packages are organized as layers stacked on top of each other. The overall model is referred to as the layer model.

One of the best-known layer models is the OSI (Open Systems Interconnection) reference model for open systems. In this model, a communication system is divided into seven layers. However, Figure B-11 shows a comparison of another well-known model, the TCP/IP layer model, that has only four layers.

![](img/9129877170834ca9d5fdac5319bf5f12_642_0.png)

Figure B-11

With the TCP/IP model, the three upper layers of the OSI model are combined into the Application layer and the two lower layers into the Network Access layer.

The following sections describe the layers in the TCP/IP model:

- Network Access Layer
- Internet Layer
- Transport Layer
- Application Layer

## Network Access Layer

In the TCP/IP layer model, the Physical layer and the Data Link layer of the OSI model are combined into the Network Access layer, as shown in Figure B-12.

![](img/9129877170834ca9d5fdac5319bf5f12_643_0.png)

Figure B-12

One reason TCP/IP is so popular is that it runs on the different network architectures for WANs and LANs, such as the following:

- Ethernet
- Token bus
- Token ring
- ATM (Asynchronous Transfer Mode)
- FDDI (Fiber Distributed Data Interface)

It also provides the following solutions via telephone for IP:

- PPP (Point to Point Protocol)
- SLIP (Serial Line Interface Protocol)

## Internet Layer

The Internet layer of the TCP/IP model ensures the connection between individual hosts in the network beyond the limits of individual networks in the Internet, as shown in Figure B-13.

![](img/9129877170834ca9d5fdac5319bf5f12_644_0.png)

Figure B-13

The main tasks of the Internet layer are providing an address space for the Internet, routing, and data transfer between end systems (host computers).

The following protocols are used by the Internet layer (with IP as the most popular):

- Address Resolution Protocol (ARP)
- Internet Protocol (IP)
- Internet Control Message Protocol (ICMP)

### Address Resolution Protocol (ARP)

ARP (Address Resolution Protocol) (RFC 826) resolves IP addresses to hardware addresses (MAC addresses, Media Access Control).

The MAC address is always composed of six bytes (in hexadecimal notation). The first three bytes indicate the manufacturer, and the last three bytes are the serial number of the network card.

If two network cards are present, both with the same serial number, you can specify (under Linux) which MAC address the network card should use to reply.

As illustrated in Figure B-14, a special MAC address (all bits to 1: ff:ff:ff:ff:ff:ff) is used for the ARP broadcast:

![](img/9129877170834ca9d5fdac5319bf5f12_645_0.png)

Figure B-14

The process is described below:

1. Host A issues a query to all computers through an ARP broadcast request via `ping C`: "Who is host C?"
2. Host C replies (ARP reply): "My hardware address is 00:50:34:B0:CF:07."
3. The communication is established.

Host A memorizes the reply to its query in a cache. You can view this cache with the `arp` (`/sbin/arp`) command. The command also provides options for editing the cache, such as deleting an invalid assignment of a MAC address to an IP address (`arp -d hostname`).

![](img/9129877170834ca9d5fdac5319bf5f12_645_1.png)

For details on the `arp` command, enter `man arp`.

You can use the `arpwatch` program (`/usr/sbin/arpwatch`) to monitor ARP requests and replies. By doing this, you can locate errors in the ARP traffic.

### Internet Protocol (IP)

IP provides the underlying services for transferring data between end systems in TCP/IP networks and is specified in RFC 791.

Data is transported through the network in packet form (also called *datagrams*). The main characteristics of this protocol are that it is connectionless and unreliable.

The fact that IP is a connectionless protocol means that no end-to-end connection of communication partners is set up for data transfer.

In addition, IP is an unreliable protocol because it has no mechanisms for error detection or error correction. In other words, IP cannot guarantee delivery of data. However, if data arrives at the destination host, the data is correct. This is guaranteed by the Network Access layer.

The following basic tasks are performed by IP:

- Specifies datagrams that form the basic units for transferring data on the Internet
- Defines the addressing scheme
- Routes, exchanges, and transfers datagrams through the network
- Fragments and assembles datagrams

Every packet or datagram transmitted over the TCP/IP network has an IP header. Figure B-15 shows how the header of an IP datagram is constructed.

![](img/9129877170834ca9d5fdac5319bf5f12_646_0.png)

Figure B-15

The IP header has the following elements:

- *Version (4 bits)*—Specifies the format of the IP packet header.
- *IHL (Internet Header Length, 4 bits)*—Specifies the length of the IP packet header.
- *TOS (Type of Services, 8 bits)*—Specifies the parameters for the type of service requested, such as priority, reliability, and monetary cost.
- *Total length (16 bits)*—Contains the length of the datagram.
- *Identification (16 bits)*—Identifies the fragments of the datagram.
- *Flags (3 bits)*—Include the following:
  - *R (Reserved, 1 bit)*—Is reserved for future use.
  - *DF (Don't Fragment, 1 bit)*—Controls the fragmentation of the datagram.
  - *MF (More Fragments, 1 bit)*—Indicates if the datagram contains additional fragments.
- *Fragment Offset (13 bits)*—Is used to direct the reassembly of a fragmented datagram.
- *TTL (Time To Live, 8 bits)*—Is used to track the lifetime of the datagram.
  When traversing a router, the TTL of a datagram is reduced by 1. If the TTL is 0, it will be discarded by a router.
- *Protocol (8 bits)*—Specifies the next encapsulated protocol (such as ICMP, TCP, or UDP).
- *Header Checksum (16 bits)*—Specifies the checksum of the IP header and IP options.
- *Source Address (32 bits)*—Specifies the IP address of the sender.
- *Destination Address (32 bits)*—Specifies the IP address of the intended receiver.
- *Options*—Is of variable length.
- *Padding (variable length)*—Is used as a filter to guarantee that the data starts at the 32-bit boundary.

The following are additional TCP/IP topics you should be familiar with:

- **Routing**—The main characteristic of IP is its connectionless data transfer (packet exchange) between two computers. This means that for each packet a new path through the network is sought.

  The advantage of this approach lies in its robustness. If a cable fails for any reason, packets can take a different route (if there is one).

  The task of packet routing is to find a path through the Internet from machine A to machine B. To do this, routing protocols and algorithms are used.
- **IP addresses**—In IP-based networks, each computer (or each network interface of a computer) has a unique, 32-bit IP address.

  For the sake of readability, these 32 bits are not shown as a sequence of 32 zeros and ones, but are divided into four bytes.

  These four bytes, called *octets*, are separated by dots (32-bit/4-byte dot notation, or dotted quad notation) and are recorded either as decimal or binary numbers.

  For example, 32 bits “in sequence” from the machine’s point of view looks like the following:

  `11000000 10000001 00110010 00000001`

  Readable IP representation in decimal format looks like the following:

  `192.129.50.1`

  An IP address consists of the *network prefix* (the front part of the IP address) and a *host number* (the end part of the IP address).

  The network prefix helps to determine the network class in which the host is located. By means of the IP address, data is delivered to the required host in the destination network.
