
```c
return NF_HOOK(PF_INET6, NF_IP_IP6_PRE_ROUTING, skb, dev,
NULL, ip6_rcv_finish);
truncated:
    IP6_INC_STATS_BH(IP6_TruncatedPkts);
err:
    IP6_INC_STATS_BH(IP6InHdrErrors);
drop:
    free_skb(skb);
out:
    return 0;
}
```

此时，处理过程与 `IPv4` 输入包处理非常相似。输入包可能在当前机器上有本地目的，也可能需要转发。数据包目的是在输入包处理的第一阶段调用 `ip_route_input` 函数时计算的。例如，如果目的是机器上的一个内部目的，`dst_entry` 中的 `input` 字段指向 `ip6_input` 函数，该函数继续输入包的处理。

### `ip6_input_finish` 函数

接下来，`ip6_input` 调用 `ip6_input_finish` 将数据包交付给上层协议。如果目的是本地可达主机，`output` 将指向 `dev_queue_xmit` 函数，该函数将输出包放入网络接口驱动程序。这一过程与 `IPv4` 相同，在前面的章节中介绍过。

```c
static inline ip6_input_finish(struct sk_buff *skb)
```

接下来，其余的处理由每个可选头部的函数完成（已处理过的逐跳头部除外）。`nextthdr` 字段可能包含可选头部的协议号，也可能是 `UDP`、`TCP`、`IGMP`、`ICMP` 或其他协议。

```c
hash = nextthdr & (MAX_INET_PROTOS - 1);
if ((ipprot = rcu_dereference(inet6_protos[hash])) != NULL) {
    int ret;
    if (ipprot->flags & INET6_PROTO_FINAL) {
```

```c
struct ipv6hdr *hdr;
nf_reset(skb);
skb_postpull_rcsum(skb, skb->raw, 
 skb->nh.raw - skb->nh.raw);

hdr = skb->nh.ipv6;
if (ipv6_addr_multicast(&hdr->daddr, &hdr->saddr)) &&
    ipv6_chk_mcast_addr(skb->dev, &hdr->saddr) &&
    ipv6_is_mld(skb, nextthdr))
 goto discard;

}
if (!(ipprot->flags & INET6_PROTO_NPOLICY)) &&
    !frm6_policy_check(NULL, XFRM_POLICY_IN, skb))
 goto discard;
```

这里我们调用为 `IP` 头 `nextthdr` 字段中定义的协议处理函数。

```c
ret = iprot->handler(&skb, &noff);
if (ret > 0)
 goto resubmit;
else if (ret == 0)
    IP6_INC_STATS_BH(IPSTATS_MIB_INDELIVERS);
else {
    if (!raw_skb) {
        if (xfrm6_policy_check(NULL, XFRM_POLICY_IN, skb))
            IP6_INC_STATS_BH(IPSTATS_MIB_INUNKNOWN_PROTOS);
            icmpv6_send(skb, ICMPV6_PARAMPROB, 
icmpv6_UNK_NEXTHDR, noff, 
skb->dev);
        }
    }
else {
    IP6_INC_STATS_BH(IPSTATS_MIB_INDELIVERS);
    kfree_skb(skb);
}
rcu_read_unlock();
return 0;
discard:
IP6_INC_STATS_BH(IPSTATS_MIB_INDISCARDS);
rcu_read_unlock();
kfree_skb(skb);
return 0;
```

# 第 11 章 协议版本 6 (IPv6)

## `IPV6` `UDP`

`IPv6` 有自己的 `UDP` 协议实现，位于 `linux/net/ipv6/udp.c` 文件。尽管 `IPv6` 的源代码大部分与 `IPv4` 分离，但所有的 socket 结构都是共享的，包括动态状态信息。

## `udpv6_init` 函数

与 `IPv4` 一样，`UDP` 有一个从 IP 初始化函数调用的初始化函数，如前文所示。`UDP` 的初始化函数是 `ipv6_init`，它位于 `linux/net/ipv6/udp.c` 文件。

```c
void __init udpv6_init(void)
{
```

与 `IPv4` 函数一样，`inet_add_protocol` 注册了协议处理程序。

```c
if (inet6_add_protocol(&udpv6_protocol, IPPROTO_UDP) < 0)
    printk(KERN_ERR "udpv6_init: Could not register protocol\n");
    inet6_register_protos(&udpv6_protos);
}
```

## `udpv6_protocol` 结构

这里显示了来自 `linux/net/ipv6/udp.c` 的 `udpv6_protocol` 结构。处理入站 `UDP` 包的处理程序是 `udpv6_recv`。

```c
static struct inet6_protocol udpv6_protocol = {
    .handler = udpv6_rcv,
    .err_handler = udpv6_err,
```

`flags` 字段被初始化为允许在入站 `UDP` 包上使用 XFR 变换。这将允许使用 SDB 进行数据安全检查。

```c
.flags = INET6_PROTO_NOLICY|INET6_PROTO_FINAL,
};
```

## `udpv6_protosw` 结构

```c
static struct inet6_protosw udpv6_protosw = {
    .type = SOCK_DGRAM,
    .protocol = IPPROTO_UDP,
```

接下来，`prot` 和 `ops` 结构在 `linux/net/ipv6/udp.c` 中初始化。

```c
.prot = &udp6_prot,
.ops = &inet6_dgram_ops,
```

`capability` 字段与权限有关。与 `IPv4` 的情况类似，每个人都拥有发送数据报的权限。

```c
.capability = -1,
.no_check = UDP_CSUM_DEFAULT,
.flags = INET_PROT_PERMANENT,
};
```

## `udpv6_prot` 结构

`IPv6` 的 `UDP` `prot` 函数定义如下。该结构将 socket 调用映射到特定的协议函数。此数据结构在 `linux/net/ipv6/udp.c` 中初始化。

```c
struct proto udpv6_prot = {
.name = "UDPv6",
.close = ipv6_close,
.connect = ipv6_udp_connect,
```

以下函数是与 `IPv4` 共享的。有趣的是，尽管对于 `SOCK_DGRAM` socket，socket `ioctl` 是不同的，但协议级的 `ioctl` 与 `IPv4` 相同。

```c
.disconnect = udpv6_disconnect,
.ioctl = ipv6_ioctl,
.destroy = ipv6_destroy,
.setsockopt = ipv6_setsockopt,
.getsockopt = ipv6_getsockopt,
.sendmsg = ipv6_sendmsg,
.recvmsg = ipv6_recvmsg,
.backlog_rcv = ipv6_queue_rcv,
.hash = ipv6_hash,
.unhash = ipv6_unhash,
.get_port = ipv6_get_port,
.obj = sizeof(struct ipv6_sock),
};
```

# 第 11 章 协议版本 6 (IPv6)

我们之前注意到 `IPv6` 有自己的 `UDP` 实现。需要独立函数有两个原因：由于地址格式需要不同的比较逻辑，在对入站包查找目的 socket 时需要进行地址比较；第二个原因是我们需要通过 `IPv6` socket 发送和接收 `AF_INET` 目的的消息，这需要一些处理。

## `udpv6_sendmsg` 函数
