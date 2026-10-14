
sk->>receive_queue

![](img/b3f231108facab5be0138b2cfd3f681a_458_3.png)

图 11.29. 入队新段后的乱序队列。

将只剩下一个段 $[seq\_i, end\_seq\_j]$，因为它没有被 `tp->>rcv_nxt` 覆盖，如图 11.30 所示。最终的序列空间如图 11.31 所示。

接下来，我们考虑一个新序列数据段完全覆盖该段的情况，如图 11.32 所示。进入例程前的序列状态为：

```
tp->>rcv\_nxt > end\_seq\_i
n = tp->>rcv\_nxt - end\_seq\_i
```

sk->out_of_order_queue

![](img/b3f231108facab5be0138b2cfd3f681a_459_0.png)

图 11.30. 乱序队列中仅剩下一个段，因为一个顺序内段被移动到了接收队列。

tp->rcv_nxt

![](img/b3f231108facab5be0138b2cfd3f681a_459_1.png)

图 11.31. 从乱序队列重牌段到接收队列后的序列空间。

tp->rcv_nxt

![](img/b3f231108facab5be0138b2cfd3f681a_459_2.png)

图 11.32. 新 ACK 覆盖了乱序队列中一个段的序列空间。

sk->>receive_queue

![](img/b3f231108facab5be0138b2cfd3f681a_459_3.png)

图 11.33. 新段被排入接收队列。

在这里，段 $[seq\_1, end\_seq]$ 被新段完全覆盖，因此它从队列中移除，因为所有位已经在接收队列中，如图 11.33 所示。乱序队列将只剩下一个段 $[seq\_2, end\_seq]$，如图 11.30 所示。最终序列空间将只显示一个空洞。在下面解释的两个示例中，在 `tcp_sack_remove()` 重新组织 SACK 块之前，我们有以下 SACK 和 DSACK 块。`tcp_sack_remove()` 在之后立即调用，以移除所有被 `tp->rcv_nxt` 覆盖的 SACK 块。

我们获得了部分覆盖段 $[seq\_i, seq\_j]$ 的段，如图 11.28 所示。由于序列 $seq\_i \le tp->rcv\_nxt < seq\_j$，我们已经通过 `tcp_of_queue()` 完成了处理，处理后的接收队列如图 11.29 所示。该队列将包含重叠的段，因为我们没有在此例程中进行任何截断。接收程序在读取数据时会处理这个问题。乱序队列将

将只剩下一个段 $[seq\_i, end\_seq\_j]$，因为它没有被 `tp->>rcv_nxt` 覆盖，如图 11.30 所示。最终的序列空间如图 11.31 所示。

接下来，我们考虑一个新序列数据段完全覆盖该段的情况，如图 11.32 所示。进入例程前的序列状态为：

```
tp->>rcv\_nxt > end\_seq\_i
n = tp->>rcv\_nxt - end\_seq\_i
```

sk->out_of_order_queue

![](img/b3f231108facab5be0138b2cfd3f681a_459_0.png)

图 11.30. 乱序队列中仅剩下一个段，因为一个顺序内段被移动到了接收队列。

tp->rcv_nxt

![](img/b3f231108facab5be0138b2cfd3f681a_459_1.png)

图 11.31. 从乱序队列重牌段到接收队列后的序列空间。

tp->rcv_nxt

![](img/b3f231108facab5be0138b2cfd3f681a_459_2.png)

图 11.32. 新 ACK 覆盖了乱序队列中一个段的序列空间。

sk->>receive_queue

![](img/b3f231108facab5be0138b2cfd3f681a_459_3.png)

图 11.33. 新段被排入接收队列。

