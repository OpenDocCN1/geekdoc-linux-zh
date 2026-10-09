
TCP is connection oriented and establishes a virtual circuit between two systems, this protocol is not suitable for one-to-many transmissions (see the discussion of UDP, following). TCP has builtin mechanisms for dealing with congestion (or flow) control over busy networks and throttles back (slows the speed of data flow) when it has to retransmit dropped packets. TCP can also deal with acknowledgments, wide area links, high-delay links, and other situations.

### UDP: User Datagram Protocol

UDP runs at layer 4 of the IP stack, just as TCP does, but is much simpler. Like TCP, UDP works with multiple ports and multiple applications. It has checksums for error detection but does not automatically retransmit datagrams (page 1144) that fail the checksum test. UDP is a datagram-oriented protocol: Each datagram must carry its own address and port information. Each router along the way examines each datagram to determine the destination, one hop at a time. You can broadcast or multicast UDP datagrams to many destinations at the same time by using special addresses.

### PPP: Point-to-Point Protocol

PPP provides serial line point-to-point connections that support IP. This protocol compresses data to make the most of the limited bandwidth available on serial connections. PPP, which replaces SLIP (Serial Line IP), acts as a point-to-point layer 2/3 transport that many other types of protocols can ride on. It is used mostly for IP-based services and connections, such as TCP or UDP.

### XREMOTE AND LBX

Two protocols that speed up data transfer over serial lines are Xremote and LBX. Xremote compresses the X Window System protocol so that it is more efficient over slower serial lines. LBX (low-bandwidth X) is based on the Xremote technology and is part of X Window System release X11R6 and higher.

### Host Address

Each computer interface has a unique identifier called a MAC address (page 1158). A system attached to more than one network has multiple interfaces—one for each network, each with its own MAC address.

Each packet of information that is broadcast over the network has a destination address. All hosts on the network must process each broadcast packet to see whether it is addressed to that host. If the packet is addressed to a given host, that host continues to process it. If not, the host ignores the packet.

- 5. SLIP was one of the first serial line implementations of IP and has slightly less overhead than PPP. PPP supports multiple protocols (such as AppleTalk and IPX), whereas SLIP supports only IP.
- 6. Contrast broadcast packets with unicast packets: Ethernet hardware on a computer filters out unicast packets that are not addressed to that machine; the operating system on that machine never sees these packets.

The network address of a machine is an IP address, which, under IPv4, is represented as one number broken into four segments separated by periods (for example, 192.168.184.5). Domain names and IP addresses are assigned through a highly distributed system coordinated by ICANN (Internet Corporation for Assigned Names and Numbers—www.icann.org) via many registrars (see www.internic.net). ICANN is funded by the various domain name registries and registrars and by IP address registries, which supply globally unique identifiers for hosts and services on the Internet. Although you may not deal with any of these agencies directly, your Internet service provider most assuredly does.

How a company uses IP addresses is determined by the system or network administrator. For example, the leftmost two sets of numbers in an IP address might represent a large network (campuswide or companywide); the third set, a subnetwork (perhaps a department or a single floor in a building); and the rightmost number, an individual computer. The operating system uses the address in a different, lower-level form, converting it to its binary equivalent, a series of 1s and 0s. See the following optional section for more information. Refer to “Private address space” on page 642 for information about addresses you can use on a LAN without registering them.

### STATIC VERSUS DYNAMIC IP ADDRESSES

A static IP address is one that always remains the same. A dynamic IP address is one that can change each time you connect to the network. A dynamic address remains the same during a single login session. Any server (mail, Web, and so on) must have a static address so clients can find the machine that is acting as the server. End-user systems usually work well with dynamic addresses. During a given login session, they can function as a client (your Web browser, for example) because they maintain a constant IP address. When you log out and log in again, it does not matter that you have a different IP address because your computer, acting as a client, establishes a new connection with a server. The advantage of dynamic addressing is that it allows inactive addresses to be reused, reducing the total number of IP addresses needed.

### IP CLASSES

To facilitate routing on the Internet, IP addresses are divided into *classes*. These classes, which are labeled class A through class E, allow the Internet address space to be broken into blocks of small, medium, and large networks that are designed to be assigned based on the number of hosts within a network.

When you need to send a message to an address outside the local network, your system looks up the address block/class in its routing table and sends the message to the next router on the way to the final destination. Every router along the way does a similar lookup and forwards the message accordingly. At the destination, local routers direct the message to the specific address. Without classes and blocks, your host would have to know every network and subnetwork address on the Internet before it could send a message. This setup would be impractical because of the huge number of addresses on the Internet.

