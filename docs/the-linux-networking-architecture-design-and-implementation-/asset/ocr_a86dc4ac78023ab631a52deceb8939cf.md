# 486 Chapter 24 Transmission Control Protocol (TCP)

net/ipv4/tcp_minisocks.c

# tcp_timewait()

This function deletes a connection, or its representation in the form of a tcp_tw_bucket structure, from the hash table for established connections.
The receipt of packets for a connection currently in the TIME_WAIT state is separated in the function tcp_v4_do_rcv() and taken over by the function tcp_timewait_state_process() for further handling.

# tcp_timewait_state_process()

net/ipv4/tcp_minisocks.c

This function processes a packet in the TIME_WAIT state, a state in which packets can be received only under specific conditions. Specifically, in relation to the tcp_v4_rcv() function, the following three cases are handled: receiving of a SYN-ACK packet, and of an RST packet. The connection is reestablished when a SYN packet arrives under certain conditions. Also, an ACK is sent as a response to a SYN-ACK packet under certain coactions. In contrast, an RST packet is normally sent as a response to an RST packet.

# 24.4 PROTOCOL MECHANISMS FOR DATA EXCHANGE

The following subsections introduce several protocol mechanisms of the TCP protocol. However, the TCP protocol uses a large number of algorithms: a detailed description of all of these mechanisms would go beyond the scope and volume of this chapter, but we will discuss selected parts of the TCP instance here.

To begin with, Section 24.4.1 will discuss flow control by using of the sliding-window method. In addition to flow control, we will look at the methods for window scaling, zero-window probing, and the PAWS mechanism, including the timestamp option. Subsequently, Section 24.4.2 will discuss methods for detection, handling, and avoidance of congestions: slow-start, congestion-avoidance, fast-retransmit, and fast-recovery methods. Finally, Section 24.4.3 covers methods for load avoidance, concentrating on the Nagle algorithm and the transmission of delayed acknowledgments.

The different timers used by a TCP instance and their management will be discussed in Section 24.5.

# 24.4.1 Flow Control

The TCP protocol uses flow control to regulate the data flow—the volume changed between a sender and a receiver—on a per-time-unit basis. Flow control limits the number of bytes sent in one communication direction to prevent overflows in

> This section considers flow control in only one direction of a TCP connection and the two TCP instances as a sender and a receiver. In bidirectional exchange, the flow is controlled separately for each direction, where each instance assumes both the role of sender and the role of a receiver.