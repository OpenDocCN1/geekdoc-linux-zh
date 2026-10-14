
`sk` 设置为 `data` 指向的 `sock` 结构，`tp` 设置为 `sock` 结构中的 TCP 选项结构。

```
struct sock *sk = (struct sock)*data;
struct tcp_opt *tp = tcp_sk(sk);
int event;
```

为了安全，套接字被锁定。套接字锁定详情见第 5 章。如果已锁定，为了稍后重试，我们将超时设置为 20 秒并返回。

```
bh_lock_sock(sk);
if (sock_owned_by_user(sk)) {
    if (!timer(&tp->retransmit_timer, jiffies + (HZ/20))) {
        sock_hold(sk);
    }
    goto unlock;
}
```

检查套接字状态 `sk->state` 和快速确认状态 `tp->pending` 以检查套接字是否关闭以及是否存在未被确认的待处理状态。

```
if (sk->state == TCP_CLOSE || !tp->pending)
    goto out;
```

如果超时值在未来，则将重传定时器重置为超时选项结构中的值。`mod_timer` 返回 0 表示定时器仍处于挂起。如果定时器仍挂起，则套接字引用计数加 ，函数返回。

```
if (time_after(tp->timeout, jiffies) > 0) {
    if (!timer(&tp->retransmit_timer, tp->timeout))
        sock_hold(sk);
    goto out;
}
```

如前所述，写入定时器有两个用途。它用于重传定时器 `TCP_TIME_RETRANS` 或窗口探测定时器 `TCP_TIME_PROBE0`。我们通过查看选项结构中的探测字段来确定正在执行的角色。如果当前超时是重传定时器，我们调用函数 `tcp_retransmit_timer`；但如果当前超时是窗口探测定时器，我们调用 `tcp_probe_timer`。这些定时器是后续节中的函数。

```
event = tp->pending;
tp->pending = 0;
switch (event) {
    case TCP_TIME_RETRANS:
        tcp_retransmit_timer(sk);
        break;
    case TCP_TIME_PROBE0:
        tcp_probe_timer(sk);
        break;
}
TCP_CHECK_TIMER(sk);
out:
    tcp_mem_reclaim(sk);
un:
    bh_unlock_sock(sk);

sock_put(sk);

}
```

## 8.9.2 TCP 重传定时器

当重传定时器过期时会调用 `Tcp_retransmit_function`，表示未收到预期确认。该函数从通用 TCP 定时器函数 `tcp_write_timer` 调用，该函数在 [第 8.9.1 节](Section 8.9.1) 中讨论过。

```
static void tcp_retransmit_timer(struct sock *sk)

{

    struct tcp_opt *tp = tcp_sk(sk);

    if (tp->packets_out == 0)

        goto out;

    BUG_TRAP(!skb_queue_empty(&sk->write_queue));

```

接下来，我们检查连接应该超时，还是发送端已经减小了处于 `ESTABLISHED` 状态的套接字的窗口。如果接收到了窗口且接收包中的时间戳显示数据早于最大重传时间，则下次调用重传定时器时，它将变为窗口探测定时器。通过调用 `tcp_enter_loss` 进入拥塞避免 (CA) 处理状态或丢失状态。

```c
if (tp->snd_wnd == 0 && !sk->dead &&

    !(1<<sk->state & (TCP_SYN_RECV|TCP_SYN_RECV))) {

#ifdef TCP_DEBUG

    if (net_ratelimit(1)) {

        struct inet_opt *inet = inet_sk(sk);

        printk(KERN_DEBUG "TCP: Treason uncloaked!\nPeer %u.%u.%u.%u: shrinks window %u:%u\n");

    }

#endif

}
```

（注：OCR 文本逻辑块中存在一些损坏，此处已根据提供的 OCR 修复明显的语法错误。）

```
goto out;

}
```

重传超时时间 `r` 在 TCP 选项结构中每次发生重传时都会增加；实际上，它每次都会翻倍。重传超时时间的最大值为 `TCP_RTO_MAX`，即 120 秒，这这也是 RTT 的最大值。Van Jacobson 在其关于拥塞避免的论文 [JACOB88] 中建议重传定时器翻倍。往返时间估计 (RTT) 不会因为超时而改变。如果重传次数大于 `TCP_RETR1`（即 3），则检测缓存将失效。

```
tp->backoff++;
tp->retransmits++;
out_reset_timer;
tp->rto = min(tp->rto << 1, TCP_RTO_MAX);
tcp_reset_mit_timer(sk, TCP_TIME_RETRAN, tp->rto);
if (tp->retransmits > sysctl_tcp_retries1)
    __sk_dst_reset(sk);
```

```
out;
;
```

## 8.9.3 窗口探测定时器 (Window Probe Timer)

窗口探测 `tcp_probe_timer` 位于文件 `linux/net/ipv4/tcp_timer.c` 中，由通用 TCP 写端定时器函数 `tcp_write_timer` 调用。如节 8.9.1 所示，当等待事件是窗口探测时，会调用 `tcp_probe_timer`。当连接的这一端响应对端的窗口宣告发送零窗口探测时，会设置零窗口定时器。在该函数中，我们避免在收到零窗口探测的响应之前定时器就过期。

`Tp` 指向套接字状态 `sk` 的选项结构。首先，`tcp_probe_timer` 检查是否存在有效的零窗口事件，这只有在上一个包发送了零窗口探测时才会发生。会检查 TCP 选项结构中的 `packet_out` 和 `send_head` 字段，确认是否存在未确认的待处理数据或正在发送的段。如果存在其中任一条件，我们将返回，因为这不可能是有效的窗口探测事件。

```
static void tcp_probe_timer(struct sock *sk) {

    struct tcp_opt *tp = tcp_sk(sk);

    int max_probes;

    if (tp->packets_out || !tp->send_head) {

        tp->probes_out = 0;

        return;

    }
```

我们将最大探测次数 `max_probes` 设置为 `TCP_RETR2` 的值，该值在 `linux/include/net/tcp.h` 文件中被定义为数字 15。我们会检查套接字是否为孤儿节点（orphaned）。Linux 不会因为长时间宣告零窗口大小就杀死连接，因此我们等待查看是否需要保持连接活跃。因此，我们检查下一个重传超时值 `rto` 是否仍然小于最大 RTO `TCP_RTO_MAX`。会为孤儿套接字重新计算 `max_probes`。调用 `tcp_out_of_resources` 是为了确保孤儿套接字不会消耗过多内存，因为它不应该永远保持活跃。如果套接字将被杀死，`tcp_probe_timer` 将在此处返回。

```
max_probes = sysctl_tcp_retries2;

if (sk->>dead) {

    int alive = ((tp->tcp->backoff) < TCP_RTO_MAX);

    max_probes = tcp_orphan_retries(sk, alive);

    if (tcp_out_of_resources(sk, alive || tp->probes_out <= max_probes)

        return;

}
```

接下来，我们检查套接字中零窗口探测的数量，看其是否超过了 `max_probes` 中定义的最大探测数（这是之前调用过的一个值）。如果是，则指示错误条件并返回函数。只有在所有先前的检查都通过时，才会发送另一个窗口探测。

```
if (tp->probes_out > max_probes) {

    tcp_write_err(sk);

} else {
```
