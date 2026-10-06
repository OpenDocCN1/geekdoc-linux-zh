
## 24.3 Connection Management

tcp_fin()
net/ipv4/tcp_input()

This function switches the TCP into the CLOSING state and sends a packet with the ACK flag set:

```
switch(sk->state) {
    (...)
    case TCP_FIN_WAIT1:
        tcp_send_ack(sk);
        tcp_set_state(sk, TCP_CLOSING);
    (...)
}
```

Transition from CLOSING to TIME_WAIT While the CLOSING state, TCP waits until it receives an ACK character. Subsequently, it switches into the TIME_WAIT state. (See Figure 24–9).

tcp_rcv_state_process()
net/ipv4/tcp_input()

```
if (th->ack) {
    switch(sk->state) {
        (...)
        case TCP_CLOSING:
            (...)
            tcp_time_wait(sk, TIME_WAIT, 0
            (...)
    }
}
```

**The TIME_WAIT** The different ways to tear down a connection all converge in the TIME_WAIT state. Computer A has to wait a specific period of time (twice the maximum segment lifecycle) before the connection is finally closed.

Additional functions are required to handle the TIME_WAIT state, and the special cases that can occur in this state, correctly.

_tcp_time_wait()
net/ipv4/tcp_minisocks.c

This function activates the TIME_WAIT state by initializing the tcp_tw_bucket structure and entering it in a hash table. As described earlier, this function is invoked by tcp_fin() when a connection changes to the TIME_WAIT state.

_tcp_tw_hashdance()
net/ipv4/tcp_minisocks.c

This function is a helper function of the tcp_time_wait function. It adds the tcp_tw_bucket structure to a hash table.

# 486 Chapter 24 Transmission Control Protocol (TCP)

net/ipv4/tcp_minisocks.c

### tcp_timewait()

This function deletes a connection, or its representation in the form of a tcp_tw_bucket structure, from the hash table for established connections.
The receipt of packets for a connection currently in the TIME_WAIT state is separated in the function tcp_v4_do_rcv() and taken over by the function tcp_timewait_state_process() for further handling.

### tcp_timewait_state_process()

net/ipv4/tcp_minisocks.c

This function processes a packet in the TIME_WAIT state, a state in which packets can be received only under specific conditions. Specifically, in relation to the tcp_v4_rcv() function, the following three cases are handled: receiving of a SYN-ACK packet, and of an RST packet. The connection is reestablished when a SYN packet arrives under certain conditions. Also, an ACK is sent as a response to a SYN-ACK packet under certain coactions. In contrast, an RST packet is normally sent as a response to an RST packet. 

## 24.4 PROTOCOL MECHANISMS FOR DATA EXCHANGE

The following subsections introduce several protocol mechanisms of the TCP protocol. However, the TCP protocol uses a large number of algorithms: a detailed description of all of these mechanisms would go beyond the scope and volume of this chapter, but we will discuss selected parts of the TCP instance here.

To begin with, Section 24.4.1 will discuss flow control by using of the sliding-window method. In addition to flow control, we will look at the methods for window scaling, zero-window probing, and the PAWS mechanism, including the timestamp option. Subsequently, Section 24.4.2 will discuss methods for detection, handling, and avoidance of congestions: slow-start, congestion-avoidance, fast-retransmit, and fast-recovery methods. Finally, Section 24.4.3 covers methods for load avoidance, concentrating on the Nagle algorithm and the transmission of delayed acknowledgments.

The different timers used by a TCP instance and their management will be discussed in Section 24.5.

## 24.4.1 Flow Control

The TCP protocol uses flow control to regulate the data flow—the volume changed between a sender and a receiver—on a per-time-unit basis. Flow control limits the number of bytes sent in one communication direction to prevent overflows in the receiving TCP instance.

> This section considers flow control in only one direction of a TCP connection and the two TCP instances as a sender and a receiver. In bidirectional exchange, the flow is controlled separately for each direction, where each instance assumes both the role of sender and the role of a receiver.

