
## Transport Mechanisms

Internet Protocol defines a Network layer protocol of the OSI model. There are also other Network layer protocols, but I will be concentrating solely on IP because it is by far the most popular Network layer protocol in use today. Above the Network layer on the OSI model is the Transport layer. As you might expect, the Transport layer has its own set of protocols. Two of the Transport layer protocols are of interest: UDP and TCP. This section examines each of these protocols.

### UDP

UDP, or User Datagram Protocol, is a connectionless protocol used for such services as DNS queries, SNMP, and RADIUS. Being connectionless, UDP is akin to a “fire and forget” type of protocol. The client sends a UDP packet, sometimes referred to as a datagram, and assumes that the server will receive the packet. It’s up to a higher layer protocol to assemble the packets in order. The UDP header, shown in Figure 1.4, is 8 bytes in length.

![](img/d1359a287d9d43cd5ed19f3a7b55d40d_39_0.png)

The UDP header begins with the source port number and the destination port number. Next up is the length of the entire packet, including data. Obviously because the header itself is 8 bytes in length, the minimum value for this portion of the header is 8. The final portion of the UDP header is the checksum, which includes both the header and the data.

### TCP

TCP, an abbreviation for Transmission Control Protocol, is a connection-oriented protocol that is frequently used with IP. Referring to TCP as connection-oriented means that it provides reliable service to the layers above it. Recall the telephone conversation analogy given earlier in this chapter. As in that analogy, two applications wanting to communicate using TCP must also establish a connection (sometimes referred to as a session). The TCP header is shown in Figure 1.5.

The TCP header.

| Field | Description |
| :--- | :--- |
| Source Port | |
| Destination Port | |
| Sequence Number | |
| Acknowledgment Number | |
| Data Offset | |
| Unused | |
| Flags | |
| Window | |
| Checksum | |
| Urgent Pointer | |

As you can see from Figure 1.5, the 20-byte TCP header is significantly more complicated than the other protocol headers shown in this chapter. Like the UDP header, the TCP header begins with both the source and the destination ports. The combination of the source and destination ports along with the IP addresses of the sender and receiver identifies the connection. The TCP header has a 32-bit sequence number and a 32-bit acknowledgment. Remember that TCP is a connection-oriented protocol and provides reliable service. The sequence and acknowledgment numbers are the primary (but not the only) mechanism used to provide that reliability. As data is passed down to the Transport layer, TCP divides the data into what it believes to be the most appropriate size. These pieces are known as TCP segments. As TCP sends data down the protocol stack, it creates a sequence number that indicates the first byte of data for the given segment. On the opposite end of the communication, the receiver sends an acknowledgment indicating that the segment has been received. The sender keeps a timer running, and if an acknowledgment isn't received in a timely fashion, the segment will be resent.

Another mechanism for reliability that TCP provides is a checksum on both the header and the data. If the checksum set within the header by the sender does not match the checksum as computed by the receiver, the receiver will not send an acknowledgment. If an acknowledgment gets lost in transit, the sender will likely send another segment with the same sequence number. In such an event, the receiver will simply discard the repeated segment.

A four-bit field is used for header length, including any options provided as part of the header. There are six individual bit flags within the TCP header: URG, ACK, PSH, RST, SYN, and FIN. A description of these flags is contained in Table 1.4.

## CHAPTER 1: Preliminary Concepts Underlying Packet-Filtering Firewalls

### TABLE 1.4
### TCP Header Flags

| FLAG | DESCRIPTION |
| :--- | :--- |
| URG | Indicates that the urgent pointer portion of the header should be examined. |
| ACK | Indicates that the acknowledgment number should be examined. |
| PSH | Indicates that the receiver should hand this data up to the next layer as soon as possible. |
| RST | Indicates that the connection should be reset. |
| SYN | Initiates a connection. |
| FIN | Indicates that the sender (could be either side of the connection) is done sending data. |

The 16-bit *Window* field is used to provide a sliding window mechanism. The receiver sets the *window* number to indicate the size that the receiver is ready to receive, beginning with the *acknowledgment* number. This is a form of flow control for TCP.

