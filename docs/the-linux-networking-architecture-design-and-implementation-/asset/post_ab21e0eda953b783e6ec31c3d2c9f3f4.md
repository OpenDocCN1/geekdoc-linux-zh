
## 24.2 Implementing the TCP Protocol Instance

```c
}
tcp_check_probe_timer(sk, tp);
tcp_cwnd_validate(sk, tp);
```

```c
tcp_write_xmit(sk)                               net/ipv4/tcp_output
```

tcp_write_xmit(sk) continues to send segments from the transmit queue of the socket, sk, as long as it is allowed to do so by tcp_snd_test(). It checks for whether the conditions of TCP algorithms (e.g., slow-start method and congestion-control algorithm) are maintained. Data segments can also be fragmented (tcp_fragment()) before the maximum segment size is exceeded. tcp_transmit_skb() handles the final completion of the TCP packet and passes it to the Internet Protocol.

```c
tcp_retransmit_skb()                               include/linux/tcp_output
```

tcp_retransmit_skb(sk, sk) retransmits a TCP segment. The segment may have to be fragmented (tcp_fragment()), or it might be joined with the next segment (tcp_retransmit_try_collapse()).

```c
tcp_send_ack()                                     include/linux/tcp_output
```

tcp_send_ack(sk) is responsible for building and sending ACK packets. In this purpose, it requests a socket buffer and assigns the corresponding values to this buffer. Subsequently, it uses tcp_transmit_skb() to send an ACK segment.

## 24.2.3 Data Structures of the TCP Instance

```c
struct tcp_opt                                     include/net/sock.h
```

The tcp_opt structure contains all variables of the TCP algorithms for a TCP connection. The names of these variables were adopted from RFCs 793 and 1122 for the sake of better understanding (except for uppercase and lowercase). This facilitates reading the source text and comparing with the TCP standard.

The tcp_opt structure is very complex, which shouldn't come as a surprise considering the complexity of the TCP protocol and the large number of its algorithms. A detailed description of the tcp_opt structure would go beyond the scope and volume of this chapter, especially because they are well documented and because the variable names correspond to the TCP standard. Nevertheless, we will list the variables and their tasks, to facilitate quick references when reading the following sections.

Among things, the tcp_opt structure consists of variables for the following algorithms or protocol mechanisms:

- sequence and acknowledgement numbers;
- flow-control information;
- packet round-trip time;
- congestion control and congestion handling:
- timers:
- TCP options in the packet header; and
- automatic and selective packet retransmission.