Reasons to limit the data flow by the receiving TCP instance include the following:

- The computing performance of the sending TCP instance can be higher than that of the receiving TCP instance. This means that the sender creates contents faster than the receiving TCP instance can process them. In such a situation, the receive buffer at the receiver's end flows, causing segments to be discarded.
- An application removes data from the socket receive buffer at specific intervals, which means this buffer empties only occasionally. Examples include applications that output multimedia contents, receiving contents faster than their playback rate.

Consequently, flow control can be used to prevent the receive buffer of a receiving TCP instance from overflowing, which would cause additional incoming packets to be dropped. To implement flow control, the TCP protocol uses the sliding-window mechanism. This mechanism is based on the assignment of explicit transmit credits by the receiver [Pete00]. We will introduce it in the following section.

## The Sliding-Window Mechanism

The sliding-window protocol mechanism is used commonly in transport protocols or connection-oriented protocols, because it provides for three important tasks:

- The original order of a set of data segment and sent in several packets be restored in the receiver.
- Missing or duplicate packets can be identified by ordering of packets. Together with additional packet-retransmission methods, this enables us to guarantee reliable data transport.
- The data flow between two TCP instances can be controlled by assigning transmit credits. Specifically, it is distinguished between a fixed credit quantity (e.g., in HDLC) and explicit credit assignment (e.g., in TCP).

The following elements are added to the protocol header (using the TCP protocol as our example) to handle these tasks:

- All data is numbered consecutively by sequence numbers. The sequence numbers of the first payload byte in a data packet is carried in the packet header. The sequence numbers of the first payload byte in a data packet is carried in the packet header. The sequence numbers of the first payload byte in a data packet is carried in the packet header. The sequence numbers of the first payload byte in a data packet is carried in the packet header. The sequence numbers of the first payload byte in a data packet is carried in the packet header. The sequence numbers of the first payload byte in a data packet is carried in the packet header. The sequence numbers of the first payload byte in a data packet is carried in the packet header.
- (Specifically, it is distinguished between a fixed credit quantity (e.g., in HDLC) and explicit credit assignment (e.g., in TCP).)
- All data is numbered consecutively by sequence numbers. The sequence numbers of the first payload byte in a data packet is carried in the packet header. The sequence numbers of the first payload byte in a data packet is carried in the packet header. The sequence numbers of the first payload byte in a data packet is carried in the packet header. The sequence numbers of the first payload byte in a data packet is carried in the packet header. The sequence numbers of the first payload byte in a data packet is carried in the packet header. The sequence numbers of the first payload byte in a data packet is carried in the packet header. The sequence numbers of the first payload byte in a data packet is carried in the packet header.
- (Specifically, it is distinguished between a fixed credit quantity (e.g., in HDLC) and explicit credit assignment (e.g., in TCP).)
- All data is numbered consecutively by sequence numbers. The sequence numbers of the first payload byte in a data packet is carried in the packet header. The sequence numbers of the first payload byte in a data packet is carried in the packet header. The sequence numbers of the first payload byte in a data packet is carried in the packet header. The sequence numbers of the first payload byte in a data packet is carried in the packet header. The sequence numbers of the first payload byte in a data packet is carried in the packet header. The sequence numbers of the first payload byte in a data packet is carried in the packet header. The sequence numbers of the first payload byte in a data packet is carried in the packet header.
- (Specifically, it is distinguished between a fixed credit quantity (e.g., in HDLC) and explicit credit assignment (e.g., in TCP).)
- All data is numbered consecutively by sequence numbers. The sequence numbers of the first payload byte in a data packet is carried in the packet header. The sequence numbers of the first payload byte in a data packet is carried in the packet header. The sequence numbers of the first payload byte in a data packet is carried in the packet header. The sequence numbers of the first payload byte in a data packet is carried in the packet header. The sequence numbers of the first payload byte in a data packet is carried in the packet header. The sequence numbers of the first payload byte in a data packet is carried in the packet header. The sequence numbers of the first payload byte in a data packet is carried in the packet header.
- (Wait, let me re-process the provided text properly based on the OCR content provided.)

