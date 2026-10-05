

# 传输 535

```c
451      * 但它限制了 rto 过快减少，
452      * 发生在纯 Eifel。
453      /*
454      if (m > 0)
455          m >>= 3;
456
457  } else {
458      m = (tp->mdev >> 2); /* 对 mdev 进行类似的更新 */
459      tp->mdev = m;      /* mdev = 3/4 mdev + 1/4 new */
460      if (tp->mdev > tp->mdev_max) {
461          tp->mdev_max = tp->mdev;
462          if (tp->mdev_max > tp->rttvar) {
463              tp->rto = tp->mdev_max;
464          }
465          if (after(tp->snd_una, tp->rtt_seq)) {
466              if (tp->mdev_max < tp->rttvar)
467                  tp->rto = (tp->rttvar-tp->mdev_max)>>2;
468              tp->rtt_seq = tp->snd_una;
469              tp->mdev_max = TCP_RTO_MIN;
470          }
471      }
472  }  /* 无之前的测量值。 */
473      tp->rto = m(3);      /* 取测量得的时间作为 rtt */
474      tp->mdev = min(2);   /* 确保 rto = 3*rtt */
475      tp->mdev_max = tp->rttvar = max(tp->mdev, TCP_RTO_MIN);
476      tp->rtt_seq = tp->snd_nxt;
477
478  }
```

当一个段被 TCP 确认机制确认时，它们已被 SACKed 的这一事实就不再需要记录了。

# 防止序列号回绕保护–PAWS

这是 RFC 1323 中描述的高性能 TCP 扩展。在高带宽远距离链路中，存在序列计数在网络中仍有有效旧段时发生回绕的危险。PAWS 算法通过使用时间戳选项防止这种情况，该选项携带一个非递增的整数。基本思想是，如果一个段的时间戳小于最近收到的某个时间戳，则丢弃该段。tcp_opt 中的以下变量被使用：

- rcv_tsval—此段中的时间戳
- ts_recent—最近收到的时间戳
- ts_recent_stamp—ts_recent 变得的时间

# 图 7.65 往返估计 (iii)。

```c
/* 在不进行回退的情况下计算 rto。这是上述 Van Jacobson
 * 例程的后半部分。
 * __inline__
 static __inline__ void tcp_set_rto(struct tcp_opt *tp)
{
     * 旧的垃圾被新的替换了。8
     * 更严重地说；
 * 1. 如果 rto 差是由于 50 毫秒引起的，那是幻觉。
 * 它不可能是由于由 solaris 和 freed 产生的完全不稳定的 ACK 生成导致的。
 * “不稳定的 ACK”与延迟 ACK 无关，
 * 在 cvnd 时超时是不可见的。
 * 实际上，往返 linux-2.4 在某些情况下会产生不稳定的
 * ACK。
 */
tp->rto = (tp->rtt >> 3) + tp->rttvar;
/* 2. 较早发生的错误不可能是正确的。
 * 如果我们没有在它们的情况下正确估计 RTO，
 * 所有的逻辑都是狗屁，应该被
 * 正确的替换。这正是我们假装所做的。
 */
/* 注意：在 TCP_RTO_MIN 处截断是不需要的，当前算法
 * 保证了 rto 更高。
 */
 static __inline__ void tcp_bound_rto(struct tcp_opt *tp)
{
    if (tp->rto > TCP_RTO_MAX)
        tp->rto = TCP_RTO_MAX;
}
```

# 往返估计

为了在带宽利用率方面从 TCP 连接中获得更多，需要一种准确的方法来确定用于超时的往返时间。该机制在 Stevens [8] 中描述，并在图 7.63-7.64 中展示了实现。

# 图 7.66 在 SYN 包上构建选项。

```c
/* 为 SYN 或 SYN_ACK 包构建 tcp 选项标头。
 * 如果这里有任何更改，请确保更改
 * MAX_SYN_SIZE 的定义，以匹配你可以
 * 生成的最大选项数量。
 */
```

# 传输 537

```c
1441 static inline void tcp_syn_build_options(__u32_ptr, int mss, int ts, int sack,
1442                             offset_wscale, int wscale, __u32 tstamp, __u32
1443                             ts_recent)

1444 (
1445      /* 我们总是获得一个 MSS 选项。
1446      * 在正常数据
1447      * 包中看到的选项字节应该被使用，必须在通告的
1448      * MSS 中。但我们从 tp 中减去
1449      * mdev 的计算更简单。
1450      * 所以我们在这里检查是否有必要。
1451      * 如果不这样做，作为接收者我们将
1452      * 识别全大小包，因此无法遵守
1453      * ACK 规则。
1454      * SACK 与此无关，我们并不
1455      * 有这些出去时发送 ACK。
1456      * 正确的。
1457      /
1458      *ptrtr = htonll((TCPOPT_MSS << 24) | (TCPOLEN_MSS << 16) | mss);
1459  if (ts)
1460    if (sack)
1461          *ptrtr = __htonl((TCPOPT_SACK_PER << 24) | (TCPOLEN_SACK_PER
1462                                 << 16) | sack);
1463    else
1464          *ptrtr = __htonl((TCPOPT_NOP << 24) | (TCPOLEN_NOP << 16)
1465                                     (TCPOPT_TAMP << 8) | (TCPOLEN_TAMP));
1466          *ptrtr = htonl(timestamp);      /* TSVAL */
1467          *ptrtr = htonl(ts_recent);     /* TSCR */
1468  } else if (sack)
1469    *ptrtr = __htonl((TCPOPT_NOP << 24) | (TCPOLEN_NOP << 16
1470                                 (SACK_PER);
1471  if (offset_wscale)
1472    *ptrtr = htonl((TCPOPT_NOP << 24) | (TCPOLEN_NOP << 16)
1473                                 (wscale);
1474 )
```

# 图 7.67 往返估计 (iv)。

# 窗口缩放

SYN 包上的窗口缩放允许该值如 RFC 1323 所示进行扩展。随着带宽和距离的不断增加，这不再足够（见图 7.67）。

