Ethernet is called a *frame* (the re-encapsulation of data at the next layer up is called a *datagram* in IP, and encapsulation at two levels up is called a *packet* for TCP.)

Keep in mind that Ethernet and IEEE 802.3 can run on the same physical connection, but there are indeed differences between the two encapsulation methods.

# Network Layer

Next we work up to the third layer, which is the network layer. This layer is synonymous with Internet Protocol (IP). Data at this layer is called a *datagram*. This is the layer that handles the routing of data around the network. Data that gets routed with IP sometimes encounters an error of some type, which is reported back to the source system with an Internet Control Message Protocol (ICMP) message.

Unfortunately, the information that IP uses does not conveniently fit inside an Ethernet frame, so you end up with fragmented data. This is really re-encapsulation of the data, so you end up with a lot of inefficiency as you work your way up the layers.

IP handles routing in a simple fashion. If data is sent to a destination connected directly to your system, then the data is sent directly to that system. If, on the other hand, the destination is not connected directly to your system, the data is sent to the default router. The default router, sometimes called a gateway, then has the responsibility to handle getting the data to its destination.

# Transport Layer

This layer can be viewed as one level up from the network layer, because it communicates with *ports*. TCP is the most common protocol found at this level, and it forms packets that are sent from port to port. These ports are used by network programs such as **telnet**, **rlogin**, **ftp**, and so on. You can see that these programs, associated with ports, are the highest level I have covered while analyzing the layer diagram.