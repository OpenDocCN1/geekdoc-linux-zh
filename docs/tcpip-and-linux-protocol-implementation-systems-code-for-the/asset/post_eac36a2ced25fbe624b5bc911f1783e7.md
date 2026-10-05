
## 3c501 Interrupt Handling

At the top level, we have to handle a generic device interrupt from this device and figure figure out then what actually happened that it is trying to tell us about (i.e., another example of demultiplexing).

Figure 5.35 Ethernet driver 3–interrupt a1: linux/net/drivers/3c501.c.

```
581      /*
582
583      * What happened ?
584      */
585
586      axsr = inb(AX_STATUS);
587
588      /*
589      * Log it
590      */
591
592      if (el_debug > 3)
593          printk(KERN_DEBUG KERN_DEBUG "%s: el_interrupt() ax=%#02x", dev->name, axsr);
594
595      if (lp->loading==1 && !lp->txing)
596          printk(KERN_WARNING "%s: Inconsistent state loading while not in tx\n",
597dev->name);
```

We now read from the status card to figure which event triggered it.

Figure 5.36 Ethernet driver 3–interrupt a2: linux/net/drivers/3c501.c.

```
599  if (lp->txing)
600  {
601      /*
602      * Board in transmit mode. May be loading. If we are
603          loading we shouldn't have got this.
604      */
605
606
607      int txsr = inb(TX_STATUS);
608
609      if (lp->loading==1)
610          {
611              if (el_debug > 2)
612                  {
613                  printk(KERN_DEBUG "%s: Interrupt while loading [%s]", dev->name);
614                  printk("txsr=0x%04x gp=0x%04x\n", txsr, inw(GP_LOW),
615                  inw(RX_LOW));
616              }
617          lp->loading=2; /* Force a reload */
618          spin_unlock(lp->lock);
619          return;
```

## TCP/IP and Linux Protocol Implementation

```
619	}
620	if (el_debug > 6)
621	printk(KERN_DEBUG "txsr=%%02x gp=%04x rp=%04x", txsr, inw(GP_LOW), inw(
622      RX_LOW));
```

In many cases it may have been an error condition (such is life on a CSMA/CD network). In a few cases, we are done with something, and we want to get on with the next piece of work, so we call netif_wake_queue to find what more there might be sent.

Figure 5.37 Ethernet driver 3-interrupt b1: linux/drivers/net/3c501.c.

```
624	if ((axsr&0x80) && (txsr & TX_READ) == 0)
625	/*
626	/*
627		FIXME: there is a logic to keep from trying or
628		reset immediately ?
629	*/
630	if (el_debug)
631		printk("%s: Unusual interrupt during Tx, txsr=%%02x axsr=%%02x "
632		gp=0x%0x=%%03x.\n", dev->name, txsr, axsr,
633		inw(ioaddr+ELI_1DATAPTR),inw(ioaddr+ELI_RXRPTR));
634		lp->tring = 0;
635		netif_wake_queue(dev);
636	}
637	else if (txsr & TX_16_COLLISIONS)
638	/*
639		/* Timed out
640		*/
641	if (el_debug)
642		printk("%s: Transmit failed 16 times, Ethernet jammed\n",dev->name)
643		;
644		outbh(AK_SYS_AK_CMD);
645		lp->tring = 0;
646		lp->stats.aborted_errors++;
647		netif_wake_queue(dev);
648	}
```

Figure 5.38 Ethernet driver 3-interrupt b2: linux/drivers/net/3c501.c.

```
649	else if (txsr & TX_COLLISION)
650	{
651	/*
652		Retrigger xmit.
653	*/
```

## Protocol Implementation Framework 137

```
654
655
    if (el_debug > 6)
656
        printk("retransmitting after a collision.\n");
657
        /*
658 *        Poor little chip can't reset its own start pointer
659
        */
660
661
        outb(AX_SYS, AX_CMD);
662
        inw(lp->tx_start, GP_LOW);
663
        outb(AX_XMIT, AX_CMD);
664
        lp->stats.collisions++;
665
666        spin_unlock(&lp->lock);
667
668        return;
669 }
670    else
671 {
672        /*
673 *It worked. we will now fall through and receive
674
        */
675
        lp->stats.tx_packets++;
676        if (el_debug > 6)
677            printk("tx succeeded %s\n",
678                (txsr & TX_RDY) ? "%s" : "but is busy!");
679
            /*
680 *This is safe the interrupt itself.
681 */
682
            lp->timing = 0;
683
            netif_wake_queue(dev); /* In case more to transmit */
```

