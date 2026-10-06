# skb_get() include/linux/skbuff.h

This increments the number of user references to the skb_buff structure by one.

# skb_unshare() include/linux/skbuff.h

skb_unshared(skb) uses skb_cloned to check for the socket buffer is available for exclusive use. If it isn't, then a copy of skb is created and returned so that an exclusive socket buffer is available. In the original packet, the reference counter is decremented by a value of one.

# skb_put() include/linux/skbuff.h

skb_put(skb, len) is an inline function that appends data to the end of the current data range of a packet. Though this occurs seldom, because most protocols write their PCI (Protocol Control Information) before the current packet data unit, there are a few protocols, that require this. More specifically, skb_put() increments the point-tail and the parameter skb->len by len. Note that skb_put() merely sets the point again; the caller is responsible for copying the correct data to the packet data space, so to be able to add new packet data to the correct place. Before calling skb_put(), we should confirm that the tailroom is sufficient (the old value of skb->tail),; otherwise, the kernel will output an error message and call skb_over_panic().

# skb_push() include/linux/skbuff.h

skb_push(skb, len) works like skb_put(), but increases the current packet data space at the beginning of the packet by len bytes. This means the data-point is decremented by len, and skb->len is incremented by this amount. The return value of skb_push() points to the new data space (skb->data; in this case). Again, we should first check the headroom size.

# skb_pull() include/linux/skbuff.h

skb_pull(skb, len) serves to truncate len bytes at the beginning of a packet. The pointer skb->data is adjusted, and the length of the packet (skb->len) is reduced accordingly—but, first we check on whether there are still bytes in the free part of the packet data space.

# skb_tailroom() include/linux/skbuff.h

skb_tailroom(skb) returns the bytes still free at the end of the data space. If skb_put() requests more data in this space skb_tailroom states, then this will lead to a kernel panic.