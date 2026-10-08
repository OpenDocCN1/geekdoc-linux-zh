# Don't Forget ARP

The client acknowledges the SYN-ACK by sending another segment with the ACK flag set and by incrementing the ISN by one. This completes the three-way handshake and the connection is said to be in an ESTABLISHED state.

As with the protocol for connection initiation, there is also a protocol for connection termination. The protocol for terminating a TCP connection is four steps as opposed to the three for connection establishment. The additional step is due to the full duplex nature of a TCP connection insofar as each side may be sending data at any given time.

Closing a connection on one side is accomplished by sending a TCP segment with the FIN flag set. Either side of the connection can send a FIN to indicate that it is sending data. The other side can also send data. However, in practice, after a FIN is received the connection termination sequence will normally begin. For this discussion I'll call the side wanting to terminate the connection side.

The termination process begins with the client sending a segment with the FIN flag set, known as the CLOSE_WAIT state on the server side and FIN_WAIT_1 on the client side. After the FIN is received by the server, the server sends an ACK back to the client, incrementing the sequence number by one. At this point the connection goes into the FIN_WAIT_2 state. The server also closes its own higher layer protocols that the connection is terminated. The server closes a segment with the FIN sent to the client, which causes the server to go into a LAST_ACK state while the client goes into a TIME_WAIT state. Finally, the client acknowledges this FIN with an ACK and increments the sequence number by one, which causes the connection to go into a CLOSED state. Because TCP connections can be terminated by either side, a TCP connection can exist in a half-close mode in which one end initiated the FIN sequence but the other side has not done so.

TCP connections can be terminated by one end sending a segment with the reset (RST) flag set. This tells the other side to use an abortive release method. This is as opposed to the normal termination of a TCP connection sometimes referred to as an orderly release.

An optional part of the TCP connection sequence is the establishment of the Maximum Segment Size (MSS). The MSS is the maximum chunk of data that the connection is able to receive. Because the MSS is the maximum size that a given end of the connection can receive, it's perfectly fine to send a chunk of data smaller than the MSS. In general, you should consider a larger MSS to be good, keeping in mind that fragmentation should be avoided because it adds overhead (the additional bytes for each IP and TCP header required for fragmented packets).

# Don't Forget ARP

Address Resolution Protocol, or ARP, is the protocol used to link a physical device such as a network card to an IP address. Network devices use a 48-bit address (known as a MAC address) that is unique across all devices in a given segment. Although sometimes devices have the same MAC address, this is quite rare within the same network segment.

When capturing traffic in a network, you will encounter ARP packets at varying frequencies as devices locate one another as they pass traffic. ARP requests are broadcast so all devices will see them. However, most ARP replies are unicast to only the