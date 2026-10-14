
`if (work >= quota || jiffies - start_time > 1)`
  `break;`

如果配置了硬件流控，则调用 `netdev_wakeup` 来控制注册了流控的网络设备的活动。

```c
#ifdef CONFIG_NET_FLOWCONTROL

  if (queue->throttle && queue->input_pkt_queue.qlen < thresh) {

    queue->throttle = 0;

    if (atomic_dec_and_test(&netdev_dropping)) {

      netdev_wakeup();

    }

  }

#endif
```

如果在处理所有包之前耗尽时间，我们将在此退出。非零返回值告诉调用者 `net_rx_action` 我们没有完成工作。调用者的 `budget` 会被调整。

```c
backlog_dev->quota = work;
*budget -= work;
return -1;
```

一旦成功处理了队列上的所有包，我们就跳转到这里。

```c
job_done:
backlog_dev->quota = work;
*budget -= work;
list_del(&backlog_dev->poll_list);
smp_mb();
netif_poll(backlog_dev);
if (queue->throttle) {
  queue->throttle = 0;
  #ifdef CONFIG_NET_FLOWCONTROL
  if (atomic_dec_and_test(&netdev_dropping)) {
    netdev_wakeup();
  }
  #endif
}
```

我们在退出前重新启用中断。

```c
local_irq_enable();
return 0;
```

### 6.6.2 netif_receive_skb 函数

我们讨论的下一个函数来自上一节描述的 `process_backlog`。`netif_receive_skb` 处理输入队列上的每个包。

```c
int netif_receive_skb(struct sk_buff *skb)
```

`ptype` 和 `pt_prev` 用于遍历 `packet_type` 结构体列表。这些列表指向在队列层注册了处理函数的网络层协议。

```c
struct packet_type *ptype, *pt_prev;
int ret = NET_RX_DROP;
```

类型被设为 `skb` 中 `protocol` 字段的值，该字段包含了来自链路层头的协议号。我们在 `skb` 的 `stamp` 字段中为每个传入的数据包设置时间。接收统计也会增加。

```c
unsigned short type = skb->protocol;
if (!skb->stamp_tv)
    do_getimeofday(&skb->stamp);
skb_bound(skb);
__get_cpu_var(netdev_rx_stat).total++;
```

`CONFIG_NET_FASTROUTE` 配置了快速路由。它通过直接从输入接口到输出接口来跳过大部分 IPv4 的处理。如果设置了此选项且包类型指示需要路由，则数据包将立即传输而不进一步处理。有关 IP 路由实现的更多细节，请参阅第 9 章。

```c
#ifdef CONFIG_NET_FASTROUTE
if (skb->pkt_type == PACKET_FASTROUTE) {
    __get_cpu_var(netdev_rx_stat).fastroute_deferred_out++;
    return dev_queue_mit(skb);
}
#endif
```

在此时，我们处于数据包处理的早期阶段；网络层处理尚未发生。因此，`skb` 字段数据指向头部信息的开头，我们更新原始头指针指向头部起始。

```c
skb->h_raw = skb->nh_raw = skb->data;
pt_prev = NULL;
```

此循环用于杂散包处理。变量 `ptype_all` 是注册了杂散数据包接收的协议列表的起始。

```c
list_for_each_entry_rcu(ptype, ptype_all, list)
    if (!ptype->dev || ptype->dev == skb->dev)
        if (pt_prev)
```

`Deliver_skb` 更新 `skb` 中的引用计数，并通过 `pt_prev` 的 `func` 字段调用协议的包处理函数。

```c
ret = deliver_skb(skb, pt_prev, 0);
pt_prev = ptype;
```

Linux 有一个帧分流器（frame diverter）选项，允许在包传递给协议处理之前在这一层进行快速包处理。`handle_diverter` 函数将检查 `skb` 是否应该被分流。

```c
handle_diverter(skb);
```

接下来，我们查看是否实现了桥接（bridging）。记得前面的章节，桥接本质上是二层层的数据包拷贝。桥接会消耗传入的数据包，因此如果进行了桥接，我们就不需要进一步处理。

```c
if (__handle_bridge(skb, &pt_prev, &ret))
    goto out;
```

在这里，我们找到了注册接收特定类型数据包的协议，例如类型为 `0x800` 的 IPv4 包。我们在该函数中使用与之前处理杂散模式处理器（promiscuous handlers）相同的函数。然而，对于注册处理器列表上与传入包中的协议匹配的每个包类型，都会调用 `deliver_skb`。例如，IP 协议注册的包处理函数是 `ip_rc`，因为它在类型为 `0x0800` 的数据包中，被设置在包处理器结构体的 `func` 字段中。

```c
list_for_each_entry_rcu(ptype, &ptype_base[ntohs(type)&15], list) {
    if (ptype->type == type &&
        (ptype->dev == skb->dev)) {
        if (pt_prev)
```

在这里我们调用协议的包处理函数。

```c
ret = deliver_skb(skb, pt_prev, 0);
pt_prev = ptype;
if (pt_prev) {
    ret = pt_prev->func(skb, skb->dev, pt_prev);
} else {
    ret = pt_prev->func(skb, skb->dev, pt_prev); // 注意：OCR 可能遗漏了这里的逻辑错误
    kfree(skb);
    ret = NET_RX_DROP;
}
```

```c
out:
    rcu_read_unlock();
    return ret;
}
```

## 6.7 传输层解复用与内部包路由

传输层解复用（de-multiplexing）是在 IP 处理完成后，决定由哪个传输层协议接收传入数据包的过程。当 IPv4 完成对接收包的处理时，它必须将协议向上传递给传输协议或 IPv4 内部的协议（如 ICMP 或 IGMP）。头部中的协议字段决定了 AF_INET 族中的哪一个成员协议将接收该包。在初始化时注册的每个协议都会接收由头部中 1 字节协议字段所指定类型的数据包。我们回想起，协议字段与以太网头部中的协议字段并不相同。链路层和 IPv4 封装将在第 3 章中讨论。

### 6.7.1 `inet_protos` 数组

在内核初始化时，通过文件 `linux/net/ipv4/af_inet.c` 中的 `inet_init` 函数注册这些协议。作为初始化的一部分，指向每个协议的指针被放置在一个名为 `inet_protos` 的指针数组中。该数组在文件 `linux/net/ipv4/protocol.c` 中声明。

```c
struct inet_protocol *inet_protos[MAX_INET_PROTOS];
```

每个协议都会声明 `inet_protocol` 结构体的实例。

```c
struct inet_protocol {
```

`handler` 指向协议的输入函数，`err_handler` 指向协议的错误函数（如果有定义）。稍后我们将介绍如何 TCP/IP 中的高层协议初始化这些字段。

```c
int (*handler)(struct sk_buff *skb);
void (*err_handler)(struct sk_buff *skb, u32 info);
```
