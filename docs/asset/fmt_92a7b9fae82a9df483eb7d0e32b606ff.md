
我们收到了对端的最后一个 ACK，因此我们必须发送最后的 ACK 来关闭连接。

```c
case TCP_TW_ACK:
    tcp_v4_timewait_ack(sk, skb);
    break;
```

收一个 FIN，我们通过发送 RST 来重置连接，这在 `no_tcp_socket` 完成。

```c
case TCP_TW_RST:
    goto no_tcp_socket;
```

收到了重复的 ACK 或延迟数据段，因此我们将其丢弃。

```c
case TCP_TW_SUCCESS:
}
goto discard_it;
```

### 10.5.2 TCP 快速预队列处理 (Fast Prequeue Processing)

Linux TCP 有两种包处理路径：“慢”路径和“快”路径。慢路径是标准的输入处理。如第 5 章所述，每个 socket 有两个队列：接收队列和阻塞队列（backlog queue），当接收队列满或 socket 忙时会使用阻塞队列。在慢路径上，TCP 接收到的数据包只有在数据包被验证为包含有序段数据的有效段后，才被放入 socket 的接收队列中。这是一大量的处理，并且全部是在 Linux 的“下半部”（bottom half）上下文，即网络接口函数的范围内。一旦数据包进入队列，socket 将被唤醒，调度器执行用户级任务，该任务从 socket 队列读取数据包。作为慢处理的一部分，当接收队列满或用户级任务被锁时，数据包被放入阻塞队列。

除了慢路径中使用的两个队列外，TCP 还有一个用于预队列（prequeue）的三队列。这第三个队列用于快速处理。由于预计 TCP 需要处理海量数据，Linux 将快速路径作为优化性能的各种加速手段之一。正如我们在第 6 章中看到的，Linux TCP/IP 的重要增强功能之一是头部预测。头部预测算法确定了当 socket 处于 TIME_WAIT 状态时，数据包是否可能是包含数据的有序段 [JACOB93]。如果满足这些条件，该数据包将被选用于快速路径处理。通常情况下，Van Jacobson 算法假设在连接建立期间到达的所有数据包中，有一半是数据段而非 ACK。通过使用头部预测，TCP 的低层接收函数尝试确定哪些数据包符合标准，这些数据包会被立即放入预队列中。当任务被唤醒时，TCP 对预队列中数据包的处理由用户级任务完成，该任务跳过了慢路径中的处理步骤。路径处理发生在对常规队列上任何数据包的正常处理之前。

预队列位于 `linux/include/linux/tcp.h` 中也定义的 `ucopy` 结构中，位于 sock 结构中的 TCP 选项部分。关于基本结构的更多细节，请参第 8 章。`prequeue` 字段包含用于处理的 socket 缓冲区列表。这是接收数据的用户级任务。`iov` 字段指向用户数据数组，`memory` 包含预队列上所有 socket 缓冲器的实际长度。`len` 是预队列上的缓冲区数量。

```c
struct {
    struct sk_buff_head prequeue;
    struct task_struct *task;
    struct iov *iov;
    int memory;
    int len;
} ucopy;
```

`tcp_prequeue_init` 定义在 `linux/include/net/tcp.h` 中，初始化 `ucopy` 结构的元素，包括预队列中的 socket 缓冲区列表。每当为 AF_INET 地址打开 SOCK_STREAM 类型的 socket 时，就会作为函数 `tcp_v4_init_sock` 初始化 socket 状态信息的一部分发生这种初始化。

```c
static __inline__ void tcp_prequeue_init(struct tcp_opt *tp)
{
    tp->ucopy.task = NULL;
    tp->ucopy.len = 0;
    tp->ucopy.memory = 0;
    skb_queue_head_init(&tp->ucopy.prequeue);
}
```

`tcp_prequeue` 是将 socket 缓冲区放入队列的函数，也定义在 `linux/include/net/tcp.h` 中。只有当当前有用户等待 socket 时，它才会队列缓冲区。这通过 `ucopy` 结构中 `task` 字段的非空值表示。当 socket 被唤醒时，应用程序对 socket 执行读取操作，`tcp_prequeue` 在通过系统调用“正式”调用 socket 的接收函数之前，会立即处理 socket 的预队列。

```c
static __inline__ int tcp_prequeue(struct sock *sk, struct sk_buff *skb)
{}
```

`tp` 是 TCP 选项结构，从 socket 中获取。

```c
struct tcp_opt *tp = &sk->tp_info.af_tcp;
```

在这里我们检查当前是否有用户在等待 socket。如果是，我们将该段放入预队列。如果不是，我们将该段放入预队列。

```c
if (tp->ucopy.task) {
    skb_queue_tail(&tp->ucopy.prequeue, skb);
    tp->ucopy.memory += skb->len;
}
```

如果内存大于 socket 的接收缓冲区，缓冲区将从预队列移除并放入阻塞队列。

```c
if (tp->ucopy.memory > sk->rcbuf) {
    struct sk_buff *sk1;
    while ((sk1 = skb_dequeue(&tp->ucopy.prequeue)) != NULL) {
        tcp_rcv(sk1);
        NET_INC_STATS(TCPDropped);
    }
    tp->ucopy.memory = 0;
}
```

当预队列中只有一个 skb 时，socket 被唤醒。回顾第 8 章 8.4 节关于延迟确认的内容，我们讨论了如何在数据段上奇载 ACK。

```c
} else if (skb_queue_len(&tp->ucopy.prequeue) == 1) {
    wake_up_interruptible(sk);
    if (!tcp_ack_scheduled(tp))
        tcp_reset_timer(sk, TCP_DACK, (3*RTO_MIN)/4);
}
return 1;
return 0;
```

### 10.5.3 TCP 阻塞队列处理 (Backlog Queue Processing)

`tcp_v4_rcv` 函数是 TCP 的阻塞接收函数。它设置在 `net/ipv4/tcp_ipv4.c` 中 proto 结构的 `backlog_rcv` 字段中。当 socket 无法在接收队列上更多数据时，调用 `tcp_v4_rcv`。

```c
int tcp_v4_rcv(struct sock *sk, struct sk_buff *skb)
{
```

首先，我们检查是否处于 ESTABLISHED 状态。如果是，sk 是快速路径处理的候选。调用 `tcp_rcv_established` 来处理 ESTABLISHED 状态下的输入包。它通过头部检查确定 sk 是否可以在快速路径处理。`tcp_rcv_established` 在我们需要向对端重置时返回一个，在成功处理数据包时返回零。

```c
if (sk->state == ESTABLISHED) {
    TCP_CHECK_TIMER(sk);
    if (tcp_rcv_established(sk, skb, sk->h->th, sk->len))
        goto reset;
    TCP_CHECK_TIMER(sk);
    return 0;
}
```

如果内存大于 socket 的接收缓冲区，缓冲区将从预队列移除并放入阻塞队列。内存字段被重置。

```c
if (tp->ucopy.memory > sk->rcbuf) {
    struct sk_buff *sk1;
    while ((sk1 = skb_dequeue(&tp->ucopy.prequeue)) != NULL) {
        tcp_rcv(sk1);
        NET_INC_STATS(TCPDropped);
    }
    tp->ucopy.memory = 0;
}
```

当预队列中只有一个 skb 时，socket 被唤醒。回顾第 8 章 8.4 节关于延迟确认的内容，我们讨论了 ACK 如何奇载在数据段上。

```c
```
