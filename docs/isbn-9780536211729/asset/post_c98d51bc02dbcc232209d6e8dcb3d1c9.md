
## 4.2 The ICMP

Holding a special place, some say, within the IP layer is ICMP. You're probably familiar with ICMP when you use the `ping` command because `ping` uses ICMP. ICMP, or Internet Control Message Protocol, has several uses, including being the underlying protocol for the `ping` command. There are 15 functions within ICMP, each denoted by a type code. For instance, the type for ICMP Echo Request (think: ping) is 8; the reply to that request, aptly an Echo Reply, is type 0. Within the different types, there also exist codes to specify the condition for the given type. The types and codes for ICMP messages are shown in Table 4.3.

### Table 4.3 ICMP Message Types and Codes

| Type | Code | Description |
| :--- | :--- | :--- |
| 0 | 0 | Echo Reply |
| 3 | 0 | Destination Unreachable |
| | 1 | Host Unreachable |
| | 2 | Protocol Unreachable |
| | 3 | Port Unreachable |
| | 4 | Fragmentation Needed and DF Set |
| | 5 | Source Route Failed |
| | 6 | Destination Network Unknown |
| | 7 | Destination Host Unknown |
| | 8 | Source Host Isolated |
| | 9 | Destination Network Administratively Prohibited |
| | 10 | Destination Host Administratively Prohibited |
| | 11 | Network Unreachable for Type of Service |
| | 12 | Host Unreachable for Type of Service |
| | 13 | Communication Administratively Prohibited |
| | 14 | Host Precedence Violation |
| | 15 | Precedence Cutoff in Effect |
| 4 | | Source Quench |
| 5 | | Redirect |
| | 0 | Network Redirect |
| | 1 | Host Redirect |
| | 2 | Type of Service and Network Redirect |
| | 3 | Type of Service and Host Redirect |
| 8 | 0 | Echo Request |
| 9 | 0 | Router Advertisement |
| 10 | 0 | Router Solicitation |
| 11 | 0 | Time Exceeded TTL (Time to Live) Exceeded in Transit |
| | 1 | Fragment Reassembly Time Exceeded |
| 12 | 0 | Parameter Problem |
| 13 | 0 | Timestamp Request |
| 14 | 0 | Timestamp Reply |
| 15 | 0 | Information Request |
| 16 | 0 | Information Reply |
| 17 | 0 | Address Mask Request |
| 18 | 0 | Address Mask Reply |

The type and the code of an ICMP message are contained in the ICMP header, shown in Figure 4.3.

## 4.3 Transport Mechanisms

Internet Protocol defines a Network layer protocol of the OSI model. There are other Network layer protocols, but we will be concentrating solely on IP because it is by far the most popular Network layer protocol in use today. Above the Network layer on the OSI model is the Transport layer. As you might expect, the Transport layer has its own set of protocols. Two of the Transport layer protocols are of interest: UDP and TCP. This section examines each of these protocols.

### 4.3.1 UDP

UDP, or User Datagram Protocol, is a connectionless protocol used for such services as DNS queries, SNMP, and RADIUS. Being connectionless, UDP is akin to a “fire and forget” type of protocol. The client sends a UDP packet, sometimes referred to as a datagram, and assumes that the server will receive the packet. It is up to a higher layer protocol to assemble the packets in order. The UDP header, shown in Figure 4.4, is 8 bytes in length.

| Source Port | Destination Port |
| :--- | :--- |
| UDP Packet Length | Checksum |

**Figure 4.4** The UDP header.

The UDP packet length is the length of the entire packet, including data. Obviously, because the header itself is 8 bytes in length, the minimum value for this portion of the header is 8. The final portion of the UDP header is the checksum, which includes both the header and the data.

### 4.3.2 TCP

TCP, an abbreviation for Transmission Control Protocol, is a connection-oriented protocol that is frequently used with IP. Referring to TCP as connection-oriented means that it provides reliable service to the layers above it. Recall the telephone conversation analogy given earlier in this chapter. As in that analogy, two applications wanting to communicate using TCP must also establish a connection (sometimes referred to as a session). The TCP header is shown in Figure 4.5.

