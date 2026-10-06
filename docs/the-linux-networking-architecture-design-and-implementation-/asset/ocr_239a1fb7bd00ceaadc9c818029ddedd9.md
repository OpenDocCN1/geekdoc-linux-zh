# Chapter 24 Transmission Control Protocol (TCP)

These actions complete the process of handling a received TCP segment section is only an overview of the rough process involved in handling incoming segments. At some point, we mentioned functions invoked in Fast Path or Slow Path, we didn't explain them in detail. For this reason, we will briefly describe these functions in the following subsection.

# Helper Functions for Handling Incoming TCP Segments

tcp_ack() ... net/ipv4/tcp_input.c

tcp_ack(sk, th, ack_seq, ack, len) handles all tasks involved in receiving an acknowledgement packet or a data packet with valid ACK number (piggybacking):

+   - Adapt the receive window (tcp_ack_update_window).
- Delete acknowledged packets from the retransmission queue (tcp_clean_retx_queue).
- Check for Zero Window Probing acknowledgement.
- Adapt the connection window (tcp_may_raise_cwnd).
- Update the packet round-trip time (RTT) and the timeout for packet retransmissions (Retransmission Timeout—RTO).
- Retransmit packets and update the retransmission timer.
- Activate the Fast Retransmit mode, if necessary.

tcp_event_data_recv() ... net/ipv4/tcp_input.c

tcp_event_data_recv(tp, skb) handles all management work required for receiving payload. This includes the maximum segment size, and the timer for delayed acknowledgments (Acknowledgement Timeout—ATO).

tcp_data_snd_check() ... net/ipv4/tcp_input.c

tcp_data_snd_check(sk) checks on whether data is ready and waiting in the transmit queue, and it starts the transmission, if permitted by the transmit window of the sliding-window mechanism and the congestion-control window. The actual mission is initiated by tp_write_xmit():

```
static __inline__ void tcp_data_snd_check(struct sock *sk) {
    struct sk_buff *skb = sk->tp_pinfo.af_tcp->snd_head;
    struct tcp_opt *opt = &(sk->tp_pinfo.af_tcp->snd_snd);

    if (skb == NULL) {
        if (after(TCP_SK_CB(skb)->end_seq, tp->snd_una + tp->snd_snd) ||
            tcp_packets_in_flight(tp) >= tp->snd_cwnd ||
            tcp_check_probe_timer(sk, tp))
    }
    tcp_check_space(sk);
}
```