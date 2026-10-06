# 7.1. Introduction to Network I/O

Network traffic in Linux and every other operating system is abstracted as a series of hardware and software layers. The link, or layer contains network hardware such as Ethernet devices. When moving network traffic, this layer does not distinguish types of traffic but just transmits and receives data (frames) as fast as possible.

Stacked above the link is the network layer. This layer uses the Internet Protocol (IP) and Internet Control Message Protocol (ICMP) to address and route packets of data from machine to machine. IP/ICMP make their best-effort attempt to pass the packets between machines, but they make no guarantees about whether a packet arrives at its destination.

Stacked above the network layer is the transport layer, which defines the Transport Control Protocol (TCP) and User Datagram Protocol (UDP). TCP is a reliable protocol that guarantees that a message is delivered over the network or generates an error if the message is not delivered. TCP’s bubbling protocol, UDP, is an unreliable protocol that delivers deliberately (to achieve the highest rates) but no guarantee delivery. UDP and TCP define the concept of "service" to IP and UDP receive messages on numbered "ports". By convention, each type of network service is assigned a different number. For example, Hypertext Transfer Protocol (HTTP) is typically port 80, Secure Shell (SSH) is typically port 22, and File Transfer Protocol (FTP) is typically port 21. In a Linux system, the file `/etc/services` defines the ports and types of services they provide.

The final layer is the application layer. It includes all the applications that use the layers below to transmit packets over the network. These include Web servers, SSH clients, or peer-to-peer (P2P) file-sharing clients like bitorrent.

The lowest three layers (link, network, and transport) are implemented or controlled within the Linux kernel. The kernel provides statistics about how each layer is performing, including information about the bandwidth usage and error count as data flows through each of the layers. The tools covered in this chapter enable you to extract and verify statistics.

# 7.1.1. Network Traffic in the Link Layer

At the lowest levels of the network stack, Linux can detect the rate at which data traffic is flowing through the link layer. The link layer, layers above have pieces of information much larger than the frame size, the link layer breaks everything into frames to send them over the network. This maximum size of data in a frame is known as the maximum unit (MTU). You can use network configuration tools such as ip or ifconfig to set the MTU. For Ethernet, the maximum size is 1,500 bytes, although some hardware supports jumbo frames up to 9,000 bytes. The size of the MTU has a direct impact on the efficiency of the network. The frame in the link layer has a small header, so using a large MTU increases the ratio of data to overhead (header). When using a large MTU, each frame of data has a higher chance of being corrupted or dropped. For noisy links, a high MTU usually hurts performance because it requires less overhead; however, a smaller MTU may actually enhance performance because less data has to be re-sent when a single frame is corrupted.

At the physical layer, frames flow over the physical network; the Linux kernel collects a number of statistics about the types of frames:

+   * Transmitted/received—If the frame successfully flowed in or out of the machine, it is counted as a transmitted or received frame.

+   * Errors—Frames with errors (possibly because of a bad network cable or duplex mismatch)

+   * Dropped—Frames that were discarded (most likely because of low amounts of memory or buffers).