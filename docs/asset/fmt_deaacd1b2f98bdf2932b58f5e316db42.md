
设置应用程序的地址长度。检查套字队列是否有任何消息，如果有，通过调用 `ip_rcv_error` 处理。通过通用 datagram 函数 `skb_recv_datagram` 从套字接收队列中移除数据包，如果返回错误则退出。

```c
if (addr_len)
    *addr_len = sizeof(struct sockaddr_in);
if (flags & MSG_REQUEUE)
    return ip_rcv_error(sk, msg, len);
```

```c
skb = skb_recv_datagram(sk, flags, &err);
if (!skb)
    goto out;
```

检查用户请求的数据多于 `skb` 中的负载。

```c
copied = skb->len - sizeof(struct udphdr);
if (copied > len)
    msg->msg_flags |= MSG_TRUNC;
```

套字缓冲区中的 `ip_summed` 字段决定了是否需要校验和。如果 `ip_summed` 不等于 `CHECKSUM_UNNECESSARY`，则必须在计算校验和的同时将数据从内核空间拷贝到用户空间。拷贝和校验和由 `skb_copy_datagram_iovec` 完成。然而，如果不需要校验和，由于数据跨越了多个缓冲区，计算了部分校验和，在这种情况下，`__udp_checksum_complete` 完成校验和。校验和是整数和为零量。校验和可以部分并在稍后完成。

```c
if (skb->ip_summed == CHECKSUM_UNNECESSARY) {
    err = skb_copy_datagram_iovec(skb, sizeof(struct udphdr),
                               msg->msg_iov, copied);
} else if (msg->msg_flags & MSG_TRUNC) {
    if (__udp_checksum_complete(skb))
        goto csum_copy_err;
    err = skb_copy_datagram_iovec(skb, sizeof(struct udphdr),
        msg->msg_iov, copied);
} else {
    err = skb_copy_and_csum_datagram_iovec(skb, sizeof(struct udphdr),
        msg->msg_iov);
}
    if (err == -EINVAL) {
        goto csum_copy_err;
    }
if (err) {
    out_free;
}
```

接下来，为数据包源打戳。如果用户提供了有效的缓冲区 `sin` 来接收数据包的源地址和端口，则信息从数据包头拷贝。

```c
recv_timestamp(msg, sk, skb);
if (sin) {
    sin->sin_family = AF_INET;
    sin->sin_port = skb->uh->source;
    sin->sin_addr.saddr = skb->ip->saddr;
    memset(sin->sin_zero, 0, sizeof(sin->sin_zero));
}
```

在离开之前，`udp_recv` 检查控制消息标志 `cmsg_flags` 以查看是否设置了任何 IP 套字选项。例如，某些套字如 `IP_TOS` 需要将 IP 头部的一部分拷贝到用户空间。如果设置了任何标志，`cmsg_recv` 将检索相关的选项值。

```c
if (sk->protinfo.af_inet.cmsg_flags)
    ip_cmsg_recv(msg, skb);
err = copied;
```

`udp_recv` 结尾有三个错误。最有趣的是 `csum_copy_err`。

```c
out_free:
    skb_free_datagram(sk, skb);
out:
    return err;
csum_copy_err:
    UDP_INC_STATS_BH(UdpInErrors);
```

```c
skb_unlink(skb, &sk->receive_queue);
clear = 1;
}
spin_unlock_irq(&sk->receive_queue.lock);
if (clear)
kfree_skb(skb);
}
skb_free_datagram(sk, skb);
return -EAGAIN;
```

## 10.5 TCP 中的接收接收

在 10.3 节中，我们展示了 IP 协议如何根据 IP 头的协议字段分发 UDP 接收函数。这一机制在第 6 章中进行了详细介绍。与 UDP 类似，TCP 也会初始化一个 `inet_protocol` 结构体实例。该结构允许网络层（IP）根据 IP 头部协议字段的值来分发传输层处理函数，而无需了解每个传输层协议的内部结构。能够可视化状态管理对于深入理解 TCP 很有帮助。图 10.1 显示了 TCP 接收端状态机。发送端 TCP 状态图请参见第 8 章图 8.1。

![](img/c1f701734d482a86a48e8bfd231c6fdb_372_0.png)

图 10.1：TCP 接收端状态图。

一些关键标志位定义主要用于 TCP 的接收端（参见表 10.1）。这些定义位于 `linux/net/ipv4/tcp_input.c` 文件，主要用于管理 TCP 连接接收端期间的状态处理。标志位如表 10.1 所示。它们被作为慢启动、拥塞避免、选择性确认（SACK）以及最后确认实现的一部分，但不应与第 8 章讨论的 TCP 控制缓冲区中的标志位混淆。

| 表 10.1：接收状态标志位 |
| 标志位 | 值 | 描述 |
|---|---|---|
| FLAG_DATA | 0x01 | 传入的帧包含的数据。 |
| FLAG_WIN_UPDATE | 0x02 | 传入的 ACK 是窗口更新。 |
| FLAG_DATA_ACKED | 0x04 | 此 ACK 确认了新数据。 |
| FLAG_RETRANS_DATA_SACKED | 0x08 | 此 ACK 确认了新数据，其中部分已重传。 |
| FLAG_SYN_ACKED | 0x10 | 此 ACK 确认了 SYN。 |
| FLAG_DATA_SACKED | 0x20 | 新的 SACK。 |
| FLAG_ECE | 0x40 | 此 ACK 中设置了 ECE 标志。 |
| FLAG_DATA_LOST | 0x80 | SACK 检测到数据丢失。 |
| FLAG_SLOWPATH | 0x100 | 不跳过窗口更新的 RFC 检查。 |
| FLAG_ACKED | | (FLAG_DATA_ACKED|FLAG_SYN_ACKED) |
| FLAG_NOT_DUP | | (FLAG_DATA|FLAG_WIN_UPDATE|FLAG_ACKED) |
| FLAG_CA_ALERT | | (FLAG_DATA_SACKED|FLAG_ECE) |
| FLAG_FORWARD_PROGRESS | | (FLAG_ACKED|FLAG_DATA_SACKED) |

## 10.5 TCP 接收处理函数，tcp_v4_rcv

在本节中，我们将检查 TCP 输入段处理以及 AF_INET 协议中为 TCP 协议注册的处理函数。图 10.2 显示了 TCP 接收包流。

![](img/c1f701734d482a86a48e8bfd231c6fdb_373_0.png)

图 10.2：TCP 接收包流。

与 AF_INET 族中的所有其他协议一样，TCP 通过初始化 `inet_protocol` 结构体实例，将处理函数与协议字段值 `IPPROTO_TCP`（数字 6）关联。这一过程在第 6 章中描述。`handler` 字段被设置为函数 `tcp_v4_rcv`。因此，定义在 `linux/net/ipv4/tcp_ipv4.c` 文件中的 `tcp_v4_rcv` 会在 IP 头部中的协议类型包含 TCP 协议号时由 IPv4 调用。

```c
int tcp_v4_rcv(struct sk_buff *skb)
{
  struct tcphdr *th;
  struct sock *skb;
  int ret;
  if (skb)->pkt_type!=PACKET_HOST
    goto discard_it;
```
