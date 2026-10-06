> * If some error occurs while trying to transmit this
* packet, you should return '1' from this function.
* In such a case you may not_ do anything to the
* SKB, it is still owned by the network queuing
* layer when an error is returned. This means you
* may not modify any SKB fields, you may not free
* the SKB, etc.
/

```
#if TX_RING
/* This is the most common case for modern hardware.
* The spinlock protects this code from the TX complete
* hardware interrupt handler. Queue flow control is
* thus managed under this lock as well.
*/
spin_lock_irq(&np)->lock);

add_to_tx_ring(np, skb, length);
dev->trans_start = jiffies;

/* If we just used the very last entry in the
* TX ring on this device, tell the queuing
* layer to send no more.
*/
if (tx_full(dev))
netif_stop_queue(dev);

/* When the TX completion hw interrupt arrives,
* is the transmit statistics are updated.
*/

spin_unlock_irq(&np)->lock);
elelse
/* This is the case for older hardware which takes
* a single transmit buffer at a time, and it is
* just written to the device via PIO.

* No spin locking is needed since there is no TX complete
* event. If by chance your card does have a TX complete
* hardware IRQ you may need to utilize np->lock here.
*/
hardware_send_packet(ioaddr, buf, length);
p->stats.tx_bytes += skb->len;

dev->trans_start = jiffies;

/* might need to clean up and record TX statistics. here */
if (inw(ioaddr) == /*RU*/81)
np->stats.tx_aborted_errors++;
```