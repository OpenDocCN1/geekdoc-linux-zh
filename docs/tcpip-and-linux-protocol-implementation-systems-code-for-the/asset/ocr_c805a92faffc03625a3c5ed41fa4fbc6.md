```
if (!ack_scheduled(tp))
    goto no_ack;

}

if (eaten) {
```

tcp_v4_do_rcv (see Figure 7.41) in the connection setup section fast-paths if the socket is in an established state to tcp_rcv_established, this being the most common state, and also that which requires fastest processing.

# Figure 7.44 Receiving a socket buffer on an established connection (iv).

```
if (tcp_im_quickack_mode(tp)) {
    tcp_send_ack(sk);
} else {
    tcp_send_delayed_ack(sk);
}
else {
    __tcp_ack_snd_check(sk, 0);
}

no_ack:
if (eaten) {
    __kfree_skb(skb);
} else {
    sk->data_ready(sk, 0);
    return 0;
}

low_path:
if (len < (th->doffff<<2) || tcp_checksum_complete_user(sk, skb)) {
    goto csum_error;
}
/*
 * RFC 1238: Apply PAWS checks first.
 */
if (tcp_fast_parse_options(sk, th, tp) && tp->saw_tstamp &&
    tcp_paws_discard(tp, sk)) {
    if (th->rst) {
        NET_INC_STATS_BH(PAWsetabRejected);
        tcp_send_dupack(sk, skb);
        goto discard;
    }
}
/* Resets are accepted if PAWS failed.
ts_recent update must be made after we are sure
   that the packet is in window.
 */
```