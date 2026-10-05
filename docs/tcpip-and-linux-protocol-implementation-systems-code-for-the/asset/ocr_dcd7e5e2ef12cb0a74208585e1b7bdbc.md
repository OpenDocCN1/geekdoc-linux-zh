```
/* 4.1.3.4. It's configurable by the application setsockopt() */
/* (MAY) and it defaults to on (MUST). */
```

```
err = ip_build_xmit(
    (skb)->no_check == UDP_CSUM_NOXIT ?
    udp_getfrag_nosum :
    udp_getfrag(),
    ufh, ulen, ipc, rt, msg->msg_flags);
```

# 3.3.2 UDP Input

UDP is small enough that it is all in one C file. For receive, the function of interest is udp_recvmsg().

Figure 3.13 UDP input: linux/net/ipv4/udp.c.

```
skb = skb_recv_datagram(sk, flags, noblock, &err);
if (!skb) {
    goto out;

    copied = skb->len - sizeof(struct udphdr);
    if (copied > len) {
        copied = len;
        msg->msg_flags |= MSG_TRUNC;
    }
\if (skb)->ip_sum==CHECKSUM_UNNECESSARY) {
    err = skb_copy_datagram_iov(skb, sizeof(struct udphdr), msg->msg_iov,
        copied);
} else if (msg->msg_flags&MSG_TRUNC) {
    if (skb)->checksum_complete(skb)) {
        goto csum_copy_err;
    }
    err = skb_copy_datagram_iov(skb, sizeof(struct udphdr), msg->msg_iov,
        copied);
} else {
    err = copy_and_checksum_tolovec(msg->msg_iov, skb, sizeof(struct udphdr));
}

if (err) {
    goto csum_copy_err;
}

if (err) {
    goto out_free;
}
nsock_recv_timestamp(msg, skb);
/* Copy the address. */
if (sin) {
    sin->sin_family = AF_INET;
    sin->sin_port = skb->uh->hs_source;
```