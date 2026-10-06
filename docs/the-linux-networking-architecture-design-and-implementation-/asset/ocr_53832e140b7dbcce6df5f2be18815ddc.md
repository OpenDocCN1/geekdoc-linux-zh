# 24.2 Implementing the TCP Protocol Instance 473

```
u32 srtt; /* smoothed round trip time << 3 *
uu32 mdev; /* medium deviation *
uu32 mdev_max; /* maximal mdev for the last rtt period *
uu32 rttvar; /* smoothed mdev_max *
uu32 rttvar_seq; /* sequence number to update rttvar *
uu32 rto; /* retransmit timeout *
uu32 packets_out; /* Packets which are "in flight" *
uu32 left_out; /* Packets which left network *
uu32 retrans_out; /* Retransmitted packets out */
```

```
/ Slow start and congestion control (see also Nagel & Karn & Part.) */
uu32 snd_sstresh; /* Slow start size threshold *
uu32 cwnd; /* Sending congestion window *
uu16 cwnd_cnt; /* Linear increase counter *
u16 cwnd_clamp; /* Do not allow snd_cwnd to grow above this *
uu32 cwnd_used; 
```

```
/ Two commonly used timers in both sender and receiver paths.
unsigned long timeout;
struct timer_list retransmit_timer; /* Resend (no ack) *
struct timer_list delack_timer; /* Ack delay *
struct sk_buf head_out_of_order_queue; /* Out of order segments here */
struct tcp_func *af_specific; /* AF_INET{4,6} specific operations *
struct sk_buf *send_head; /* Front of stuff to transmit *
u32 rcv_wnd; /* Current receiver window *
u32 rcv_wup; /* rcv_next on last window update sent *
u32 write_seq; /* Tail(+1) of data held in tcp send buffer *
u32 pushed_seq; /* Last pushed seq, required to talk to windows *
u32 copied_seq; /* Head of yet unread data */
```

```
/ Options received (usually on one SYN packets) */
char timestamp_op; /* TIMESTAMP seen on SYN packet *
char wscale_ok; /* Wscale seen on SYN packet *
char sack_out; /* SACK seen on SYN packet *
char saw_timestamp; /* Saw TIMESTAMP on last packet *
u8 snd_wscale; /* Window scaling received from sender *
u8 rcv_wscale; /* Window scaling to send to receiver *
u8 nonagle; /* Disable Nagle algorithm? *
u keepalive_probes; /* num of allowed alive probes
```

```
/ PAWS/RTT data */
uu32 rcv_tsval; /* Time stamp value *
uu32 rcv_tssec; /* Time stamp echo reply *
uu32 ts_recent; /* Time to echo to next *
long ts_recent_stamp; /* Time we stored ts_recent (for aging) */
```

```
/ Sacks data */
u16 user_mss; /* mss requested by user in ioctl */
```