The 16-bit *urgent* pointer indicates the offset from the *sequence number* where *urgent* data ends. This enables the sender to indicate that there is data that should be handled in an *urgent* manner and can be used in conjunction with the *PSH* flag as well.

Now that you have a feeling for the TCP header, it’s time to examine how TCP connections are established and ended.

## TCP CONNECTIONS

Whereas UDP is a connectionless protocol, TCP is a connection-oriented protocol. With UDP there is no concept of a connection; there is only a sender and a receiver of a UDP datagram. With TCP, on the other hand, either side of the connection can send or receive data, possibly doing both at the same time. This is what makes TCP a full-duplex protocol. The process of establishing a TCP connection is sometimes called the three-way *handshake*—you’ll see why shortly.

With a connection-oriented protocol, there is a specific set of procedures that takes place in order to establish a TCP connection. During this process, various states exist for the TCP connection. The connection establishment procedures and their corresponding states are detailed next.

The side of the communication wanting to initiate the connection (*client*) sends a TCP segment with the *SYN* flag set, as well as an *initial Sequence Number* (*ISN*) and the *port number* for the connection to the other side, normally referred to as the server side of the connection. This is frequently referred to as a *SYN* packet or *SYN* segment, and the connection is said to be in the *SYN_SENT* state.

The server side of the connection responds with a TCP segment with the **SYN** flag set as well as the **ACK** flag set. In addition, the server sets the ISN with a value one higher than the ISN sent by the client. This is frequently referred to as a **SYN-ACK** packet or **SYN-ACK** segment, and the connection is said to be in the **SYN_RCVD** state.

The client then acknowledges the **SYN-ACK** by sending another segment with the **ACK** flag set and by incrementing the ISN by one. This completes the three-way handshake and the connection is said to be in an **ESTABLISHED** state.

As with the protocol for connection initiation, there is also a protocol for connection termination. The protocol for terminating a TCP connection is four steps as opposed to the three for connection establishment. The additional step is due to the full duplex nature of a TCP connection insofar as either side may be sending data at any given time.

Closing a connection on one side is accomplished by that side sending a TCP segment with the **FIN** flag set. Either side of the connection can send a **FIN** to indicate that it is done sending data. The other side can still send data. However, in practice, after a **FIN** is received the connection termination sequence will normally begin. For this discussion I’ll call the side wanting to terminate the connection the client side.

The termination process begins with the client sending a segment with the **FIN** flag set, known as the **CLOSE_WAIT** state on the server side and **FIN_WAIT_1** on the client side. After the **FIN** is received by the server, the server sends an **ACK** back to the client, incrementing the sequence number by one. At this point the client goes into the **FIN_WAIT_2** state. The server also indicates to its own higher layer protocols that the connection is terminated. Next the server closes the connection, which causes a segment with the **FIN** flag to be sent to the client, which in turn causes the server to go into a **LAST_ACK** state while the client goes into a **TIME_WAIT** state. Finally, the client acknowledges this **FIN** with an **ACK** and increments the sequence number by one, which causes the connection to go into a **CLOSED** state. Because TCP connections can be terminated by either side, a TCP connection can exist in a half-close mode in which one end has initiated the **FIN** sequence but the other side has not done so.

TCP connections can also be terminated by one end sending a segment with the reset (**RST**) flag set. This tells the other side to use an abortive release method. This is as opposed to the normal termination of a TCP connection sometimes referred to as an orderly release.

An optional part of the TCP connection sequence is the establishment of the Maximum Segment Size (**MSS**). The **MSS** is the maximum chunk of data that the respective end of communication is able to receive. Because the **MSS** is the maximum size that a given end of the connection can receive, it’s perfectly fine to send a chunk of data smaller than the **MSS**. In general, you should consider a larger **MSS** to be good, keeping in mind that fragmentation should be avoided because it adds overhead (the additional bytes for each IP and TCP header required for fragmented packets).
