
## CHAPTER 25
## User Datagram Protocol (UDP)

### 25.1 INTRODUCTION

The User Datagram Protocol (UDP) is described in RFC 768 [Post80] and represents a minimal transport protocol. It runs on top of the Internet Protocol (IP) and essentially offers the same functionality as IP itself: an unreliable, connectionless datagram service. In this case, unreliable means that there are no mechanisms to detect and handle or duplicate packets. However, packets can be optionally protected against bit errors by a checksum, which covers both the packet header and the payload of each packet, in contrast to IP. Otherwise, there is only one additional option, compared to IP: Port numbers can be used to address different applications in a specific end system.

On the one hand, UDP is used for transaction-oriented applications, such as the Domain Name System (DNS), where only one request and the relevant reply have to be transmitted, so is not worth establishing a connection context; for example in TCP, that three additional messages for the establishment and four messages for the tear-down were required. On the other hand, UDP is also used where reliability of a transmission plays a secondary role, because one is primarily interested in transmitting data easily and quickly. For example, it is normally not a problem if some packets are lost when audio streams are transmitted in small packets. On the contrary, an automatic flow and error control with retransmission of lost packets would be disturbing to the smooth playback of the stream.

### 25.1.1 Packet Format

Figure 25–1 shows the format of UDP packets. The header fields are briefly described below.

| 0 | 15 16 | 31 |
|---|---|---|
| Source port | Destination port |
| Length | Checksum |
| Payload | | |
| 0 | 78 | 15 16 | 31 |
| Source address | | |
| Destination address | | |
| 0 | Protocol | UDP length |

FIGURE 25–1 UDP packet format.

FIGURE 25–2 Pseudo header format for checksum calculation.

- Source port: the source port is the port number used by the sending process, in the range from 1 to 65535; normally, the receiver of a request sent over UDP direct its reply to this port. RFC 768 specifies that giving the source port number is optional, and the field can have the zero value, if it is not used. However, for UDP over the socket programming interface in Linux (see Chapters 26 and 27), this is not possible, because a port number from zero is automatically assigned to each socket, if the user does not state one.
- *Destination port:* The destination port is used to address the application in the destination system that is to receive a UDP packet.
- *Length:* The length is specified in octets and refers to the entire UDP packet, consisting of packet header and payload. The smallest possible length is eight octets, and the largest possible UDP packet can transport 65535-8=65527 payoctets.
- *Checksum:* As in TCP, the calculation of the checksum includes a pseudo header in addition to the packet header and payload. The format of this pseudo header is shown in Figure 25–2. It includes the IP source and destination addresses, the UDP protocol identifier (17), and the length of the UDP packet. The checksum is computed as a 16-bit one complement of the one-complement sum over the data mentioned above, where a zero is appended if the octet number is uneven. This method can be implemented efficiently for all processor types (as described in RFCs 1071, 1141, and 1624 [BrBP88,MaKu90,Rijs94]). If the computation results in the checksum zero, the all-1-bit value is transmitted instead, which is equivalent in one-complement arithmetic. A zero in the checksum field means that the sender has not computed a checksum.

## DATA STRUCTURES

The implementation of UDP in the Linux kernel does not require any additional or particularly complex data structures. This section describes the data structure used to pass payload at the socket interface, the UDP datagram interface, which is included in the general socket buffer structure, and the data structures used to pass payload.

### 25.2 Passing the Payload

The payload is passed at the socket interface via the `msghdr` structure, which is included in the general socket buffer structure, and are the data structures used to pass payload.

```c
struct msghdr {
    void *name;
    int namelen;
    struct iovec *iov;
    size_t iovlen;
    void *control;
    size_t croll;
    int flags;
};
```

The `msghdr` structure is used with the `sendmsg()` and `recvmsg()` system calls. The `name` field points to a `sockaddr` structure (see Section 27.1), which contains the address and port. The `iov` field points to an array of `iovec` structures, which describe the payload. The `control` field can be used for protocol-specific messages.

The following flags are only some examples: we will not describe all flags:

- MSG_ROUTE specifies that the destination must be in the local network and, for this reason, the datagram should not be sent.
- MSG_DONTWAIT prevents the system call from blocking if, for example, there are no data to be received.
- MSG_ERR means that no packet should be fetched, but instead an error message, which might be available.
- MSG_TRUNC indicates that the buffer space provided for receiving was insufficient, so some of the packet data were lost.

### 25.2.2 The UDP Datagram

The union element `h` of the `sk_buff` structure includes a pointer, `struct udphdr` which refers to the UDP header within the packet. The `udphdr` structure is declared as follows, based on the packet format shown in 25–1:

```c
struct udphdr {
    __u16 source;
    __u16 dest;
    __u16 len;
    __u16 check;
};
```

When sending a packet and computing the checksum, as required, the data structure used is somewhat more complex. In addition to a `udphdr` structure, where the packet header is built, from which it is copied into the packet later, it also includes the other data required to create the pseudo IP header:

```c
struct udpfakeheader {
    struct udphdr uh;
};
```

### 25.2.3 Integration of UDP into the Network Architecture

As a transport protocol, UDP has two interfaces: one “downwards” to the network layer (the Internet Protocol) and one “upwards” to the application layer. The latter is formed by the sockets created in Chapter 26—more specifically, by the sockets of the PF_INET protocol family. (See Section 26.3.1.).