Each of the four numbers in the IP address is in the range 0–255 because each segment of the IP address is represented by 8 bits (an **octet**), with each bit being capable of taking on two values; the total number of values is therefore 2⁸ = 256. When you start counting at 0, the range 1–256 becomes 0–255.⁷ Each IP address is divided into a net address (*netid*) portion, which is part of the class, and a host address (*hostid*) portion. See Table 10-2.

**Table 10-2 IP classes**

| Class | Start bits | Address range | Structure |
| :--- | :--- | :--- | :--- |
| Class A | 0 | 0.0.0.0–126.255.255.255 | 0-netid | | | ======hostid======= |
| Class B | 10 | 128.0.0.0–191.255.255.255 | 10------netid------- | | -----hostid----- | |
| Class C | 110 | 192.0.0.0–223.255.255.255 | 110----------netid--------- | | =hostid= | |
| Class D (multicast) | 1110 | 224.0.0.0–239.255.255.255 | 1110 | | | |
| Class E (reserved) | 11110 | 240.0.0.0–255.255.255.255 | 11110 | | | |

The first set of addresses, defining class A networks, is reserved for extremely large corporations, such as General Electric (3.0.0.0) and Hewlett-Packard (15.0.0.0), and for ISPs. One start bit (0) in the first position designates a class A network, 7 bits holds the network portion of the address (*netid*), and 24 bits holds the host portion of the address (*hostid*; see Table 10-2). This setup means that GE can have 2²⁴, or approximately 16 million, hosts on its network. Unused address space and *subnets* (page 1174) lower this number quite a bit. The 127.0.0.0 subnet (page 387) is reserved, as are several others (see *private address space* on page 1166).

Two start bits (10) in the first two positions designates a class B network, 14 bits holds the network portion of the address (*netid*), and 16 bits holds the host portion of the address, for a potential total of 65,53⁴ hosts.⁸ A class C network uses 3 start bits (110) in the first three positions designates a class C network, 21 bits holds the network portion of the address (*netid*), and 8 bits holds the host portion of the address (*hostid*; see Table 10-2). This setup means that a class C network can have 2⁸ = 256 hosts.⁹ A class D network is reserved for multicasting (1110 in the first four positions designates a class D network, 11 bits holds the network portion of the address (*netid*), and 12 bits holds the host portion of the address (*hostid*; see Table 10-2). This setup means that a class D network can have 2¹² hosts.¹⁰ A class E network is reserved for future use (11110 in the first five positions designates a class E network, 13 bits holds the network portion of the address (*netid*), and 11 bits holds the host portion of the address (*hostid*; see Table 10-2). This setup means that a class E network can have 2¹¹ hosts.¹¹ A class A network uses 1 start bit (0) in the first position designates a class A network, 7 bits holds the network portion of the address (*netid*), and 24 bits holds the host portion of the address (*hostid*; see Table 10-2). This setup means that GE can have 2²⁴, or approximately 16 million, hosts on its network. Unused address space and *subnets* (page 1174) lower this number quite a bit. The 127.0.0.0 subnet (page 387) is reserved, as are several others (see *private address space* on page 1166).

- 7. Internally, the IP address is represented as a set of four unsigned 8-bit fields or a 32-bit unsigned number, depending on how programs are using it. The most common format in C is to represent it as a union of an unsigned 32-bit long integer, four unsigned shorts, and two unsigned short integers.
- 8. A 16-bit (class B) address can address 2¹⁶ = 65,53⁶ hosts, yet the potential number of hosts is two fewer than that because the first and last addresses on any network are reserved. In a similar manner, an 8-bit (class C) address can address only 25⁴ hosts (2⁸ – 2 = 25⁴). The 0 host address (for example, 194.16.100.0) for a class C network or 131.204.0.0 for a class B network is reserved as a designator for the network itself. Several older operating systems use this as a broadcast address. The 25⁵ host address (for example, 194.16.100.255 for a class C network or 131.204.255.255 for a class B network) is reserved as the IP broadcast address. An IP packet (datagram) that is sent to this address is broadcast to all hosts on the network.
- The netid portion of a subnet does not have the same limitations. Often you are given the choice of reserving the first and last networks in a range as you would a host, but this is rarely done in practice. More often the first and last networks in the netid range provide more usable address space. Refer to “Subnets” on page 385.