在这里，段 $[seq\_1, end\_seq]$ 被新段完全覆盖，因此它从队列中移除，因为所有位已经在接收队列中，如图 11.33 所示。乱序队列将只剩下一个段 $[seq\_2, end\_seq]$，如图 11.30 所示。最终序列空间将只显示一个空洞。在下面解释的两个示例中，在 `tcp_sack_remove()` 重新组织 SACK 块之前，我们有以下 SACK 和 DSACK 块。`tcp_sack_remove()` 在之后立即调用，以移除所有被 `tp->rcv_nxt` 覆盖的 SACK 块。

在两种情况下，DSACK 块将是，因为规范说 DSACK 块应该被完全覆盖。由于新段填充了空洞，边界匹配。见 11.34。

tp->rcv_nxt

![](img/b3f231108facab5be0138b2cfd3f681a_460_0.png)

图 11.34. 新段移动到接收队列后的序列空间。

| end\_seq+q | seq\_q |
| :--- | :--- |
| tp->rcv\_nxt | selective\_acks[0] |
| end\_seq | selective\_acks[1] |
| end\_seq | selective\_acks[2] |

# 摘要

## 443

`tp->duplicate_sack[]`

`tp->selective_acks[]`

`tp->duplicate_sack[]`

`tp->selective_acks[]`

![](img/b3f231108facab5be0138b2cfd3f681a_462_0.png)

图 11.36. 按照 DSACK 格式调整的 SACK 块。

如果 TCP 数据按顺序接收，并且该套接字安装了接收器且我们正在用户上下文中处理数据包，则会将 TCP 数据直接复制到用户缓冲区。

TCP 时间戳选项用于在 `tcp_paws_discard()` 中检查 PAWS（保护已序列数）。在 `tcp_replace_ts_recent()` 中应用所有条件后，来自到达段的新时间戳将被较旧的时间戳替换。

进入的 ACK 在 `tcp_ack()` 中被处理。它处理以下内容：

- 用于清理重传队列的确认序列号
- SACK/DSACK 块
- ECE 标志
- 重复 ACK
- 拥塞控制

进入的 SACK/DSACK 在 `tcp_sacktag_write_queue()` 中处理。`tcp_packets_in_flight()` 给出了消耗网络资源的包数量。这是一个简单的计算，即传输的包总数减去离开网络的包数（丢失 + SACK）。

`tcp_clean_rtx_queue()` 从重传队列中移除已确认（ACKED）的段。

`tcp_ack_probe()` 检查拥塞窗口，取决于我们处于慢启动阶段还是拥塞恢复阶段。

`tcp_urg()` 如果处理的段中存在任何 TCP 紧急数据，则对之进行处理。

`tcp_data_queue()` 处理乱序段，并被调用以管理套接字的内存池。

## 444

# TCP 核心处理

应用程序接收数据

应用程序发送数据

![](img/b3f231108facab5be0138b2cfd3f681a_463_0.png)

sk->write_queue

tp->send_head

新的 ACK 确认了数据，使 `tp->snd` 向顺时针方向移动

tp->snd_und

新数据已传输，使 `tp->snd` 向反时针方向移动

数据已在接收队列中。

传输杠杆

minimum(拥塞窗口, 发送窗口)

已确认的数据

处理进入的 ACK。如果新数据被确认，`tp->snd_una` 向顺时针方向移动。如果新的发送窗口和拥塞窗口允许，杠杆向右移动，可以传输新数据。如果感知到拥塞或宣告了零窗口，杠杆向左移动，从而停止新段的传输。

连接 `tp->snd_una` 的段未被确认且超时（拥塞）。我们需要重传此段。传输杠杆向左移动，防止传输新数据。

从网络接口接收到 TCP 包

从网络接口传输段段

图 11.37 TCP 核心处理。

`tcp_data_snd_check()` 传输发送队列中悬挂的且拥塞状态允许的任何数据。这在一个进入的段被完全处理后被调用一次。

`tcp_ack_snd_check()` 如果有任何待处理的 ACK，则发送 ACK。这是在调用 `tcp_data_snd_check()` 时调用的；否则，我们可能会分别发送两个段——ACK 和数据段。

# 12

# TCP 状态处理
