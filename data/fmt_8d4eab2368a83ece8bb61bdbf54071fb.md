
现在我们尝试根据给定的目的地址获取目的地址的路由，目前是 `nexhop`、源地址和网络接口。`Ip_route_connect` 如果成功，将返回 0。如果找到了路由，它将把 `rt` 设置为新的缓存路由。

```c
if (inet->opt && inet->opt->srr) {
  if (daddr == 0)
    return (-EINVAL);
  nexhop = inet->opt->faddr;
}
```

我们不允许 TCP 连接到非单播地址；因此，如果缓存中的路由不是单播路由，我们将返回一个错误。

```c
if (rt->rt_flags& (RTCF_MULTICAST|RTCF_BROADCAST)) {
  ip_rt_put(rt);
  return -ENETUNREACH;
}
```

```c
if (!inet->opt || !inet->opt->srr)
  daddr = rt->rt_dst;
```

```c
if (!inet->saddr)
  inet->saddr = rt->rt_src;
inet->rcv_saddr = inet->saddr;
```

```c
if (tp->ts_recent_stamp && inet->daddr != daddr) {
```

在这里，我们重置了继承的状态。

```c
/* Reset inherited state */
tp->ts_recent = 0;
tp->ts_recent_stamp = 0;
tp->write_seq = 0;
}
if (sysctl_tp_recycle &&
!tp->ts_recent_peer && rt->dst == daddr) {
struct inet_peer *peer = rt_get_peer(rt);
```

```c
if (peer && *peer->ts_stamp + TCP_PAWS_MSL >= xtime_to_sec) {
tp->ts_recent_stamp = peer->ts_stamp;
tp->ts_recent = peer->tcp_ts;
}
```

请参考第 10 章“传输层中的数据接收：UDP 和 TCP”，以获取有关代码中注释的更多信息，这些时间戳保存的想法来源于 Van Jacobson 的想法。最后使用的时间戳值保存在 socket 处于 `TIME_WAIT` 状态时的路由条目的 `inet_peer` 结构中。然后，当请求新连接时，接收到的时间戳以及 `tcp_opt` 结构中的时间戳字段将从 `inet_peer` 结构中的保存值恢复。这是为了在连接建立后检测重复段。

```c
inet->dport = usin->sin_port;
inet->daddr = daddr;
```

```c
tp->ext_header_len = 0;
if (inet->opt) {
tp->ext_header_len = inet->opt->optlen;
```

这是最小 MSS 值。

```c
tp->mss_clamp = 536;
```

虽然我们正在进行主动打开（active open），但 socket 的身份尚未确定。我们不知道源端口，因为我们还没有分配临时端口。然而，我们将自己置于 `TCP_SYN_SENT` 状态，并将 `sk` 加入 TCP 连接哈希表。初始化连接的剩余工作将在稍后完成。

```c
tcp_set_state(sk, TCP_SYN_SENT);
```

我们调用 `tcp_v4_hash_connect()` 来连接连接哈希表中的 socket。这为连接分配了一个临时端口，并将其放入 socket 的 `sport` 字段中。临时端口号作为在哈希表中查找连接 socket 的哈希码。稍后当 socket 处于 `ESTABLISHED` 状态且入站包到达该端口时，TCP 可以快速找到正确的打开 socket。

```c
err = tcp_v4_hash_connect(sk);
if (err)
    goto failure;
err = ip_route_newports(&rt, inet->sport, inet->dport, sk);
if (err)
    goto failure;
```

我们通过设置 `sock` 结构的 `dst` 字段来提交此连接的目的，使其指向与路由相关的目的。对于发送到外部目的地的数据包，`dst` 将指向网关。然而，如果目的是一个直接连接的主机，`dst` 将指向该主机的信息。

```c
__sk_dst_set(sk, &rt->u.dst);
tcp_v4_setup_caps(sk, &rt->u.dst);
tp->ext_header_len = rt->u.dst.header_len;
```

我们初始化序列号。

```c
if (!tp->write_seq)
    tp->write_seq = tcp_sequence_number(inet->saddr,
                        inet->daddr,
                        inet->sport,
                        usin->sin_port);
```

我们调用 `tcp_connect()` 完成设置连接的工作。

```c
err = tcp_connect(sk);
rt = NULL;
if (err)
    goto failure;
return 0;
```

failure:

如果失败，我们从连接哈希表中取出 socket 并释放本地端口。

```c
tcp_set_state(sk, TCP_CLOSE);
ip_rt_put(rt);
sk->sk = 0;
inet->dport = 0;
return err;
```

# 8.5 从 Socket 发送数据

在本节中，我们展示了 UDP 协议如何处理从应用层发送数据报的请求。当通过 `sendmsg()` 或任何应用层函数向 `SOCK_DGRAM` 类型写入数据时，UDP 协议处理该请求。UDP 非常简单，主要由帧组成。与 TCP 不同，它没有缓冲或连接管理。使用 UDP 头部时，目的和源端口在 socket 的 `name` 中指定。通常，当端口已知，IP 地址也是已知的。如果在 socket 的 `name` 中指定了目的地址，则在传递给 IP 之前将其保存。此外，在 IP 上传递数据包之前，UDP 检查目的是否为内部地址或必须为数据包确定路由。此外，目的可能是组播或广播地址，在这种情况下 IP 不需要路由数据包。在 UDP 完成之前，源目的端口放在 UDP 头部中，IP 地址留给 IP 处理。为了效率，构建 TCP/IP 栈时已尽可能避免拷贝或不必要的处理。所有的处理复杂度都在数据路径之外。实际数据只有一份拷贝，UDP 中只有一个层的处理。当应用调用打开 socket 上的写函数时，socket 层调用 `struct` 中 `msg` 字段指向的函数。这导致了对 `udp_sendmsg()` 的调用，它位于 `linux/net/ipv4/udp.c`。这是 `SOCK_DGRAM` socket 执行的函数。参见表 8.1 的所有 UDP 协议函数列表。

```c
int udp_sendmsg(struct sock *sk, struct msghdr *msg, int len)
```

我们检索 socket 结构的特定部分。

```c
struct inet_opt *inet = inet_sk(sk);
struct udp_opt *up = udp_sk(sk);
```

Ip 将持有第 8.3.1 节讨论的 `ip_cmg_send()` 函数的返回值。

```c
int ulen = len;
struct ip_cookie ipc;
struct rtable *rt = NULL;
int free = 0;
int connected = 0;
```

Daddr 是目的 IP 地址，`tos` 是 IP 头的 `TOS` 字段。

```c
u32 daddr, faddr, saddr;
u16 dport;
```

```c
u8 tos;
int err;
int corkreq = up->corkflag | msg->msg_flags&MSG_MORE;
```

第一个 `udp_sendmsg()` 会检查字段中的范围值，并检查调用者是否为该 socket 请求了任何非法标志。UDP 的非法标志是 `MSG_OOB`，它仅用于 `SOCK_STREAM` 类型。

```c
if (len < 0 || len > 0xFFFF)
    return -EMSGSIZE;
if (msg->msg_flags&MSG_OOB)
    return -EOPS;
```

现在，检查是否存在待处理帧。当 socket 阻塞以处理待处理帧时，必须持有 socket 锁。

```c
if (up->pending)
    lock_sock(sk);
    if (unlikely(up->pending) != AF_INET) {
```
