
IPv6—The principle reason for changing the IP protocol is the limited address space, which could cause a shortage of addresses in the near future.

Because of these demands and the problems with IPv4, the IETF (Internet Engineering Task Force) began working on a new version of IP in 1990: Internet Protocol Version 6—IPv6 (IP Next Generation).

The basic aims of the project are as follows:

- Support of billions of hosts, even if address space is used inefficiently
- Reduction in size of Internet routing tables
- Simplification of the protocol to allow packets to be processed by a router more quickly
- Higher security (authentication and data security) than today's IP
- More emphasis on types of service, especially for real-time applications
- Support for multicasting
- Openness of the protocol for future developments

![](img/9129877170834ca9d5fdac5319bf5f12_648_0.png)

## Internet Control Message Protocol (ICMP)

Internet Protocol (IP) was not designed for the purpose of ensuring faultless data transmission.

In the event of a communication problem during the transmission of an IP datagram, the sender of the datagram receives a corresponding error report through ICMP.

However, this error report can only be transmitted to the sender of the IP datagram if a gateway or the recipient of the IP datagram can analyze the error that occurred.

Because of this, ICMP (as defined in RFC 792) is a protocol that is usually used for transmitting error reports to the senders of IP datagrams.

For example, an IP datagram should be sent to a specific destination network through a specific router. However, if the router in question is not able to reach the destination, a destination unreachable message is sent.

Or, if the router notices that the received packet can reach the destination quicker via another path (another gateway), a redirect message is sent.

The analysis tool ping also uses the ICMP protocol for transmitting ping control messages (echo request and echo reply).

In turn, ICMP uses IP for transmitting the control messages and packs the control messages into the data section of the IP header.

ICMP places the type ID of the control message in the first octet of the data section in the IP header. The type ID classifies the control message and defines which and how much data is contained in the subsequent bytes of the datagram.

ICMP uses the message types shown in Table B-1.

| Type | Name | Description |
|---|---|---|
| 0 | Echo Reply | Answers the request (Type 8). |
| 3 | Destination Unreachable | A destination (host/network/protocol/port) cannot be reached. |
| 4 | Source Quench | The destination or a gateway currently is not able to process the IP datagrams (for example, due to overload). |
| 5 | Redirect Message | A gateway informs the sender of an IP datagram about a shorter route to the destination. |
| 8 | Echo Request | Sends a request for a response (Type 0: Echo Reply). |
| 11 | Time Exceeded | The TTL (Time To Live) of an IP datagram has reached the value 0. The datagram was discarded. |
| 12 | Parameter Problem | An IP datagram was discarded due to invalid parameters. |
| 13 | Time Stamp Request | Sends a request for a response, including the time in milliseconds since 0:00 UT. |
| 14 | Time Stamp Reply | Replies to the request (type 13) and sends its own time in milliseconds since 0:00 UT. |

Table B-1

Figure B-16 shows how an ICMP packet header is constructed.

![](img/9129877170834ca9d5fdac5319bf5f12_649_0.png)

Figure B-16

The following describes each component of the header:

- *Type (8bits)*—Specifies the format of the ICMP message, such as Type 0 (echo reply) or Type 8 (echo request)
- *Code (8 bits)*—Further qualifies the ICMP message
- *Checksum (16 bits)*—Of the ICMP message
- *ICMP Message (variable length)*—Contains the data specific to the message type indicated by the Type and Code fields

## Transport Layer

The third layer in the TCP/IP architecture is the Transport layer, as illustrated in Figure B-17.

![](img/9129877170834ca9d5fdac5319bf5f12_650_0.png)

Figure B-17

The transport layer enables communication between source and destination hosts, and uses the following end-to-end protocols:

- Transmission Control Protocol (TCP)
- User Datagram Protocol (UDP)

In addition, you need to know about the following:

- Ports and Port Numbers

## Transmission Control Protocol (TCP)

The Transmission Control Protocol (TCP) is a reliable, connection-oriented, bytestream protocol.

The protocol was originally defined in RFC 793. Over the course of time, these definitions were improved by removing errors and inconsistencies (RFC 1122) and expanded with a number of requirements (RFC 1323).

The main task of TCP is to provide secure transport of data through the network.

TCP provides reliability of the data transfer with a mechanism referred to as Positive Acknowledgement with Retransmission (PAR).

The sending system repeats the transfer of data until it receives positive confirmation from the receiver that the data has been received.

The data units exchanged between the sending and receiving TCP units are called packets. A TCP packet consists of a protocol header, at least 20 bytes in size, and the data to transmit.

Each of these packets includes a checksum by means of which the receiver can check to see if the data is error-free.

In the case of an error-free transmission, the receiver sends a confirmation of receipt to the sender. Otherwise, the packet is discarded and no confirmation of receipt is sent. If, after a specific length of time (timeout period) no receipt has arrived, the sender resends the packet in question. Figure B-18 shows how a TCP packet header is constructed.

![](img/9129877170834ca9d5fdac5319bf5f12_651_0.png)

Figure B-18

The following describes the components of a TCP packet header:

- *Source Port (16 bits)*—Specifies the port of the sender.
- *Destination Port (16 bits)*—Specifies the port of the receiver.
- *Sequence Number (32 bits)*—Sequence number of the first data byte in this segment. If the SYN bit is set, the sequence number is the initial sequence number and the first data byte is the initial sequence number +1.
- *Acknowledgement Number (32 bits)*—If the ACK bit is set, this field contains the value of the next sequence number the sender of the segment is expecting to receive. Once a connection is established, this is always sent.
- *Data Offset (4 bits)*—Indicates where the data begins. The length of the TCP header is always a multiple of 32 bits.
- *Reserved (4 bits)*—Must be set to zero.
- *Control Bit (6 bits)*—For example, it can be ACK, SYN, FIN.
- *Window (16 bits)*—The number of data bytes, beginning with the one indicated in the acknowledgement field, that the sender of this segment is willing to accept.
- *Checksum (16 bits)*—The complement sum of a pseudoheader of information from the IP header, TCP header, and the data, padded as needed with 0 bytes at the end to make a multiple of 2 bytes. The pseudoheader contains the source address, destination address, IP protocol, and total length.
- **Urgent Pointer (16 bits)**—If the URG bit is set, this field points to the sequence number of the last byte in a sequence of urgent data.
- **Options (0-44 bytes)**—Occupies space at the end of the TCP header. All options are included in the checksum.
- **Padding**—The TCP header must be padded with zeros to make the header length a multiple of 32 bits.

Because TCP is a connection-oriented byte-stream protocol, a client/server dialog connection is required before data can be transmitted.

The process of setting up this connection is referred to as the TCP handshake or three-way handshake, as shown in Figure B-19.

![](img/9129877170834ca9d5fdac5319bf5f12_652_0.png)

Figure B-19

The following describes the TCP handshake process:

- 1. The client sends a TCP packet to the server with the SYN flag set.
  This tells the server that the client wants to synchronize a connection. The SYN flag is used to synchronize the connection.
- 2. If the opposite side accepts the connection, the server receives the packet and takes out the sequence number (400).
- 3. The server sends a TCP packet to the client with a SYN flag set (with sequence number 600) and an ACK flag with sequence number 401 (Client SYN +1).
  With this, the server acknowledges the receipt of the client packet and tells the client that it wants to synchronize the connection.