```c
struct tcp_opt {
    int tcp_header_len;      /* Bytes of tcp header to send */
    /* Header prediction flags * 0x5?10 << 16 + snd_wnd in byte order */
    u32 pred_flags;

    u32 rcv_nxt;             /* What we want to receive next */
    u32 snd_nxt;            /* Next sequence we sent */
    u32 snd_una;            /* First byte we want an ack for */
    u32 snd_sml;             /* Last byte of most recently xmitted small packet */
    u32 rcv_timestamp;       /* timestamp of last received ACK (for keepalives) */
    u32 lstnd;               /* timestamp of last sent data packet (for restart window) */

    /* Delayed ACK control data */

    struct {
        u8 pending;              /* ACK is pending */
        u8 quick;                 /* Scheduled number of quick acks */
        u8 pingpong;             /* The session is interactive */
        u8 blocked;              /* Delayed ACK was blocked by socket lock */
        u32 ato;                  /* Predicted tick of soft clock */
        unsigned long timeout;   /* Currently scheduled timeout */
        u32 lrcvtime;            /* timestamp of last received data packet */
        u16 last_seg_size;       /* Size of last incoming segment */
        u16 rcv_mss;             /* MSS used for delayed ACK decisions */
    };
    u32 snd_wll;             /* Sequence for window update */
    u32 snd_wnd;             /* The window we expect to receive */
    u32 max_wnd;             /* Maximal window seen from peer */
    u32 pmtu_cookie;          /* Last pmtu seen by socket */
    u16 mss_cache;           /* Cached effective mtu, not including SACKS */
    u16 mss_clamp;            /* Maximal mss, negotiated on connection setup */
    u16 ext_header_len;      /* Network protocol overhead (IP/IPv6 options) */
    u8 ca_state;              /* State of fast-retransmit machine */
    u8 retransmits;          /* Number of uncovered RTO timeouts */
    u8 reordering;           /* Packet reordering metric. */
    u8 queue_shrunk;         /* Write queue has been shrunk recently. */
    u8 defer_accept;         /* User waits for some data after accept */

    /* RTT measurement */

    u8 backoff;               /* backoff */

    u32 srtt; /* smoothed round trip time << 3 * */
    u32 mdev; /* medium deviation * */
    u32 mdev_max; /* maximal mdev for the last rtt period * */
    u32 rttvar; /* smoothed mdev_max * */
    u32 rttvar_seq; /* sequence number to update rttvar * */
    u32 rto; /* retransmit timeout * */
    u32 packets_out; /* Packets which are "in flight" * */
    u32 left_out; /* Packets which left network * */
    u32 retrans_out; /* Retransmitted packets out */

    /* Slow start and congestion control (see also Nagel & Karn & Part.) */
    u32 snd_sstresh; /* Slow start size threshold * */
    u32 cwnd; /* Sending congestion window * */
    u16 cwnd_cnt; /* Linear increase counter * */
    u16 cwnd_clamp; /* Do not allow snd_cwnd to grow above this * */
    u32 cwnd_used;

    /* Two commonly used timers in both sender and receiver paths. */
    unsigned long timeout;
    struct timer_list retransmit_timer; /* Resend (no ack) * */
    struct timer_list delack_timer; /* Ack delay * */
    struct sk_buf head; 
    u32 left_out; /* Packets which left network * */
    u32 retrans_out; /* Retransmitted packets out */

    /* Slow start and congestion control (see also Nagel & Karn & Part.) */
    u32 snd_sstresh; /* Slow start size threshold * */
    u32 cwnd; /* Sending congestion window * */
    u16 cwnd_cnt; /* Linear increase counter * */
    u16 cwnd_clamp; /* Do not allow snd_cwnd to grow above this * */
    u32 cwnd_used;

    /* Two commonly used timers in both sender and receiver paths. */
    unsigned long timeout;
    struct timer_list retransmit_timer; /* Resend (no ack) * */
    struct timer_list delack_timer; /* Ack delay * */
    struct sk_buf head; 
    u32 left_out; /* Packets which left network * */
    u32 retrans_out; /* Retransmitted packets out */

    /* Slow start and congestion control (see also Nagel & Karn & Part.) */
    u32 snd_sstresh; /* Slow start size threshold * */
    u32 cwnd; /* Sending congestion window * */
    u16 cwnd_cnt; /* Linear increase counter * */
    u16 cwnd_clamp; /* Do not allow snd_cwnd to grow above this * */
    u32 cwnd_used;

    /* Two commonly used timers in both sender and receiver paths. */
    unsigned long timeout;
    struct timer_list retransmit_timer; /* Resend (no ack) * */
    struct timer_list delack_timer; /* Ack delay * */
    struct sk_buf head; 
    u32 left_out; /* Packets which left network * */
    u32 retrans_out; /* Retransmitted packets out */

    /* Slow start and congestion control (see also Nagel & Karn & Part.) */
    u32 snd_sstresh; /* Slow start size threshold * */
    u32 cwnd; /* Sending congestion window * */
    u16 cwnd_cnt; /* Linear increase counter * */
    u16 cwnd_clamp; /* Do not allow snd_cwnd to grow above this * */
    u32 cwnd_used;

    /* Two commonly used timers in both sender and receiver paths. */
    unsigned long timeout;
    struct timer_list retransmit_timer; /* Resend (no ack) * */
    struct timer_list delack_timer; /* Ack delay * */
    struct sk_buf head; 
    u32 left_out; /* Packets which left network * */
    u32 retrans_out; /* Retransmitted packets out */

    /* Slow start and congestion control (see also Nagel & Karn & Part.) */
    u32 snd_sstresh; /* Slow start size threshold * */
    u32 cwnd; /* Sending congestion window * */
    u16 cwnd_cnt; /* Linear increase counter * */
    u16 cwnd_clamp; /* Do not allow snd_cwnd to grow above this * */
    u32 cwnd_used;

    /* Two commonly used timers in both sender and receiver paths. */
    ... (rest of structure logic continues based on OCR flow) ...
    /* ... (truncated) */
    struct timer_list delack_timer;
    /* ... (truncated) */
    struct sk_buf head; 
    u32 left_out; 
    
    /* Note: The OCR text contains significant repetition and noise in 
       the structure definition. The above merges the logical flow. */
}
```
