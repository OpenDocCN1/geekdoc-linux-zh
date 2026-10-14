
在这里我们进入“真实的”TIME_WAIT 状态。RFC 1122 第 4.2.2.13 节规定，如果在 TIME_WAIT 状态下收到 SYN，我们可以重新打开连接。然而，我们必须将新连接的初始序列号赋值为比之前连接使用的最大序列号更大的值。如果传入的 SYN 是之前连接的重复，我们必须返回 TIME_WAIT 状态。

```c
if (!paws_reject &&
    (TCP_SKB_CB(sk)->seq == tw->tw_rcv_nxt &&
    TCP_SKB_CB(sk)->seq == TCP_SKB_CB(sk)->end_seq || tw->rst)) {
```

`paws_reject` 的值为 0 表示传入的段在窗口内；因此，它是 RST 或没有数据的 ACK。

```c
if (tw->rst) {
```

此 RST 可能在 TIME_WAIT 杀手（TWA）中返回。系统控制 `sysctl_tcp_rfc1337` 可以设置以防止 TWA。Linux TCP 默认行为并不防止 TWA，如果未设置系统控制，我们将杀死连接 [RFC1337]。

```c
if (sysctl_tcp_rfc1337 == 0) {
kill:
    tcp_tw_deschedule(tw);
    tcp_tw_put(tw);
    return TCP_SUCCESS;
}
```

传入的段必须是重复的 ACK，因此我们丢弃它。我们通过调用 `tcp_tw_schedule` 更新定时器。

```c
tcp_tw_schedule(tw, TIMEWAIT_LEN);
```

```c
if (tp_saw_timestamp) {
tw->tw_recent = tp.rcv_tsval;
tw->ts_recent_stamp = xtime_sec;
}
tcp_tw_put(tw) {
  return TCP_TW_SUCCESS;
}
```

如果到达，PAWS 测试必须失败，因此必须是一个窗口外的段或新的 SYN。接受新的 SYN 必须不是重复。RFC 793 标记的检查仅在低于 40Mb 的速度下有效。尽管 PAWS 检查确保了我们不需要检查序列号。

```c
if (th->syn && !rst && !ack && !paws_reject &&
(after(TCP_SKB_CB(sk))->seq, tw->tw_rcv_nxt) ||
(tp.saw_timestamp && (tw->ts_recent - tp.rcv_tsval) < 0))) {
  u32 is = tw->tw_rcv_nxt+65535+2;
  if (is == 0) {
    is++;
    TCP_SKB_CB(sk)->when = is;
    return TCP_TW_SYN;
  }
  if (paws_reject) {
    NET_INC_STATS(rejected);
  }
 (!th->rst) {稍后重置 TIME_WAIT 状态，但是传入的段是 ACK 或窗口外的。
```

```c
tcp_tw_schedule(tw, TIMEWAIT_LEN);
```

我们告诉调用者确认该段。

```c
return TCP_ACK;
}
```

我们必须收到 RST，因此杀死连接。

```c
tcp_tw_put(tw);
return TCP_TW_SUCCESS;
}
```

## 10.9 Socket 层接收

当用户被通知 socket 上有数据等待时，会调用 open socket 的接收系统调用。这些函数在 socket 层翻译为 `linux/ipv4/tcp.c` 中的 `tcp_recvmsg`。`tcp_recvmsg` 从 socket 拷贝数据到用户缓冲区。从 Linux 内核版本 2.3 开始，socket 是锁定的。

```c
int tcp_recvmsg(struct sock *sk, struct msg *msg,
    int len, int nonblock, int flags, int *addr_len)
{
    struct tcp_opt *tp = tcp_sk(sk);
    int copied = 0;
    u32 peek_seq;
    u32 *seq;
    unsigned long used;
    int err;
```

`target` 设置该函数应该返回的最小字节数。

```c
int target;
long time;
struct task_struct *user_recv = NULL;
lock_sock(sk);
TCP_CHECK_TIMER(sk);
err = -ENOTCONN;
if (sk->state == TCP_LISTEN)
    goto out;
time = sock_rcv(sk, nonblock);
```

设置了 `MSG_OOB` 标志，紧急数据（带有 URG 标志的传入段）会被特殊处理。在入口处，`seq` 初始化为读取的下一个字节，`tcp_opt` 结构中的 `copied_seq` 字段包含已处理的最后一个字节。

```c
if (flags & MSG_OOB)
    goto recv_urg;
seq = &tp->copied_seq;
if (flags & MSG_PEEK) {
    peek_seq = tp->copied_seq;
    seq = &peek_seq;
}
```

读取的字节数 `target` 设置为 socket 的低水位线 `sk->rclowat` 或 `len`，取较小者。`MSG_WAITALL` 表示是否阻塞目标字节数。

```c
target = sock_rclowat(sk, flags, MSG_WAITALL, len);
```

此 do 循环是 `tcp_recvmsg` 的主循环。在这个循环中，我们将继续拷贝字节到用户，直到到达目标或在处理传入数据段时检测到异常条件。

```c
do {
    struct sk_buff *skb;
    u32 offset;
```

拷贝一些后，如果在处理段时遇到紧急数据，我们停止处理。

```c
if (copied && tp->urg_data && tp->urg_seq == *seq)
  break;
```

在这里我们检查此 socket 上是否有挂起的信号，以确保正确处理 SIGUR 信号。代码中的注释说明：“FIXME: 需要检查这是否影响 SIGUSR-1 并将其移动到循环底部。”接下来，我们检查 socket 是否超时，在这种情况下我们返回一个错误。

```c
if (signal_pending(current)) {
  if (copied)
    break;
  copied = timeo ? sock_intr_errno(timeo) : -EAGAIN;
}
```

我们有一个接收队列上第一个缓冲区的指针，在内部 do 循环中遍历接收队列直到找到第一个段。当我们找到该段并知道要拷贝多少字节时，跳转到 `found_ok_skb`。在此过程中，我们使用 `offset` 变量从 `skb` 计算要拷贝的字节数。

```c
skb = skb_peek(&sk->sk_receive_queue);
```

在这个循环中，我们继续检查数据包直到找到有效的数据段。在此，我们检查 FIN 和 SYN。如果我们有一个 SYN，我们通过减一个 offset 来调整要拷贝的字节数。FIN 跳出循环。

```c
do {
  if (!skb)
    break;
```

现在我们检查要处理的当前字节是否不是最近收到的段中的第一个字节，以查看在处理数据队列时是否丢失了同步。这实际上是一个冗余检查，因为 socket 锁定和多个队列防止了我们的丢失。

```c
if (before(*seq, TCP_SK_CB(skb)->seq)) {
  printk(KERN_INFO, "recvmsg bug: copied %X seq %X\n",
    *seq, TCP_SK_CB(skb)->seq);
  break;
}
offset = *seq - TCP_SK_CB(skb)->seq;
if (skb->th->syn)
  offset--;
  if (offset < skb->th->len)
    goto found_ok_skb;
  if (skb->th->fin)
    goto found_ok_fin_ok;
  BUG_TRAP (flags&MSG_PEEK);
  skb = skb->next;
}
```
