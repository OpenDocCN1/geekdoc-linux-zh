
> `cs 11.32. tcp_ack_update_window()`.

`net/ipv4/tcp_input.c`

```c
1852 static __inline_int

1853 tcp_may_update_window(struct tcp_opt *tp, u32 ack, u32 ack_seq, u32 nwin)

1854 {

1855     return (after(after(ack, tp->snd_una) ||

1856         after(ack_seq, tp->snd_wnd)) ||

1857         (ack_seq == tp->snd_wnd && nwin > tp->snd_wnd));

1858 }
```

> `cs 11.33. tcp_ack_update_window()`.

需要初始化，因为它考虑了窗口。如果通告的窗口比之前看到的窗口大，则同步 `tp->max_window`。最后，确认的序列号在第 1890 行同步。

## 11.4.5 tcp_may_update_window

我们可以在以下条件下更新窗口（RFC 793，第 72 页）：

- 1. 如果新数据被确认，第 1855 行，`cs 11.3`。
- 2. 如果第一个条件失败，段的序列号应该高于更新窗口时的序列号 (`tp->snd_wnd`)，第 1856 行。此检查的原因是相对于更新窗口的段带有新数据。
- 3. 如果两个条件都失败，我们检查段的序列号是否等于 `tp->snd_wnd`，但通告的窗口大于记录的窗口 (`tp->snd_wnd`)，第 1857 行。这种情况可能是因为对方打开了窗口。段可能乱序且窗口不正确。在这种情况下丢弃窗口更新。

## 11.4.6 tcp_clean_rtx_queue()

当我们在处理传入 ACK 时调用该程序（`cs 11.34`）。该程序从重传队列中移除确认的段。如果段被标记为 SACKED、重传或丢失，该程序会更新特定的 SACKED-out、丢失段和重传段计数器。遍历写队列直到找到下一个未确认的字节，在调用前已更新 `una`。接下来需要检查确认的是否 SYN 段。由于我们已经确认了一些数据，我们在这里。如果是确认的 SYN 段，因为 SYN 携带一个字节。两种情况下都会设置 `FLAG`。下一步是处理段上的标记。

如果段被标记，我们首先检查段是否已重传。如果段被标记为重传，`tp->retrans_out` 减 1（第 1677–1770 行）。否则，如果段从未重传且未记录 RTT（第 1772 行），我们根据当前时间戳和发送段的时间计算 RTT。不要为重传段计算 RTT（第 1773 行）。如果段是 SACKed out，我们需要减少 SACK 计数器（第 1775 行）。如果段被标记为丢失，丢失计数器减 1。我们检查是否设置了用户模式（见第 11.7.1）。如果设置了，检查段是否覆盖用户点（第 1779–1780 行）。如果两个都真，则确认了紧急字节并使用紧急模式。

否则，确认的段未标记（未重传、未 SACK、未标记为丢失）且我们没有计算 RTT，记录 RTT（第 1784 行）。接下来检查段是否为 FACK out，减少 FACK 段（第 1786 行）。减少发送包数量。通过调用它从重传队列中移除确认的段（第 1788 行）。

下一步是根据 TCP 时间戳选项或上述计算的 `rtt` 估计 RTO。这是通过调用 `tcp_ack_update(rtt)` 实现的。我们有三个字段用于计算 RTO：

- 1. `tp->srtt` RTT。每次接收 RTT 值时，我们根据 `srtt` 和新值计算误差。计算公式为 7/8(`srtt`) + 1/8 (新值)。
- 2. `tp->mdev` 是 RTT 的平均偏差计算，再次计算为 3/4 (`mdev`) + 1/4 的新偏差。
- 3. `tp->rttvar` 是 `rtt` 计算中的变异。

最后，RTO 的计算公式为：

1/8 (平滑 RTT) + 变异 RTT

```c
net/ipv4/tcp_clean_rtx_queue(struct sk_
```

```c
1733 static int tcp_clean_rtx_queue(struct sk *sk)
1740     ...
1741     while((scb=skb->peek(&sk->write_queue)) && (skb !=tp->send_head)) {
1742         struct tcp_skb_cb cb = TCP_SKB_CB(skb);
1743             u8 sacked = scb->acked;
1749         if (after(scb->end_seq, tp->snd_una))
1750             break;
1759         if(scb->flags & TPCB_SYN)) {
1760             acked = FLAG_DATA_ACKED;
1761         } else {
1762             acked = FLAG_SYN_ACKED;
1763             tp->retrans_stamp = 0;
1764         }
1766         if (acked) {
1767             if(acked & TPCB_RETRANS) {
1768                 if(acked & TPCB_SACK_RETRANS) {
1769                     tp->retrans_out=;
1770                 acked = FLAG_RETRANS_DATA_ACKED;
1771                 seq_rtt = -1;
1772             } else if (seq_rtt < 0) {
1773                 seq_rtt = now - scb->when;
1774                 if(acked & TPCB_SACK_ACKED) {
1775                     tp->acked_out=;
1776                 } if(acked & TPCB_LOST) {
1777                     tp->lost_out=;
1778                 } if(acked & TPCB_URG) {
1779                     if(before(scb->end_seq, tp->snd_up)) {
1780                         tp->urg_mode = 0;
1781                     }
1782                 }
1783             }
1784         }
1785             if(acked & TPCB_FACK) {
1786                 tp->fackets_out=;
1787                 tp->packets_out=;
1788                 skb_unlink(skb, skb->list);
1789                 tcp_free_skb(skb, skb);
1790             }
1791         }
1816     return acked;
1817 }
```

# net/ipv4/tcp_input.c

```c
1723 static __inline_ void tcp_ack_packets_out(struct sock *sk, struct tcp_opt *tp)
1724 {
1725     if (tp->packets_out==0) {
1726         tcp_clear_xmit_timer(sk, TCP_TIME_RETRANSM);
1727     } else {
1728         tcp_reset_xmit_timer(sk, TCP_TIME_RETRANSM, tp->rto);
1729     }
1730 }
```

`11.35, tcp_ack_packets_out()`.

最后，我们需要通过 `tcp_ack_packets_out()` 根据是否仍有未确认的数据包 (`tp->packets_out>0`) 来调整重传定时器。如果我们拥有所有数据，则应该停止重传定时器（第 1726 行，`11.35`）。否则，我们将重传定时器设置为下一个待确认分段的当前 RTO 值（第 1728 行）。

我们在例程中设置的标志位将在稍后用于确定行动方案。

## 11.5 SACK 块的处理
