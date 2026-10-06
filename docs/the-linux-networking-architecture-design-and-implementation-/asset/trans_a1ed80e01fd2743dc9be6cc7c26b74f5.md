
```c
/* 如果发生错误，没有非重启的恢复方法。
*/
static int net_open(struct net_device *dev) {
    struct net_local *np = (struct net_local *)dev->priv;
    int ioaddr = dev->base_addr;
    /*
     * 如果中断线可以关闭（共享）时使用此项。
     * 关于在配置时选择 IRQ 的示例请参考 3c53.c。
     */
    if (request_irq(dev->irq, &net_interrupt, 0, codname, dev)) {
        return -EAGAIN;
    }
    /*
     * 始终在 IRQ 之后分配 DMA 通道，并在失败时清理。
     */
    if (request_dma(dev->dma, codname)) {
        free_irq(dev->irq, dev);
        return -EAGAIN;
    }

    MOD_INC_USE_COUNT;
    /*
     * 在此处重置硬件。别忘记设置站地址。
     */
    chipset_init(dev, 1);
    outb(0x00, ioaddr);
    np->open_time = jiffies;
    /*
     * 我们现在准备好接收来自网络
     * 层的传输请求。
     */
    netif_start_queue(dev);
    return 0;
}
```

# 停用网络适配器

example_stop()                               drivers/net/isa_skeleton.c

在停用网络适配器时，应该撤销适配器打开时执行的所有操作。这主要涉及分配的系统资源（中断、DMA 通道等），这些资源现在应该被释放。

对于模块化驱动程序，必须用 `MOD_DEC_USE_COUNT` 减少计数器，并且网络设备不能接受来自上层的任何数据包（netif_stop_queue）。同样，如果成功则返回 0，否则返回负错误代码。

```c
/* net_open(struct net_device *dev) 的逆向例。*/
static int net_close(struct net_device *dev) {
    struct net_local *lp = (struct net_local *)dev->priv;
    int ioaddr = dev->base_addr;
    lp->open_time = 0;

    netif_stop_queue(dev);

    /* 在此处刷新 Tx 并禁用 Rx。 */
    disable_dma(dev->dma);

    /* 如果没有跳线到 IRQ 或 DMA，则释放该线路。 */
    outww(0x00, ioaddr+0); /* 释放物理中断线。 */

    free_irq(dev->irq, dev);
    free_dma(dev->dma);

    /* 在此处更新统计信息。 */
    MOD_DEC_USE_COUNT;

    return 0;
}
```

# 5.3.3 传输数据

Linux 网络适配器架构中的每次数据传输都通过网络设备发生，具体来说是通过使用 `hard_start_xmit()` 方法（开始传输）实现的。当然，这是一个函数指针，指向特定驱动程序的任务函数。...start_xmit()。该方法负责以套接字缓冲区（socket buffer）的形式转发数据包并启动传输。在本节讨论驱动方法 `dev->hard_start_xmit()` 中的通常步骤之前，我们将简要描述网络适配器的通用架构。

网络适配器是一种接口适配器，它根据定义的 MAC 协议（以太网、令牌环等）自动发送和接收网络数据包。这意味着网络适配器有一套独立的逻辑，与常规中央处理器并行工作。网络适配器和系统处理器通过 I/O 端口（硬件寄存器）和中断进行交互。当处理器想要将数据传递给网络适配器时，适配器将数据写入适当的 I/O 端口并启动所需的操作。当适配器想要将数据传递给处理器时（例如它收到的数据包），适配器会触发中断，处理器使用网络适配器的中断处理运行时来服务该网络适配器。这清楚地表明系统处理器相对于接口适配器起着主导作用（主从关系）。

# 传输数据包

```
net_start_xmit()
```

dev->hard_start_xmit(skb, dev) 负责将数据包转发到网络适配器，以便后者进行传输。套接字缓冲区的数据包数据被复制到网络适配器内部的缓冲区位置，并附上时间戳 `dev->trans_start = jiffies`，标记该传输的开始。如果此复制操作成功，则假设传输也将成功。在这种情况下，`hard_start_xmit()` 必须返回 0。否则，它应该返回 1，以便内核知道数据包无法发送。

在操作系统和网络适配器之间转发网络数据包时，我们可以区分两种不同的技术：

- 旧的网络适配器（例如 3Com3509）在适配器上有一个用于发送数据包的内部缓冲区内存。这意味着内核每次只能向适配器转发一个单一数据包。如果缓冲区空闲，数据包就会被复制到适配器，内核就可以删除相应的套接字缓冲区。
-较新的网络适配器工作方式不同。驱动程序管理一个由 16 到 64 个缓冲区指针组成的环形缓冲区。当数据包准备好发送时，驱动程序管理一个由 16 到 64 个缓冲区指针组成的环形缓冲区……（此处原文存在大量重复，已根据逻辑流清理）。

```c
static int net_send_packet(struct sk_buff *skb, struct net_device *dev) {
    struct net_local *np = (struct net_local *)dev->priv;
    int iaddr = dev->base_addr;
    short length = ETH_ZLEN < skb->len : ETH_ZLEN;
    unsigned char *buf = skb->data;

    /* 如果尝试传输此数据包时发生错误，
     * 你应该从此函数返回 '1'。
     * 在这种情况下，你可以不对 SKB 做任何操作，
     * 它仍由网络层所有。
     * 你可以修改任何 SKB 字段，可以释放 SKB 等。
     */

#if TX_RING
    /* 这是现代硬件最常见的情况。
     * 自旋锁保护此代码免受 TX 完成
     * 中断的影响。队列控制
     * 也在此锁下进行管理。
     */
    spin_lock_irq(&np->lock);

    add_to_tx_ring(np, skb, length);
    dev->trans_start = jiffies;

    /* 如果我们使用了设备 TX 环中的最后一个条目，
     * 通知层停止发送。
     */
    if (tx_full(dev))
        netif_stop_queue(dev);

    /* 当 TX 完成中断到达时，
     * 统计信息会被更新。
     */
    spin_unlock_irq(&np->lock);
#else
    /* 这是旧硬件的情况，它一次处理
     * 单个传输缓冲区，并通过 PIO 写入。

     * 不需要自旋锁，因为没有 TX 完成
     * 事件。如果你的卡有 TX 完成
     * 硬件中断，你可能需要利用 np->lock。
     */
    hardware_send_packet(iaddr, buf, length);
    np->stats.tx_bytes += skb->len;

    dev->trans_start = jiffies;

    /* 此处可能需要清理并记录 TX 统计信息。 */
    if (inw(iaddr) == 81)
        np->stats.tx_aborted_errors++;
}
```
