
`ptype` 和 `pt_prev` 用于遍历 `packet_type` 结构体列表。这些列表项指向在队列层注册了接收处理函数的网络层协议。

```c
struct packet_type ptype, *pt_prev;

struct net_device *orig_dev;

int ret = NET_RX_DROP;
```

我们在每个入站数据包的 `skb` 的 `stamp` 字段中设置了到达时间。接收统计信息也会增加。

```c
unsigned short type;

if (skb->dev->poll && netpoll_rx(skb))
    return NET_RX_DROP;

if (!skb->timestamp.off_sec)
    net_timestamp(skb);

if (!skb->input_dev)
    skb->input_dev = skb->dev;

orig_dev = skb_dev(skb);

__get_cpu_var(netdev_rx_stat).total++;
```

### 第 5 章 TCP/IP 协议栈

此时，我们处于数据包处理的早期阶段；网络层处理尚未发生，且 `skb` 仍然包含包头。因此，`skb` 字段指向包头的开头，我们更新原始包头以指向该头部。

```c
skb->h_raw = skb->nh_raw = skb->data;
skb->mac_len = skb->nh_raw;

pt_prev = NULL;
rcu_read_lock();

#ifdef CONFIG_NET_CLS
if (skb->tc_dev & TC_CLS) {
    skb->tc_dev = TC_OK(skb->tc_dev);
    goto ncls;
}
#endif
```

此循环用于混杂模式数据包处理。变量 `type_all` 是请求混杂接收的协议列表的起点。

```c
list_for_each_entry_rcu(type, &pt_all, list)
    if (!ptype->dev || ptype->dev == skb->dev) {
        if (!pt_prev)
```

`deliver_skb` 更新 `skb` 中的使用计数，并通过 `pt_prev` 的 `func` 字段调用协议的数据包处理程序。

```c
ret = deliver_skb(skb, pt_prev, 0);
pt_prev = ptype;
}

#ifdef CONFIG_NET_CLS
if (pt_prev) {
    ret = deliver_skb(skb, pt_prev, orig_dev);
    pt_prev = NULL; /* 不应该有 else 处理此 */
} else {
    skb->tc_dev = TC_OK(skb->tc_dev);
}

ret = ip_filter(skb);
if (ret == TC_ACT_SHOT || (ret == TC_ACT_STOLEN)) {
    kfree(skb);
    goto out;
}

skb->tc_dev = 0;

ncls:
#endif
```

Linux 有一个名为 `diverter` 的选项，用于在数据包传递到处理层之前进行硬件协助。`handle_diverter` 会检查数据包是否应该被转向。

```c
handle_diverter(skb);
```

接下来，我们查看是否实现了桥接（bridging）。从之前的章节知道，桥接是二层的一种操作。桥接消耗了入站数据包，如果它被桥接，则不再需要进一步处理。

```c
if (__handle_bridge(skb, &pt_prev))
    goto out;
```

这里是注册以接收 IP 头中协议字段指定类型数据包的协议。我们使用了之前在协议处理函数中使用的类型为 `0x08` 的数据包。

```c
list_for_each_entry_rcu(type, &pt_base[ntoh(type)], list) {
    if (!ptype->dev || ptype->dev == skb->dev) {
        if (pt_prev)
```

在这里我们调用协议的数据包处理函数。

```c
ret = deliver_skb(skb, pt_prev, 0);
pt_prev = ptype;
}

if (pt_prev)
    ret = pt_prev->func(skb, skb->dev, pt_prev);
} else {
    kfree_skb(skb);
    ret = NET_RX_DROP;
}

out:
rcu_read_unlock();
return ret;
```

## 传输层复用与内部路由

传输层复用是在 IP 处理完成后，决定哪个传输层协议接收入站 IP 包的过程。当 IPv4 完成对数据包的处理时，它将其传递给传输层协议或 IPv4 的内部协议（如 ICMP 和 IGMP）。IP 头中的协议字段决定了 `AF_INET` 族的哪种协议将接收该数据包。初始化时注册的每个协议都会接收 IP 头中协议字段指定的单字节类型数据包。我们回顾一下，该字段与以太网 MAC 头中的协议字段不同。链路层和 IPv4 头部封装在第 2 章中讨论过。

### `inet_protos` 数组

这些协议在内核初始化时（在 `linux/net/ipv4/af_inet.c` 文件中）通过 `inet_init` 函数进行注册。作为初始化的一部分，每个协议的指针被放置在一个名为 `inet_protos` 的指针数组中。该数组定义在 `linux/net/ipv4/protocol.c` 文件中。数据结构 `net_protocol` 定义在 `linux/include/net/protocol.h` 中。

```c
struct net_protocol *inet_protos[MAX_INET_PROTOS];
```

### `net_protocol` 结构

每个协议都声明了一个 `net_protocol` 结构实例。

```c
struct net_protocol
{
    int (*handler)(struct sk_buff *skb);
    void (*err_handler)(struct sk_buff *skb, u32 info);

    int no_policy;
};
```

`handler` 指向协议的输入函数，而 `err_handler` 指向协议的错误处理函数（如果有定义）。稍后，我们将展示如何为 TCP/IP 中的高层协议初始化这些字段。最后一个字段在 IPv4 中没有用。它对应于 IPv6 中的一个字段，用于确定该协议的安全关联策略。

每个协议都被放置在名为 `inet_protos` 的哈希数组中。该数组最多可以容纳 255 个协议。当添加 IPv4 协议族的基础组成部分四种协议（UDP、TCP、ICMP 和 IGMP）时，数组中的四个位置会被填充。这是在 `AF_INET` 族初始化期间完成的。通过调用 `inet_add_protocol` 将协议放入 `inet_protos` 哈希表。初始化完成后，可以动态地添加协议。

## `AF_INET` 族成员协议的初始化

这是为 IPv4 协议族中的三个永久协议（TCP、UDP 和 ICMP）初始化 `net_protocol` 实例的方法。图中也显示了 IGMP，因为如果在编译 Linux 内核时配置了组播路由，则会配置该协议。

```c
#ifdef CONFIG_IP_MULTICAST
static struct inet_protocol igmp_protocol = {
    .handler = igmp_rcv,
};
#endif

static struct inet_protocol tcp_protocol = {
    .handler = tcp_v4_rcv,
    .err_handler = tcp_v4_err,
    .no_policy = 1,
};

static struct inet_protocol udp_protocol = {
    .handler = udp_rcv,
    .err_handler = udp_err,
    .no_policy = 1,
};

static struct inet_protocol icmp_protocol = {
    .handler = icmp_rcv,
};
```
