
**Check sum.** Specifies any damage to the header that occurred during transmission.

**Urgent Pointer.** The optional first urgent byte in a packet, which indicates the end of urgent data.

**Options.** TCP options, such as the maximum TCP segment size.

**Data.** Upper-layer information.

Now take a look at the snapshot of a TCP header, shown in Figure 1.17a, and compare it with the fields shown in Figure 1.17b.

## Ports, Endpoints, Connection Establishment

TCP enables simultaneous communication between different application programs on a single machine. TCP uses port numbers to distinguish each of the receiving station's destinations. A pair of *endpoints* identifies the connection between the two stations, as mentioned earlier. Colloquially, these endpoints are defined as the connection between the two stations' applications as they communicate; they are defined by TCP as a pair of integers in this format: (host, port). The *host* is the station's IP address, and *port* is the TCP port number on that station. An example of a station's endpoint is:

206.0.125.81:1026

(host)(port)

An example of two stations' endpoints during communication is:

**STATION 1** **STATION 2**
206.0.125.81:1022 207.63.129.2:26
(host)(port) (host)(port)

This technology is very important in TCP, as it allows simultaneous communications by assigning separate ports for each station connection.

When a connection is established between two nodes during a TCP session, a *three-way handshake* is used. This process starts with a one-node TCP request by a SYN/ACK bit, and the second node TCP response with a SYN/ACK bit. At this point, as described previously, communication between the two nodes will proceed. When there is no more data to send, a TCP node may send a FIN bit, indicating a close control signal. At this intersection, both nodes will close simultaneously. Some common and well-known TCP ports and their related connection services are shown in Table B.1 in Appendix B on page 793.

------- TCP header -------
TCP:
TCP: Source port
= 80 (WWW-HTTP)
TCP: Destination port
= 1033
TCP: Sequence number
= 135179
TCP: Acknowledgment number
= 3440695
TCP: Data offset
= 20 bytes
TCP: Flags
= 10
TCP: ...0. .....
= (No urgent pointer)
TCP: .....1 .....
= Acknowledgment
TCP: ...0...
= (No push)
TCP: ....0..
= (No reset)
TCP: .....0..
= (No SYN)
TCP: .......0
= (No FIN)
TCP: Window
= 8389
TCP: Checksum
= 9A48 (correct)
TCP: No TCP options
TCP: [1460 Bytes of data]

**Figure 1.17a** Extracted from an HTTP Internet Web server transmission.

------- TCP header -------
TCP:
TCP: Source port
= 1027
TCP: Destination port
= 4107
TCP: Sequence number
= 2126033619
TCP: Acknowledgment number
= 2666894
TCP: Data offset
= 20 bytes
TCP: Flags
= 18
TCP: ...0. .....
= (No urgent pointer)
TCP: .....1 .....
= Acknowledgment
TCP: .....1 ...
= Push
TCP: ...0...
= (No reset)
TCP: ....0..
= (No SYN)
TCP: .......0
= (No FIN)
TCP: Window
= 16060
TCP: Checksum
= EF41 (correct)
TCP: No TCP options
TCP: [224 Bytes of data]

**Figure 1.17b** Extracted from a sliding window sequence transmission.

## User Datagram Protocol

The User Datagram Protocol (UDP) operates in a connectionless fashion; that is, it provides the same unreliable, datagram delivery service as IP. Unlike TCP, UDP does not send SYN/ACK bits to assure delivery and reliability of transmissions. Moreover, UDP does not include flow control or error recovery functionality. Consequently, UDP messages can be lost, duplicated, or arrive in the wrong order. And because UDP contains smaller headers, it expends less network throughput than TCP and so can arrive faster than the receiving station can process them.

UDP is typically utilized where higher-layer protocols provide necessary error recovery and flow control. Popular server daemons that employ UDP include Network File System (NFS), Simple Network Management Protocol (SNMP), Trivial File Transfer Protocol (TFTP), and Domain Name System (DNS), to name a few.

UDP does not include flow control or error recovery, and can be easily duplicated.

## UDP Formatting, Encapsulation, and Header Snapshots

UDP messages are called user datagrams. These datagrams are encapsulated in IP, including the UDP header and data, as it travels across the Internet. Basically, UDP adds a header to the data that a user sends, and passes it along to IP. The IP layer then adds a header to what it receives from UDP. Finally, the network interface layer inserts the datagram in a frame before sending it from one machine to another.

As just mentioned, UDP messages contain smaller headers and consume fewer overheads than TCP. The UDP datagram format is shown in Figure 1.18, and its components are defined in the following list.

