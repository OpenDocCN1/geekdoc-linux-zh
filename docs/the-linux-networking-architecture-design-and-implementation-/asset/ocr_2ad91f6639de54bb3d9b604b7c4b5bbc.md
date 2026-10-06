# 96 Chapter 5 Network Devices

```
/*
* For Ethernet adaptors the first three octets of the station address
* contains the manufacturer's unique code. That might be a good probe
* method. Ideally you would add additional checks.
*/
if (inb(ioaddr + 0) != SA_ADDR0
    inb(ioaddr + 1) != SA_ADDR1
    inb(ioaddr + 2) != SA_ADDR2) {
    return -ENODEV;
}
```

```
if (net_debug && KERN_DEBUG == 0)
    printk(KERN_INFO "%s: %s found at #%x, " dev->name, cardname, ioaddr);
```

```
/* Fill in the 'dev' fields. */
dev->base_addr = ioaddr;
```

```
/* Retrieve and fill the Ethernet address. */
for (i = 0; i < 6; i++)
    printk("%2.x", dev->dev_addr[i] = inb(ioaddr + i));
```

```
##ifdef jumper_interrupts
/* if this board has jumped interrupts, allocate the interrupt
* vector now. There is no point in waiting since no other device
* can use the interrupt, and this marks the irq as busy.
* interrupts are typically not reported by the boards, and we must
* used AUTOIRQ to find them. */
/* ... REMOVED for this book, details see in drivers/net/isa-skeleton.c */
#endif /* jumped interrupt */
```

```
##ifdef jumper_dma
/* if we use a DMA channel, that should be probed for and
* allocated here as well. Lance.c for an example. */
/* ... REMOVED for this book, details see in drivers/net/isa-skeleton.c */
#endif /* jumped dma */
```

```
/* Initialize the device structure. */
if (dev->priv == NULL)
    dev->priv = kmalloc(sizeof(struct net_local), GFP_KERNEL);
    return -ENOMEM;
```