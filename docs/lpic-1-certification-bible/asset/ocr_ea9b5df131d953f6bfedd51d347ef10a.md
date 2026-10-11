+   - 192.168.1.128/28
+   - 192.168.1.144/28
+   - 192.168.1.160/28
+   - 192.168.1.176/28
+     - 192.168.1.192/28
+       - 192.168.1.208/28
+       - 192.168.1.224/28

This allows for 14 network segments that each support up to 14 network interfaces. These interfaces must include all routers, print devices, and network adapters on the segment. Some machines may contain more than one network adapter, and each must have a unique host ID. By carefully examining the needs of your network and the potential growth, it is possible to determine the correct subnetting scheme that will work for you now and in the future.

# Protocols

TCP/IP is actually a suite of protocols including the TCP and IP. There are many different protocols in this suite that are used for specific network communication needs. The primary protocols used in the TCP/IP suite are IP (Internet Protocol), ARP (Address Resolution Protocol), ICMP (Internet Control Message Protocol), TCP (Transmission Control Protocol), and UDP (User Datagram Protocol). These protocols work together transmitting message units across the network. The TCP/IP suite of protocols is scalable, allowing them to function well whether on a small, home network or on the Internet.

All of these protocols work together to provide transmission of data across the network. They each manage data differently and when combined provide end-to-end data delivery for all situations.

# Internet Protocol

The *Internet Protocol* (IP) handles the delivery of datagrams across the network; this includes the packet fragmentation and routing. IP is an unreliable protocol because it does not establish a direct connection between the sending and receiving hosts. Instead the packets are sent on the assumption that they will reach the intended recipient. This procedure can result in datagrams being received out of order, duplicated, delayed, and even lost. Other protocols are used to ensure reliable delivery of data, so IP doesn’t duplicate the work of these protocols. IP is responsible for delivering datagrams to hosts. When the host is located on a remote network, IP makes use of routers to get the datagram to the receiving network and host. IP uses *IP headers* to label the datagram with information about the data contained in the datagram. These headers also contain information about the sender, recipient, and protocol for which the datagram is intended. This allows the datagram to be transmitted to the correct recipient and allows for the correct protocol to handle the datagram once it has been delivered.