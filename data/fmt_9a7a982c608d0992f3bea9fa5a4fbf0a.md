
```c
rth->u.dst.output = ip_rt_output;
atomic_set(&rth->u.dst_refcnt, 1);
rth->u.dst.flags = DST_HOST;
  if (in->dev->cnf.no_policy)
    rth->u.dst.flags = DST_NOLPOLICY;
rth->fl1_fl4_dst = daddr;
rth->rt_dst = daddr;
rth->fl1_fl4_tos = tos;
#ifdef CONFIG_IP_ROUTE_FWMARK
  rth->fl1_fl4_fwmark = skb->nfmark;
#endif
rth->fl1_fl4_src = saddr;
rth->rt_src = saddr;
#ifdef CONFIG_NET_CLS_ROUTE
  rth->u.dst.tclassid = itag;
#endif
```

目的设备是回环设备。输入接口被设置为接收我们尝试路由的数据包的网络接口。`dst_entry` 结构最重要的字段是输入函数指针，它被设置为 `ip_local_deliver`。该函数将接收任何使用路由缓存中该条目的输入包。除了路由标志外，如果 `rt_flags` 具有 `RTCF_LOCAL`，则表示入站数据包用于本地消费。

```c
rth->rt_iif = dev->ifindex;
rth->fl1_iif = dev->ifindex;
rth->u.dst.dev = &loopback_dev;
dev_hold(rth->u.dst.dev);
rth->idev = in_dev_get(rth->u.dst.dev);
rth->rt_gateway = daddr;
rth->rt_spec_dst = spec_dst;
rth->u.dst.input = ip_local_deliver;
rth->rt_flags = flags|RTCF_LOCAL;
```

`done:`

```
in_dev_put(in_dev);

if (out_dev)
    in_dev_put(out_dev);

if (free_res)
    fib_res_put(&res);

out: return err;
```

## 406 嵌入式系统的 Linux TCP/IP 网络

如果我们从 `no_route` 标签跳转到这里，说明 FIB 结果中的路由类型为不可达，此时我们指示错误并设置本地标志。

```c
if (res.type == RTN_UNREACHABLE) {
    rth->u.dst.input = ip_error;
    rth->u.dst.error = -err;
    rth->rt_flags = -RTFC_LOCAL;
}
rth->rt_type = res.type;
```

在这里，我们计算哈希码并设置路由，同时在套接缓冲区中设置目的缓存项。任何后续到达相同目的的数据包将通过本章之前介绍的路径进入内部目的地。

```c
hash = rt_hash_code(daddr, saddr ^ (fl.if << 5), tos);
err = rt_intern_hash(hash, rth, rth, (struct rtable*)&skb->dst);
goto done;
```

如果 FIB 搜索表明我们尝试路由的数据包目的地不可达，则会进入 `no_route` 标签。

```c
no_route:
RT_CACHE_STAT_INC(in_no_route);
spec_dst = inet_select_addr(dev, 0, RT_SCOPE_UNIVERSE);
res.type = RTN_UNREACHABLE;
goto local_input;
```

如果我们之前的 FIB 搜索表明目的地址是“火星地址”（完全未知），我们会记录相应的错误，但不缓存路由。

```c
martian_destination:
RT_CACHE_STAT_INC(in_martian_dst);
#ifdef CONFIG_IP_ROUTE_VERBOSE
    if (IN_DEV_LOG_MARTIANS(in_dev) && net_ratelimit())
        printk(KERN_WARNING "martian destination %u.%u.%u.%u from "
               "%u.%u.%u.%u"
```

```c
e_hostunreach:
    err = -EHOSTUNREACH;
goto done;
e_invalid:
    err = -EINVAL;
goto done;
```

## 第 8 章 网络层，IP 407

```c
e_nbufs:
    err = -ENOBUFS;
goto done;
```

FIB 搜索表明源地址是火星地址，我们同样增加了统计信息。RFC 1812 第 5.3.8 节根据数据包进入接口源地址的可达性对源地址验证提供了一些提示。这些操作都在 `ip_handle_martian_source` 函数中完成。

```c
martian_source:
ip_handle_martian_source(dev, in_dev, skb, daddr, saddr);
goto e_inval;
}
```

## 路由输出包

在本节中，我们将讨论 IP 在数据包传输之前如何为数据包选择路由。如果目的主机直接连接到发送机，则目的地址可以通过 ARP 或其他地址解析协议转换为链路层地址，数据包可以通过这种方式发送。这看起来似乎是一个相当简单的过程。然而，如果目的不可直接到达，情况就会变得复杂。如果发送机上有多个网络接口设备，IP 协议必须决定如何路由数据包。此外，它必须选择将接收数据包的网关或下一跳。

在 UDP 发送数据报文之前，它会请求目的地址的路由。然而，TCP 在发送数据包时已经建立了到目的地的路由。TCP 在应用程序发出套接字调用时请求输出包的路由。这是因为一旦 TCP 激活，TCP 传输对于通过打开套接字发送的所有分段都会使用缓存的路由。

## `ip_route_connect` 函数

无论传输 TCP 还是 UDP 数据包，定义在 `linux/include/net/route.h` 中的 `ip_route_connect` 解析输出包路由的主要函数。

```c
static inline int ip_route_connect(struct rtable **rp,
                               u32 dst, u32 src,
                               u32 tos, int oif, u8 protocol,
                               u16 sport, u16 dport, struct sock *sk)
```

## 408 嵌入式系统的 Linux TCP/IP 网络

作为输入路由解析函数，之前检查过的 `flowi` 结构体使用尝试在路由缓存中进行路由匹配的信息进行初始化。如果缓存中无法匹配路由，它还被用于 FIB 搜索。

```c
struct flowi fl = { .oif = .oif,
                   .nl_u = { .ip4_u = { .addr = dst,
                               .saddr = src,
                               .tos = tos },
                   .proto = protocol,
                   .uli_u = { .sport = sport,
                             .dport = dport } };
```

```c
int err;
if (!dst && !src) {
```

我们调用快速路径路由函数。随后，如果缺失，我们会尝试更新源地址和目的地址。如果源地址和目的地址都已定义，则向 `sk` 传递指针。

```c
return ip_route_output_flow(rp, &fl, sk);
}
```

## `ip_route_output_flow` 函数

`linux/net/ipv4/route.c` 文件中的 `ip_route_output_flow` 函数如果 `flowi` 结构中的协议设置为 NAT 或其他非零值，它可以自动转换路由。

## 第 8 章 网络层，IP 409

```c
int ip_route_output_flow(struct rtable **rp, struct flowi *fl, struct sock *sk, int flags)
{
  int err;

  if ((err = ip_route_output_key(rp, fl)) != 0)
    return err;
```
