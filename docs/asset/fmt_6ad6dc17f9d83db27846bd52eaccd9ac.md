
```
3360        if (tp->in_quick_mode(tp)) {

3361            tcp_send_ack(sk);

3362        } else {

3363            tcp_send_delayed_ack(sk);

3364        }

3366    } else {

3367        tcp_ack_snd_check(sk, 0);

3369 no_ack:
3370    if (even) {
3371        kfree_skb(skb);
3372    } else
3373        sk->data_ready(sk, 0);
3374        return 0;
3375    }
3376    }
```

`cs 11.8. tcp_rcv_established()`.

点；即我们不确定是否能够传输新数据。因此，通过在第 3355 行调用 `tcp_ack_scheduled(tp)` 来检查接收到的数据是否仍然调度了 ACK。如果没有调度 ACK，说明我们已经将数据拷贝到用户缓冲区，只需在第 3371 行释放缓冲区即可。否则，我们将数据已入了接收队列，并且需要在第 3373 行调用 `sk->data_ready(= sock_def_readable(sk))` 来唤醒睡眠的套接字以接收更多数据。如果已经调度了 ACK，那么我们需要根据许多因素（第 3359–3367 行）决定是立即发送 ACK 还是延迟发送。这在第 10.4 节（TCP 定器章节）中有详细的讨论。

# 11.3 慢路径处理（除非另有说明，参见 cs 11.10）

慢路径处理从第 3379 行开始。首先我们进行完整性检查。如果段的长度小于 TCP 头部字段中指定的头部长度，或者如第 3379 行 `tcp_checksum_complete_user()` 所示校验和不正确，则我们丢弃该段。我们对回绕的时间戳进行 PAWS 检查。为了实现此点，我们首先在第 3385 行通过 `tcp_fast_parse_options()` 解析 TCP。如果存在时间戳选项，我们将继续 PAWS 检查；否则继续进行慢路径处理。当存在时间戳选项时，我们在第 3386 行调用 `tcp_paws_discard()` 来检查数据包是否被丢弃。

慢路径处理

`net/ipv4/tcp_input.c`

```
2186 static inline int tcp_sequence(struct tcp_opt *opt, u32 seq, u32 end_seq)
2187 {
2188     return before(end_seq, tp->rcv_wup) &&
2189         after(seq, tp->rcv_rst + tcp_receive_window(tp));
2190 }
```

`cs 11.9. tcp_sequence()`.

丢弃是因为 PAWS 失败了（详情见节 11.3.1）。在存在 RST 段的情况下，如果 PAWS 失败，我们将处理该段，否则不再进一步处理该段。接下来我们通过 `tcp_sequence()` 检查该段是否维持了序列号的完整性。

### 11.3.1 tcp_sequence()

此检查我们是否已经获得了完全确认的数据，并且我们已经拥有了段中的所有位，2188。当我们在 `tcp_select_window()` 中发送 ACK 时，`tp->rcv_wup` 与 `tp->rcv_nxt` 同步。如果段的结束序列低于 `tp->rcv_wup`，则我们不应该接受此段。我们已经对直到 `tp->rcv_wup` 的所有数据发送了 ACK。我们在此进行的第二个检查是，段的起始序列不应超过对应接收窗口端的序列号，2189，这本质上意味着该段相对于已确认的数据不应超出窗口。在这种情况下，如果不是 RST 段，我们将通过第 3411 行（cs 11.10）调用 `tcp_send_dupack()` 发送重复 ACK（带 DSACK），并丢弃数据包。RST 段的序列字段不应超出窗口，也不应对应已确认的序列号（参见 RFC 793）。

现在我们确定该段的序列字段是有效的且 PAWS 也是接受的。如果段带有 RST 位，我们将通过第 3416 行（cs 11.10）调用 `tcp_reset()` 重置我们的连接并停止进一步处理该段。`tcp_reset()` 会唤醒等待的套接字并关闭 TCP 连接。现在我们通过在第 3420 行（cs 11.10）调用 `tcp_replace_ts()` 检查段的时间戳是否可以作为最新的时间戳记录。

### 11.3.2 tcp_replace_ts_insert()

这将确保我们不会保留乱序段的时间戳。段的序列起始应最大等于已确认的（`tp->rcv_wup`），2110（cs 11.1）。如果段的时间戳大于当前记录的时间戳（`ip->ms_timestamp`），我们通过第 2120 行调用 `tcp_store_ts()` 将其替换。否则，如果时间戳小于记录的时间戳，我们需要检查自记录以来是否超过了 24 天。如果是，我们将替换为段的时间戳，因为记录的时间戳太旧了。

# TCP 处理

`net/ipv4/tcp/input.c`

```
tcp_rcv_established() 继续....
3378 slow_path:
3379     if (len < (th->doff<2) || tcp_checksum_complete_user(sk, skb))
3380         goto csum_error;
3385     if (tcp_fast_parse_options(skb, th, tp) && tp->saw_ts &&
3386         tcp_paws_discard(sk, skb))
3387         if (th->rst)
3388             NET_INC_STATS_BH(PAWS_Rejected);
3389             tcp_send_dupack(sk, skb);
3390             goto discard;
3391         }
3397 }
3403 if (!tcp_sequence(tp, TCP_SKB_CB(skb)->seq, TCP_SKB_CB(skb)->end_seq)) {
3410     if (th->rst)
3411         tcp_send_dupack(sk, skb);
3412         goto discard;
3413     }
3415     if (th->rst)
3416         tcp_reset(sk);
3417         goto discard;
3418 }
3420     tcp_replace_ts_recent(tp, TCP_SKB_CB(skb)->seq, tp->rcv_nxt);
3422     if (th->syn && before(TCP_SKB_CB(skb)->seq, tp->rcv_nxt)) {
3423         TCP_INC_STATS_BH(pErrors);
3424         NET_INC_STATS_BH(TCPAbortSyn);
3425         tcp_reset(sk);
3426         return 1;
3427     }
3429 step:
3430     if (th->ack)
3431         tcp_ack(sk, skb, FLAG_SLOWPATH);
3434         ...
3435         tcp_sk(sk, skb);
3437         tcp_data_queue(sk, skb);
3438         ...
3439         tcp_data_nd_check(sk);
3440         tcp_ack_nd_check(sk);
3441         return 0;
3444         ...
3446 discard:
3447     kfree_skb(skb);
3448     return 0;
3449 }
```

`cs 11.10. tcp_rcv_established()`.

继续 `tcp_rcv_established()` 第 3422 行，如果它不是 RST 段且设置了 SYN 位，我们处理序列号不小于预期数的情况（第 3422 行）。这可能是因为连接请求端的 SYN 段发生了重传，原始段和重传段连续到达了另一端。如果是慢路径处理

```c
2107 export __inline void
2108 tcp_replace_ts(struct tcp_opt *tp, u32 seq)
2109 {
```
