
尽管已经计算了头部预测标志，但在 `ESTABLISHED` 状态下处理传入包时，仍有一些检查会导致数据包被重定向到慢路径。

- 我们连接的一端通告了零窗口。零窗口探测的处理仅在慢路径中被正确处理。有关零窗口探测的信息请参见第 8 章第 8.9 节。
- 如果此侧条件接收到乱序段，则禁用快速路径处理。
- 如果遇到紧急数据，将禁用快速路径处理，直到紧急数据被复制到上。
- 如果没有更多的接收缓冲区，将禁用快速路径。
- 头部预测的任何失败都会将特定段定向到慢路径。
- 快速路径仅支持单向数据传输，如果我们必须向另一个方向发送数据，我们对传入的数据包默认为使用慢路径处理。
- 如果传入的数据包中有除超时以外的任何选项，我们将将其定向到慢路径。

文件 `linux/net/tcp/tcp_input.c` 中的 `Tcp_rcv_established` 是处理传入段的大型工作函数。该函数仅在连接已处于 `ESTABLISHED` 状态时接收数据包时调用。因此，它的假设是数据包将在快速路径中处理。在此过程中，如果发现传入的数据包需要更仔细的检查，它就会被定向到慢路径。

```c
int tcp_rcv_established(struct sock *sk, struct sk_buff *skb,
struct tcphdr *th, unsigned len)
struct tcp_opt *tp = &(sk->tp_pinfo.af_tcp);
tp->saw_tstamp = 0;
```

在这里，预测标志与传入的段进行比较。我们还检查序列号是否有序。传入包中的 `PSH` 标志被忽略。

```c
if ((tcp_flag_word(th) & TCP_HP_BITS) == tp->pred_flags &&
    TCP_SK_CB(skb)->seq == tp->rcv_nxt) {
    int tcp_header_len = tp->tcp_header_len;
```

检查除时间戳之外是否有其他选项，如果有，则将此包发送到慢路径。TCP 选项字段 `saw_tstamp` 表示传入的数据包包含时间戳选项。

```c
if (tcp_header_len == sizeof(struct tcphdr) + 
    TCPOLEN_STAMP_ALIGNED) {
    u32 *ptr = (__u32 *)(th + 1);
```

如果数据包包含 TCP 选项，我们将将其发送到慢路径。

```c
if (*ptr! != ntohl(TCOPT_NOP << 24) | (TCOPT_NOP << 16)
    | (TCOPT_TIMESTAMP << 8) | TCPOLEN_TIMESTAMP)
goto slow_path;

tp->saw_tstamp = 1;
++ptr;
tp->rcv_tsval = ntohl(*ptr);
++ptr;
tp->rcv_tsecr = ntohl(*ptr);
++ptr;
```

现在我们对 PAWS 进行快速检查。如果检查失败，数据包将在慢路径中接受更仔细的检查。

```c
if ((s32) tp->rcv_tsval - tp->ts_recent) < 0
goto slow_path;
```

在这里我们检查头部长度是否太小以及数据包中是否有数据。

```c
if (len <= tcp_header_len) {
```

我们检查发送端的快速路径。基本上，如果我们接收到带有有效头部但没有数据的数据包，这可能表明我们正在向输出方向进行单向数据（批量）传输。因此，我们确认该包，释放它，并检查发送端。然而，我们不对传入的数据包进行校验和，因为这已经对无头部数据包执行了校验。

```c
if (len == tcp_header_len) {
```

预测的数据包在窗口内。

```c
if (tcp_header_len == (sizeof(struct tcphdr) +
    TCPOLEN_STAMP_ALIGNED) && tp->rcv_nxt)
tcp_store_recent(tp);
tcp_ack(sk, skb);
__kfree_skb(skb);
tcp_snd_check(sk);
} else {
    TCP_INC_STATS(BR);
} else {
    int eaten = 0;
}
```

```c
else
    sk->data_ready(sk, 0);
    return 0;
}
```

以下代码部分是接收到的数据段的慢路径处理。如果此函数是从内核的“下半部”（bottom half）内部调用的，或者由于某种原因继续了预队列处理，我们将进入到这里。

```c
slow_path:
    if (len < (th->doff<<2) || tcp_checksum_complete_user(sk, skb))
        goto csum_error;
```

我们通过 TCP 时间戳选项对乱序数据段进行 PAWS 检查。

```c
if (tcp_fast_parse_options(skb, th, tp) && tp->saw_tstamp &&
    tcp_paws_discard(tp, skb)) {
```

即使 PAWS 检查确认我们收到了一个乱序段，仍然必须检查传入的 RST 包。

```c
if (!->rst) {
    NET_INC_STATS_BH(PAWEstabRejected)
    tcp_send_dupack(sk, skb);
    goto discard;
}
```

我们按照 RFC 793 的规定恢复对数据段的标准慢路径处理。我们检查所有传入数据的序列号。

```c
if (!->sequence(tp, TCP_SKB_CB(skb)->seq, TCP_SKB_CB(skb)->end_seq)) {
```

如果传入的数据段不可接受的，则发送一个确认包。

```c
if (!->rst) {
    tcp_send_dupack(sk, skb);
    goto discard;
}
```

如果我们收到 RST，则丢弃该段。

```c
if (!->rst) {
    tcp_reset(sk);
    goto discard;
}
tcp_replace_ts_recent(tp, TCP_SKB_CB(skb)->seq);
if (th->syn && !before(TCP_SKB_CB(skb)->seq, tp->rcv_nxt)) {
    NET_INC_STATS_BH(TcpInErrors);
    NET_INC_STATS_BH(TCPAbortOnSyn);
    tcp_reset(sk);
}
return 1;
}
```

`ESTABLISHED` 状态（RFC 793 第 72 页）的第五步是检查 ACK 字段。
第六步是处理 URG 标志。

```c
step5:
  if(th->ack)
    tcp_ack(sk, skb, FLAG_SLOWPATH);
    tcp_urg(sk, skb, th);
```

我们处于慢路径中，尚未排除这些数据段，因此我们遵循 RFC 793 的步骤。RFC 第 74 页的第七步是处理段段数据。`tcp_data_queue` 将数据放入套接字的正常接收队列中。它会将乱序段放入 `order_queue`。对于套接字的正常接收队列，当应用程序在打开的套接字上执行读取调用时将继续处理，这将调用 `tcp_recvmsg`。套接字级接收的解释见第 10.9 节。

```c
tcp_data_queue(sk, skb);
  tcp_data_snd_check(sk);
  tcp_ack_snd_check(sk);
  return 0;
csum_error:
  TCP_INC_STATS_BH(TcpInrs);
discard:
  kfree_skb(skb);
  return 0;
```
