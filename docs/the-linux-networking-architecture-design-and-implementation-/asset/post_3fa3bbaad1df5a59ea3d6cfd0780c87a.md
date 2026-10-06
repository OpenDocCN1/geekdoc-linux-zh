
## 24.2 Implementing the TCP Protocol Instance

TCP connection within a local area network and from 83% to 99% of all cases in a WAN connection. Though these results are not necessarily representative and depend on the actual load of the networks, they show that it appears to differentiate between Slow Path and Fast Path.

Packets are processed in Fast Path in the following two situations:

- *The segment received is a pure ACK segment for the data sent last (no duplicate ACK).*
- *The segment received includes data expected next, so that they are consecutive with the data received until then.*

Fast Path is not accessed in the following situations (and so a detailed protocol-handling process is performed in Slow Path):

Unexpected TCP flags: The process continues in Slow Path if a SYN, FIN, or RST flag is set. These cases are detected by the Header Prediction described later. If the sequence number of an incoming segment does not correspond to the sequence number received next (tp->rcv_nxt), then the segment is either a transmitted segment or an out-of-order segment.

Both communication partners exchange data: Fast Path cannot be used in situations where the relevant TCP instance either sends only or receives (i.e., where either the sequence number or the acknowledgement number remains constant).

The current TCP instance sets a Zero Window (i.e., no transmit credit granted to the communication partner).

Unexpected TCP options are processed in Slow Path. The Timestamp option is the only option that can be handled in Fast Path.

To make the differentiation between Fast Path and Slow Path worthwhile, Fast Path has to be detected quickly and reliably. Most of the cases mentioned above can be detected by the so-called Header Prediction, which uses a simple comparative operation on the Header Length, Flags, and Window Size fields and a predicted value to decide whether the Fast Path can be used:

```
/* pred_flags = 0XS0 << 16 + snd_wnd
 * if header_prediction is to be made
 * 'S' will always be tp->tcp_header_len >> 2
 * '?' will be 0 for the fast path, otherwise pred_flags is 0 to
 * turn it off (when there are holes in the receive space
 * for instance), PSH flag is ignored.
 * /
```

```c
if ((tcp_fast_word(th) & TCP_HP_BITS) == tp->pred_flags &&
  TCP_SKB_cb(sk)->seq == tp->rcv_nxt)
{ (...FAST PATH...) }
else
{ (...SLOW PATH...) }
```

## Chapter 24 Transmission Control Protocol (TCP)

comparative value (tp->pred_flags) is computed in the tcp_fast_path_on() function in america, which means that it activates processing over the Fast Path with the preconditions:

```c
static __inline__ void __tcp_fast_path_on(struct tcp_opt *tp, u32 snd_wnd) {
    tp->pred_flags = htonl(tp->tcp_header_len << 26) | ntohl(TCP_FLAG_ACK) | snd_wnd;
}
static __inline__ void tcp_fast_path_on(struct tcp_opt *tp) {
    __tcp_fast_path_on(tp, tp->snd_wnd) -> tp->snd_wscale);
}
```

It should even happen that the TCP connection gets into a situation where Fast Path cannot be used, the problem is solved by simply writing a null to the comparative operator of the Header Prediction—for example, much like what is done when sending a Zero Window in tcp_select_window().

Fast Path Once an incoming segment has successfully passed the Header Prediction, its processing in the Fast Path begins, the following operations are done:

- The sequence number is checked to filter out-of-order packets (TCP_SKB, CB(skb)->seq == tp->rcv_nxt).
- The Timestamp option is checked, but only by evaluating the length of the packet header. Subsequently, all options fail the Header Prediction, which means a simple check of the packet-header length is sufficient. The Timestamp values, Tval and Tsecr, are read directly.(See Section 24.4.1). If the subsequent PAWS checks fail, then the process continues in Slow Path; otherwise, the segment is all right. If the condition to update the tp->ts_recent timestamp is met, it is accepted by tcp_store_ts_recent().
- ACK segment: The acknowledgement number. if present, in a packet that contains no payload is processed in tcp_ack. __kfree_skb() releases the socket buffer, which completes the process of handling this segment.
- Finally, tcp_data_snd_check() checks whether local packets can be sent. Data segment: In this case, the segment contains the data expected next (was previously checked).