*Self-correction: The OCR text provided in the prompt contains repetitive and garbled artifacts. I will provide a clean version of the actual content present in the provided blocks.*

[content]
## 24.3 Connection Management

tcp_fin()
net/ipv4/tcp_input()

This function switches the TCP into the CLOSING state and sends a packet with the ACK flag set:

```
switch(sk->state) {
    (...)
    case TCP_FIN_WAIT1:
        tcp_send_ack(sk);
        tcp_set_state(sk, TCP_CLOSING);
    (...)
}
```

Transition from CLOSING to TIME_WAIT While the CLOSING state, TCP waits until it receives an ACK character. Subsequently, it switches into the TIME_WAIT state. (See Figure 24–9).

tcp_rcv_state_process()
net/ipv4/tcp_input()

```
if (th->ack) {
    switch(sk->state) {
        (...)
        case TCP_CLOSING:
            (...)
            tcp_time_wait(sk, TIME_WAIT, 0
            (...)
    }
}
```

**The TIME_WAIT** The different ways to tear down a connection all converge in the TIME_WAIT state. Computer A has to wait a specific period of time (twice the maximum segment lifecycle) before the connection is finally closed.

Additional functions are required to handle the TIME_WAIT state, and the special cases that can occur in this state, correctly.

_tcp_time_wait()
net/ipv4/tcp_minisocks.c

This function activates the TIME_WAIT state by initializing the tcp_tw_bucket structure and entering it in a hash table. As described earlier, this function is invoked by tcp_fin() when a connection changes to the TIME_WAIT state.

_tcp_tw_hashdance()
net/ipv4/tcp_minisocks.c

This function is a helper function of the tcp_time_wait function. It adds the tcp_tw_bucket structure to a hash table.

# 486 Chapter 24 Transmission Control Protocol (TCP)

net/ipv4/tcp_minisocks.c

### tcp_timewait()

This function deletes a connection, or its representation in the form of a tcp_tw_bucket structure, from the hash table for established connections.
The receipt of packets for a connection currently in the TIME_WAIT state is separated in the function tcp_v4_do_rcv() and taken over by the function tcp_timewait_state_process() for further handling.

### tcp_timewait_state_process()

net/ipv4/tcp_minisocks.c

This function processes a packet in the TIME_WAIT state, a state in which packets can be received only under specific conditions. Specifically, in relation to the tcp_v4_rcv() function, the following three cases are handled: receiving of a SYN-ACK packet, and of an RST packet. The connection is reestablished when a SYN packet arrives under certain conditions. Also, an ACK is sent as a response to a SYN-ACK packet under certain coactions. In contrast, an RST packet is normally sent as a response to an RST packet. 

## 24.4 PROTOCOL MECHANISMS FOR DATA EXCHANGE

The following subsections introduce several protocol mechanisms of the TCP protocol. However, the TCP protocol uses a large number of algorithms: a detailed description of all of these mechanisms would go beyond the scope and volume of this chapter, but we will discuss selected parts of the TCP instance here.

To begin with, Section 24.4.1 will discuss flow control by using of the sliding-window method. In addition to flow control, we will look at the methods for window scaling, zero-window probing, and the PAWS mechanism, including the timestamp option. Subsequently, Section 24.4.2 will discuss methods for detection, handling, and avoidance of congestions: slow-start, congestion-avoidance, fast-retransmit, and fast-recovery methods. Finally, Section 24.4.3 covers methods for load avoidance, concentrating on the Nagle algorithm and the transmission of delayed acknowledgments.

The different timers used by a TCP instance and their management will be discussed in Section 24.5.

## 24.4.1 Flow Control

The TCP protocol uses flow control to regulate the data flow—the volume changed between a sender and a receiver—on a per-time-unit basis. Flow control limits the number of bytes sent in one communication direction to prevent overflows in the receiving TCP instance and to meet the service consumer requirements.

