# Transport 503

```
goto do_error;
/* Update the skb. */
if (merge) {
    skb_shinfo(skb)->frags[i-1].size += copy;
} else {
    full_page_desc(sk, i, page, off, copy);
    if (TCP_PAGE(sk)) {
        get_page(page);
    } else if (off + copy < PAGE_SIZE) {
        get_page(page);
        TCP_PAGE(sk) = page;
    }
}
TCP_OFF(sk) = off+copy;
```

We now loop through the message blocks and build segments. As TCP is byte-oriented, the blocks can be divided and joined in order to achieve full segments where possible. The first socket buffer at the end of the write queue is examined. If this doesnt exist (say because it has been transmitted and acknowledged) or it is full, a new socket buffer is allocated. If there is room, the space left is calculated. By the end of Figure 7.27, copy contains the number of bytes that can be added to this sk_buff.

# Figure 7.30 Rest of tcp send.

```
if (!copied)
    TCP_SKB_CB(skb)->flags &= ~TCPCB_FLAG_PSH;
    tp->write_seq += copy;
    TCP_SKB_CB(skb)->end_seq += copy;
    from += copy;
    copied += copy;
    segl -= copy;
    if (skb->len != mss_now || (flags&MSG_OOB))
        continue;
    if (forced_push(tp)) {
        tcp_mark_push(tp, skb);
        __tcp_push_pending_frames(sk, tp, mss_now, 1);
    } else if (skb == tp->send_head) {
        tcp_push_one(sk, mss_now);
    continue;
wait_for_sndbuf;
```