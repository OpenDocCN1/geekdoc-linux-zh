
```c
/* 更新我们的发送窗口。 
 * 窗口更新算法，描述于 RFC793/RFC1122（用于 linux-2.2）
 * 以及在 FreeBSD 中。NetBSD 的（更糟）是错误的。 */
static int tcp_ack_update_window(struct sock *sk, struct tcp_opt *tp,
                               struct sk_buff *skb, u32 ack, u32 ack_seq)
{
    int flag = 0;
    u32 win = ntohs(skb->h->th->window) << tp->snd_wscale;
    if (tcp_may_update(tp, ack, ack_seq, win)) {
        flag = FLAG_WIN_UPDATE;
        tcp_update_wl(tp, ack, ack_seq);
        if (tp->snd_wnd != win) {
            tp->snd_wnd = win;
            /* 注意，这是发送 TCP 时
             * 恢复快速路径的唯一地方。 */
            tcp_fast_path_check(sk, tp);
            if (win > tp->max_window) {
                tcp_sync_mss(sk, tp->mtu_cookie);
            }
        }
    }
    tp->snd_una = ack;
    return flag;
}
/* 此例处理传入的 ack，但不处理发出的 ack。 */
static int tcp_ack_struct(struct sock *sk, struct sk_buff *skb, int flag)
{
    struct tcp_opt *tp = &(sk->tp.tp_info.afc);
    u32 prior_snd_una = tp->snd_una;
    u32 ack_seq = TCP_SKB_CB(skb)->seq;
    u32 ack_seq = TCP_SKB_CB(skb)->ack_seq;
    u32 prior_in_flight;
    int prior_packets;
    /* 如果 ack 永远未发送或比之前的 ack 旧，
     * 那么我们可以正确地忽略它。 */
    if (after(ack, tp->snd_nxt)) {
        goto uninteresting_ack;
    }
    if (before(ack, prior_snd_una)) {
        goto old_ack;
    }
    if (!(flag&FLAG_SLOWPATH) && after(ack, prior_snd_una)) {
```

```c
1917      /* 窗口保持不变，纯粹的前推进。
1918      * 无需进行更多检查。
1919      * 注意，我们利用了 SND_UNA=SND_WL2 的事实。
1920      */
1921      tcp_update_wl(tp, ack, ack_seq);
1922      tp->snd_una = ack;
1923          flag = FLAG_WIN_UPDATE;
1924
1925          NET_INC_STATS_BH(TCPHacks);
1926
1927  } else {
1928      if (ack == TCP_SK_CB(skb)->end_seq)
1929          flag = FLAG_DATA;
1930      else
1931          NET_INC_STATS_BH(TCPPureAcks);
1932          flag = tp->ack_update_window(sk, tp, sk, ack, seq);
1933
1934      if (TCP_SK_CB(skb)->sacked)
1935          flag = tcp_sackack_write_queue(sk, prior_snd_una);
1936
1937      if (TCP_ECN_rcv_ecn(tp, sk->th.th))
1938          flag = FLAG_ECE;
1939
1940      }
1941      /* 我们传递了数据并收到了确认，移除任何软错误
1942       * 日志生效...
1943       */
1944      sk->err_soft = 0;
1945      tp->rcv_timestamp = tp->time_stamp;
1946      if ((prior_packets = tp->packets_out) == 0)
1947          goto no_queue;
1948
1949      prior_in_flight = tp->packets_in_flight(tp);
1950      /* 查看我们是否可以从重传队列中移除某些包。 */
1951      flag = tp->cfl_rtx_queue(sk);
1952
1953      if (tp->ack_is_doubling(tp, flag)) {
1954          /* 推进 cwnd，如果状态为 snd_cwnd &&
1955          if ((flag&FLAG_DATA_ACKED) && prior_in_flight >= tp->snd_cwnd &&
1956              tp_may_raise_cwnd(tp);
1957              tcp_fastretrans(sk, prior_snd_una, prior_packets);
1958      } else {
1959      if ((flag&FLAG_DATA_ACKED) && prior_in_flight >= tp->snd_cwnd)
1960          tcp_cwnd_avoid(tp);
1961
1962      if ((flag & FLAG_PROGRESS) || !(flag&FLAG_DUP))
1963          dst_confirm(sk->dst_cache);
1964
1965          return 1;
1966
1967  no_queue;
1968      tp->probes_out = 0;
```

```c
1972  /* 如果此 ack 开启了零窗口，清除退避。它
1973  用于探测，并且可能比
1974  * 需要重传的高。
1975  */
1976  if (tp->send_head)
1977      tcp_ack_probe(sk);
1978      return 1;
1979
1980  old_ack:
1981      if (TCP_SKB_CB(skb)->sacked)
1982          tcp_sacks_write_queue(sk, skb, prior_snd_una);
1983
1984  interesting_ack:
1985      SOCK_DEBUG(sk, "Ack %u of %u", ack, tp->snd_una, tp->snd_next);
1986          return 0;
1987  }
```

发生乱序包，会发送重复 `ACK` 并调用 `tcp_dup()`。如果成功，调用 `tcp_ack_snd_check`，且 `tcp_ack_snd_check` 会发送立即 `ACK` 或调度延迟 `ACK`（图 48）。