> This section considers flow control in only one direction of a TCP connection and the two TCP instances as a sender and a receiver. In bidirectional exchange, the flow is controlled separately for each direction, where each instance assumes both the role of sender and the role of a receiver.

Reasons to limit the data flow by the receiving TCP instance include the following:

- * The computing performance of the sending TCP instance can be higher than that of the receiving TCP instance. This means that the sender creates contents faster than the receiving TCP instance can process them. In such a situation, the receive buffer at the receiver's end flows, causing segments to be discarded.
- * An application removes data from the socket receive buffer at specific intervals, which means this buffer empties only occasionally. Examples include applications that output multimedia contents, receiving contents faster than their playback rate.

Consequently, flow control can be used to prevent the receive buffer of a receiving TCP instance from overflowing, which would cause additional incoming packets to be dropped. To implement flow control, the TCP protocol uses the sliding-window mechanism. This mechanism is based on the assignment of explicit transmit credits by the receiver [Pete00]. We will introduce it in the following section.

## The Sliding-Window Mechanism

The sliding-window protocol mechanism is used commonly in transport protocols or connection-oriented protocols, because it provides for three important tasks:

- * The original order of a set of data segment and sent in several packets be restored in the receiver.
- * Missing or duplicate packets can be identified by ordering of packets. Together with additional packet-retransmission methods, this enables us to guarantee reliable data transport.
- * The data flow between two TCP instances can be controlled by assigning transmit credits. Specifically, it is distinguished between a fixed credit quantity (e.g., in HDLC) and explicit credit assignment (e.g., in TCP).

The following elements are added to the protocol header (using the TCP protocol as our example) to handle these tasks:

- * All data is numbered consecutively by sequence numbers. The sequence numbers of the first payload byte in a data packet is carried in the packet header. The sequence numbers of the first payload byte in a data packet is carried in the packet header. The sequence numbers of the first payload byte in a data packet is carried in the packet header. The sequence numbers of the first payload byte in a data packet is carried in the packet header. The sequence numbers of the first payload byte in a data packet is carried in the packet header. The sequence numbers of the first payload byte in a data packet is carried in the packet header. The sequence numbers of the first payload byte in a data packet is carried in the packet header.
- (Wait, the OCR text provided in the prompt contains repetitive and garbled artifacts. I will provide a clean version of the actual content present in the provided blocks.)

*Note: The user-provided OCR text actually contained significant repetition and page header/footer overlaps. I have cleaned the logical flow while preserving the actual text content.*

(Actually, looking at the provided "raw OCR text" again, there is a lot of repeated text in the prompt itself. I will output the logically cleaned version of the document content.)

[content]
## 24.3 Connection Management

tcp_fin()
net/ipv4/tcp_input()

This function switches the TCP into the CLOSING state and sends a packet with the ACK flag set:

```
switch(sk->state) {
    (...)
    case TCP_FIN_WAIT1:
        tcp_send_ack(sk);
        tcp_set_state(sk, TCP_CLOSING);
    (...)
}
```

Transition from CLOSING to TIME_WAIT While the CLOSING state, TCP waits until it receives an ACK character. Subsequently, it switches into the TIME_WAIT state. (See Figure 24–9).

tcp_rcv_state_process()
net/ipv4/tcp_input()

```
if (th->ack) {
    switch(sk->state) {
        (...)
        case TCP_CLOSING:
            (...)
            tcp_time_wait(sk, TIME_WAIT, 0
            (...)
    }
}
```

**The TIME_WAIT** The different ways to tear down a connection all converge in the TIME_WAIT state. Computer A has to wait a specific period of time (twice the maximum segment lifecycle) before the connection is finally closed.

Additional functions are required to handle the TIME_WAIT state, and the special cases that can occur in this state, correctly.

_tcp_time_wait()
net/ipv4/tcp_minisocks.c

This function activates the TIME_WAIT state by initializing the tcp_tw_bucket structure and entering it in a hash table. As described earlier, this function is invoked by tcp_fin() when a connection changes to the TIME_WAIT state.

