
如所述，写定时器有两个用途。它被用作重传定时器 `TCP_TIME_RETRANS` 或窗口探测定时器 `TCP_TIME_PROBE`。我们通过查看 `icsk->pending` 字段来确定正在执行哪一个。如果当前 timeout 是重传定时器过期，我们调用函数 `tcp_retransmit_timer`，但如果当前 timeout 是窗口探测定时器过期，我们调用 `tcp_probe_timer`。这些定时器函数将在后续章节讨论。

```c
event = icsk->pending;
icsk->pending = 0;
switch (event) {
case TCP_TIME_RETRANS:
    tcp_retransmit_timer(sk);
    break;
case TCP_TIME_PROBE:
    tcp_probe_timer(sk);
    break;
}
TCP_CHECK_TIMER(sk);
out:
    sk_stream_reclaim(sk);
out_unlock:
    bh_unlock_sock(sk);
    sock_put(sk);
```

## `tcp_retransmit_timer` 函数

重传定时器过期时，调用 `tcp_retransmit_timer` 函数。该定时器用于指示未收到确认。该函数从通用 TCP 写定时器 `tcp_write_timer` 起。

```c
static void tcp_retransmit_timer(struct sock *sk)
{
    struct tcp *tp = tcp_csk(sk);
    struct inet_connection_sock *icsk = inet_csk(sk);
    if (tp->packets_out == 0)
        goto out;
    BUG_ON(skb_queue_empty(&sk->write_queue));
```

首先，我们检查连接应该是超时，还是发送端在套接字仍处于 `ESTABLISHED` 状态时将窗口大小减为零。如果收到零窗口且接收包中的时间戳表明收到的包旧于重传时间，下次调用写定时器时它变为零探测定时器。通过调用 `tcp_enter_loss` 进入拥塞避免（CA）处理状态或更低状态。

```c
if (!tp->snd_wnd && sock_flag(sk, SOCK_DEAD)) &&
    !((1<<sk->sk_state) & (TCP_SYN_SENT|TCP_SYN_RECV)) {
    #ifdef TCP_DEBUG
        if (net_ratelimit()) {
            struct inet_opt *inet = inet_sk(sk);
            printk(KERN_DEBUG "Reason uncloaked!\n"
                   "Peer %u.%u.%u.%u/%u shrinks window %u:%u. Repaired.\n",
                   NIPQUAD(inet->daddr), htons(inet->dport),
                   tp->snd_num, tp->snd_una, tp->snd_nxt);
#endif
```

如果收到的时间戳超过两分钟，我们指示写入错误、套接字超时并丢弃套接字和连接。

```c
if (tcp_time_stamp - tp->rcv_tstamp > TCP_RTO_MAX) {
    tcp_write_err(sk);
    goto out;
}
```

现在是 `tcp_enter_loss` 的第二个参数被设置为 0，表示从重传超时进入丢失状态。拥塞避免的这部分将在第 9 章详细讨论。接下来，我们调用 `tcp_retransmit_timer`，通过 `tcp_retransmit_skb` 尝试重传位于重试队列头部的 `skb`。此时，如果对方没有完全消失，连接处于可疑状态，因此调用 `_sk_dst_reset` 来重置目标缓存。参考第 5 章关于缓存的信息。

```c
tcp_enter_loss(sk, 0);
tcp_retransmit_skb(sk, skb_peek(&sk->write_queue));
    _sk_dst_reset(sk);
goto out_reset_timer;
```

接下来，我们调用 `tcp_write_timeout` 来检查是否有足够的重试次数并完成最后重试尝试的处理。

```c
if (tcp_write_timeout(sk))
    goto out;
```

在下面的代码部分中，我们增加 `/proc` 文件系统的 TCP 统计。我们检查 TCP 选项结构中的拥塞避免状态 `icsk_ca_state` 字段，以查看是什么故障触发了重传超时。有关如何访问 `/proc` 中的 TCP/IP 统计的更多信息，请参考第 5 章。

```c
if (icsk->retransmits == 0) {
    if (icsk->icsk_ca_state == TCP_CA_Disorder ||
        icsk->icsk_ca_state == TCP_CA_Recovery) {
```

# 340 嵌入式系统的 Linux TCP/IP 网络

```c
if (icsk->icsk_sack_ok) {
    if (icsk->icsk_ca_state == TCP_CA_Recovery)
        NET_INC_STATS_BH(LINUX_MIB_TCPSACKRECOVERYFAIL);
    else
        NET_INC_STATS_BH(LINUX_MIB_TCPSACKFAILURES);
} else {
    if (icsk->icsk_ca_state == TCP_CA_Recovery)
        NET_INC_STATS_BH(LINUX_MIB_TCPRENORECOVERYFAIL);
    else
        NET_INC_STATS_BH(LINUX_MIB_TCPRENORECOVERYFAILURES);
    }
} else if (icsk->icsk_ca_state == TCP_CA_Loss) {
    NET_INC_STATS_BH(LINUX_MIB_TCPLOSSFAILURES);
} else {
    NET_INC_STATS_BH(LINUX_MIB_TCPTIMEOUTS);
}
```

现在，进入丢失状态，启动拥塞避免处理并尝试进行重传。

```c
if (tcp_use_frto(sk)) {
    tcp_enter_frto(sk);
} else {
    tcp_enter_loss(sk, 0);
}
if (tcp_retransmit_skb(sk, skb_peek(&sk->sk_write_queue)) > 0) {
```

如果 `tcp_retransmit_skb` 返回值大于零，是因为底层 IP 传输函数由于本地传输问题（如繁忙的网卡驱动程序）失败了。必须重置重传计时器稍后重试。

```c
if (!tp->retransmits)
    tp->retransmits=1;
tcp_reset_xmit_timer(sk, TCP_TIME_RETRANS, min(tp->rto,
    TCP_RESOURCE_PROBE_INTERVAL));
```

TCP 结构中的重传超时 `rto` 在每次发生重传时都会增加；实际上它每次都会翻倍。重传超时的最大值为 `TCP_RTO_MAX`，即 120 秒，这这也是 RTT 的最大值。Van Jacobson 在他关于拥塞避免的论文 [JACOB88] 中建议重传计时器翻倍。

RTT 估计值不会因为超时而改变。如果重传次数大于 `TCP_RETR1`（即 3），则目标缓存将老化删除。

```c
icsk->icsk_backoff++;
icsk->icsk_retransmits++;
out_reset_timer:
icsk->icsk_rto = min(icsk->icsk_rto << 1, TCP_RTO_MAX);
tcp_reset_xmit_timer(sk, TCP_TIME_RETRANS, tp->rto);
if (icsk->icsk_retransmits > sysctl_tcp_retries)
    sk_dst_reset(sk);
out();
```

# 第 7 章 通过 UDP 和 TCP 从 Socket 发送数据 341
