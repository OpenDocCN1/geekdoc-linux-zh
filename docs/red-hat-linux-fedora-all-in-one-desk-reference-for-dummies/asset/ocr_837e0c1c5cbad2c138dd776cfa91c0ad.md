+   - **Physical layer:** Refers to the physical networking hardware (such as an Ethernet card or Token Ring card) that carries the data packets in a network.

The beauty of the layered model is that each layer only takes care of its specific task, leaving the rest to the other layers. The layers can mix and match — you can have a TCP/IP network over any type of physical network medium, from Ethernet to radio waves (in a wireless network). The software is modular as well because each layer can be implemented in different modules. For example, typically the Transport and Internet layers already exist as part of the operating system; any application can make use of these layers.

# TCP/IP and the Internet

TCP/IP has become the protocol of choice on the Internet — the "network of networks" that evolved from ARPAnet. The U.S. Government's Advanced Research Projects Agency (ARPA) initiated research in the 1970s on a new way of sending information, using packets of data sent over a network. The result was ARPAnet: a national network of linked computers. Subsequently, ARPA acquired a Defense prefix and became DARPA. Under the auspices of DARPA, the TCP/IP protocols emerged as a popular collection of protocols for internetworking — communication among networks.

TCP/IP has flourished because the protocol is open. That means the technical descriptions of the protocol appear in public documents, so anyone can implement TCP/IP on specific hardware and software.

TCP/IP also made great inroads because stable, working software was available. Instead of a paper description of network architecture and protocols, the TCP/IP protocols started out as working software — and who can argue with what's already working? These days (as a result), TCP/IP rules the Internet.

# IP addresses

When you have many computers on a network, you need a way to identify each one uniquely. In TCP/IP networking, the address of a computer is the IP address. Because TCP/IP deals with internetworking, the address is based on the concepts of a network address and a host address. You may think of the idea of a network address and a host address as having to provide two addresses to identify a computer uniquely:

+   - Network address indicates the network on which the computer is located.
+   - Host address indicates a specific computer on that network.