Of course, this is also the case that we have received a packet. Then we need to deal with that, too.

Figure 5.39 Ethernet driver 3–interrupt c: linux/drivers/net/3c501.c.

```
685    else
686    {
687        /*
688 *        In receive mode.
689        */
690
        int rxser = inb(RX_STATUS);
691
        if (el_debug > 5)
692            printk("rxser=%02x txsr=%02x rp=%04x", rxser, inw(TX_STATUS),inw(
693      RX_LOW));
694
        /*
695 *        Just reading rx_status fixes errors.
696        */
697        if (rxser & RX_MISSED)
698            lp->stats.rx_missed_errors++;
699        else if (rxser & RX_OK)
```

## 138 TCP/IP and Linux Protocol Implementation

Many problems can still be present even though the hardware has delivered a packet and an interrupt to say. We have to check for these (remember the start of Chapter 3?).

Figure 5.40 Ethernet driver 3-interrupt d: linux/drivers/net/3c501.c.

```
726      /*
727      * Move into receive
728      */
729      outb(AX_RX, AX_CMD);
730      inw(0x00, RX_BUF_CLR);
731      inw(RX_STATUS);      /* Be certain that interrupts are cleared. */
732      inw(TX_STATUS);
733      spin_unlock(&lp->lock);
734      return;
735  }
739 /**
740  * el_receive:
741    * @dev: Device to pull the packets from
742  */
743  * We have a good packet. Well, not "good", just not broken.
744  * We must check everything to see if it is good. In particular
```

## 139 Protocol Implementation Framework

```
* get packet sizes from the card. If the packet seems sane we do PIO
* off the card and queue it for the protocol layers.
*/
```

We start the work of receiving a packet in earnest. We check for simply illegal packet lengths, for example.

Figure 5.41 Ethernet driver 4-receive: linux/drivers/net/3c501.c.

```
/*
 * el_receive:
 * @dev: Device to pull the packets from
 *
 * We have a good packet. Not "good", just not broken.
 * We must check everything to see if it is good. In particular we
 * get packet sizes from the card. If the packet seems sane we do PIO it
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
        printf("el_receive %d\n", pkt_len);

    if ((pkt_len < 60) || (pkt_len > 1536)) {
        if (el_debug)
            printf("%s: bogus packet, length=%d\n", dev->name, pkt_len);
        lp->stats.rx_over_errors++;
    }
    return;
}
```

Finally, if all is well, we call netif_rx on the socket buffer that has the packet data.

Figure 5.42 Ethernet driver 4-receive: linux/drivers/net/3c501.c.

```
/*
 * Command mode so we can empty the buffer
 * */
outb(AX_SYS, AX_CMD);
```

## 140 TCP/IP and Linux Protocol Implementation

```
774 skb = dev_alloc_skb(pkt_len+2);
775
776 /*
777      * Start of frame
778      */
779
780 outw(0x00, GP_LGW);
781  if (skb == NULL)
782  {
783      printk("%s: Memory squeeze, dropping packet.\n", dev->name);
784      lp->stats.rx_dropped++;
785      return;
786  }
787  else
788  {
789      skb_reserve(skb,2); /* Force 16 byte alignment */
790      skb->dev = dev;
791      /*
792      * The read increments by the bytes. The interrupt
793         handler fixes the pointer when it returns to
794         receive mode.
795      */
796      insb(DATAPORT, skb_put(skb,pkt_len), pkt_len);
797      skb->protocol=eth_type_trans(skb,dev);
798      netif_rx(skb);
799      lp->stats.rx_packets++;
800      lp->stats.rx_bytes+=pkt_len;
801  }
802  return;
```

## 3c501 Device-Specific Statistics

Figure 5.43 Ethernet driver 4-stats: linux/drivers/net/3c501.c.

```
879 {
880     struct net_local *lp = (struct net_local)dev->priv;
881     return &lp->stats;
882 }
883 /**
884  * el_receive:
885    * @dev: Device to pull the packets from
886  */
885  * set_multicast_list:
886  * dev: The device to adjust
887  
888  * Set or clear the multicast filter for this adapter adapt to the best-effort
889  * filtering supported. The 3c501 supports only three modes of filtering.
890  * It always receives broadcasts and packets for itself. You can choose to
891  * optionally receive all packets, or all multicast packets on top of this.
892  */
893  static void set_multicast_list(struct net_device *dev)
```
