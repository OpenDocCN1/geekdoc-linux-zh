
```c
if (!xfrm_policy_check(sk, XFRM_POLICY_IN, sk)) {
    kfree_skb(skb);
    return -1;
}
}
```

首先，我们检查这是否是一个用于 IPSec 的封装套接字。

```c
if (up->encap_type) {
```

如果我们有一个封装套接字，则传入的数据包必须是封装的。如果是，我们就转换输入包。如果不是，它就是一个普通的 UDP 包，我们都直接向下执行。

```c
int ret;
ret = udp_encap_rc(sk, skb);
if (ret == 0) {
  kfree_skb(skb);
  return 0;
}
```

```c
if (ret < 0) {
```

在这里，我们处理 ESP 包。

```c
ret = xfrm4_rc_encap(skb, up->encap_type);
UDP_INC_STATS_BH(UdpInDatagrams);
return -ret;
}
```

如果我们直接向下执行，包必须是一个普通的 UDP 包。

```c
}
```

现在，我们完成校验和。

```c
if (sk->sk_summed && skb->ip_summed != CHECKSUM_UNNECESS) {
  if (__udp_checksum_complete(skb)) {
    UDP_INC_STATS_BH(UdpInErrors);
    kfree_skb(skb);
    return -1;
  }
  skb->ip_summed = CHECKSUM_UNNECESSARY;
}
```

接下来，我们调用套接字级别的接收函数 `sock_queue_rcv`（该函数在第 5 章中介绍），它将包放在套接字的接收队列上并唤醒套接字以便应用程序读取数据。如果接收队列空间不足，则增加错误统计并静默丢弃包。

```c
if (sock_queue_rcv(sk, skb) < 0) {
```

如果套接字返回错误，我们增加统计信息并退出。

```c
UDP_INC_STATS_BH(dpInErrors);
IP_INC_STATS_BH(IpDiscards);
statistics[id].IpDelivers++;
kfree_skb;
return -1;
}
```

一旦增加了计数器，我们就完成了。在此处，套接字级处理将允许用户级完成。

```c
UDP_INC_STATS_BH(dpInDatagrams);
return 0;
}
```

### 10.4 套接字级接收

在第 8 章中，我们看到了 `send` 如何在传输层汇聚到一个函数。在发送端，套接字级发送函数在套接字层汇聚到一个函数。对于 UDP，该函数是 `udp_recvmsg`。在 `linux/ipv4/udp.c` 中，对于 `SOCK_DGRAM` 类型，执行该接收函数。

```c
int udp_recvmsg(struct sock *sk, struct msghdr *msg, int len,
    int noblock, int flags, int *addr_len)
{
    struct inet_opt *inet = inet_sk(sk);
    struct sockaddr_in *sin = (struct sockaddr_in *)msg->name;
    struct sk_buff *skb;
    int err;
```

检查套接字 `sk` 队列是否有任何消息，如果是，通过调用 `ip_recv` 处理它们并退出。

```c
if (addr_len < sizeof(*))
    *addr_len = sizeof(struct sockaddr_in);
if (flags & MSG_REQUEUE)
    return ip_recv(sk, msg, len);
```

通过调用通用数据报接收函数 `skb_recv_datagram` 从接收队列中取消队列，如果它返回了包，则退出。

```c
skb = skb_recv_datagram(sk, flags, noblock, &err);
if (!skb)
    goto out;
```

检查用户请求的数据是否多于包 `skb` 中的负载。

```c
copied = skb->len - sizeof(struct udphdr);
if (copied > len)
    copied = len;
    msg->msg_flags |= MSG_TRUNC;
```

套接字缓冲区 `ip` 字段决定是否需要校验和。如果 `ip_summed` 不等于 `CHECKSUM_UNARY`，则必须进行校验和，并在计算校验和的同时从内核空间拷贝到用户空间。拷贝和校验和由 `skb_copy_datagram_iovec` 完成。但也可能因为数据跨越了多个缓冲区而计算校验和，在这种情况下，`__udp_checksum_complete` 完成校验和。校验和是一个整数和为零的值。检查可以稍后完成。

```c
if (skb->ip_summed != CHECUM_UNARY)
    err = skb_copy_datagram_iovec(sk, sizeof(struct udphdr),
        msg->msg_iov, copied);
```

```c
} else if (msg->msg_flags & MSG_TRUNC) {
    if (__udp_checksum_complete(skb))
        goto csum_copy_err;
    err = skb_copy_datagram_iovec(skb, sizeof(struct udphdr),
        msg->msg_iov,
        copied);
} else {
    err = skb_copy_and_csum_datagram_iovec(skb, sizeof(struct udphdr),
        msg->msg_iov);
    if (err == -EINVAL)
        goto csum_copy_err;
}
}
if (err)
    goto_free;
```

接下来，为传入包标记时间戳。如果用户提供了有效的缓冲区 `sin` 来接收包的源地址和端口，信息将从包头拷贝。

```c
recv_timestamp(msg, sk, skb);
if (sin)
{
    sin->sin_family = AF_INET;
    sin->sin_port = sk->h.uh->source;
    sin->sin_addr.s_addr = sk->nh.ip->saddr;
    memset(sin->sin_zero, 0, sizeof(sin->sin_zero));
```

离开之前，`udp_recv` 检查控制消息标志 `cmsg_flags` 以查看是否设置了任何 IP 套接字选项。例如，某些如 `IP_` 的接字选项需要将 IP 头部拷贝到用户空间。如果设置了标志，`cmsg_recv` 获取关联选项值。

```c
if (sk->protinfo.af_inet.cmsg_flags)
    ip_cmg_recv(msg, skb);
err    = copied;
```

`udp_recv` 结尾有三个错误。最重要的是 `csum_copy_err`。

```c
free:
    skb_free_datagram(sk, skb);
out:
    return err;
csum_copy_err:
    UDP_INC_STATS_BH(UdpInErrors);
```

当 `flags` 参数被设置为 `MSG_PEEK` 时，意味着调用者想要“查看”传入的消息而不将其从接收队列中移除。然而，我们知道该包的校验和错误，因此在删除它之前将其从接收队列中移除。

```c
if (flags & MSG_PEEK)
    int clear = 0;
    spin_lock_irq(&sk->receive_queue.lock);
    if (skb = skb_peek(&sk->receive_queue)) {
```

```c
skb_unlink(skb, &skb->receive_queue);
clear = 1;
}
spin_unlock_irq(&skb->receive_queue.lock);
if (clear)
 kfree_skb(skb);
}
skb_free_datagram(sk, skb);
return -EAGAIN;
```
