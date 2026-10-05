# 502 TCP/IP and Linux Protocol Implementation

Figure 7.28 Finding space to copy the data to (i).

```
```c
1078  /* Where to copy to if? */
if (skb_tailroom(skb) > 0) {
    /* We have some space in skb head. Super! *
    if (copy > skb_tailroom(skb)) {
        copy = skb_tailroom(skb);
        if ((err == skb_add_data(skb, from, copy)) != 0)
            goto do_fault;
    }
} else {
    int merge = 0;
    int i = skb_shinfo(skb)->nr_frags;
    struct page *page = TCP_PAGE(skb);
    int off = -TCP_OFF(sk);
    if (can_coalesce(skb, i, page, off) && off != PAGE_SIZE) {
        /* We can extend the last page fragment. *
        merge = 1;
    } else if (i == MAX_SKB_FRAGS) {
        if (i == 0 && !(sk->route_cache&NETIF_F_SG)) {
             /* Need to add new fragment and cannot */
             * do this because interface is not-SG,
             * or because all the page slots are busy.
             */
            tcp_mark_push(tp, skb);
            goto next_segment;
    }
    } else if (page) {
        /* If page is cached, aligned
         * offset to L1 cache boundary
         */
        off = (off+L1_CACHE_BYTES-1)&(L1_CACHE_BYTES-1);
        if (off == PAGE_SIZE) {
            put_page(page);
            TCP_PAGE(skb) = page = NULL;
        }
}
if (!page) {
    /* Allocate new cache page. */
    if (!(page=tcp_alloc_page(skb))
        goto wait_for_memory;
}
off = 0;
```
```
```

Figure 7.29 Finding space to copy the data to (ii).

```
```c
if (copy > PAGE_SIZE-off) {
    copy = PAGE_SIZE-off;
}
/* Time to copy data. We are close to the end! */
err = tcp_copy_to_page(sk, from, skb, page, off, copy);
if (err)
```
```