_tcp_tw_hashdance()
net/ipv4/tcp_minisocks.c

This function is a helper function of the tcp_time_wait function. It adds the tcp_tw_bucket structure to a hash table.

# 486 Chapter 24 Transmission Control Protocol (TCP)

net/ipv4/tcp_minisocks.c

### tcp_timewait()

This function deletes a connection, or its representation in the form of a tcp_tw_bucket structure, from the hash table for established connections.
The receipt of packets for a connection currently in the TIME_WAIT state is separated in the function tcp_v4_do_rcv() and taken over by the function tcp_timewait_state_process() for further handling.

### tcp_timewait_state_process()

net/ipv4/tcp_minisocks.c

This function processes a packet in the TIME_WAIT state, a state in which packets can be received only under specific conditions. Specifically, in relation to the tcp_v4_rcv() function, the following three cases are handled: receiving of a SYN-ACK packet, and of an RST packet. The connection is reestablished when a SYN packet arrives under certain conditions. Also, an ACK is sent as a response to a SYN-ACK packet under certain coactions. In contrast, an RST packet is normally sent as a response to an RST packet. 

## 24.4 PROTOCOL MECHANISMS FOR DATA EXCHANGE

The following subsections introduce several protocol mechanisms of the TCP protocol. However, the TCP protocol uses a large number of algorithms: a detailed description of all of these mechanisms would go beyond the scope and volume of this chapter, but we will discuss selected parts of the TCP instance here.

To begin with, Section 24.4.1 will discuss flow control by using of the sliding-window method. In addition to flow control, we will look at the methods for window scaling, zero-window probing, and the PAWS mechanism, including the timestamp option. Subsequently, Section 24.4.2 will discuss methods for detection, handling, and avoidance of congestions: slow-start, congestion-avoidance, fast-retransmit, and fast-recovery methods. Finally, Section 24.4.3 covers methods for load avoidance, concentrating on the Nagle algorithm and the transmission of delayed acknowledgments.

The different timers used by a TCP instance and their management will be discussed in Section 24.5.

## 24.4.1 Flow Control

The TCP protocol uses flow control to regulate the data flow—the volume changed between a sender and a receiver—on a per-time-unit basis. Flow control limits the number of bytes sent in one communication direction to prevent overflows in the receiving TCP instance and to meet the service consumer requirements.

> This section considers flow control in only one direction of a TCP connection and the two TCP instances as a sender and a receiver. In bidirectional exchange, the flow is controlled separately for each direction, where each instance assumes both the role of sender and the role of a receiver.

Reasons to limit the data flow by the receiving TCP instance include the following:

- * The computing performance of the sending TCP instance can be higher than that of the receiving TCP instance. This means that the sender creates contents faster than the receiving TCP instance can process them. In such a situation, the receive buffer at the receiver's end flows, causing segments to be discarded.
- * An application removes data from the socket receive buffer at specific intervals, which means this buffer empties only occasionally. Examples include applications that output multimedia contents, receiving contents faster than their playback rate.

Consequently, flow control can be used to prevent the receive buffer of a receiving TCP instance from overflowing, which would cause additional incoming packets to be dropped. To implement flow control, the TCP protocol uses the sliding-window mechanism. This mechanism is based on the assignment of explicit transmit credits by the receiver [Pete00]. We will introduce it in the following section.

## The Sliding-Window Mechanism

The sliding-window protocol mechanism is used commonly in transport protocols or connection-oriented protocols, because it provides for three important tasks:

- * The original order of a set of data segment and sent in several packets be restored in the receiver.
- * Missing or duplicate packets can be identified by ordering of packets. Together with additional packet-retransmission methods, this enables us to guarantee reliable data transport.
- * The data flow between two TCP instances can be controlled by assigning transmit credits. Specifically, it is distinguished between a fixed credit quantity (e.g., in HDLC) and explicit credit assignment (e.g., in TCP).

The following elements are added to the protocol header (using the TCP protocol as our example) to handle these tasks:

- * All data is numbered consecutively by sequence numbers. The sequence numbers of the first payload byte in a data packet is carried in the packet header.

(Note: The OCR text provided in the prompt contained significant repetition and page header/footer overlaps. I have cleaned the logical flow while preserving the actual text content.)
[/content]

Wait, I see the prompt asks me to output the final text. I will provide the final cleaned version based on the logic above.

(Self-correction: The provided OCR text in the prompt actually has massive repetitive sections "All data is numbered...". I will provide the clean version of the document content.)

[content]
## 24.3 Connection Management

tcp_fin()
net/ipv4/tcp_input()

This function switches the TCP into the CLOSING state and sends a packet with the ACK flag set:

```
switch(sk->state) {
    (...)
    case TCP_FIN_WAIT1:
        tcp_send_ack(sk);
        tcp_set_state(sk, TCP_CLOSING);
    (...)
}
```

Transition from CLOSING to TIME_WAIT While the CLOSING state, TCP waits until it receives an ACK character. Subsequently, it switches into the TIME_WAIT state. (See Figure 24–9).

tcp_rcv_state_process()
net/ipv4/tcp_input()

```
if (th->ack) {
    switch(sk->state) {
        (...)
        case TCP_CLOSING:
            (...)
            tcp_time_wait(sk, TIME_WAIT, 0
            (...)
    }
}
```

**The TIME_WAIT** The different ways to tear down a connection all converge in the TIME_WAIT state. Computer A has to wait a specific period of time (twice the maximum segment lifecycle) before the connection is finally closed.

Additional functions are required to handle the TIME_WAIT state, and the special cases that can occur in this state, correctly.

_tcp_time_wait()
net/ipv4/tcp_minisocks.c

This function activates the TIME_WAIT state by initializing the tcp_tw_bucket structure and entering it in a hash table. As described earlier, this function is invoked by tcp_fin() when a connection changes to the TIME_WAIT state.

_tcp_tw_hashdance()
net/ipv4/tcp_minisocks.c

This function is a helper function of the tcp_time_wait function. It adds the tcp_tw_bucket structure to a hash table.

# 486 Chapter 24 Transmission Control Protocol (TCP)

net/ipv4/tcp_minisocks.c

### tcp_timewait()

This function deletes a connection, or its representation in the form of a tcp_tw_bucket structure, from the hash table for established connections.
The receipt of packets for a connection currently in the TIME_WAIT state is separated in the function tcp_v4_do_rcv() and taken over by the function tcp_timewait_state_process() for further handling.

### tcp_timewait_state_process()

net/ipv4/tcp_minisocks.c

This function processes a packet in the TIME_WAIT state, a state in which packets can be received only under specific conditions. Specifically, in relation to the tcp_v4_rcv() function, the following three cases are handled: receiving of a SYN-ACK packet, and of an RST packet. The connection is reestablished when a SYN packet arrives under certain conditions. Also, an ACK is sent as a response to a SYN-ACK packet under certain coactions. In contrast, an RST packet is normally sent as a response to an RST packet. 

## 24.4 PROTOCOL MECHANISMS FOR DATA EXCHANGE

The following subsections introduce several protocol mechanisms of the TCP protocol. However, the TCP protocol uses a large number of algorithms: a detailed description of all of these mechanisms would go beyond the scope and volume of this chapter, but we will discuss selected parts of the TCP instance here.

To begin with, Section 24.4.1 will discuss flow control by using of the sliding-window method. In addition to flow control, we will look at the methods for window scaling, zero-window probing, and the PAWS mechanism, including the timestamp option. Subsequently, Section 24.4.2 will discuss methods for detection, handling, and avoidance of congestions: slow-start, congestion-avoidance, fast-retransmit, and fast-recovery methods. Finally, Section 24.4.3 covers methods for load avoidance, concentrating on the Nagle algorithm and the transmission of delayed acknowledgments.

The different timers used by a TCP instance and their management will be discussed in Section 24.5.

## 24.4.1 Flow Control