At this point, the only thing tested is whether the payload can be copied directly into the user-address space:

If the payload can be copied directly into the user-address space, then the statistics of this connection are updated, the relevant process is inspected.

the payload is copied into the receive memory of the process, the TCP packet header is removed, and, finally, the variable with the sequence number expected is updated.

If the payload cannot be directly copied into the user-address space, then the availability of buffer memory in the socket is checked, statistical information is updated, the TCP packet header is removed, and, finally, the variable with the sequence number expected is updated.

If the payload cannot be directly copied into the user-address space, then the availability of buffer memory in the socket is checked, statistical information is updated, the TCP packet header is removed, and, finally, the variable with the sequence number expected is updated.

If the payload cannot be directly copied into the user-address space, then the availability of buffer memory in the socket is checked, statistical information is updated, the TCP packet header is removed, and, finally, the variable with the sequence number expected is updated.

If the payload cannot be directly copied into the user-address space, then the availability of buffer memory in the socket is checked, statistical information is updated, the TCP packet header is removed, and, finally, the variable with the sequence number expected is updated.

If the payload cannot be directly copied into the user-address space, then the availability of buffer memory in the socket is checked, statistical information is updated, the TCP packet header is removed, and, finally, the variable with the sequence number expected is updated.

If the payload cannot be directly copied into the user-address space, then the availability of buffer memory in the socket is checked, statistical information is updated, the TCP packet header is removed, and, finally, the variable with the sequence number expected is updated.

If the payload cannot be directly copied into the user-address space, then the availability of buffer memory in the socket is checked, statistical information is updated, the TCP packet header is removed, and, finally, the variable with the sequence number expected is updated.

If the payload cannot be directly copied into the user-address space, then the availability of buffer memory in the socket is checked, statistical information is updated, the TCP packet header is removed, and, finally, the variable with the sequence number expected is updated.

If the payload cannot be directly copied into the user-address space, then the availability of buffer memory in the socket is checked, statistical information is updated, the TCP packet header is removed, and, finally, the variable with the sequence number expected is updated.

If the payload cannot be directly copied into the user-address space, then the availability of buffer memory in the socket is checked, statistical information is updated, the TCP packet header is removed, and, finally, the variable with the sequence number expected is updated.

If the payload cannot be directly copied into the user-address space, then the availability of buffer memory in the socket is checked, statistical information is updated, the TCP packet header is removed, and, finally, the variable with the sequence number expected is updated.

If the payload cannot be directly copied into the user-address space, then the availability of buffer memory in the socket is checked, statistical information is updated, the TCP packet header is removed, and, finally, the variable with the sequence number expected is updated.

If the payload cannot be directly copied into the user-address space, then the availability of buffer memory in the socket is checked, statistical information is updated, the TCP packet header is removed, and, finally, the variable with the sequence number expected is updated.

If the payload cannot be directly copied into the user-address space, then the availability of buffer memory in the socket is checked, statistical information is updated, the TCP packet header is removed, and, finally, the variable with the sequence number expected is updated.

If the payload cannot be directly copied into the user-address space, then the availability of buffer memory in the socket is checked, statistical information is updated, the TCP packet header is removed, and, finally, the variable with the sequence number expected is updated.

If the payload cannot be directly copied into the user-address space, then the availability of buffer memory in the socket is checked, statistical information is updated, the TCP packet header is removed, and, finally, the variable with the sequence number expected is updated.

If the payload cannot be directly copied into the user-address space, then the availability of buffer memory in the socket is checked, statistical information is updated, the TCP packet header is removed, and, finally, the variable with the sequence number expected is updated.

If the payload cannot be directly copied into the user-address space, then the availability of buffer memory in the socket is checked, statistical information is updated, the TCP packet header is removed, and, finally, the variable with the sequence number expected is updated.

## 24.2 Implementing the TCP Protocol Instance 465

