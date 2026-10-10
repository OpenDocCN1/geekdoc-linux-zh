```
to DMA this received packet */
packet_size = mydev_data->dma_buffer_rx[1];
/* In real world drivers, the sk_buff is pre-allocated, stream-
mapped, and supplied to the card after setting the FREE_FLAG
during device open(). The received data is directly
DMA'ed to this sk_buff instead of the memcpy() performed here,
as you will learn in Chapter 15. The card clears the FREE_FLAG
before the DMA */
skb = dev_alloc_skb(packet_size); /* See Figure 15.2 of Chapter 15 */
skb->dev = mydev_data->ndev; /* Owner network device */
memcpy(skb, mydev_data->dma_buffer_rx[24], packet_size);
/* Pass the received data to higher-layer protocols */
skb_put(skb, packet_size);
netif_rx(skb);
/* ... */
/* Make the descriptor available to the card again */
mydev_data->dma_buffer_rx[2] |= FREE_FLAG;
}

/* This function is registered in Listing 10.3 and is called from
the networking layer. More on network device interfaces in
Chapter 15 */
static int
mydevce_xmit(struct sk_buff *skb, struct net_device *dev)
{
/* Use a valid TX descriptor. Look at Figure 10.2 */
/* Locking has been omitted for simplicity */
if (mydev_data->dma_buffer_tx[2] & FREE_FLAG) {
/* Use first TX descriptor */
/* In the real world, DMA occurs directly from the sk_buff as
you will learn later on! */
memcpy(mydev_data->dma_buffer_tx[24], skb->data, skb->len);
mydev_data->dma_buffer_tx[1] = skb->len;
mydev_data->dma_buffer_tx[2] &= ~FREE_FLAG;
mydev_data->dma_buffer_tx[2] |= INTERRUPT_FLAG;
} else if (mydev_data->dma_buffer[5] & FREE_FLAG) {
/* Use second TX descriptor */
memcpy(mydev_data->dma_buffer_tx[1560], skb->data, skb->len);
mydev_data->dma_buffer_tx[4] = skb->len;
mydev_data->dma_buffer_tx[5] &= ~FREE_FLAG;
mydev_data->dma_buffer_tx[5] |= INTERRUPT_FLAG;
} else {
return -EIO; /* Signal error to the caller */
}
wmb(); /* Don't reorder writes across this barrier */

/* Ask the card to initiate DMA. ioaddr is defined
in Listing 10.3 */
outl(INITIATE_XMIT, ioaddr + CONTROL_REGISTER);
}
```

When the CardBus device receives an Ethernet packet, it DMAs it to a free RX descriptor and interrupts the CPU. The interrupt handler mydevice_interrupt() collects the packet from the receive DMA buffer, copies it to a networking data structure (sk_buff), and passes it on to higher protocol layers.