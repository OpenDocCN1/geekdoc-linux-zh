

## 24.4 数据交换的协议机制

一个带有新广告窗口大小零的确认，这意味着它不能发送更多数据。

现在的问题是，它只有在带有新数据包时才能接收到新的窗口大小（即传输额度）。由于它无法发送更多数据，因此没有确认，这意味着发送端现在依赖于另一端发送的任何内容。如果接收端没有数据要发送，或者它也被授予了一个窗口大小为零的窗口，那么通信双方将永远等待以便能够继续发送。

为了解决这个问题，传输控制协议包含一种名为“零窗口探测”（zero-window probing）的机制。该机制基于一个额外的计时器，即探测计时器（probe timer）。当该计时器超时时，会发送一个广告窗口大小为零的 TCP 数据包。该包只包含一个数据包头部：它不携带负载，因为在这种情况下不允许传输数据。

通信对端会确认此数据包，如果对方在此期间在某种程度上消除了其拥塞，则会通过此确认授予一个更大的窗口，以便恢复数据传输。如果窗口大小再次变为零，则通信双方将等待探测超时后发送另一个探测。

```
tcp_probe_timer()
net/ipv4/tcp_timer.c
static void tcp_probe_timer(struct sock *sk)
{
    (..)
    if (tp->probes_out > max_probes) {
        tcp_write_err(sk);
    } else {
        /* 只有在我们没有关闭连接时才发送另一个探测。 */
        tcp_send_probe0(sk);
    }
}
```

`tcp_probe_timer(sk)` 是零窗口探测计时器的处理例程，如果它导致了超时。它首先检查接收端在很一段时间内是否提供了有意义的传输窗口。如果发送了多个（超过 `max_probes`）窗口探测均未成功，则将输出错误消息，宣布 TCP 连接存在严重问题（`tcp_write_err()`），并通过 `tcp_done()` 关闭此连接。

如果尚未达到最大窗口探测次数，`tcp_send_probe0()` 会发送一个不带负载的 TCP 段，然后确认段随后希望会授予一个大于零的额度（广告窗口）。

```
tcp_send_probe0()
net/ipv4/tcp_output.c
```

`max_probes` 的值初始化为 15，可以在 proc 文件 `/proc/sys/net/ipv4/tcp_retries2` 中设置。

## 494 第24章 传输控制协议 (TCP)

```
void tcp_send_probe0(struct sock *sk)
{
    struct tcp_opt *tp = &(sk->tp_pinfo.af_tcp);
    int err;
    err = tcp_xmit_wakeup(sk);
    if (tp->packets_out || !tp->send_head) {
        /* 如果不需要探测计时器，则取消它。 */
        tp->probes_out = 0;
        tp->backoff = 0;
        return;
    }
    if (err <= 0) {
        tp->backoff++;
        tp->probes_out++;
        tcp_reset_xmit_timer(sk, TCP_TIME_PROBE, min(tp->rto << tp->backoff, TCP_RTO_MAX));
    }
}
```

`tcp_send_probe0(struct sock *sk)` 使用 `tcp_wakeup` 生成并发送零窗口探测包。如果探测计时器不再需要（这是因为当前没有数据要发送（`tp->send_head == NULL`），或者当前仍有数据包在途中且它们的 ACK 可能包含新额度），则不会重启它，并重置 `probes_out` 和 `backoff` 参数。否则，在发送探测后，这些参数会增加，探测计时器将重启，以便它在一段时间后再次超时。

```
tcp_xmit_wakeup(struct sock *sk)
net/ipv4/tcp_output.c
```

```
{
    if (tp->send_head != NULL &&
        after(TCP_(B(skb), tp->snd_una))
        {
            /* 探测窗口

                               慢窗口避免 (SWS) */
            err = tcp__sksk(skb), GFP_ATOMIC);
        }
    else {
        tcp_probeb(sk);
    }
}
```

`tcp_xmit_wakeup(sk)` 检查在长时间内接收端是否提供了有意义的传输窗口。如果发送了多个（超过 `max_probes`）窗口探测均未成功，则输出错误消息宣布 TCP 连接存在严重问题（`tcp_write_err()`）并通过 `tcp_done()` 关闭此连接。

如果尚未达到最大窗口探测次数，`tcp_send_probe0()` 会发送一个不带负载的 TCP 段，确认段随后希望能授予一个大于零的额度（广告窗口）。

```
tcp_send_probe0()
net/ipv4/tcp_output.c
```

`max_probes` 的值初始化为 15，可以在 proc 文件 `/proc/sys/net/ipv4/tcp_retries2` 中设置。

`tcp_probe_timer(sk)` 是零窗口探测计时器的处理例程，如果它导致了超时。它首先检查接收端在很一段时间内是否提供了有意义的传输窗口。如果发送了多个（超过 `max_probes`）窗口探测均未成功，则将输出错误消息宣布 TCP 连接存在严重问题（`tcp_write_err()`）并通过 `tcp_done()` 关闭此连接。

如果尚未达到最大窗口探测次数，`tcp_send_probe0()` 会发送一个不带负载的 TCP 段，确认段随后希望会授予一个大于零的额度（广告窗口）。

```
tcp_probe_timer()
net/ipv4/tcp_timer.c
static void tcp_probe_timer(struct sock *sk)
{
    (..)
    if (tp->probes_out > max_probes) {
        tcp_write_err(sk);
    } else {
        /* 只有在我们没有关闭连接时才发送另一个探测。 */
        tcp_send_probe0(sk);
    }
}
```

`tcp_send_probe0(struct sock *sk)` 使用 `tcp_wakeup` 生成并发送零窗口探测包。如果探测计时器不再需要（这是因为当前没有数据要发送（`tp->send_head == NULL`），或者当前仍有数据包在途中且它们的 ACK 可能包含新额度），则不会重启它，并重置 `probes_out` 和 `backoff` 参数。否则，在发送探测后，这些参数会增加，探测计时器将重启，以便它在一段时间后再次超时。

### 防止序列号回绕的保护 (PAWS)

PAWS 机制防止字节序列号溢出，溢出会在带宽/延迟过大的连接中（即管道中有过量数据）导致不一致。

TCP 连接的字节序列号长度为 32 位。具有足够的传输速率和足够大的数据包往返时间，字节序列号可以在数据包在路由器队列中延迟的时间内到达范围的边界，从而导致字节序列号溢出。在这种情况下，字节序列号将取序列范围的初始值。在这种情况下，TCP 协议无法识别出处于窗口内的延迟重复序列号，因此无法丢弃它们。

PAWS 机制的引入是为了解决这个问题。我们使用时间戳（Timestamps）选项来保护 TCP 连接免受多个具有相同字节序列号段引起的影响。PAWS 机制的基本原理是为 TCP 段附加时间戳，如果其时间戳小于最后收到的段的时间戳，则将其作为重复包丢弃，这会导致接收窗口向前移动。（见第 24.4.1 节）。