the payload is copied into the receive memory of the process, the TCP packet header is removed, and, finally, the variable with the sequence number expected is updated.

If the payload cannot be directly copied into the user-address space, then the availability of buffer memory in the socket is checked, statistical information is updated, the TCP packet header is removed, and, finally, the variable with the sequence number expected is updated.

If the payload cannot be directly copied into the user-address space, then the availability of buffer memory in the socket is checked, statistical information is updated, the TCP packet header is removed, and, finally, the variable with the sequence number expected is updated.

If the payload cannot be directly copied into the user-address space, then the availability of buffer memory in the socket is checked, statistical information is updated, the TCP packet header is removed, and, finally, the variable with the sequence number expected is updated.

At this point, the only thing tested is whether the payload can be copied directly into the user-address space:

If the payload can be copied directly into the user-address space, then the statistics of this connection are updated, the relevant process is inspected.

## 24.2 Implementing the TCP Protocol Instance 465 (continued)the payload is copied into the receive memory of the process, the TCP packet header is removed, and, finally, the variable with the sequence number expected is updated.

If the payload cannot be directly copied into the user-address space, then the availability of buffer memory in the socket is checked, statistical information is updated, the TCP packet header is removed, and, finally, the variable with the sequence number expected is updated.

If the payload cannot be directly copied into the user-address space, then the availability of buffer memory in the socket is checked, statistical information is updated, the TCP packet header is removed, and, finally, the variable with the sequence number expected is updated.

If the payload cannot be directly copied into the user-address space, then the availability of buffer memory in the socket is checked, statistical information is updated, the TCP packet header is removed, and, finally, the variable with the sequence number expected is updated.

If the payload cannot be directly copied into the user-address space, then the availability of buffer memory in the socket is checked, statistical information is updated, the TCP packet header is removed, and, finally, the variable with the sequence number expected is updated.

If the payload cannot be directly copied into the user-address space, then the availability of buffer memory in the socket is checked, statistical information is updated, the TCP packet header is removed, and, finally, the variable with the sequence number expected is updated.

If the payload cannot be directly copied into the user-address space, then the availability of buffer memory in the socket is checked, statistical information is updated, the TCP packet header is removed, and, finally, the variable with the sequence number expected is updated.

If the payload cannot be directly copied into the user-address space, then the availability of buffer memory in the socket is checked, statistical-information is updated, the TCP packet header is removed, and, finally, the variable with the sequence number expected is updated.

If the payload cannot be directly copied into the user-address space, then the availability of buffer memory in the socket is checked, statistical information is updated, the TCP packet header is removed, and, finally, the variable with the sequence number expected is updated.

## Chapter 24 Transmission Control Protocol (TCP)

These actions complete the process of handling a received segment section is only an overview of handling incoming segments. At some point, we mentioned functions in Fast Path or Slow Path, we didn't explain them in detail. For this reason, we will briefly describe these functions.

### Helper Functions for Handling Incoming Segments

tcp_ack() ... net/ipv4/tcp_input.c

tcp_ack(sk, th, ack_seq, len) handles all tasks involved in receiving an acknowledgement or a data packet with valid ACK (piggybacking):

- Adapt the receive window (tcp_update_window).
- Delete acknowledged packets from the retransmission queue (tcp_clean_retx_queue).
- Check for Zero Window Probing.
- Adapt the connection window (tcp_may_raise_cwnd).
- Update the packet round-trip time (RTT) and the timeout for retransmissions (Retransmission Timeout—RTO).
- Retransmit packets and update the retransmission timer.
- Activate the Fast Retransmit mode, if necessary.

tcp_event_data_recv() ... net/ipv4/tcp_input.c

tcp_event_data_recv(tp, skb) handles all management work required for payload. This includes the maximum segment size, and the timer for delayed acknowledgments (Acknowledgement Timeout—ATO).

tcp_data_snd_check() ... net/ipv4/tcp_input.c

tcp_data_snd_check(sk) checks on whether data is ready and waiting in the transmit queue, and it starts the transmission, if permitted by the transmit window of the sliding-window mechanism and the congestion-control window. The actual mission is initiated by tp_write_xmit():

