```
```
mydev_data->dma_buffer_tx[0] = cpu_to_le32((unsigned long)
(mydev_data->dma_bus_tx + 24));  /* Buffer address */
mydev_data->dma_buffer_tx[1] = 1536;        /* Buffer length */
/* Valid descriptor. Generate an interrupt
   after completing the DMA */
mydev_data->dma_buffer_tx[2] = (FREE_FLAG | INTERRUPT_FLAG);
/* TX descriptor 2 */
mydev_data->dma_buffer_tx[3] = cpu_to_le32((unsigned long)
(mydev_data->dma_bus_tx + 1560)); /* Buffer address */
mydev_data->dma_buffer_tx[4] = 1536;        /* Buffer length */
mydev_data->dma_buffer_tx[5] = (FREE_FLAG | INTERRUPT_FLAG);

wmb(); /* Write Memory Barrier */
/* Write the address of the transmit descriptor to the appropriate
   register in the card. The I/O base, ioaddr, was populated in
   Listing 10.3 */
outl(cpu_to_le32((unsigned long)mydev_data->dma_bus_tx),
     ioaddr + DMA_TX_REGISTER_OFFSET);
}

/* Invoked from Listing 10.3 */
static void
dma_descriptor_release(struct pci_dev *pdev)
{
    pci_free_consistent(pdev, 3096, mydev_data->dma_bus_tx);
    pci_free_consistent(pdev, 3096, mydev_data->dma_bus_rx);
}
```
```

Listing 10.5 enforces a write barrier by calling `wmb()` to prevent the CPU from reordering the `outl()` before populating the DMA descriptor. On an x86 processor, `wmb()` reduces to a NOP because Intel CPUs enforce writes in program order. When writing the DMA descriptor address to the card and when populating the buffer’s bus address inside the DMA descriptor, the driver converts the native byte order to PCI little-endian format using `cpu_to_le32()`. On Intel CPUs, this again has no effect because both PCI and Intel processors communicate in little-endian. On several other architectures, for example, an ARM9 CPU running in the big-endian mode, both `wmb()` and `cpu_to_le32()` assume significance.

Now that you have the descriptors and buffers mapped and ready to go, it’s time to look at how data is exchanged between the system and the CardBus device, as shown in Listing 10.6. We won’t dwell on the network interfaces and networking data structures because Chapter 15 is devoted to doing that.

# ### Listing 10.6. Receiving and Transmitting Data

```
```
Code View:
/* The interrupt handler */
static irqreturn_t
mydevice_interrupt(int irq, void *dev_id)
{
    struct sk_buff *skb;
/* ... */
/* If this is a receive interrupt, collect the packet and pass it
   on to higher layers. Look at the control word in each RX DMA
   descriptor to figure out whether it contains data. Assume for
   convenience that the first RX descriptor was used by the card
```
```