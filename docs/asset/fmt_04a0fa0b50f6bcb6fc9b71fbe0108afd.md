
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

如果没有找到有效的目的地址，`udp_sendmsg` 返回 `EINVAL`。

### 8.5.1 处理控制消息

让我们继续查看 `udp_sendmsg` 如何处理控制消息。它通过 `msghdr` 中的 `name` 字段来验证地址。如果应用程序调用了 `sendto` socket API 调用，那么 `msghdr` 的 `name` 将包含最初在 `sendto` 调用字段中指定的地址。

```c
struct sockaddr_in *usin = (struct sockaddr_in*)msg->msg_name;
if (msg->msg_len < sizeof(*usin))
    return -EINVAL;
if (usin->sin_family == AF_INET) {
    if (usin->sin_family != AF_UNSPEC)
        return -EINVAL;
}
```

`Udp_msg` 通过查找 `msghdr` 结构体中 flags 字段的 `MSG_CONFIRM` 标记来检查应用程序是否请求路由确认。如果需要，将调用 `dst_confirm` 来执行路由。

```c
if (msg)->msg_flags&MSG_CONFIRM)
    goto do_confirm;
```

在此时，将调用 `ip_build_xmit` 将数据包传递到 IP 层。

```c
back_from_confirm:
saddr = rt->rt_src;
if (!ipc.addr)
    daddr = ipc->addr = rt->rt_dst;
lock_sock(sk);
if (unlikely(up->pending)) {
```

检查 sock 是否正确。这一定是一个 cork（套塞）空气相关的 bug。

```c
release_sock(sk);
NETDEBUG(if (net_ratelimit())) printk(KERN_DEBUG "udp app bug 2 \n");
err = -EINVAL;
    goto out;
}
```

为了追加额外数据，对 socket 进行 cork 操作。

```c
inet->cork.cork_fl4_dst = daddr;
inet->cork.cork_fl4_ipport = dport;
inet->cork.cork_fl4_src = saddr;
inet->cork.cork_fl4_ipport = inet->sport;
up->pending = AF_INET;
```

现在我们通过调用 `ip_append_data` 将数据发送到 IP，该函数从单个数据片段构建一个大的数据报文。第二个参数 `ip_generic_getfrag` 是回调函数，由 IPV4 在准备好从用户空间复制实际数据到数据报文时执行。

```c
do_append_data:
up->len += ulen;
err = ip_append_data(sk, ip_generic_getfrag, msg->msg_iov, ulen,
    sizeof(struct udphdr), &ipc, rt,
    corkreq = msg->msg_flags|MSG_MORE : msg->msg_flags;);
if (err)
    udp_flush_pending_frames(sk);
else if (!corkreq)
    err = udp_push_pending_frames(sk, up);
release_sock(sk);
out:
ip_rt_put(rt);
if (free)
    kfree(ipc->opt);
if (err)
    UDP_INC_STATS_USER(UdpOutDatagrams
```

`return len;`
`return err;`
`do_confirm:`

如果该路由存在邻接缓存，`dst_confirm` 会为邻接缓存中的现有条目加上戳。

```c
dst_confirm(&rt->u.dst);
```

如果此 socket 设置了 `MSG_PROBE` 标记，则应该对传输路径探测最大 MTU，但不应发送缓冲区。

```c
if (!msg->msg_flags&MSG_PROBE) || len
goto back_from_confirm;
err = 0;
goto out;
```

## 8.5.3 从用户空间拷贝数据到数据报文

本节涵盖了从用户空间获取数据片段并追加到数据报文函数 `ip_generic_getfrag`。该函数定义在 `linux/net/ipv4/dp_output.c` 中。该函数作为回调由同一文件中的 `ip_append_data` 函数调用。

`ip_append_data` 检查校验和是否禁用。用户数据组织在由 `iov` 的一个或多个指针中。通常，每个 UDP 数据报文只有一个缓冲区。

```c
int ip_generic_getfrag(void *from, char *to, int offset, int len,
int odd, struct sk_buff *kb)
(
```

UDP 头部不需要从用户空间拷贝到内核空间。我们通过 `udp_msend` 函数调用两个函数之一，根据我们的输出缓冲区是否具有硬件校验和能力来拷贝数据。两个函数之一的 `checksum_part_from_end` 在拷贝时计算部分校验和。另一个函数 `memcpy_from_end` 是我们在硬件中计算校验和时使用的函数，因为该函数本身不计算校验和。UDP 校验和包含了 IP 头部的部分、源地址和目的地址、IP 头部协议以及长度。因此，校验和分三个阶段完成：一次针对数据，一次针对实际的 UDP 头部，第三次针对 IP 头部。

```c
struct iov *iov = from;
if (kb->ip_summed == CHECKSUM_HW) {
	if (memcpy_from_end(to, iov, offset, len) < 0) {
	return -EFAULT;
}
} else {
unsigned int csum = 0;
```
