![](bbox=[0.13, 0.05, 0.51, 0.29])

Figure 1.19 Extracted after the IP portion of a domain name resolution from a DNS request transmission (discussed in Chapter 5).

# Internet Control Message Protocol

The Internet Control Message Protocol (ICMP) delivers message packets, reporting errors and other pertinent information to the sending station or source. Hosts and infrastructure equipment use this mechanism to communicate control and error information, as they pertain to IP packet processing.

# *ICMP Format, Encapsulation, and Delivery*

ICMP message encapsulation is a two-fold process. The messages are encapsulated in IP datagrams, which are encapsulated in frames, as they travel across the Internet. Basically, ICMP uses the same unreliable means of communications as a datagram. This means that ICMP error messages may be lost or duplicated.

The ICMP format includes a *message type* field, indicating the type of message; a *code* field that includes detailed information about the type; and a *checksum* field, which provides the same functionality as IP’s checksum (see Figure 1.20). When an ICMP message reports an error, it includes the header and data of the datagram that caused the specified problem. This helps the receiving station to understand which application and protocol sent the datagram. (The next section has more information on ICMP message types.)

> **Hacker’s Note:** Like UDP, ICMP does not include flow control or error recovery, and so can be easily duplicated.

| Message Type | Code | Checksum |
| :----------- | :----------- | :----------- |

Figure 1.20 Illustration of an ICMP datagram.