| Source Port | Destination Port |
| :--- | :--- |
| | Sequence Number |
| | Data Offset | Unused | Flags | Window |
| | Checksum | Urgent Pointer |

**Figure 4.5** The TCP header.

As you can see from Figure 4.5, the 20-byte TCP header is significantly more complicated than the other protocol headers shown in this chapter. Unlike the UDP header, which begins with both the source and destination ports, the combination of the source and destination ports along with the IP addresses of the sender and receiver identifies the TCP connection. The TCP header has a 32-bit sequence number and a 32-bit acknowledgment number. Remember that TCP is a connection-oriented protocol and provides reliable service. The sequence and acknowledgment numbers are the primary (but not the only) mechanism used to provide reliability. As data is passed down to the Transport layer, TCP divides the data into what it believes to be the most appropriate size. These pieces are known as TCP segments. TCP sends data down the protocol stack; it creates a sequence number that indicates the first byte of data for the given segment. On the opposite end of the communication, the receiver sends an acknowledgment indicating that the segment has been received. The sender keeps a timer running, and if an acknowledgment is not received in a timely fashion, the segment will be resent.

Another mechanism for reliability is that TCP provides a checksum on the header and the data. If the checksum set within the header by the sender does not match the checksum as computed by the receiver, the receiver will not send an acknowledgment. If an acknowledgment gets lost in transit, the sender will likely send another segment with the same sequence number. In such an event, the receiver will simply discard the repeated segment.

A four-bit field is used for header length, including any options provided as part of the header. There are six individual flags within the TCP header: URG, ACK, PSH, RST, SYN, and FIN. A description of these flags is contained in Table 4.4.

### Table 4.4 TCP Header Flags

| Flag | Description |
| :--- | :--- |
| URG | Indicates that the urgent pointer portion of the header should be examined. |
| ACK | Indicates that the acknowledgment number should be examined. |
| PSH | Indicates that the receiver should handle this data up to the next layer as soon as possible. |
| RST | Indicates that the connection should be reset. |
| SYN | Initiates a connection. |
| FIN | Indicates that the sender (could be either side of the connection) is finished sending data. |

The 16-bit Window field is used to provide a sliding window mechanism. The receiver sets the window number to indicate the size that the receiver is ready to receive, beginning with the acknowledgment number. This is a form of flow control for TCP.

The 16-bit urgent pointer indicates the offset from the sequence number where urgent data is that should be handled in an urgent manner and can be in conjunction with the PSH flag as well.

Now that you have a feeling for the TCP header, it's time to examine how TCP connections are established and ended.

### TCP Connections

Whereas UDP is a connectionless protocol, TCP is a connection-oriented protocol. With UDP there is no concept of a connection; there is only a sender and a receiver of a UDP datagram. With TCP, on the other hand, either side of the connection can send or receive data, possibly doing both at the same time. This is what makes TCP a full-duplex protocol. The process of establishing a TCP connection is sometimes called the three-way handshake—you'll see why.

With a connection-oriented protocol, there is a specific set of procedures that take place in order to establish a TCP connection. During this process, various states exist for the TCP connection. The connection establishment procedures and their corresponding states are detailed next.

The side of the communication wanting to initiate the connection (client) sends a TCP segment with the SYN flag, as well as an Initial Sequence Number (ISN) and the port number for the connection, to the other side, normally referred to as the server side of the connection. This is frequently referred to as a SYN packet or SYN segment, and the connection is said to be in the SYN_SENT state.

The server side of the connection responds with a TCP segment with the SYN flag as well as the ACK flag. In addition, the receiver sets the ISN with a value higher than the ISN sent by the client. This is frequently referred to as a SYN-ACK packet or SYN-ACK segment, and the connection is said to be in the SYN_RCVD state.
