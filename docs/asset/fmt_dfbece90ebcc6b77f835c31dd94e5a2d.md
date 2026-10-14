
发送端 TCP 发送一个数据段并等待发送数据的 ACK。数据传输速率随着接收到的 ACK 呈指数级增长，因为拥塞窗口在慢启动阶段呈指数级增长。我们不断增加数据传输速率，直到利用整个网络容量使网络饱和。进一步增加传输速率时，我们可能会看到其中一个中间路由器丢弃数据包，因为它无法处理它。在理想情况下，这会导致窗口内传输的所有包被丢弃，因为它们都是在第一行传输的。当 TCP 没有收到当前窗口内传输的首个段的 ACK 且超时时，它就会知道丢失。在这种情况下，我们需要开始重传丢失的段，并减慢数据传输速率。

上述是拥塞的示例之一。在不同的情况下，我们可以感知到拥塞。我们可以及早检测拥塞的算法之一是快速恢复和快速重传。通过这种算法，我们可以通过计算重复 ACK 来通过经验发现更多问题。

使用 IP 头部中的 `ECN`（显式拥塞通知）位，其中一个中间路由器可以告诉接收端 TCP 它所遭遇的拥塞。这是路由器提前通知 TCP 拥塞的主动方法。接收端 TCP 通过在 TCP 头部中设置 `ECE` 标志向发送端发送拥塞通知。这样，发送端 TCP 降低了数据传输速率，可以避免我们因路由器拥塞导致的丢包而产生损失。

设计了一些智能算法，用于检测 `(a)` 快速重传和快速恢复以及 `(b)` `RTO` 情况下的虚假重传。带有

`TCP/IP Architecture, Design, and Implementation in Linux.` By `S. Seth` and `M. A. Venkatesulu`

`Copyright © 2008 the IEEE Computer Society`

`445`

在这些算法的帮助下，当我们进入丢失状态（包在网络中延迟或 ACK 丢失）时，我们可以获得更好的网络性能。

在本章中，我们将学习 TCP 拥塞状态的处理。我们将看到在什么条件下进入和退出 TCP 拥塞状态。然后我们还将学习如何在拥塞状态下控制数据传输和重传。完整的拥塞控制实现在 `tcp_fasttrans_alert()` 中。我们将大纲分为不同的部分：

- `TCP` 状态中的处理
- 退出拥塞状态的处理

# 12.1 状态处理概览

（除非另有说明，参见 12.1）

让我们从 `tcp_fasttrans_alert()` 开始。我们在接收到 ACK 后在 `tcp_ack()` 中调用此例程，在处理完 ACK 和 SACK 段后仅当 ACK 可疑时才调用。这简单来说意味着我们是第一次感知到拥塞，或者处理已处于拥塞状态（`OPEN` 状态外）。我们实现了以下内容：

1. 虚假重传
2. 从不同的拥塞状态恢复
3. 由于数据包传输延迟感知到的虚假拥塞状态
4. 回到打开 状态

只有当该段的 ACK 号与之前确认的序列号相同，且该段没有设置任何 `FLAG_NOT_DUP` 标志时，我们将该段标记为重复（第1494行）（见第 11.4 节）。在处理 TCP 状态之前，我们需要完成准备工作。基于重复 ACK 的 SACK 段。在支持 SACK 的情况下，一旦 SACK 段被确认，我们就计算 SACK 计数。但在不支持 SACK 的情况下……

无论处于何种状态，如果正准备从非打开状态进入，我们可能会更新 SACK 计数。

## TCP 处理概览

`net/ipv4/tcp_input.c`

```c
1489 static void
1490 tcp_fasttrans_alert(struct tcp *sk, u32 prio_of_una,
                     int pracks, int flag)
1492                 struct tcp_cp *tp = &(sk->tp);
1493     is_dup = (tp->snd_una == pracks && !flag&FLAG_DUP);
1494 if (tp->sacked_out)
1498     tp->sacked_out = 0;
1500     /* 2. 在不准确的情况下处理 sfack 计数。 */
1501     if (tp->sacked_out == 0)
1502         tp->facks_out = 0;
1503     ...
1506     if (flag&FLAG_ECE)
1507         tp->prio_sstresh = 0;
1508
1509     /* B. 在所有情况下检查更新的 SACK。 */
1510     if (tp->sacked_out && check_sack_renew(sk, tp))
1511         return;
1512
1513     /* C. 如果有效，则处理丢失通知。 */
1514     if ((flag&FLAG_DATA_LOST) &&
1515         before(tp->snd_una, tp->high_seq) &&
1516         tp->state == TCP_CA_Ordering &&
1517         tp->facked_out > tp->high_seq)
1518             tcp_mark_head_loss(sk, tp, tp->facked_out-tp->high_seq);
1519             NET_INC_SACK_BH(TCPloss);
1520     )
1521     /* D. 同步 left_out。 */
1522     tcp_sync_left_out(tp);
```
