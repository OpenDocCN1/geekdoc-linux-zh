character devices. Streaming protocols can break up long sequences of bytes but they are sequenced, so they arrive in the order they were sent. Streaming protocols are also known as reliable protocols because they take great pains to ensure that network messages are delivered intact or they otherwise notify the sender that one or more errors occurred and the message should be resent.

Packet-based protocols, on the other hand, create artificially sized packages (packets) of data with a fixed size. These protocols do not break up packets to send them, and they only deliver complete packets.

With these terms in mind, it is fairly simple to classify most network protocols, including TCP/IP, the basis of the Internet, and local IPC (formerly known as UNIX domain sockets), into one of two categories. Datagram protocols, such as UDP (the User Datagram Protocol), are packet-based, connectionless, non-sequencing, and offer no error control. Stream protocols, conversely, are byte-oriented and offer both sequencing and error control. TCP, the Transmission Control Protocol, is a classic example of a stream protocol.

# ### The Berkeley Socket API

Given the huge variety of network protocols, the prospect of having to learn a new programming interface each time you want to learn or use a new protocol is surely daunting. Fortunately, the Berkeley socket API, usually called Berkeley sockets and so-named because it was popularized in the BSD versions of UNIX, was designed to encapsulate a variety of networking protocols and to provide a single programmatic interface for network programmers.

This generality introduces extra complexity, but the complexity is a small price to pay over not having to learn the low-level interfaces for AppleTalk, AX.25, IPX, NetRom, local IPC, and TCP/IP. This chapter uses Berkeley sockets to program both POSIX local IPC, which works only on a single machine, and TCP/IP, which enables computers across the Internet to communicate with each other.

The fundamental data structure of the socket API is the sockaddr structure, which stores a network address, the most essential feature of any network protocol. It is declared in <sys/socket.h> as follows:

```
```
struct sockaddr {
  unsigned short int sa_family;
  char sa_data[14];
};
```
```