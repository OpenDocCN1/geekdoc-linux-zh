
cs 14.16, `ip_route_output_key()`.

为所有需要使用相同路由的数据包/连接缓存路由项。当第一次建立连接时，首先查询路由缓存，通过路由项查找检查项是否已在路由中缓存，即 `ip_route_output_key()` (cs 14.16)。此例遍历路由项链以确定是否命中了缓存（循环 2007–2025）。在每次迭代中，我们检查匹配路由键的项（第 2008–2016 行）。如果未命中缓存，则查询 FIB 构建请求路由的路由项，调用 `ip_route_output_slow()`（第 2028 行），这最终会将项添加到缓存中。

### 管理路由缓存

`dst_entry` 对象的 `__use` 字段会加 1。该字段在销毁缓存路由条目时不会被使用，不应与引用计数 (`__refcount`) 混淆。每当条目发生缓存命中时，该字段就会增加，并用于统计目的。同样，我们在 2020 年更新了 CPU 上的缓存命中中的统计数据。

## 14.8.1 本地连接的路由缓存

让我们看看在启动 TCP 连接时是如何查询路由缓存的。当用户应用程序发出新的 TCP 连接请求时，内核会调用 `tcp_v4_connect()` (cs 14.17)。它在第 773 行调用 `ip_route_connect()` 来获取目的地的路由。如果找到了目的地的路由，则首先将其作为参数返回给路由；否则返回错误。获取路由信息的简单步骤是：首先检查内核路由缓存，如果条目不存在，则根据 FIB 提供的信息构建新的路由条目并将其缓存在内核中。`ip_route_output_key()` 用于在内核路由缓存中搜索连接所需的条目。如果在缓存中找到了路由条目，我们将按照第 14.12.2 节所述的方式持有该路由条目的引用。我们在第 783 行通过调用 `__sk_dst_set()` 为 socket 缓存路由信息。路由为 socket (`sock` 对象) 创建一个 `dst_cache` 字段，指向新的路由 (`dst_entry` 对象)。该路由信息将用于在该连接上发送的所有数据包。

每当通过 socket 发送数据包时，会在 `ip_queue_xmit()` (cs 14.18) 中检查缓存路由信息的有效性。在数据包被 IP 层处理之前，会在第 354 行调用 `__sk_dst_check()`。如果缓存的路由条目被标记为过期，该函数返回 NULL；否则，它将返回在 `tcp_v4_connect()` 建立连接时 socket 缓存的值（由 `sk->dst_cache` 指向）。在路由过期的情况下，我们在第 367 行调用 `ip_route_output()` 为目的地构建路由条目。我们在第 371 行通过 `__sk_dst_set()` 将新的路由条目缓存到 socket 中。每个传出的数据包也会指向该路由条目，这是通过第 374 行调用 `dst_clone()` 完成的。`dst_clone()` 增加了路由条目 (`dst_entry` 对象) 的引用计数，使其在数据包最终发送之前不会被销毁。

`net/ipv4/ipv4.c`

```c
int tcp_v4_connect(struct sock *sk, struct sockaddr *uaddr, int addr_len)
(
...
struct tcp_opt *ip = &sk->tp_info.of_tcp);
...
tmp = ip_route_connect(&rt, nexthop, saddr,
RT_CONN_FLAGS(sk), sk->bound_dev);
__sk_dst_set(sk, &sk->u_dst);
...
)
```

> cs 14.17, `tcp_v4_connect()`.

`net/ipv4/ip_output.c`

```c
int ip_queue_xmit(struct sk_buff *skb)
{
    struct sock *sk = skb->sk;
    ...
    rt = (struct rtable *) skb->dst;
    if (rt != NULL)
        goto packet_routed;

    /* 确保我们可以路由此数据包。 */
    rt = (struct rtable *) sk_dst_check(sk, 0);
    if (rt == NULL) {
        if (ip_route_output(&rt, daddr, sk->saddr,
                            RT_CONN_FLAGS(sk),
                            sk->bound_dev))
            goto no_route;
        sk_dst_set(sk, &rt->u.dst);
    }
    skb->dst = dst_clone(&rt->u.dst);
}
```

cs 14.18. `ip_queue_xmit()`.

## 14.8.2 `__sk_dst_check()`

`__sk_dst_check()` 在第 1100 行检查路由是否存在 (`dst != NULL`) 以及是否过期 (`dst->obsolete > 0`) (cs 14.19)。如果两者均为真，则调用特定于 IP 版本的检查函数。在 IPv4 下，该函数调用 `ipv4_dst_check()`。该函数通过调用 `dst_release()` 减少 `dst_entry` 对象的引用计数。只有当路由过期时我们才调用 `ipv4_dst_check()`，由于我们不再引用该路由条目，引用计数减 1，并在第 1101 行将 `sk->dst_cache` 设置为 NULL。

`include/net/sock.h`

```c
static inline struct dst_entry *
    sk_dst_check(struct sock *
```

cs 14.19. `__sk_dst_check()`.

## 14.8.3 链路故障与系统报告

在本节中，我们将看到当路由链路故障时路由缓存是如何失效的。数据包传输的最后一步是构建链路层头部。为了这一点，需要目的地的硬件地址。咨询邻居系统来解析该地址。它发送 ARP 请求并将数据包放入其队列。为此 ARP 请求安装一个定时器以便检查 ARP 结果，`neigh_timer_handler()` 是邻居定时器到期运行时的函数 (cs 14.20)。在该函数中，我们在 650 行检查是否在没有获得 ARP 回复的情况下耗尽了重试 ARP 请求的次数。如果是，我们在 663 行对邻居队列中等待 ARP 解析的每个数据包进行错误处理。我们在 665 行调用邻居特定的错误处理函数 `neigh_ops->error_report`。`error_report()` 会释放 `sk_buff`，并通过调用 `dst_link_failure()` 确保与数据包相关的路由条目从系统中移除。

```c
net/core/neighbour.c

static void neigh_timer_handler(unsigned long arg)
{
    unsigned long now = jiffies;
    struct neighbour *neigh = (struct neighbour*)arg;
    if (atomic_read(&neigh->probes) != neigh_max_probes(neigh)) {
        struct sk_buff *skb =
        while(neigh->state!=FAILED && (skb= dequeue(neigh->arp_queue)) != NULL) {
            write_lock(&neigh->lock);
            neigh->ops->error_report(neigh, skb);
            write_lock(&neigh->lock);
        }

    neigh_release(neigh);
}
```
