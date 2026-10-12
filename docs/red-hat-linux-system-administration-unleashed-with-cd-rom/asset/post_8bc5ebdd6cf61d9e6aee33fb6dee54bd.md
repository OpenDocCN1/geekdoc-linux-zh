
The current popular implementation of TCP/IP (IPv4) allows for 32-bit source and destination addresses in IP datagrams. The destination address is used by routers and gateways to determine where the datagram should be sent.

One of the crucial features of IP is that it provides for fragmentation and reassembly of datagrams. Physical networks differ in how much data can be contained in a single frame; this amount is called the MTU, or Maximum Transmission Unit. For example, FDDI has an MTU of 4500 bytes, but for Ethernet it is only 1500 bytes. When a datagram is forwarded from a network with a large MTU to one with a smaller MTU, IP splits the datagram into several fragmented datagrams, each of which will fit into a single frame on the physical network. Then, the IP implementation on the receiving system reassembles the fragmented data into a single datagram, using control information inserted into the IP headers by the forwarding system. This ability to reliably fragment datagrams is a requirement for a network protocol that, like IP, can use any of a variety of different physical links.

The Internet Layer also includes ICMP, the Internet Control Message Protocol. ICMP uses the IP datagram delivery facility to send messages that function as meta-data for the network. Perhaps the most common use of ICMP is the Echo Request/Echo Reply facility, usually accessed by the ping program, which essentially checks whether a given system is up and connected to the network. Other ICMP message types are Source Quench (a simple form of flow control), Destination Unreachable, and Redirect.

## Transport Layer

The Transport Layer (or more properly the Host-to-Host Transport Layer) provides application-usable communication protocols. For TCP/IP, these protocols are UDP (the User Datagram Protocol) and TCP (the Transmission Control Protocol).

UDP provides applications with a connectionless, unreliable datagram-oriented protocol that has a minimum of overhead. UDP also extends the 32-bit source/destination addresses used by IP with 16-bit source and destination port numbers. The use of port numbers allows a system to have many UDP-based applications running on it, and still ensures that each application sees only the data intended for it.

TCP is a reliable, connection-oriented protocol that provides a straightforward byte-stream model to applications. Reliability of TCP communications is ensured by requiring the receiving system to acknowledge successful receipt of data; if the sending system doesn’t get the acknowledgement, it retransmits the data. TCP communications employ a logical connection between a pair of systems: The application is presented with the illusion of a physical circuit existing between the two communication endpoints. This logical connection is established and maintained by an initial three-way handshake (so-called because the handshake needs three TCP segments to set up) and by sequence numbers attached to each byte of the stream in each direction. Like UDP, TCP provides a 16-bit port number for source and destination. As you might imagine, the error checking involved in tracking the connection sequence for TCP imposes an additional overhead compared to UDP. However, for many applications, a reliable data stream is a requirement, so this overhead is unavoidable.

## Application Layer

The Application Layer includes the protocols normally thought of as network services. These protocols are built on top of TCP streams or UDP messages. For example, HTTP, the Hypertext Transfer Protocol which underpins the World Wide Web, is a stream-oriented protocol normally sent over TCP, and NTP, the Network Time Protocol, is a message-oriented protocol sent over UDP. Such protocols normally also specify a default port number on the server to which clients should connect. For example, HTTP defaults to TCP port 80, and NTP uses UDP port 123. Application-level services are described in more detail elsewhere in the book.

Up to this point, we have been discussing "addresses" of communication endpoints, but we have not yet mentioned the form these addresses take. Because their precise nature will be important later, the following sections describe them in detail.

## IP Addresses

IPv4, the current IP standard, uses a 32-bit numerical address for each Internet host. (The next-generation standard, IPv6, uses 128-bit addresses.) These addresses are customarily written as a dotted quad—a series of four numbers in the range 0 to 255, separated by periods. IP addresses also encode some structured information: They are divided into a network part and a host part. These parts vary in length, and the length of the network part is determined by an address class or by a subnet mask.

