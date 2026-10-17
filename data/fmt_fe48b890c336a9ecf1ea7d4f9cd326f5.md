
cs 11.13, `tcp_incr_quickack()`. ACK 计数只是分段数量的一半，意味着每两个分段可以发送一次 ACK。快速 ACK 的其余计算假设最小值为 2，最大值为 `TCP_MAX_QUICKS`。

## 11.3.5 `tcp_grow_window()` (参见 cs 11.14)

当我们接收到一个数据段时，我们需要根据分段大小计算一个需要宣告给发送者的接收窗口。其思想是避免在应用程序读取缓慢且数据包以高速传输时用过多的分段填满接收缓冲区，避免通过修剪队列来为接收队列留空间。由于发送端可以发送数百万个拥塞窗口和通告窗口，接收端通过缓慢增加接收窗口来占得机机。这种想法不仅是为了减少网络拥塞，还要考虑接收缓冲区管理。考虑一种发送端以高速发送小分块数据，而应用程序无法以高速度读取数据的情况。在这种情况下，数据段将队列在接收队列中，导致队列满。如果分段非常小，缓冲区开销会被数据占用。在这种情况下，我们需要修剪队列以为接收队列留空间，这是一个昂贵的过程。因此，为了避免频繁修剪队列，我们根据接收分段的大小操作宣告给发送者的接收窗口。如果发送者发送小分段，我们就不增加接收窗口，这样发送者就无法以极高速率传输，应用程序就有机会从队列中读取。

`net/ipv4/tcp_input.c`

```c
static int
    tcp_grow_window(struct sock *sk, struct tcp_opt *tp, struct sk_buff *skb)
    {
        /* Optimize this! ! */
        int truesize = tcp_full_win_from_space(skb->truesize)/2;
        int window = tcp_full_space(sk)/2;

        while (tp->rcv_ssthresh <= window) {
            if (truesize <= tp->rcv_len)
                return 2*tp->ack_rcv_mss;

            truesize >>= 1;
            window >>= 1;
        }
        return 0;
    }
```

cs 11.17. `_grow_tcp_window()`.

- `tp->rcv_ssthresh` 小于可用的接收缓冲区总空间，即第 230 行。
- 缓冲区占用的空间最大等于段长度，即第 231 行。

在每次迭代中，我们减少了接收缓冲区中的总可用空间和缓冲区大小。如果跳出循环是因为第一个条件变为 FALSE（假），我们不应该增加接收窗口，原因是缓冲区溢出的风险太大，无法在可用空间内容纳。简单来说，我们可以说这种膨胀（bloat）程度非常严重（非常小的段），以至于即使我们继续按相同比例减少总可用空间和总缓冲区大小，即使接收缓冲区中的总可用空间少于要通告的窗口，缓冲区溢出的概率仍然太高。
如果是因为后续条件为 TRUE 而退出循环，意味着缓冲区开销是可以接受的，因为段长度足够被接收缓冲区容纳。在这种情况下，我们可以通过目前为止看到的最大段长度的两倍来增加接收缓冲区。

## 11.3.7 我们如何计算通告的窗口

我们在 `tcp_select_window()` 中计算接收窗口。如第 11.3.9 节所述，我们知道有两个因素决定接收窗口。它们是 `tp->window_clamp` 和 `tp->rcv_ssthresh`。这两个参数的作用已经在第 11.3.9 节中讨论过，因此不再重复。在接收数据段时，我们计算 `tp->rcv_ssthresh` 并使用该参数来计算接收窗口。
首先，我们从第 150 行（cs 11.18）的 `tcp_receive_window()` 获取当前窗口。我们根据接收缓冲区中的可用空间、接收窗口的上限（`tp->window_clamp`）以及 `tp->rcv_ssthresh` 通过调用 `_tcp_select_window()` 计算新窗口。如果计算出的窗口小于当前窗口，则将新窗口提升为当前窗口。我们这样做是因为不应该允许通告窗口缩小。新窗口

### 慢路径 TCP 处理

```c
net/ipv4/tcp_output.c
static __inline__ __u16 tcp_select_window(struct sock *sk)
{
     struct tcp_opt *tp = &(sk->tp->pinfo.of_af_tcp);
     u32 cur_win = tcp_receive_window(tp);
     u32 new_win = __tcp_select_window(sk);

     ....
     if(new_win < cur_win) {
         new_win = cur_win;
     }
     tp->rcv_wnd = new_win;
     tp->rcv_up = tp->rcv_nxt;

     new_win >>= tp->rcv_scale;
     ....
     if (new_win == 0)
         tp->pred_flags = 0;
     
     return new_win;
}
```

```c
cs 11.18. tcp_select_window().
include/net/net.h
include/net/tcp.h
static __inline__ __u32 tcp_receive_window(struct tcp_opt *tp)
{
     u32 win = tp->rcv_up + tp->rcv_wnd - tp->rcv_nxt;
     
     if (win < 0)
         win = 0;
     return (u32)win;
}
```

`_tcp_select_window()` 返回 0 是因为可用空间已低于 1 mss。但我们不能突然通告窗口。在这种情况下，`tcp_receive_window()` 返回的当前窗口将获得精确窗口。同样，当窗口很小（小于 1 mss）时，除非通告至少 1 mss 的窗口，否则 `_tcp_select_window()` 会处理这种情况（cs 11.18）。

## 11.3.8 `tcp_receive_window()`

它是通过上一次通告窗口减去未确认的数据长度计算出的。我们在 `tcp_select_window()` 发送 ACK 时，`tp->rcv_up` 与下一个接收的字节（`tp->rcv_nxt`）同步。如果没有未确认的数据，该程序返回精确窗口（cs 11.19）。

## 11.3.9 `_tcp_select_window()`

我们被调用来计算新的通告窗口。窗口计算的基础是：

```c
net/ipv4/tcp_output.c
u32 __tcp_select_window(struct sock *sk)
    {
        struct tcp_opt *opt = &sk->tp->pinfo.of_tcp;
        int mss = tp->ack_rcv_mss;
        int free_space = tcp_space(sk);
        int full_space = min(tp->window_clamp, tcp_full_space(sk));
        int window;

        if (mss > free_space/2)
            mss = full_space;
            if (free_space < full_space/2)
                tp->ack_quick = 0;

                if (tp->memory_pressure)
                    tp->rcv_thresh = min(tp->rcv_thresh, 4*tp->adv_mss);
                if (free_space < mss)
                        return 0;
                }
```
