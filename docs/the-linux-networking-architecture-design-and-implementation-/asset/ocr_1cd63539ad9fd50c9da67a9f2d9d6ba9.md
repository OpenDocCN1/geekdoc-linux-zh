# 494 Chapter 24 Transmission Control Protocol (TCP)

```
void tcp_send_probe0(struct sock *sk)
{
    struct tcp_opt *tp = &(sk->tp_pinfo.af_tcp);
    int err;
    err = tcp_xmit_wakeup(sk);
    if (tp->packets_out || !tp->send_head) {
        /* Cancel probe timer, if it is not required. */
        tp->probes_out = 0;
        tp->backoff = 0;
        return;
    }
    if (err <= 0) {
        tp->backoff++;
        tp->probes_out++;
        tcp_reset_xmit_timer(sk, TCP_TIME_PROBE, min(tp->rto << tp->backoff, TCP_RTO_MAX));
    }
}
```

tcp_send_probe0(struct sock *sk) uses tcp_wakeup to generate and send a zero-window probe packet. If the probe timer is no longer needed, been from the fact that there is currently nothing to be sent (tp->send_head == NULL), or if there are still packets currently under way and their ACKs could contain new credits, it is not restarted, and the probes_out and backoff parameters are reset.
Otherwise, these parameters are incremented after a probe packet has been sent, and the zero-window probe timer is restarted, so that it expires again after some time. This time is tp->rto*2^tp->backoff or a maximum of TCP_RTO_MAX (120 seconds).

```
tcp_xmit_wakeup(struct sock *sk)
net/ipv4/tcp_output.c
```

```
{
    if ((skb != tp->send_head) != NULL &&
        before(TCP_SKB_CB(skb)->seq, tp->send_una+tp->send_snd))
        {
            (...)
            /* We are probing the opening of a window
               * but the window size is != 0
               * must have been a result SWS avoidance ( sender ) */
            (...)
            err = tcp_transmit_skb(sk, skb_clone(skb, GFP_ATOMIC);
            (...)
        }
    }
else {
    tcp_xmit_probe_skb(sk);
```