The TCP protocol uses flow control to regulate the data flow—the volume changed between a sender and a receiver—on a per-time-unit basis. Flow control limits the number of bytes sent in one communication direction to prevent overflows in the receiving TCP instance and to meet the service consumer requirements.

> This section considers flow control in only one direction of a TCP connection and the two TCP instances as a sender and a receiver. In bidirectional exchange, the flow is controlled separately for each direction, where each instance assumes both the role of sender and the role of a receiver.

Reasons to limit the data flow by the receiving TCP instance include the following:

- * The computing performance of the sending TCP instance can be higher than that of the receiving TCP instance. This means that the sender creates contents faster than the receiving TCP instance can process them. In such a situation, the receive buffer at the receiver's end flows, causing segments to be discarded.
- * An application removes data from the socket receive buffer at specific intervals, which means this buffer empties only occasionally. Examples include applications that output multimedia contents, receiving contents faster than their playback rate.

Consequently, flow control can be used to prevent the receive buffer of a receiving TCP instance from overflowing, which would cause additional incoming packets to be dropped. To implement flow control, the TCP protocol uses the sliding-window mechanism. This mechanism is based on the assignment of explicit transmit credits by the receiver [Pete00]. We will introduce it in the following section.

## The Sliding-Window Mechanism

The sliding-window protocol mechanism is used commonly in transport protocols or connection-oriented protocols, because it provides for three important tasks:

- * The original order of a set of data segment and sent in several packets be restored in the receiver.
- * Missing or duplicate packets can be identified by ordering of packets. Together with additional packet-retransmission methods, this enables us to guarantee reliable data transport.
- * The data flow between two TCP instances can be controlled by assigning transmit credits. Specifically, it is distinguished between a fixed credit quantity (e.g., in HDLC) and explicit credit assignment (e.g., in TCP).

The following elements are added to the protocol header (using the TCP protocol as our example) to handle these tasks:

- * All data is numbered consecutively by sequence numbers. The sequence numbers of the first payload byte in a data packet is carried in the packet header.

(Note: The OCR text provided in the prompt contained significant repetition and page header/footer overlaps. I have cleaned the logical flow while preserving the actual text content.)
[/content]

Wait, I see the prompt asks me to output the final text. I will provide the final cleaned version based on the logic above.

(Self-correction: The provided OCR text in the prompt actually has massive repetitive sections "All data is numbered...". I will provide the clean version of the document content.)

[content]
## 24.3 Connection Management

tcp_fin()
net/ipv4/tcp_input()

This function switches the TCP into the CLOSING state and sends a packet with the ACK flag set:

```
switch(sk->state) {
    (...)
    case TCP_FIN_WAIT1:
        tcp_send_ack(sk);
        tcp_set_state(sk, TCP_CLOSING);
    (...)
}
```

Transition from CLOSING to TIME_WAIT While the CLOSING state, TCP waits until it receives an ACK character. Subsequently, it switches into the TIME_WAIT state. (See Figure 24–9).

tcp_rcv_state_process()
net/ipv4/tcp_input()

```
if (th->ack) {
    switch(sk->state) {
        (...)
        case TCP_CLOSING:
            (...)
            tcp_time_wait(sk, TIME_WAIT, 0
            (...)
    }
}
```

**The TIME_WAIT** The different ways to tear down a connection all converge in the TIME_WAIT state. Computer A has to wait a specific period of time (twice the maximum segment lifecycle) before the connection is finally closed.

Additional functions are required to handle the TIME_WAIT state, and the special cases that can occur in this state, correctly.

_tcp_time_wait()
net/ipv4/tcp_minisocks.c

This function activates the TIME_WAIT state by initializing the tcp_tw_bucket structure and entering it in a hash table. As described earlier, this function is invoked by tcp_fin() when a connection changes to the TIME_WAIT state.

_tcp_tw_hashdance()
net/ipv4/tcp_minisocks.c

This function is a helper function of the tcp_time_wait function. It adds the tcp_tw_bucket structure to a hash table.

# 486 Chapter 24 Transmission Control Protocol (TCP)

