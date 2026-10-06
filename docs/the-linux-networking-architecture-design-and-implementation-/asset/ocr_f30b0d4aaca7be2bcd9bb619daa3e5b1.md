# # CHAPTER 24

# # Transmission Control Protocol (TCP)

The *Transmission Control Protocol (TCP)* offers a reliable, byte-oriented, connection-oriented transport service, in contrast to the unreliable datagram service used by the Internet Protocol (IP). Providing these abilities makes the TCP transport protocol very complex. A large number of protocol mechanisms are required to achieve the expected-service. This chapter introduces these protocol mechanisms and describes how they were implemented in the Linux kernel.

The TCP protocol belongs to the transport layer and can be used as an alternative to the *User Datagram Protocol (UDP)* which offers a connectionless transport service. (See Chapter 25.) The transport layer is immediately below the application layer. Consumers using the service of the protocol are applications. and they reach the services of the TCP protocol instance over the socket interface introduced in Chapters 26 and 27. To implement the transport service, the TCP layer uses the *Internet Protocol (IP)*. It provides an unreliable, connectionless datagram service, as described in Chapter 14.

# 24.1 OVERVIEW

The protocol units that exchange TCP instances in this way are called *segments*, and the protocol units of the IP protocol instances are called *IP packets* or datagrams.

# 24.1.1 Requirements to TCP

The TCP protocol was developed in the beginning of the eighties to run on top of the IP protocol and provide a byte-oriented, reliable, connection-oriented transport service. The requirements on such a protocol are as follows [Pete00]:

+   - to guarantee transmission of byte streams;
- to maintain the transmission order when delivering byte streams;