
```c
    if (oif)
        oif = sk->protoinfo.of_inet.mc_index;
    if (saddr)
        saddr = sk->protoinfo.of_inet.mc_addr;
}
```

这是该函数中最重要的调用。`ip_route_connect` 获取通往 `usin` 中目的地的路由，并设置 `rt` 指向缓存的路由。如果它返回非零值，说明它找到了路由或在路由缓存中添加了新路由，因此我们返回错误错误。如果它找到了广播路由，我们也返回错误。

```c
err = ip_route_connect(&rt, usin->sin_addr.addr, saddr,
              RT_CONN_FLAGS(sk), oif, IPPROTO_UDP, inet->sport,
              usin->sin_port, sk);
```

```c
if (err) {
    return err;
}
if ((rt)->rt_flags & RTCF_BROADCAST) && !sk_flag(sk, SOCK_BROADCAST)) {
    ip_rt_put(rt);
    return -EACCES;
}
if (!sk->saddr)
```

在这里，我们通过路由缓存项中的字段更新出站数据包的源地址和目的地址。目的由用户指定。

```c
sk->saddr = rt->rt_src;
if (!sk->rcv_saddr)
    sk->rcv_saddr = rt->rt_dst;
sk->dport = usin->sin_port;
```

我们将状态置为 `TCP_ESTABLISHED`，以表示这是一个缓存路由。此值对于 UDP 套接字来说是误导性的，但它仅仅是为了显示该套接字关联了一个缓存路由。稍后，当用户尝试传输数据包且在 `send` 调用中缺少源地址时，我们认为这是正常的，因为状态表明路由已建立。

```c
sk->state = TCP_ESTABLISHED;
inet->id = jies;
```

最后，指向路由的指针被设置在 `dst` 字段中。

```c
sk_dst_set(sk, &rt);
return(0);
}
```

## 8.5 通过 UDP 从 Socket 发送数据

在本节中，我们将展示 UDP 协议如何处理来自应用层的发送数据报的请求。当用户程序通过调用 `sendmsg` 或任何其他应用程序发送函数向 `SOCK_DGRAM` 类型写入数据时，UDP 协议将处理该请求。UDP 相当简单，主要由一个分帧层组成。它做的事情仅仅是在用户数据前加上一个 UDP 头部。与 TCP 不同，它没有缓冲或连接管理。为了构建 UDP 头部，对端名称（peer name）中共同指定了目的端口和源端口。通常，已知端口时，IP 地址也是知的。如果 socket 名称中指定了目标地址，它会在数据包传递给 IP 之前保存。此外，在将数据包传递给 IP 之前，UDP 会检查目标是内部的，还是 IP 必须为数据包确定路由。此外，目标地址可能是组播或广播地址，在这种情况下，IP 不需要对数据包进行路由。在 UDP 完成之前，源端口和目的端口被放入 UDP 头部中，IP 地址被保留以供 IP 后续处理。

了解 Linux TCP/IP 栈是如何为了效率而构建的非常有趣。所有的努力都是为了避免拷贝和不必要的处理。所有处理的复杂性都在数据包的路径之外。实际数据只有一个拷贝，且 UDP 中只有一层处理。

当应用程序调用已打开 socket 上的某个写函数时，socket 层会调用由 `prot` 结构体中 `sendmsg` 字段指向的函数。关于 socket 层发生的详细信息，请参阅第 5 章“Linux Sockets”。这将导致对 `udp_sendmsg` 的调用，该函数位于 `linux/ipv4/udp.c`。这是为 `SOCK_DGRAM` 类型 socket 执行的发送函数。请查看表 8.1 获取 UDP 的所有协议块函数列表。

```c
int udp_sendmsg(struct sock *sk, struct msghdr *msg, int len)
```

我们获取 socket 结构体的特定部分。

```c
struct inet_opt *inet = inet_sk(sk);
struct udp_opt *up = udp_sk(sk);
```

我将保留第 8.3.1 节讨论的函数 `ip_cmg_send` 的返回值。

```c
int ulen = len;
struct icmp_cookie ipc;
struct rtable *rt = NULL;
int free = 0;
int connected = 0;
```

`daddr` 用于目的 IP 地址，`tous` 用于 IP 头部的 TOS 字段。

```c
u32 daddr, faddr, saddr;
u16 dport;
```

```c
u8 tos;
int err;
int corkreq = up->corkflag || msg->msg_flags&MSG_MORE;
```

第一个 `udp_sendmsg` 确实会检查字段中超出范围的值，并检查调用者是否为该 socket 请求了任何非法标志。UDP 的唯一非法标志是 `MSG_OOB`，它仅用于 `SOCK_STREAM` 类型 socket。

```c
if (len < 0 || len > 0xFFFF)
    return -EMSGSIZE;
if (msg->msg_flags&MSG_OOB)
    return -EOPNOTSUPFS;
```

现在，检查是否存在任何待处理的帧。当 socket 被塞住（corked）以处理待处理帧时，必须持有 socket 。

```c
if (up->pending)
    lock_sock(sk);
    if (unlikely(up->pending) != AF_INET) {
        release_sock(sk);
        return -EINVAL;
    }
    goto do_append_data;
release_sock(sk);
```

我们将 UDP 头部长度加到用户数据的长度上。

```c
len += sizeof(struct udphdr);
```

接下来，`udp_sendmsg` 检查确保存在有效的目的地址，或者 socket 处于连接状态。它通过 `msghdr` 中的 `name` 字段验证地址。如果应用程序调用了 `sendto` socket API 调用，那么 `msghdr` 的 `name` 将包含最初在 `sendto` 调用字段中指定的地址。

```c
struct sockaddr_in *usin = (struct sockaddr_in*)msg->msg_name;
if (msg->msg_len < sizeof(*usin))
    return -EINVAL;
if (usin->sin_family == AF_INET) {
    if (usin->sin_family != AF_UNSPEC)
        return -EINVAL;
}
```

此时，我们已经有了目的地址和源地址。端口被放在 `msghdr` 结构体中 `usin` 指向的 `udphdr` 的 `dest` 字段中。

```c
daddr = usin->sin_addr.s_addr;
dport = usin->sin_port;
if (dport == 0)
    return -EINVAL;
} else {
```

我们指定的目的地址是 NULL。但是，如果 socket 是连接的 socket，我们可以允许数据包传输，这通过 `state` 字段被设置为 `TCP_ESTABLISHED` 来指示。当 socket 连接时，我们假设目的地址已经已知。

```c
if (sk->state != TCP_ESTABLISHED)
    return -ECONN;
daddr = inet->daddr;
dport = inet->dport;
```

如果 socket 已连接，IP 层的路由可以使用“快速路径”来绕过路由表查找并直接使用缓存。

```c
connected = 1;
```

定义在 `include/linux/udp.h` 中的 `udphdr` 结构体包含实际的 UDP 头部，包括源端口、目的端口、长度和校验和。在 `udp_sendmsg` 函数中，UDP 头部是 `udh` 结构中的一个字段。

```c
struct udphdr {
    u16 source;
    u16 dest;
    u16 len;
    u16 check;
};
```
