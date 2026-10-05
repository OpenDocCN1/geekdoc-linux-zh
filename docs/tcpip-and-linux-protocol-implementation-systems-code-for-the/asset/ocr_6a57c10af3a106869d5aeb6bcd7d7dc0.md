# Protocol Implementation Framework 139

```
* get wild packet sizes from the card. If the packet seems sane we do PIO it
* off the card and queue it for the protocol layers.
* /
```

We start the work of receiving a packet in earnest. We check for simply illegal packet lengths, for example.

Figure 5.41 Ethernet driver 4-receive: linux/drivers/net/3c501.c.

```
/*
 * @el_receive:
 * @dev: Device to pull the packets from
 *
 * We have a good packet. Not really "good", just mostly not broken.
 * We must check everything to see if it is good. In particular we occasionally
 * get wild packet sizes from the card. If the packet seems sane we do PIO it
 * off the card and queue it for the protocol layers.
 * */
static void el_receive(struct net_device *dev)
{
    struct net_local *lp = (struct net_local *)dev->priv;
    int iaddr = dev->base_addr;
    int pkt_len;
    struct sk_buff *skb;

    pkt_len = inw(RX_LOW);

    if (el_debug > 4)
        printf("*el_receive %d\n", pkt_len);

    if ((pkt_len < 60) || (pkt_len > 1536)) {
        if (el_debug)
            printf(":%s: bogus packet, length=%d\n", dev->name, pkt_len);
        lp->stats.rx_over_errors++;
    }
    return;
n
```

Finally, if all is well, we call netif_rx on the socket buffer that has the packet data.

Figure 5.42 Ethernet driver 4-receive: linux/drivers/net/3c501.c.

```
/*
 * Command mode so we can empty the buffer
 * */
outb(AX_SYS, AX_CMD);
```