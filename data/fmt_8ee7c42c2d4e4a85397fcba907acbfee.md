
```c
if (addr_type == IPv6_ADDR_MAPPED) {
    u32 exthrdlen = icsk->icsk_ext_hdr_len;
    struct sockaddr_in sin;
    SOCKET_DEBUG(sk, "connect: ipv4 mapped\n", (sk)
    if (_ipv6_only_sock(sk)) {
        return -ENETUNREACH;
        sin.sin_family = AF_INET;
        sin.sin_port = usin->sin6_port;
        sin.sin_addr.s_addr = usin->sin6_addr.s6_addr32[3];
    }
}
```

```c
icsk->icsk_af_ops = &ipv6_mapped;
sk->backlog_rcv = tcp_v4_do_rcv;
err = tcp_v4_connect(sk, (struct sockaddr*)&sin, sizeof(sin));
if (err) {
    icsk->icsk_ext_hdr_len = exthrdlen;
    icsk->af_ops = &ipv6_specific;
    sk->backlog_rcv = tcp_v4_do_rcv; // 注意：此处原文为ipv6_addr_set(&np->saddr, 0, 0, htonl(0xffff), inet->saddr); 逻辑上应为处理错误
} else {
    ipv6_addr_set(&np->saddr, 0, 0, htonl(0xffff), inet->saddr);
    ipv6_addr_set(&np->rcv_saddr, 0, 0, htonl(0xffff), inet->saddr);
}
return err;
failure:
```

我们将接收函数设置为`IPv4`的函数，然后使用地址的`IPv6`部分调用`connect`函数。

## `IPv6` ICMP 协议

`IPv6`的`ICMP`协议与`IPv4`的`ICMP`类似，但有一些变化。目的不可达（destination unreachable）、回显（echo request）和回显（echo reply）消息类似于`RFC 2463`。此外，`ICMPv6`的实现将在第 8 章讨论。

## `icmpv6_rcv` 函数

`icmpv6_rcv`函数是`IPPROTO_ICMPv6`数据包的处理程序。它实现在`net/ipv6/icmp.c`中。与本章涵盖的其他函数一样，我们不会查看整个函数。我们只检查`IPv6`特有的或感兴趣的部分。我们将跳过准备工作，展示如何处理每种`ICMPv6`数据包。

```c
static int icmpv6_rcv(struct sk_buff *pskb, unsigned int type) {
switch (type) {
case ICMPV6_ECHO_REQUEST:
    // 以与 IPv4相同的方式处理回显请求 (ping)
    icmpv6_echo_reply(pskb);
    break;
case ICMPV6_ECHO_REPLY:
    // 对于接收的回显回复 ICMP 包不需要特殊处理
    break;
case ICMPV6_BIG:
    // 在这里我们处理数据包过大的消息，因此启动 MTU 发现。注释中建议如果支持支持分片我们应该更新目的缓存。然而，当前版本的目的缓存不支持此。
    if (!pskb_may_pull(pskb, sizeof(struct ipv6hdr)))
        goto discard;
    struct icmp6hdr *hdr = (struct icmp6hdr *)pskb->raw;
    struct ipv6hdr *orig_hdr = (struct ipv6hdr *)(hdr + 1);
    // 我们尝试进行路径 MTU 发现，这有望减小该路由的 MTU。
    rt_pmtu_discovery(&orig_hdr->daddr, &orig_hdr->saddr, dev, ntohl(hdr->icmp6_mtu));
```

对于这些错误类型的数据包，我们不采取行动。通过通知它们，我们通过打开的`socket`通知应用程序该问题。

```c
case ICMPV6_DEST_UNREACH:
case ICMPV6_TIME_EXCEED:
case ICMPV6_PARAM:
  icmpv6_notify(pskb, type, hdr->icmp6_code, hdr->icmp6_mtu);
```

接下来的四个数据包类型是邻接发现包。这些将在下一节介绍。

```c
case NDIS_ROUTER_SOLICITATION:
case NDIS_ROUTER_ADVERTISEMENT:
case NDIS_NEIGHBOUR_SOLICITATION:
case NDIS_NEIGHBOUR_REDIRECT:
case NDIS_REDIRECT:
  ndisc_rcv(pskb);
  break;
```

在`IPv6`中，多播组管理报告和查询被定义为`ICMP`消息 [RFC 2710]。当我们接收这些消息时，将其转发给`IPv6`的`IGMP`协议。我们将在后面的部分讨论这些消息类型。

```c
case ICMPV6_MGM_QUERY:
  igmpv6_event_query(pskb);
  break;
case ICMPV6_MGM_REPORT:
  igmpv6_event_report(pskb);
  break;
case ICMPV6_MGM_REDUCTION:
case ICMPV6_NI_QUERY:
case ICMPV6_NI_REPLY:
case ICMPV6_MLD2_REPORT:
case ICMPV6_DHAAD_REQUEST:
case ICMPV6_DHAAD_REPLY:
case ICMPV6_MOBILE_PREFIX_SOL:
case ICMPV6_MOBILE_PREFIX_ADV:
  break;
default:
  LIMIT_NETDEBUG(KERN_DEBUG, "icmp6: msg of unknown type\n");
```

这种类型是信息性的。

```c
if (type & ICMPV6_INFOMSG_MASK)
  break;
```

我们有一个未知错误。我们将通知上层。

```c
icmpv6_notify(pskb, hdr->icmp6_code, hdr->icmp6_mtu);
}
```

## `IPv6` 邻接发现 (NDISC)

`ND`协议用于主机和路由器在本地连接网络上的相互发现 [RFC 2461]。该协议替换了`IPv4`中的两种协议。其中一种在`IPv6`中不再需要的协议是`ARP`。在`IPv4`中，`ARP`被用于将`IP`地址映射到链路层地址。正如我们在本章早期看到的，这不再是必要的，因为`IPv6`地址包含链路本地地址类型，链路层地址被构建在`IPv6`地址本身中。另一个用于`IPv4`的机制是路由器发现 [RFC 1256]。路由器发现是一种路由器定期发送包含通告地址和偏好的公告的协议。主机在公告中选择默认网关。

我们在第 5 章涵盖了通用邻居系统。在那个章节中，我们讨论了邻居系统是如何为`ND`协议设计的，尽管它也用于`ARP`缓存。在本节中，我们将看到`ND`协议如何利用通用邻居发现缓存和其他设施。我们还将看到哪些部分是`IPv6`特有的。

### `nd_table` 结构

我们创建一个通用邻居表的本地实例来形成邻居发现缓存。邻居`nd_tbl`是在`net/ipv6/ndisc.c`文件中初始化的。

```c
struct neigh_table_nd_tbl = {"
```

构造函数和代理构造函数成员函数设置如下：

```c
.constructor = ndisc_constructor,
.pconstructor = pndisc_constructor,
.pdestructor = pndisc_destructor,
.proxy_redo = pndisc_redo,
}
```

# 592 嵌入式系统的 `Linux` `TCP/IP` 网络

## `ndisc_generic_ops` 结构

该结构也实现在文件`linux/net/ipv6/ndisc`中。

```c
static struct neigh_ops ndisc_generic_ops = {
    .family = AF_INET6,
```

接下来的两个函数是`IPv6`特有的函数。

```c
.solicit = ndisc_solicit,
.error_report = ndisc_error_report,
```

接下来的四个函数与用于`IPv4`邻居缓存和`ARP`协议的函数相同。
