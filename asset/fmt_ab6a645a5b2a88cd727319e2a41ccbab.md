
这会花费大量时间且延迟会过高。当从底半部（bottom-half）处理程序调用时，它将变成递归并可能导致内核栈溢出。它使用宏 `softirq_pending` 来检查 CPU 上是否有任何待处理的 softIRQ（见 cs 17.9，第 73 行）。如果有待处理的 softIRQ，我们会在本地复制代表活跃 softIRQ 的位图，并开始逐个处理它们（见 cs 17.9，第 88–93 行）。在处理完所有 softIRQ 后，我们会检查在处理活跃 softIRQ 期间，是否又触发了任何（除了刚刚处理过的之外）softIRQ（cs 17.9，第 97–101 行）。如果是，且触发的 softIRQ 已经是正在处理的那些一个，我们将它们调度在稍后的某个时间点由 `softirqd` 守护进程处理，因为我们不希望在驱动内核路径和消耗 CPU 资源时长时间阻塞在这里（cs 17.9，第 104–105 行）。有两个将使用的局部变量：

让我们看看这是如何实现的。

- `Pending`
- `Mask`

`Pending` 存储所有当前活跃的 softIRQ 的位模式，而 `mask` 只是 `pending` 的补码。现在，在开始执行已触发 softIRQ 的 softIRQ 处理程序之前，我们已经 `pending` 和 `mask` 变量初始化为适当的值，并且 `irq_stat[cpu]...softirq_pending` 被设置为零。我们检查 `pending` 中的所有位，直到它处理完所有 softIRQ。我们通过在每次迭代中将 `pending` 左移 1 位来实现此操作（cs 17.9，第 92 行）。我们继续循环，直到 `pending` 不为零。

一旦我们处理完所有 softIRQ，我们再次检查在此期间是否又触发了任何 softIRQ（cs 17.9，第 97 行）。我们需要检查新的 softIRQ 是否是刚才未处理的那些中的之一。因为 `mask` 已将所有已处理的 softIRQ 的位都置零了。如果 `mask & pending` 的结果为正数，则只有当触发了任何确实未被处理的 softIRQ 时如此（cs 17.9，第 88–93 行）。在这种情况下，我们再次进入循环（cs 17.9，第 88–93 行）。否则，如果我们有待处理的 IRQ（`pending > 0`），则它是已处理的之一。在这种情况下，我们唤醒该 CPU 的 `softirqd` 以供用户态应用程序共享，因为内核是非抢占的。softIRQ 完成所需的时间比 IRQ 长。如果中断的频率更高，我们将花费更多时间在 softIRQ 处理上。

我们通过调用 `local_irq_save()` 和 `local_irq_disable()` 禁用本地 CPU 的 IRQ 来操作 `irq_stat[cpu]...softirq_pending`（见 cs 17.9 第 71 行和第 95 行）。在操作之后，我们通过调用 `local_irq_enable()` 和 `local_irq_restore()` 启用本地 CPU 的 IRQ（见 cs 17.9 第 84 和第 100 行）。我们这样做是因为 `irq_stat[cpu]...softirq_pending` 在中断处理程序中会被修改。

我们通过调用 `local_bh_disable()` 在禁用底半部的情况下处理 softIRQ（见 cs 17.9，第 79 行）。这会让 `irq_stat[cpu]_local_bh_count` 加 1。我们这样做是因为此 CPU 上的其他内核控制路径不能够处理 softIRQ。有一种方法可以处理这种情况。例如，一个内核控制路径正在执行 `do_softirq()`，触发了中断。中断被处理，而在从 `do_IRQ()` 中断时，如果有任何待处理的 softIRQ，我们可能会调用 `do_softirq()`（参考 cs 17.10，第 654 和 655 行）。

如果在 `do_softirq()` 中处理 softIRQ 时禁用底半部，我们就确保了它在从 `do_IRQ()` 返回时不会执行。即使在从 `do_IRQ()` 返回时进入了 `in_softirq()`，它也不会继续执行，因为 `in_interrupt()` 将始终返回正值。

`do_softirq()` 在以下情况下被调用：

- 在 `do_IRQ()` 的中断处理中返回时（cs 17.10）。我们刚刚从中断例程返回，很有可能触发了某些 softIRQ，因为大部分中断工作现在都在实现为 softIRQ 的底半部完成了。这就是我们检查的原因。可能存在某些 softIRQ

# NET SoftIRQ

`arch/i386/kernel/irq.c`

```c
asmlinkage unsigned int do_IRQ(struct pt_regs *regs)
    if (softirq_pending(cpu))
        do_softirq();
    return 1;
}
```

cs 17.10, `do_IRQ`。我们刚刚从中断例程返回，很有可能触发了某些 softIRQ，因为大部分中断工作现在都在实现为 softIRQ 的底半部完成了。这就是我们检查的原因。可能存在某些 softIRQ

## 17.3 SOFTIRQS 的注册

每个 softIRQ 都与 `irq_stat[cpu].softirq_pending` 关联。在当前设计中，`struct softirq_action` 代表 softIRQ。`softirq_action` 有两个字段：`action` 和 `data`。我们有一个 `struct softirq_action` 数组，名为 `softirq_vec`，每个元素对应一个 softIRQ。根据 17.20，`softirq_vec` 对应位。在这种设计下，我们在处理时不需要搜索 softIRQ。我们只需要遍历 `pending` 位并检查位是否被设置。

```c
// include/interrupt.h
struct softirq_action
{
    void (*action)(struct softirq_action);
    void *data;
};
```

cs 17.11, `softirq_action`.

```c
// include/interrupt.h
static struct softirq_vec[32] __cachelinealigned;
```

cs 17.12, `softirq_vec`.

```c
// kernel/softirq.c
void open_softirq(int nr, void (*action)(struct softirq_action), void *data)
 {
    softirq_vec[nr].data = data;
    softirq_vec[nr].action = action;
 }
```

cs 17.13, `open_softirq()`.

```c
// net/core/dev.c
__init net_dev_init(void)
 {
   ...
   open_softirq(NET_TX_SOFTIRQ, net_tx_action, NULL);
   open_softirq(NET_RX_SOFTIRQ, net_rx_action, NULL);
   ...
 }
```

cs 17.14, `net_dev_init()`.

## 17.4 通过 Rx SoftIRQ 进行数据包接收和延迟处理

当数据帧在网络接口的 DMA 缓冲区中完全接收时，设备的 Rx 中断会被触发。Rx 处理程序的工作是从 Rx 缓冲区中提取数据帧并将其发送到上层进行处理。Rx

# 680

# NET SoftIRQ

![](img/b3f231108facab5be0138b2cfd3f681a_695_0.png)

通过调用 `netif_rx_schedule()` 在当前 CPU 上产生 Rx 软中断（`NET_RX_SOFTIRQ`）。这是为了对接收到的数据包进行延迟处理。

如果队列未满，则将新帧队列到 CPU 的网络队列 `softnet_data[this_cpu]->input_pkt_queue` 中。

Rx 中断处理程序从设备的 DMA 缓冲区中取出帧，并通过调用 `netif_rx()` 将其发送到上层。

一旦完整帧传输到 DMA 缓冲区，就为该设备生成 Rx 中断。

在设备的 DMA 缓冲区中执行帧的 DMA 传输。

图 17.3. 使用 softirq 框架处理数据包的过程。
