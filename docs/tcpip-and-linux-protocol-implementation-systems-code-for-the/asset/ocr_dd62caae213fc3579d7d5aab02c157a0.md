# Protocol Implementation Framework 133

+   * stupid piece of technology.
* If we are handling an interrupt on the other CPU cannot load a packet
* as we may still be attempting to retrieve the last RX packet buffer.
* When a transmit times out dump the card into control mode and
* start again. It happens enough that it isnt worth logging.
* We avoid holding the spin locks when the packet load to the board.
* The device is very slow, and DMA mode is even slower. If we held the
* lock while loading 1500 bytes into the controller we would drop a lot of
* serial port characters. This requires we do extra locking, but we have
* no real choice.

The new few code extracts show the continuation of the transmission startup code. Essentials (as the comments indicate), we are telling the card that there is data ready to send, and where it is, then we tell it to go away and send it, and interrupt us when we need.

Figure 5.32 Ethernet driver 2--tstart: linux/drivers/net/3c501.c.

```
static int el_start_xmit(struct sk_buff *skb, struct net_device *dev)
{
    struct net_local *lp = (struct net_local *)dev->priv;
    int ioaddr = dev->base_addr;
    unsigned long flags;

    /*
     Avoid incoming interrupts between us flipping txing and flipping
     mode as the driver assumes txing is a faithful indicator of card
    */

    spin_lock_irqsave(lp->lock, flags);
    /*
     Avoid timer-based retransmission conflicts.
    */

    netif_stop_queue(dev);
```

Figure 5.33 Ethernet driver 2--tstart b: linux/drivers/net/3c501.c.

```
do
{
    int gp_start = 0x800 - (ETH_ZLEN < skb->len ? skb->len : ETH_ZLEN);
    unsigned char *buf = skb->data;
```