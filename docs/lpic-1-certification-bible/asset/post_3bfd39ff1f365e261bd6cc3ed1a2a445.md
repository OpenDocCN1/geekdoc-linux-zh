
- 192.168.1.128/28
- 192.168.1.144/28
- 192.168.1.160/28
- 192.168.1.176/28
- 192.168.1.192/28
  - 192.168.1.208/28
  - 192.168.1.224/28

This allows for 14 network segments that each support up to 14 network interfaces. These interfaces must include all routers, print devices, and network adapters on the segment. Some machines may contain more than one network adapter, and each must have a unique host ID. By carefully examining the needs of your network and the potential growth, it is possible to determine the correct subnetting scheme that will work for you now and in the future.

# Protocols

TCP/IP is actually a suite of protocols including the TCP and IP. There are many different protocols in this suite that are used for specific network communication needs. The primary protocols used in the TCP/IP suite are IP (Internet Protocol), ARP (Address Resolution Protocol), ICMP (Internet Control Message Protocol), TCP (Transmission Control Protocol), and UDP (User Datagram Protocol). These protocols work together transmitting message units across the network. The TCP/IP suite of protocols is scalable, allowing them to function well whether on a small, home network or on the Internet.

All of these protocols work together to provide transmission of data across the network. They each manage data differently and when combined provide end-to-end data delivery for all situations.

# Internet Protocol

The *Internet Protocol* (IP) handles the delivery of datagrams across the network; this includes the packet fragmentation and routing. IP is an unreliable protocol because it does not establish a direct connection between the sending and receiving hosts. Instead the packets are sent on the assumption that they will reach the intended recipient. This procedure can result in datagrams being received out of order, duplicated, delayed, and even lost. Other protocols are used to ensure reliable delivery of data, so IP doesn’t duplicate the work of these protocols. IP is responsible for delivering datagrams to hosts. When the host is located on a remote network, IP makes use of routers to get the datagram to the receiving network and host. IP uses *IP headers* to label the datagram with information about the data contained in the datagram. These headers also contain information about the sender, recipient, and protocol for which the datagram is intended. This allows the datagram to be transmitted to the correct recipient and allows for the correct protocol to handle the datagram once it has been delivered.

TCP/IP addresses are easy-to-remember addresses assigned by the user or systems administrator to a system. They provide unique identifiers for each network interface. Each network interface also has a physical hardware address that has been assigned by the manufacturer. This address is unique to all other network interfaces that exist. However, these addresses are very long and difficult to remember, and they aren’t *routable*, meaning that the sending interface can locate the receiving interface only if they’re on the same subnet. If there’s a router in between the sender and the receiver, the transmission will be lost. So, when TCP/IP addresses are assigned to a network interface, the system allows that TCP/IP address to represent the underlying physical address because TCP/IP is a routed protocol. This makes it easy for users and applications to communicate using the TCP/IP address. However, during the physical transmission of data across the network media, this TCP/IP address must be resolved to a matching hardware address. This is where ARP (Address Resolution Protocol) comes in. ARP uses broadcasts on the local network to find the matching physical address for each TCP/IP address that is sending or receiving data. An ARP cache is maintained on each system for a period of time, which allows for a reduction in the number of broadcasts that must occur on the network.

![](img/96d9ccd181675a8ae8b6a1146c919d2b_602_0.png)

The unique address assigned to a network card, known as a *MAC address* for media access control, can be changed via software on many adapters.

For example, suppose the router connecting your network to the Internet is sending requests to the Apache Web server located on your network. The ARP cache on the router is first checked to see whether the cache contains a matching hardware address for the TCP/IP address of the server. If no matching entry is found, the router will then send an ARP request as a Network broadcast message. This request includes the IP and hardware address of the router, along with the IP address of the server. This message is examined and then ignored by all other network interfaces on the network segment except for the Web server. The server with the matching IP address updates its local ARP cache with the information for the router. Then the server sends an ARP reply to the router. The router then updates its ARP cache with the IP address and hardware address of the server.

To prevent excessive network traffic, broadcast messages are not routed between network segments. This means that ARP cannot provide matching of IP address and hardware addresses to systems beyond the local subnet. However, this isn’t necessary. If the machine is not located on the local subnet, the data is sent to the router on the local subnet. Therefore, ARP is used to discover the mapping of the IP address to the hardware address of the router.

# Internet Control Message Protocol

The Internet Control Message Protocol (ICMP) can be used to report errors in delivery of datagrams. It does not provide reliability to IP but instead can report on some errors that are a result of a failure in an IP action. ICMP messages include the following:
- echo request
- echo reply
- redirect
- source quench
- destination unreachable

Source quench is used when a sender is transmitting data faster than the receiver can handle. A source quench signals the sender to slow the transmission rate to the receiver.

This protocol can be useful for troubleshooting TCP/IP connection problems. The utilities ping and traceroute use this protocol. Use of these utilities is discussed later in this chapter.

# Transmission Control Protocol

The Transmission Control Protocol (TCP) provides reliability that is missing in the Internet Protocol. TCP provides flow control and package sequencing to ensure reliable transfer of data. When a TCP transmission occurs, a session between the communicating hosts is established. This session allows for error recovery and flow control as an acknowledgement from the receiving system is required for each segment transmitted. Segments are numbered before they are sent, so any missing segment can be detected and resent. When the transmission of data has completed and all acknowledgements are received, the session is closed.

This process provides for reliable transmission of data, but has a cost. An overhead is associated with TCP, caused by establishing the session, sending the acknowledgements, and numbering the segments. However, for important transmissions across the network, the reliability provided by TCP can be essential.

# User Datagram Protocol

User Datagram Protocol (UDP) also provides datagram delivery. However, unlike TCP, this protocol provides unreliable transmissions. UDP does not perform error checking; applications that use UDP often use other methods of error checking to ensure the integrity of the data. UDP uses connectionless delivery, with no direct connection between communicating systems, to provide fast transmission of small messages, without the overhead associated with connection-oriented delivery methods. Because broadcast messages are not sent to a specific host, they must use the connectionless delivery provided by UDP.

# Ports

TCP and UDP use ports, similar to apartment mailboxes that receive packets for a specific application, for network communications. This strategy allows many simultaneous UDP and TCP transmissions to occur as each transmission is directed to a specific port. These port numbers are predefined by networking standards and
