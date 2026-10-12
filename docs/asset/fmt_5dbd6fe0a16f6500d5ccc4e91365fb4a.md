
## 处理 UDP 发送与路由逻辑

以下代码段展示了在 `udp_sendmsg` 处理过程中的跳转、资源释放及头部长度计算：

```c
goto do_append_data;
}

release_sock(sk);
```

我们将 UDP 头部长度加到用户数据的长度上：

```c
len += sizeof(struct udphdr);
```

接下来在 `udp_sendmsg` 中，我们检查是否存在有效的地址或者 socket 是否处于连接状态。由于历史原因，socket 的名称包含了地址。我们通过检查 `msghdr` 结构中的 `name` 字段来验证地址。如果已经在 socket 名称中指定了目标 IP 地址，它在数据包传递给 IP 之前会被保存。

```c
if (msg->name) {
    struct sockaddr_in *usin = (struct sockaddr_in*)msg->name;
    if (msg->namelen < sizeof(usin))
}
```

### `udphdr` 结构

`udphdr` 结构定义在 `linux/include/udp.h` 中，包含了实际的 UDP 头部，包括源端口、目的端口、长度和校验和。在 `udp_sendmsg` 函数中，UDP 头部是 `msghdr` 中的一个字段。

```c
struct udphdr {
    __u16 source;
    __u16 dest;
    __u16 len;
    __u16 check;
};
```

### `udp_sendmsg` 函数处理控制消息

继续分析 `udp_sendmsg` 函数查看它是如何处理控制消息的。`udp_sendmsg` 的下一步是确定 `msg` 是否指向控制消息。它检查 `msg_control` 字段是否为非零。指向 `ipc` 的 `ipcm_cookie` 结构持有控制消息处理的结果。最初 `ipc` 的某些字段会被初始化，例如 IP 选项和接口（如果有的话）。

```c
ipc.addr = inet->saddr;
ipc.oif = sk->bound_dev_if;

if (msg->msg_control) {
}
```

控制消息也被称为辅助数据（ancillary data），是扩展 IPv6 socket 接口的一部分。有关控制消息的更多信息，请参见 Linux 手页 `cmsg(3)` 和“IPv6 Socket API” [RFC 2292]。如果 `msg` 包含控制消息指针，定义在 `linux/net/ipv4/ip_sockglue.c` 中的函数 `ip_cmsg_send` 将处理该请求。这些控制消息是设置和获取 UDP 信息（如地址和端口）的一种方式。in 选项结构中的字段可以通过控制消息直接检索。

```c
err = ip_cmsg_send(msg, &ipc);
if (err)
    return err;

if (ipc.opt)
    free = 1;
connected = 0;

if (!ipc.opt)
    ipc.opt = inet->opt;

saddr = ipc.addr;
ipc.addr = faddr = daddr;

if (ipc.opt && ipc->opt->srr)
    if (!ldaddr)
        return -EINVAL;
```

函数 `ipc_cmsg_send` 将结果存储在 `ipc` 中，它指向在 `linux/include/net/ip.h` 文件定义的 `ipcm_cookie` 结构。

### `ipcm_cookie` 结构

```c
struct ipcm_cookie {
  u32 addr;
  int oif;
  struct ipcm_options *opt;
};
```

UDP 处理两种类型的消息。`IP_RECVOPTS` 从 IP 头部获取 `options` 字段并返回 IP 头部中选项的指针。如果在控制消息中指定了 `IP_PKINFO`，`ipc_cmsg_send` 会将接口索引返回 `ipc` 的 `oif` 字段，并将接口的 IP 地址返回 `addr` 字段。

### `udp_sendmsg` 函数与数据包输出

我们继续对 `udp_sendmsg` 函数进行检查。此时，UDP 头部需要的一些信息已经建立。我们可以将数据包放入 IP 队列，让其添加头部并传递给设备驱动程序进行传输。然而，我们将看到这并不简单。尽管我们拥有了所有的头部信息，但我们并没有直接传输数据包；而是将数据发布到套接字持有的队列中。实际上，内存映射页直接从用户空间映射到指向该套接字的数组上。尽管这看起来很复杂，但它允许 IP 以相同的方式处理流式数据、分段数据和数据报文。

首先，我们将检查 IP 是如何路由此数据包的。当然，我们在这里并没有实际执行路由，主要是检查我们是否有一个有效的缓存路由，以减少 IP 在接收数据包时的负载。

```c
tos = RT_TOS(inet->tos);
if (sock_flag(sk, SOCK_LOCALROUTE) ||
  (msg->msg_flags & MSG_DROUTE) ||
  (ipc->opt->is_strictroute) {
    tos |= RTO_ONLINK;
    connected = 0;
}
```

此外，如果数据包是为了通过已连接的套接字传输，则假设目标地址已经已知，并且该数据包中已经存在通往目标地址的路由。如果目标地址是多播地址，则也不需要路由该数据包。

```c
if (MULTICAST(daddr)) {
    if (!ipc.oif)
        ipc.oif = inet->mc_index;
    if (saddr)
        saddr = inet->mc_addr;
}
connected = 0;

if (connected) {
    rt = (struct rtable*)sk_dst_check(sk, 0);
    if (rt == NULL) {
}
```

如果我们没有路由，我们将通过构建一个与路由相关的流信息结构为准备路由表做准备。关于 IP 路由的更多细节，请参阅第 8 章。

```c
struct flowi fl = {.oif = ipc.oif,
                nl_u = {.ip4_u =
                    .daddr = faddr,
                    .saddr = saddr,
                    .tos = tos },
                .proto = IPPROTO_UDP,
                uli_u = {.ports =
                            .sport = inet->sport,
                            .dport = dport } };
```

我们调用 `ip_route_output` 尝试找到一条路由。关于 `ip_route_output` 以及路由表项如何被操作和搜索的更多信息，请参阅第 9 章。

```c
err = ip_route_output_flow(&rt, &fl, sk,
                                    !(msg->msg_flags&MSG_DONTWAIT));
if (err)
    goto out;
err = -EACCES;
```

如果路由缓存条目指示为广播，但套接字没有 `SO_BROADCAST` 标记，那么这是一个错误。

```c
if (rt->rt_flags&RTCF_BROADCAST &&
    sock_flag(sk, SOCK_BROADCAST))
    goto out;
```

现在我们知道有一条良好的路由，所以如果套接字已连接，我们会在目标缓存中设置指向路由的指针。关于目标缓存的更多信息，请参阅第 5 章。

```c
if (connected)
    sk_dst_set(sk, dst_clone(&rt->u.dst));
```

接下来，`udp_sendmsg` 通过查找 `msghdr` 结构字段中的 `MSG_CONFIRM` 标记来检查应用程序是否请求路由确认。如果需要，将调用 `dst_confirm` 来确认路由。

```c
if (msg->msg_flags&MSG_CONFIRM)
    goto do_confirm;
```