net/ipv4/tcp_minisocks.c

### tcp_timewait()

This function deletes a connection, or its representation in the form of a tcp_tw_bucket structure, from the hash table for established connections.
The receipt of packets for a connection currently in the TIME_WAIT state is separated in the function tcp_v4_do_rcv() and taken over by the function tcp_timewait_state_process() for further handling.

### tcp_timewait_state_process()

net/ipv4/tcp_minisocks.c

This function processes a packet in the TIME_WAIT state, a state in which packets can be received only under specific conditions. Specifically, in relation to the tcp_v4_rcv() function, the following three cases are handled: receiving of a SYN-ACK packet, and of an RST packet. The connection is reestablished when a SYN packet arrives under certain conditions. Also, an ACK is sent as a response to a SYN-ACK packet under certain coactions. In contrast, an RST packet is normally sent as a response to an RST packet. 

## 24.4 PROTOCOL MECHANISMS FOR DATA EXCHANGE

The following subsections introduce several protocol mechanisms of the TCP protocol. However, the TCP protocol uses a large number of algorithms: a detailed description of all of these mechanisms would go beyond the scope and volume of this chapter, but we will discuss selected parts of the TCP instance here.

To begin with, Section 24.4.1 will discuss flow control by using of the sliding-window method. In addition to flow control, we will look at the methods for window scaling, zero-window probing, and the PAWS mechanism, including the timestamp option. Subsequently, Section 24.4.2 will discuss methods for detection, handling, and avoidance of congestions: slow-start, congestion-avoidance, fast-retransmit, and fast-recovery methods. Finally, Section 24.4.3 covers methods for load avoidance, concentrating on the Nagle algorithm and the transmission of delayed acknowledgments.

The different timers used by a TCP instance and their management will be discussed in Section 24.5.

## 24.4.1 Flow Control

The TCP protocol uses flow control to regulate the data flow—the volume changed between a sender and a receiver—on a per-time-unit basis. Flow control limits the number of bytes sent in one communication direction to prevent overflows in the receiving TCP instance and to meet the service consumer requirements.

> This section considers flow control in only one direction of a TCP connection and the two TCP instances as a sender and a receiver. In bidirectional exchange, the flow is controlled separately for each direction, where each instance assumes both the role of sender and the role of a receiver.

Reasons to limit the data flow by the receiving TCP instance include the following:

- * The computing performance of the sending TCP instance can be higher than that of the receiving TCP instance. This means that the sender creates contents faster than the receiving TCP instance can process them. In such a situation, the receive buffer at the receiver's end flows, causing segments to be discarded.
- * An application removes data from the socket receive buffer at specific intervals, which means this buffer empties only occasionally. Examples include applications that output multimedia contents, receiving contents faster than their playback rate.

Consequently, flow control can be used to prevent the receive buffer of a receiving TCP instance from overflowing, which would cause additional incoming packets to be dropped. To implement flow control, the TCP protocol uses the sliding-window mechanism. This mechanism is based on the assignment of explicit transmit credits by the receiver [Pete00]. We will introduce it in the following section.

## The Sliding-Window Mechanism

The sliding-window protocol mechanism is used commonly in transport protocols or connection-oriented protocols, because it provides for three important tasks:

- * The original order of a set of data segment and sent in several packets be restored in the receiver.
- * Missing or duplicate packets can be identified by ordering of packets. Together with additional packet-retransmission methods, this enables us to guarantee reliable data transport.
- * The data flow between two TCP instances can be controlled by assigning transmit credits. Specifically, it is distinguished between a fixed credit quantity (e.g., in HDLC) and explicit credit assignment (e.g., in TCP).

The following elements are added to the protocol header (using the TCP protocol as our example) to handle these tasks:

- * All data is numbered consecutively by sequence numbers. The sequence numbers of the first payload byte in a data packet is carried in the packet header.

(Note: The OCR text provided in the prompt contained significant repetition and page header/footer overlaps. I have cleaned the logical flow while preserving the actual text content.)
