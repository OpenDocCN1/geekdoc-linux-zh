
```c
if (el_debug > 6)
    printk("retransmitting after a collision.\n");
/*
 *        这个糟糕的芯片无法重置自己的起始指针
 */
outb(AX_SYS, AX_CMD);
inw(lp->tx_start, GP_LOW);
outb(AX_XMIT, AX_CMD);
lp->stats.collisions++;
spin_unlock(&lp->lock);
return;
}
else
{
    /*
 *它成功了。我们现在向下执行并接收
 */
    lp->stats.tx_packets++;
    if (el_debug > 6)
        printk("tx succeeded %s\n",
            (txsr & TX_RDY) ? "%s" : "but is busy!");
        /*
 *这个中断本身是安全的
 */
        lp->timing = 0;
        netif_wake_queue(dev); /* 有更多待发送 */
```

当然，这也是收到了数据包的情况。那时我们需要处理它。

图 5.39 以太网驱动程序 3–中断 c: `linux/drivers/net/3c501.c`。

```c
else
{
    /*
 *        接收模式。
 */
    int rxser = inb(RX_STATUS);
    if (el_debug > 5)
        printk("rxser=%02x txsr=%02x rp=%04x", rxser, inw(TX_STATUS),inw(
      RX_LOW));
    /*
 *        只需读取 rx_status 即可修复错误。
 */
    if (rxser & RX_MISSED)
        lp->stats.rx_missed_errors++;
    else if (rxser & RX_OK)
```

### 138 TCP/IP 和 Linux 协议实现

尽管硬件已经交付了数据包并发出中断，仍然存在许多问题。我们必须检查这些问题（记得第 3 章开头吗？）。

图 5.40 以太网驱动程序 3-中断 d: `linux/drivers/net/3c501.c`。

```c
/*
 * 进入接收模式
 */
outb(AX_RX, AX_CMD);
inw(0x00, RX_BUF_CLR);
inw(RX_STATUS);      /* 确保中断已清除。 */
inw(TX_STATUS);
spin_unlock(&lp->lock);
return;
}
/**
  * el_receive:
  * @dev: 从设备提取数据包
  */
*它成功了。我们现在向下执行并接收
*/
lp->stats.tx_packets++;
if (el_debug > 6)
    printk("tx succeeded %s\n",
        (txsr & TX_RDY) ? "%s" : "but is busy!");
    /*
 *这个中断本身是安全的
 */
    lp->timing = 0;
    netif_wake_queue(dev); /* 有更多待发送 */
```

### 139 协议实现

```c
751
752
753
754
755
756
757
758
759
760
761
762
763
764
765
766
767
768
769
770
771
772
773
774
775
776
777
778
779
780
781
782
783
784
785
786
787
788
789
790
791
792
793
794
795
796
```

### 140 TCP/IP 和 协议实现
