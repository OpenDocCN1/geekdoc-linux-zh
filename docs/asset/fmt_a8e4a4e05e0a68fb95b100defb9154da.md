
变量 `ih3` 指向版本 3 头部。我们检查数据包长度是否足够容纳源地址（如果有的话）。

```
ih3 = (struct igmpv3 *) skb->h.raw;
```

我们检查 v3 数据包中源地址的数量。

```
if (ih3->nsrcs) {

    if (!pskb_may_pull(skb, sizeof(struct igmpv3_query)))

        + ntohs(ih3->nsrcs)*sizeof(__u32))

    return;

```

```
ih3 = (struct igmpv3_query *) skb->h.raw;

}

max_delay = IGMPV3_MRC(ih3->code) (HZ/IGMP_TIMER_SCALE);

if (!max_delay)

    max_delay = 1;

    in_dev->mr_maxdelay = max_delay;

if (ih3->qrv)

    in_dev->mr_grv = ih3->grv;
```

IGMP group 字段中的值告诉我们这是一个通用查询还是源特定查询。

```
if (!group) {
```

通用查询的源数量必须为 0。

```
if (ih3->nsrcs)

    return;
```

我们启动查询定时器。每个接口都有一个定时器，它位于第 6 节描述的 `inet_dev` 结构中。

```
igmp_qq_start_timer(in_dev);

    return;
```

如果包含源地址，我们通过设置 `mark` 来指示。

```
mark = ih3->nsrcs = 0;

}
```

现在，我们为接收查询的接口的所有成员组启动定时器。如果定时器已经在运行，则进行重置。我们不为 224.0.0.1 任何已知的组启动定时器。

```
read_lock(&in_dev->lock);

for (im=in_dev->mc_list; im!=NULL; im->next) {

    if (group && group != im->multiaddr)

        continue;

    if (im->multiaddr == IGMP_HOST_LEAVE)

        continue;

    spin_lock(&im->lock);

    if (im->running)

        im->gsquery = group && mark;

    else

        im->gsquery = mark;

    if (ih3->nsrcs, ntohs(ih3->nsrcs), ih3->srcs);

        spin_unlock(&im->lock);

        igmp_timer(im, max_delay);

}

read_unlock(&in_dev->lock);
```

### 9.12.3 处理 IGMP 报告

IGMP 报告由路由器处理。虽然 Linux 接收报告解释原始 IGMP 包并更新路由表，监听 IGMP 报告的函数是 `igmp_heard_report`。

```
static void igmp_heard_report(struct device *in_dev, u32 group);
```

`igmp_heard` 在成员报告中停止定时器之外做得更多。

### 9.12.4 添加和离开组

当应用程序使用 IGMP 版本 2 加入组时，它调用带有 `IP_ADD_MEMBERSHIP` 或 `MCAST_JOIN_GROUP` 选项的 `setsockopt` 函数。如果 `setsockopt` 看到这些选项之一，则调用 `ip_join_group`。

```
int ip_join_group(struct sock *sk, struct ip_mreq *imr);
```

该函数必须找到由 `imreq` 指定的网络接口。接下来，它检查 `imreq` 中的多播地址与分配给接口的多播地址列表之间的匹配情况。如果找到，增加引用计数并添加到组。然后，它调用 `ip_group` 为组设置定时器。当定时器过期时，报告将被传输。

如果应用程序使用 IGMP 版本 2 离开组，将调用带有 `MCAST_LEAVE_GROUP` 或 `IP_MEMBERSHIP` 选项 `setsockopt`。在这种情况下，`setsockopt` 将调用函数 `ip_leave_group`。

```
int ip_leave_group(struct sock *sk, struct ip_mreq *imr);
```

与 group 函数一样，第二个参数 `im` 指向第 9.12 节所示的多播请求结构。函数必须找到接口。然后移除指定的多播地址。

## 9.13 从 IP 发送数据包

在第 6 节中，我们解释了 IP 如何通过队列层将其发送到输出驱动。如之前所述，Linux 提供了由流量分类选择的多个队列。当 IP 构建数据包时，它将其放在这些队列之一。然而，IP 输出路由不是直接调用的。相反，它是通过邻接缓存输出路径间接完成的。

通常，所有内部包路由都通过邻接缓存。例如，如果数据包应该转发，邻接缓存输出指针将指向 `ip_forward`。一旦输出数据包的处理完成，如果数据包有一个解析的路由，邻接缓存的输出操作可能会指向函数 `ip_output`。队列层和 IP 设施的底部在第 6 节讨论过。

在本节中，我们讨论直接从上层调用的函数从 TCP 段构造 IP 数据报。IP 为此目的提供了几个函数，它们定义在 `linux/ipv4/output.c` 文件中。我们将通过 UDP 或原始套字等面向数据报的传输协议讨论其中的一些函数。其中一个函数从页面构建 IP 数据报。另一个执行相同的操作，但从映射页面构建。此外，我们将讨论一个主要供 TCP 使用的从 TCP 段制作 IP 数据报的函数。

我们讨论的下一个函数是 `ip_append_data`，它从原始、UDP 或其他上层调用。它从各种数据片段构造单个 IP 数据报。

```
int ip_append_data(struct sock *sk,

int getfrag(void *char, char *to, int offset, int len, int odd,

    struct sk_buff *skb),

void *from,

    int length,

    int transhdrlen, struct ipc_cookie *ipc,

    struct rtable *rt, unsigned int flags);
```

`Getfrag` 指向用于获取 IP 分片的函数。通常，它将指向 `ip_generic_getfrag`，在检查校验和的同时将数据从用户空间拷贝到内核缓冲区。参数 `from` 指向数据缓冲区，`offset` 是数据缓冲区中的偏移。`Transhdrlen` 是不带 IP 选项的头部长度。`ipc` 指向来自 themsg socket 的控制消息结构。这包含了放入 IP 头部的 IP 选项。输出包的缓存是 `rt`，这就是我们获取目标地址的地方。

我们在 `ip_append_data` 中做的第一件事是检查 socket 队列是否为空。它构建内核数据，将包含该 socket 发送的每个输出分片的 IP 头部。它根据 MTU 和 IP 头部计算计算碎片长度。接下来，它构建 `sk_buff` 链并将其放入 socket 队列。如果输出设备具有散聚集能力，输出数据包被设置为映射页链。对于每个 socket 缓冲区，我们调用 `__sk_queue_tail` 将 `sk` 放入 socket 的写入队列。

```
ssize_t ip_append_page(struct sock *sk, struct page

*page, int offset, size_t size, int flags)
```

通常，此函数由上层发送函数作为 `udp_sendpage` 调用，定义在文件 `linux/ipv4/udp.c`。如果 socket 写队列有空间，它会分配一个 `sk_buff`。`skb` 持 IP 头部。然后，列表中的页面追加到 `skb`。最后，调用函数 `__sk_queue_tail` 将 `sk` 放入 socket 的写入队列。

另一个功能是流式传输协议（如 TCP）高效地通过 IP 发送分段。这个函数是 `ip_queue_xmit`。

```
int ip_queue_xmit(struct sk_buff *skb, int ip_fragok)
```
