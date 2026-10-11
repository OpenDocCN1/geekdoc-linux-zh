The TCP protocol is used by upper-layer applications that require a high degree of data integrity, including

+   - Web servers
+   - E-mail servers
+   - FTP servers

However, the data fidelity offered by TCP comes at a cost, primarily in the form of latency. TCP requires a fair amount of network and processing overhead. Not all network applications actually require the high degree of data fidelity provided by TCP. Some upper-layer applications require less latency and can tolerate less reliability. These applications use the User Datagram Protocol (UDP) protocol instead of TCP. UDP functions in a manner similar to TCP; however, it is a *connectionless* protocol. With UDP, IP packets are sent unacknowledged. It is usually implemented with applications that send very small amounts of data at a time. It assumes that error checking and correction is either not necessary or will be performed by the application, avoiding the processing overhead.

In this respect, UDP is similar to sending someone a postcard through the mail. A postcard doesn't contain much data, and the receiver doesn't have to sign for it. Essentially, the sender assumes that the mail carrier is reasonably reliable and that the information on the postcard isn't important enough to require the receiver to sign for it. UDP works in much the same way. Some upper-layer applications that make use of UDP include

+   - Streaming audio and video
+   - VoIP

In addition to IP, TCP, and UDP, you also need to be familiar with the Internet Control Message Protocol (ICMP) protocol for your Linux*/LPIC-1 exam. ICMP is another core protocol in the IP protocol suite. It differs in purpose from TCP and UDP, which are transport protocols. The primary role of ICMP is to test and verify network communications between hosts.

For example, to test network connectivity, the ping utility will send ICMP Echo Request packets to a remote host. If the host receives them, it will respond with an ICMP Echo Response packet to the sender. If the ICMP Echo Response packet is received, the sender knows that a viable network connection exists between the sender and receiver and that the receiver is responding to network requests. If an ICMP Echo Response packet is not received, then the sender knows something is wrong and can begin troubleshooting communications.

For your Linux*/LPIC-1 exam, you also need to understand the concept of IP *ports*. Ports are provided by both the TCP and UDP protocols at the Transport layer. In essence, a port is a logical connection provided by TCP and UDP for upper-layer protocols. Ports allow a single host with a single IP address to provide multiple network services. Each service uses the same IP address but operates using a different TCP or UDP port number.

For example, suppose you have a network server with an IP address of 192.168.1.1 assigned to it. You could configure both a web server and an FTP server to run on it.