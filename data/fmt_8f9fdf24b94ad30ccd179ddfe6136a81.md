
将其包含在本节是因为对于服务函数，它指向 `linux/core/dev.c` 中的 `free_netdev`。

## 4.8 接收数据包

与其他系统的硬件驱动一样，接收数据包的第一步发生在设备响应中断时。对于以太网驱动以及我们的 `e100` 示例，当网络接口硬件 DMA 完成时，会调用网络驱动程序的中断处理程序。在中断处理程序，我们首先检测中断原因。判断中断是否有效，如果是，判断是发送还是接收中断。如果我们检测到接收中断，就知道有一个数据包可以处理，因此可以开始接收数据包的必要步骤。我们必须执行的操作之一是将接收到的数据包聚集到缓冲区或 `sk_buff` 中。大多数高效的驱动程序在此阶段避免拷贝数据。在 Linux 中，缓冲区用于包含数据包，它们可以设置为指向 DMA 空间。第 7 章缓冲区。通常，网络接口驱动程序在其数据结构中维护 `skbuf` 列表，一旦中断指示输入 DMA 完成，我们就可以将新数据包的缓冲区放在供协议输入函数处理的队列中。

出于出于效率考虑，我们通常希望网络驱动程序尽快从中断返回。当我们处理中断时，所有进程都会挂起；因此，我们希望在中断处理路径中尽可能少做工作。因此，我们在软中断上下文中对数据包进行排队，以便从中断处理路径中卸载尽可能多的处理。

| 来自文件 `linux/linux/netdevice.h` 的函数 | 参数 | 返回值 | 目的 |
|---|---|---|---|
| `netif_start_queue` | `struct net_device *` | `void` | 启动队列。 |
| `netif_receive_skb` | `struct sk_buff *` | `int` | 数据包接收函数。`Netif_receive_skb` 在拥塞时被调用以尝试 |

### 表 4.5: 网络队列层函数

| 来自文件 `linux/include/linux/device.h` 的函数 | 参数 | 返回 | 目的 |
| --- | --- | --- | --- |
| `netif_schedule` | `struct net_device *` | `void` | 处理积压。此函数输出队列处理。 |
| `netif_wake_queue` | `struct net_device *` | `void` | 重启传输。 |
| `netif_stop_queue` | `struct net_device *` | `void` | 关闭输出队列的传输。 |
| `netif_queue_stopped` | `struct net_device *` | `int` | 检查传输链路状态，查看传输是否关闭。 |
| `netif_running` | `struct net_device *` | `int` | 检查传输是否处于启动状态。 |

在大多数网络接口驱动程序中，中断处理程序必须与数据包接收相关的处理。它会执行一些内部管理工作，包括设备空间的映射和取消映射、设置下一次 DMA 传输，并确保有足够的套缓冲区（socket buffers）供后续 DMA 传输使用。一旦这些内部函数完成，中断处理程序通过将协议字段设置为以太网数据包头，将数据包设置在套缓冲区中。它还会调用 `skb_put` 来调整套缓冲区，以确保数据包有足够的尾部空间。参考第 7 章关于 `skb_put` 和其他套工具函数的描述。在文件 `linux/include/netdevice.h` 中定义的 `netif_rx` 函数由中断服务程序（ISR）调用，以触发数据包处理的输入端并将数据包交付给数据包接收软中断 `NET_RX_SOFTIRQ`。

```c
int netif_rx(struct sk_buff *skb);
```

第 6 章详细描述了数据包队列层和软中断（softirq）机制。`netif_rx` 函数返回一个值表示队列层检测到的网络拥塞程度或数据包是否被丢。表 4.6 显示了 `netif_rx` 的返回值。

### 表 4.6: 队列层 netif_rx 返回值

| 值 | 含义 |
| --- | --- |
| `NET_RX_SUCCESS` | 无拥塞 |
| `NET_RX_CN_LOW` | 低拥塞 |
| `NET_RX_CN_MOD` | 中度拥塞 |
| `NET_RX_CN_HIGH` | 高拥塞 |
| `NET_RX_DROP` | 数据包被丢弃 |

在 `linux/include/linux/netdevice.h` 中提供了另一个函数 `netif_rx_ni` 用于从非中断上下文中队列输入数据包。该函数在队列传入的数据包后会重新调度软中断。它还返回表 4.6 中描述的值。

接的函数 `netif_rx` 是网络接口驱动程序中从中断服务程序调用的主函数。它被传递给持有新接收数据包的套缓冲区。该函数位于 `linux/net/core/dev.c`。

```c
int netif_rx(struct sk_buff *skb) {

    int this_cpu;

    struct softnet_data *queue;

    unsigned long flags;
```

首先，我们在 `skb` 中设置时间戳（如果其中尚未设置的话），即接收数据包时的时间戳。

```c
if (skb->stamp.tv_sec == 0)
    do_gettimeofday(&skb->stamp);
```

函数中的代码编写方式确保了 CPU 拥塞时执行路径最短。我们获取当前 `softnet_data` 结构体的队列指针。

```c
local_irq_save(flags);

this_cpu = smp_processor_id();

queue = &get_cpu_var(softnet_data);

__get_cpu_var(netdev_rx_stat).total++;
```

我们通过检查输入队列是否长于 `dev.c` 中定义的 `netdev_max_backlog` 变量设置的常量值来检查积压情况。

我们还会检查 `softnet_data` 结构体是否存在 `throttle` 字段。如果没有拥塞指示，我们调用 `netif_rx_schedule`。

```c
if (queue->input_pkt_queue.len) {

    if (queue->throttle)
        goto drop;
```

入队：

```c
dev_hold(skb->dev);

__skb_queue_tail(&queue->input_pkt_queue, skb);
```

```c
#ifndef OFLINE_SAMPLE
```
`get_sample_stats(this_cpu);`
```c
#endif
local_irq_restore(flags);
    return queue->cng_level;
}
```

如果配置了流控，我们将尝试执行它。

```c
if (queue->throttle) {
    queue->throttle = 0;
#ifdef CONFIG_NET_HW_FLOWCONTROL
    if (atomic_dec_and_test(&netdev_dropping))
        netdev_wakeup();
#endif
}
```

我们不能通过 `netif_rx_schedule` 将接口添加到 poll 列表的尾部。这实际上是在软中断执行时重新调度接口进行本地处理。

```c
netif_rx_schedule(&queue->backlog_dev);
if (queue->throttle) {
    queue->throttle = 1;
    get_cpu_var(netdev_rx_stat).throttled++;
#ifdef CONFIG_NET_HW_FLOWCONTROL
    atomic_inc(&netdev_dropping);
#endif
}
```

在这里我们丢弃数据包；没什么可以做的——增加统计信息，释放 `skb`，并指示拥塞情况，当然，指示是 `NET_RX_DROP`。

```c
drop:
    get_cpu_var(netdev_rx_stat).dropped++;
    local_irq_restore(flags);
    kfree_skb(skb);
    return NET_RX_DROP;
```

自 Linux 2.4 版本开始，这包含了被称为 `backlog_dev` 的网络设备。
