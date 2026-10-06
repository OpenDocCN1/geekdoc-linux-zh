# Chapter 24 Transmission Control Protocol (TCP)

There are various functions to manage the keepalive timer:

```
tcp_delete_keepalive_timer()                               net/ipv4/tcp_timer.c
```

The function tcp_keepalive_timer(sk) removes the keepalive timer from the list of timer_list structures.

```
tcp_reset_keepalive_timer()                               net/ipv4/tcp_timer.c
```

The function tcp_reset_keepalive_timer(sk, len) sets the timer to value jiffies + len.

```
tcp_keepalive_timer()                               net/ipv4/tcp_timer.c
```

The function tcp_keepalive_timer(data) is the behavior function for the keepalive timer. When this function is invoked, the state of the connection is checked to decide whether this connection should be terminated. This function implements various logically separated TCP timers. In addition to the SYNACK timer described here, it implements the timeout in the FIN_WAIT_2 state and the actual keepalive timer.

**Retransmit Timer** The client's TCP instance sends a SYN packet to the server and waits for an answer (with SYN and ACK) while the connection-establishment phase is active. At the same time, tcp_connect() (in net/ipv4/tcp_output.c) and the function tcp_reset_xmit_timer(sk, TCP_TIME_RETRANS, tp->rto) are used to set the retransmit timer to the value TCP_TIMEOUT_INIT. TCP_TIMEOUT_INIT is set to the value 3*HZ in the file include/net.h.
The retransmit timer is also used when the connection is established and running. The duration of the retransmission timeout is doubled, in the tcp_retransmit_timer() function (net/ipv4/tcp_timer.c), upon each retransmission, until it has arrived at the maximum and the connection is reset:

```
tp->rto = min(1, RTO_MAX);
    tcp_reset_xmit_timer(sk, TCP_TIME_RETRANS, tp->rto);
    if (tp->retransmits > sysctl_tcp_retransries1)
        sk_dst_reset(sk);
```

The retransmit timer is initialized to the retransmission timeout (RTO), which is recalculated by use of various helper functions:

```
tcp_set_rto()                                   net/ipv4/tcp_input.c
```

This function computes the RTO (retransmission timeout) from the round-trip time values.