## Address Classes

Address classes are divisions of the IP address space into a small number of fixed-length structures. They have to some extent been obsoleted by the more general mechanism of variable-length subnet masks, but the terminology is still widely used. The three main address classes (class A, class B, and class C) are distinguished by which of several ranges the first octet in the dotted quad falls into, as shown in Table 14.2.

TABLE 14.2 Address Classes in IPv4

| Class | Range | Comments |
|-------|-------|----------|
| A | 0 to 127 | <128 networks, >16 million hosts |
| B | 128 to 191 | >16000 networks, >65000 hosts |
| C | 192 to 223 | >2 million networks, 254 hosts |
| D | 224 to 239 | Multicast addresses |
| E | 240 to 255 | Reserved, unassigned addresses |

Address classes D and E are rather different from the others: Class D is used for multicast (addressing multiple hosts in a single datagram) and class E is reserved for experimental use and has no assigned addresses.

Each address class provides one or more private networks, which are available for local use without needing to go through the official registration procedure. In class A, the network 10.0.0.0 is available; in class B it is all networks from 172.16.0.0 to 172.31.255.255; and in class C, the networks from 192.168.0.0 to 192.168.255.255 are available.

Two important class A networks are not allocated in the usual way. The network 127.0.0.0 is the loopback network, which allows the local host to be addressed in the same manner as remote hosts; this substantially simplifies some networking applications. The network 0.0.0.0 is not used as a network number; instead, it identifies the default route in routing tables (see the section “Routing” later in the chapter).

This scheme of address classes is not without problems. The most significant problem is that these fixed-length classes are very inflexible. Each is too large for many purposes; thus, a large part of the address space gets wasted in organizations that are unable to use all of their addresses but that have too large a network to use an address class with fewer host addresses. In some cases, an organization could use multiple smaller networks, but this would increase load on routers.

## Classless IP Addresses

By the early 1990s, it had become clear that the fixed-size structures imposed by address classes were scaling poorly to a larger Internet—and indeed, there seemed to be a genuine possibility that the class B address space would soon be exhausted. The interim solution developed is called CIDR (pronounced cider), or Classless Inter-Domain Routing. It is considered an interim solution because in the long term, networks are expected to switch to IPv6.

The central idea of CIDR is to use variable-length network masks to distinguish the network part and host part of an IP address, rather than encoding the length of the mask in the address itself. The bit pattern of the network mask is treated as a template for interpretation of the IP address: For each bit that is set in the network mask, the corresponding bit in the IP address is treated as the network part rather than the host part. The network mask is divided into two contiguous parts: a prefix of all-bits-one and a suffix of all-bits-zero.

Network masks in isolation are usually written as dotted quads, just like IP addresses. For example, a network mask allowing eight bits for the host part would be 255.255.255.0. There is also a convenient abbreviated syntax for writing an IP address and its network mask together: The IP address is followed by a slash (/) and the number of one bits in the network mask. For example, a network mask of 255.255.0.0 could be applied to the network address 192.168.0.0; it could then be written as 192.168.0.0/16, and an individual host in that network might be 192.168.17.42/16. This process (of aggregating small networks into a network larger than the natural mask of the address class structure would indicate) is called supernetting.

## Subnetting

Just as supernetting involves using in the host part of the address some bits that the natural mask would assign to the network part, so subnetting involves using bits from the host part within the network part. This increases the number of networks that can be addressed, at the cost of allowing fewer hosts within each network. Suppose we have the network address 172.16.0.0, whose natural mask is 255.255.0.0. Using a subnet mask of 255.255.240.0 gives us the network 172.16.0.0/20, in which there are 16 subnets that each contain more than four thousand host addresses.

We have now discussed the essentials of TCP/IP networking, though without reference to specific hardware or software implementations. The next section describes Ethernet, a very widely used standard for physical network connections.

## Running TCP/IP over Ethernet

IP addresses actually denote network interfaces rather than hosts on the network; this enables a single system to be present on more than one physical network and to forward packets between them.
