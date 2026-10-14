
`off = (off + L1_CACHE_BYTES - 1) & ~(L1_CACHE_BYTES - 1);`

```c
if (off == PAGE_SIZE) {
    put_page(page);
    TCP_PAGE(sk) = page = NULL;
}
}
```

如果有必要，将分配一个新页，并根据页大小对数据长度 `copy` 进行修正。

```c
if (!page) {
```

分配新的缓存页。

```c
if (!page = tcp_alloc_page(sk)) {
    goto wait_for_memory;
}
off = 0;
if (copy > PAGE_SIZE - off) {
    copy = PAGE_SIZE - off;
}
```

最后，`tcp_sendmsg` 准备好从用户空间将数据拷贝到内核空间。它调用 `tcp_copy_to_page` 执行拷贝，而后者反过来调用 `csum_copy_from_user` 通过在计算校验和的同时高效地拷贝数据。如果 `tcp_copy_to_page` 返回错误，则将空页挂载到此打开 socket `sk` 的 socket 结构的 `sndmsg_page` 字段中，这样该页在 socket 释放时会被去分配。

```c
err = tcp_copy_to_page(sk, from, skb, page, off, copy);
if (err) {
    if (TCP_PAGE(sk) == NULL) {
        TCP_PAGE(sk) = page;
        TCP_OFF(sk) = 0;
    }
    goto do_error;
}
```

现在拷贝完成，更新 skb 以反映新数据。如果 `merge` 不为零，则意味着数据已合并到最后一个碎片中，必须更新该碎片的 `size` 字段。由于分配了新页，因此调用了 `fill_page_desc`，它用关于新页的信息更新 skb 中的 frag 数组。`tcp_options` 结构中的 `sndmsg_page` 字段被更新以指向下一个页，并且

```c
if (merge) {
    skb_shinfo(skb)->frags[i-1].size += copy;
} else {
    fill_page_desc(skb, i, page, off, copy);
    if (TCP_PAGE(sk)) {
        get_page(page);
    } else if (off + copy < PAGE_SIZE) {
        get_page(page);
        TCP_PAGE(sk) = page;
    }
}
```

```c
TCP_OFF(sk) = off + copy;
```

## 8.6.3 Tcp_sendmsg 完成

在此处，`tcp_sendmsg` 的大部分工作已经完成。数据已从用户空间拷贝完成，socket 缓冲区的标志已更新为准备好发送的页列表。变量 `PSH` 的值为 0 表示这是初始段的第一次循环，TCP 头部（如在本节所示）在移除传输的 socket 缓冲区时在控制缓冲区中的设置。Stevens 在第 2.5 节对 PSH 标志的使用有精彩讨论。

```c
if (!copied)
    TCP_SKB_CB(skb)->flags &= ~TSCB_FLAG_PSH;
```

TCP 选项 `write_seq` 字段根据处理的数据量进行更新。TCP 控制缓冲区中的 `end_seq` 字段也根据处理的数据量进行更新。`from` 指向源，已处理的总字节数在此次迭代中更新。此代码循环处理 `iov`。

```c
tp->write_seq += copy;
TCP_SKB_CB(skb)->end_seq += copy;
from += copy;
copy += copy;
if ((seglen == copy && iov == 0)
    goto out;
if (skb->len != msg_now || (flags & MSG_OOB))
    continue;
```

在此点，我们决定小段应该是推出还是丢弃。我们调用 `forced_push` 来检查必须发送段的大小。如果是，则设置 PSH 标志并进行分段。

```c
if (forced_push(tp)) {
    tcp_mark_push(tp, skb);
} else if (skb->send_head)
    tcp_push(skb, msg_now);
continue;
```

如果缓冲区或页不足，`tcp_sendmsg` 在此结束。它会等待有足够的缓冲区。

```c
wait_for_sndbuf;
    set_bit(SOCK_NOSPACE, &skb->socket->flags);
wait_for_memory;
    if (copied)
```

```c
tcp_push(sk)
```

这是推送剩余数据并退出函数的标签。返回 `copied` 值告知应用程序传输了多少数据。

```c
out:
if (copied)
    tcp_push(sk, tp, flags, mss_now, tp->nagle);
    TCP_CHECK_TIMER(sk);
    release_sock(sk);
    return copied;
```

这些最后的标签意味着我们在 `tcp_sendmsg` 的末尾。如果在拷贝和处理数据的检测到错误，则在此结束。

```c
do_fault:
if (sk->len == 0)
    if (tp->send_head == skb)
        tp->send_head = NULL;
        skb_unlink(skb, skb->list);
    tcp_free_skb(sk, skb);
do_error:
if (copied)
    goto out;
out_err:
    err = tcp_error(sk, flags, err);
    TCP_CHECK_TIMER(sk);
    release_sock(sk);
    return err;
```

## 8.7 TCP 输出

第 8.4 节关于 TCP 的之前的讨论主要关注 TCP 如何接口 socket 以及数据如何从应用程序移除并放入传输队列。在本节中，我们涵盖了实际的数据包传输（见图 8.2）。

![](img/c1f01734d482a86a48ebfd231c6db_244_0.png)

图 8.2：TCP 传输序列，Tcp_transmit_Skb 函数

### 8.7.1 发送 TCP 段，tcp_transmit_skb 执行实际

现在是传输 TCP 段的时间了，`tcp_transmit_skb` 函数执行实际的数据包传输。它发送队列到 socket 的数据包。当有发送段请求时，可以在 TCP 状态处理的任何地方调用它。早些我们看到 `tcp_sendmsg` 如何读取用于传输的段并将其放入 socket 队列。

在 `tcp_transmit_skb` 中，我们构建 TCP 包头部并将包传递给 IP。

```c
int tcp_transmit_skb(struct sk_buff *sk, struct sk_buff *skb)
{
```

如果接收到 NULL socket 缓冲区，我们什么都不做。

```c
if (sk != NULL) {
```

`inet` 指向 inet 选项结构，`tp` 指向 TCP 选项结构。在 `tcp`（等待，上下文暗示是 `tcp_struct` 或类似结构）中，socket 保留了大部分 TCP 配置和连接状态信息。`tcb` 指向包含大部分标志作为部分构建 TCP 头部的 TCP 控制缓冲区。这是一个指向 TCP 头部的指针。稍后，它将指向 skb 的头部，`sysctl_flags` 用于通过 sysctl 和 `setsockopt` 配置的一些关键参数。

```c
struct inet_opt *inet = inet_sk(sk);
struct tcp_opt *tp = inet_sk(sk);
struct tcp_skb_cb *tcb = TCP_SKB_CB(skb);
int tcp_header_size = tp->tcp_header_len;
struct tcphdr *th;
sysctl_flags;
int err;
```

```c
#define SYSCTL_FLAG_TSTAMPS 0x1
#define SYSCTL_FLAG_WSCALE 0x2
#define SYSCTL_FLAG_SACK 0x4
sysctl_flags = 0;
```