- **Source/Destination Port.** A 16-bit UDP port number used for datagram processing.
- **Message Length.** Specifies the number of octets in the UDP datagram.
- **Checksum.** An optional field to verify datagram delivery.
- **Data.** The data handed down to the TCP protocol, including upper-layer headers.

Snapshots of a UDP header are given in Figure 1.19.

| Source Port | Destination Port |
| :--- | :--- |
| Message Length | Checksum |
| Data | |

**Figure 1.18** Illustration of a UDP datagram.

## Multiplexing, Demultiplexing, and Port Connections

UDP provides multiplexing (the method for multiple signals to be transmitted concurrently into an input stream, across a single physical channel) and demultiplexing (the actual separation of the streams that have been multiplexed into a common stream back into multiple output streams) between protocol and application software.

Multiplexing and demultiplexing, as they pertain to UDP, transpire through ports. Each station application must negotiate a port number before sending a UDP datagram. When UDP is on the receiving side of a datagram, it checks the header (destination port field) to determine whether it matches one of station's ports currently in use. If the port is in use by a listening application, the transmission proceeds; if the port is not in use, an ICMP error message is generated, and the datagram is discarded. A number of common UDP ports and their related connection services are listed in Table B.2 in Appendix B on page 795.

![](img/ba85bb40c695c02adae8cbd6666f2e0c_42_0.png)

**Figure 1.19** Extracted after the IP portion of a domain name resolution from a DNS request transmission (discussed in Chapter 5).

## Internet Control Message Protocol

The Internet Control Message Protocol (ICMP) delivers message packets, reporting errors and other pertinent information to the sending station or source. Hosts and infrastructure equipment use this mechanism to communicate control and error information, as they pertain to IP packet processing.

### ICMP Format, Encapsulation, and Delivery

ICMP message encapsulation is a two-fold process. The messages are encapsulated in IP datagrams, which are encapsulated in frames, as they travel across the Internet. Basically, ICMP uses the same unreliable means of communications as a datagram. This means that ICMP error messages may be lost or duplicated.

The ICMP format includes a *message type* field, indicating the type of message; a *code* field that includes detailed information about the type; and a *checksum* field, which provides the same functionality as IP’s checksum (see Figure 1.20). When an ICMP message reports an error, it includes the header and data of the datagram that caused the specified problem. This helps the receiving station to understand which application and protocol sent the datagram. (The next section has more information on ICMP message types.)

> **Hacker’s Note:** Like UDP, ICMP does not include flow control or error recovery, and so can be easily duplicated.

| Message Type | Code | Checksum |
| :--- | :--- | :--- |
| | | |

**Figure 1.20** Illustration of an ICMP datagram.

| Message Type | Description |
| :---: | :---: |
| 0 | Echo Reply |
| 3 | Destination Unreachable |
| 4 | Source Quench |
| 5 | Route Redirect |
| 8 | Echo Request |
| 11 | Datagram Time Exceeded |
| 12 | Datagram Parameter Problem |
| 13 | Timestamp Request |
| 14 | Timestamp Reply |
| 15 | Information Request |
| 16 | Information Reply |
| 17 | Address Mask Request |
| 18 | Address Mask Reply |

**Figure 1.21** ICMP message chart.

### ICMP Messages, Subnet Mask Retrieval

There are many types of useful ICMP messages; Figure 1.21 contains a list of several, which are described in the following list.

- **Echo Reply (Type 0)/Echo Request (Type 8).** The basic mechanism for testing possible communication between two nodes. The receiving station, if available, is asked to reply to the ping. An example of a ping is as follows:

STEP 1: BEGIN ECHO REQUEST

```
Ping 206.0.125.81 (at the command prompt)
```

STEP 2: BEGIN ECHO REPLY

```
Reply from 206.0.125.81: bytes=32 time<10ms TTL=128 (from receiving station 206.0.125.81)
```

```
Reply from 206.0.125.81: bytes=32 time<10ms TTL=128
```

```
Reply from 206.0.125.81: bytes=32 time<10ms TTL=128
```

```
Reply from 206.0.125.81: bytes=32 time<10ms TTL=128
```

- **Destination Unreachable (Type 3).** There are several issuances for this message type, including when a router or gateway does not know how to reach the destination, when a protocol or application is not active, when a datagram specifies an unstable route, or when a router must fragment the size of a datagram and cannot because the Don't Fragment Flag is set. An example of a Type 3 message is as follows:

STEP 1: BEGIN ECHO REQUEST

```
Ping 206.0.125.81 (at the command prompt)
```

STEP 2: BEGIN ECHO REPLY

```
Pinging 206.0.125.81 with 32 bytes of data:
```

```
Destination host unreachable.
```
