
1840     (`tp->ca_state == TCP_CA_Open`);

1841 }

```
# cs 11.29. `tcp_ack_is_dubious()`
# net/ipv4/tcp_input.c
```c
100 #define FLAG_ACKED (FLAG_DATA_ACKED|FLAG_SYN_ACKED)
101 #define FLAG_NOT_DUP (FLAG_DATA|FLAG_WIN_UPDATE|FLAG_ACKED)
102 #define FLAG_CA_ALERT (FLAG_DATA_SACKED|FLAG_ECE)
```
# cs 11.30. 入站 ACK 标志。
有一个段进入网络正在消耗资源。这就是为什么我们在计算在途数据包时考虑 `tp->retrans_out`。

## 11.4.2 `tcp_ack_is_dubious()`
这里有三个检查来确认我们处于拥塞状态或感知到了拥塞：
- 1. 当前 ACK 设置了 `FLAG_NOT_DUP` 标志。这表示我们收到了重复 ACK。
- 2. 当前 ACK 设置了 `FLAG_CA_ALERT` 标志。这表示我们需要告警。
- 3. 当前的 TCP 状态不应设置为打开 (`TCP_CA_Open`)。我们已经处于拥塞状态之一。

`FLAG_NOT_DUP` 定义为三个标志的组合：
- 1. `FLAG_DATA`
- 2. `FLAG_WIN_UPDATE`
- 3. `FLAG_ACKED`

如果上述任何标志被设置，我们需要检查稍后将讨论的其他条件。如果上述标志均未设置，则我们收到了重复 ACK。原因如下：
- 1. 如果我们获得了数据，则设置了 `FLAG_DATA`。尽管我们没有确认任何新数据，这也不应该被视为设置了 `FLAG_DATA` 的重复 ACK。一个简单的例子是考虑数据单向流动，且我们是接收方。在这种情况下，我们总是得到相同的 ACK 序列号，因为我们没有发送任何内容。我们不能将所有 ACK 都视为重复。
- 2. 如果对方的接收窗口发生了变化或它确认了新数据，则设置了 `FLAG_WIN_UPDATE`。我们讨论的重复 ACK 是指产生的乱序段已被对方接收。由于这个乱序段不会将窗口边缘向右移动，它不会改变其接收窗口。如果该段没有确认新数据且没有携带任何新数据但改变了发送窗口，它可以认为是对方的窗口更新而非重复 ACK。
- 3. 如果新数据被确认或我们获得了 SYN 段，则设置了 `FLAG_ACKED`。在这两种情况下，这不能被视为重复 ACK。

`FLAG_CA_ALERT` 有两个部分：`FLAG_DATA_SACKED` 和 `FLAG_ECE`。如果设置了这些标志中的任何，我们需要采取行动，因为我们感知到了拥塞。

`FLAG_DATA_SACKED` 在我们收到 SACK 块时设置。这表明段以乱序到达接收方。这可能是因为重序，也可能是因为某些段丢失。我们需要留留意。

`FLAG_ECE` 在我们在 TCP 头部中收到 ECE 标志时设置。对方从中间路由器收到了关于路由器拥塞的状态。路由器可能负载过重并丢弃包。在这种情况下，它在指向接收方的包 IP 头部中设置了 EC 标志。接收方转换 TCP 头部中的 ECE 标志以告知方拥塞状态。在这种情况下我们需要降低传输速率。

如果不满足上述条件，只有在我们已经处于拥塞状态时，才认为 ACK 是可疑的；此时 TCP 状态为除 `TCP_CA_Open` 以外的状态。

## 11.4.3 `tcp_cong_avoid()`
该程序在慢启动和快速重传期间实现拥塞控制。在章节 10.2.3（解释慢启动）和章节 12.5.5（解释重传）中，我们可以看到当感知到拥塞时，正如 Jacobson (SIGCOMM 88) 所的那样调整 `tp->snd_ssthresh` 和 `tp->snd_cwnd`。`tp->snd_ssthresh` 是慢启动。

# 406
# TCP 核心处理
```c
net/ipv4/tcp_input.c
1699 static __inline__ void tcp_cong_cnt_avoid(struct tcp_opt *tp)
1700
1701     if (tp->snd_cwnd <= tp->snd_ssthresh) {
1702         /* 在“安全”范围内，增加。 */
1703         if (tp->snd_cwnd < tp->snd_cwnd_clamp)
1704             tp->snd_cwnd++;
1705     } else {
1706         ....
1709         if (tp->snd_cwnd_cnt >= tp->snd_cwnd) {
1710             if (tp->snd_cwnd < tp->snd_cwnd_clamp)
1711                 tp->snd_cwnd++;
1712             tp->snd_cwnd_cnt=0;
1713         } else
1714             tp->snd_cwnd_cnt++;
1715     }
1717     tp->snd_cwnd_stamp = tp_time_stamp;
1718 }
```
cs 11.31, `tcp_cong_avoid()`.
当值非常大时，拥塞窗口会持续增加，直到我们遇到拥塞（段丢失或重复 ACK）。在此时，我们将重新计算 ssthresh 为拥塞窗口的一半或 2，以其中较大者为准（见第 10.2.3 节）。如果两个条件均为真，我们将拥塞窗口加 1（第 1704 行，cs 11.31）。

在我们进入恢复状态的情况下，这意味着拥塞窗口已超过了慢启动阈值（第 1706–1715 行）。Linux 采用根据*当前拥塞窗口*递增拥塞窗口的路径——即 `tp->snd_cwnd`，即接收到的 ACK 数量。这是因为假设在任何给定时刻，拥塞窗口都通过充分利用给定拥塞状态下的可用网络带宽，已经饱和了网络。每当我们收到一个 ACK 时，我们都会执行以下操作：
- 1. 我们检查计数器 (`tp->snd_cwnd_cnt`) 是否等于当前拥塞窗口。
- 2. 如果条件 1 为假，我们增加拥塞窗口计数器（`tp->snd_cwnd_cnt`，第 1714 行）。
- 3. 否则，只有在我们没有超过 cw clamp 时（第 1710 行），我们才准备增加拥塞窗口。如果通过此测试，则增加拥塞窗口并重置拥塞窗口计数器（第 1712 行）。

## 11.4.4 `tcp_ack_update_window()`
我们检查是否可以通过 `tcp_may_update_window()` 更新窗口。如果允许更新窗口，我们会在第 187 行（cs 11.3）设置标志 `FLAG_WIN_UPDATE`。由于窗口正在更新，我们通过调用 `tcp_update_window(tp)` 在 `tp->snd_wnd` 中记录段的序列号。在这种情况下如果通告了新窗口，我们在第 187 行同步发送窗口。我们还通过调用 `tcp_fast_path_check()` 检查是否需要切换到快速路径（关于路径的细节见第 11.1.3 节）。因为窗口已经改变且我们已经处于快速路径中，预测标志

## 传入 ACK 的处理
net/ipv4/tcp_input.c
```c
1865 static int tcp_ack_update_window(struct sock *sk, struct tcp_opt *tp,
1866             struct sock_buff *skb, u32 ack, u32 ack_seq)
1867 {
1868     int flag = 0;
1869     u32 nwin = ntohtons(sk->h->th->window) << tp->snd_wscale;
1871     if (tcp_may_update_window(tp, ack, ack_seq, nwin)) {
1872         flag = FLAG_WIN_UPDATE;
1873         tcp_update_wnd(tp, ack, ack_seq);
1874
1875     if (tp->snd_win < nwin) {
1876         tp->snd_win = nwin;
1881
1882         tcp_fast_path_check(sk, tp);
1883     if (nwin > tp->max_window) {
1884         tp->max_window = nwin;
1885         tcp_sync_mss(sk, tp->pmtu_cookie);
1886     }
1887 }
1888
1889
1890 tp->snd_una = ack;
1892     return flag;
1893 }
```
