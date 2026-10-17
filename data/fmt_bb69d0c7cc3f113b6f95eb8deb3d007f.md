
```
    struct sk_buff_head  prequeue;
    struct task_struct    *task;
    struct iovec          *iov;
    int                   memory;
    int                   len;
} ucopy;
```

`Snd_wnd` 有一个接收窗口序列号 `snd_wnd`，`SND_WND` 是对端愿意接收的最大窗口大小 [RFC 793]。此外，`max_window` 是此连接范围内从对端接收到的最大窗口。

```
__u32    snd_wnd;
__u32    snd_wnd;
__u32    max_window;
```

`Pmtu_cookie` 设置为该 socket 引用的最后一个 PMTU（路径最大传输单元），`mss_cache` 是当前的发送 MSS，而 `mss_clamp` 是连接建立时协商的最大 MSS。

```
__u32    pmtu_cookie;
__u16    mss_cache;
__u16    mss_cache_std;
__u16    mss_clamp;
```

`Ext_header_len` 是 TCP/IP 数据包头长度，包括 IP 头和 IP 选项。`Ca_state` 持有表 8.6 中列出的快速重传状态机。

```
__u16    ext_header_len;
__u16    ext2_header_len;
__u8     ca_state;
```

表 8.6: `Tcp_ca_state`, 快速重传状态

| 状态 | 取值 |
| :--- | :--- |
| `TCP_CA_Open` | 0 |
| `TCP_CA_Disorder` | 1 |
| `TCP_CA_CSR` | 2 |
| `TCP_CA_Recovery` | 3 |
| `TCP_CA_Loss` | 4 |

`Retransmits` 包含未恢复的 RTO（重传超时）数量。`Reordering` 是一个包指标，表示数据包在流中偏移的最大距离。`queue_shrunk` 表示队列大小已经缩小；一个数据包已从 `wmem` 缓冲区中被移除。

```
u8 retransmits;
u8 reordering;
u8 queue_shrunk;
```

以下字段用于 `TCP_DEFER_ACCEPT` 套接字选项，该选项允许应用程序休眠直到数据到达套接字上。此选项以秒为单位表示，但会被转换为重试次数。

```
u8 defer_accept;
```

TCP 测量往返时间 (RTT) 以支持基于 Jacobson 算法的重传 [KAR88]；另请参考 Karn Partridge 算法 [KAR91]。Stevens 在第 2.3 节和 21.4 节中讨论了 RTT 测量 [STEV94]。TCP 选项中的后续字段用于测量 RTT。`backoff` 是重传前的时间，`srtt` 是平滑后的 RTT 值，`mdev` 是最近 RTT 周期的最大偏差，而 `rto` 是 `mdev_max` 的最大偏差。`rttvar` 是更新 `rtt` 的序列号。

```
u8 backoff;
u32 srtt;
u32 mdev;
u32 mdev_max;
u32 rttvar;
u32 rtt_seq;
u32 rto;
```

接下来三个字段用于计算已传输但未确认的数据包数量——即在途包（packets in flight）。`Packets_out` 是根据字节数除以段大小计算出的未确认数据量。`Left_out` 是乱序到达的数据包数量加上丢失的分段数量。

```
u32 packets_out;
u32 left_out;
u32 retrans_out;
```

以下字段用于 Nagle 算法 [RFC896]、Karn Partridge 算法 [KAR91] 和 Jacobson 算法 [KAR88] 指定慢启动和拥塞控制。此外，RFC 2861 的第 3.2 节包含了减少拥塞窗口的建议。`Snd_sstresh` 是慢启动阈值。`Snd_cwnd` 是发送拥塞窗口，而 `snd_cwnd_cnt` 是线性增加计数。`Snd_cwnd_clamp` 是 `snd_cwnd` 的最大允许值。`snd_cwnd_used` 是使用的窗口变量，而 `snd_cwnd_stamp` 是拥塞窗口时间戳。

```
u32 snd_sstresh;
u32 snd_cwnd;
u16 snd_cwnd_cnt;
u16 medical_clamp;
u32 snd_cwnd_used;
u32 medical_stamp;
```

这些字段是发送和接收双方广泛使用的定时器。`timeout` 是用于重传值的变量，`retransmit_timer` 是 TCP 重传定时器，`delay_timer` 是延迟确认定时器。关于 TCP 定时器的更多信息请参见第 8.6 节。

```
unsigned long timeout;
struct timer_list retransmit_timer;
struct timer_list delack_timer;
```

套接字队列 `out_of_order_queue` 持有乱序段。`Af_specific` 指向 `AF_INET` 族的 TCP 选项。`Send_head` 指向传输的套接字队列。

```
struct sk_buff_head out_of_order_queue;
struct tcp_func *af_specific;
struct sk_buff *send_head;
```

`RCV_wind` 是接收窗口大小，即 RFC 793 中的 `RCV_WND` 变量。`RCV_wup`（接收窗口更新）是当前的宣告窗口大小。`Write_seq` 是发送序列号，实际上等于发送缓冲区数据加 1 字节。`P_seq` 是最后一个推送序列号。`Copied_seq` 是未被用户进程读取的接收数据的起始位置。

```
u32 rcv_wind;
u32 rcv_wup;
u32 write_seq;
u32 pushed_seq;
u32 copied_seq;
```

以下字段用于接收的 TCP 选项。TCP 选项见表 8.7。某些选项仅在 SYN 包中接收，而其他可以在任何数据包中找到。下一个字段 `timestamp_ok` 表示 SYN 包中收到了时间戳。`wscale_ok` 表示 SYN 包中收到了窗口缩放选项。窗口缩放通过减少 ACK 的数量来提高 TCP 效率。窗口缩放选项指定一个计数，即左移窗口大小的位数。TCP 头中的此 16 位字段表示比 65535 更大的数字。关于窗口缩放的讨论请见 Stevens 的 24.4 节 [STEV94]。`sack_ok` 表示 SYN 包中收到了 `TCP_SACK` 选项，`saw_timestamp` 表示最近数据包中的时间戳选项（`TCPOPT_TIMESTAMP`）已被看到并处理。

```
char tstamp_ok,
wscale_ok,
sack_ok;
saw_timestamp;
```
