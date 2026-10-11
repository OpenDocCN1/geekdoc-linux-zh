
```c
my_card_setup_receive_buffer(struct my_card *cp, char *buffer, int len)
{
    dma_addr_t mapping;

    mapping = pci_map_single(cp->pdev, buffer, len, PCI_DMA_FROMDEVICE);
    cp->rx_buf = buffer;
    cp->rx_len = len;
    cp->rx_dma = mapping;
    give_rx_buf_to_card(cp);
}

...

my_card_interrupt_handler(int irq, void *devid, struct pt_regs *regs)
{
    struct my_card *cp = devid;
    ...
    if (read_card_status(cp) == RX_BUF_TRANSFERRED) {
        struct my_card_header *hp;

        /* 检查头部以查看我们是否希望
        * 接受数据。但首先要同步
        * DMA 传输与 CPU，
        * 以便我们看到更新的内容。
        */
        pci_dma_sync_single(cp->pdev, cp->rx_buf, cp->rx_len,
                           PCI_DMA_FROMDEVICE);

        /* 现在检查缓冲区是安全的。 */
        hp = (struct my_card_header *) cp->rx_buf;
        if (header_is_ok(hp)) {
            pci_unmap_single(cp->pdev, cp->rx_buf, cp->rx_len,
                            PCI_DMA_FROMDEVICE);
            pass_to_upper_layers(cp->rx_buf);
            make_and_setup_new_rx_buf(cp);
        } else {
            /* 只需将缓冲区交还给卡。 */
            // ...
        }
    }
}
```

已经完全转换到该接口的驱动程序不应再使用`virt_to_bus`，也不应使用`bus_to_virt`。由于动态 DMA 映射方案中不再有`bus_to_virt`的等效物，某些驱动程序需要进行少量修改；您必须始终将`pci_alloc_consistent`和`pci_map_single`调用返回的 DMA 地址（如果平台在硬件中支持动态 DMA 映射，`pci_map_sg`会将它们存储在分散列表本身中）保存在您的驱动程序结构体中，以及/或者在卡寄存器中。

## 中断处理

对于操作系统开发人员来说，中断是生活中重大且不愉快的事实。在编写中断处理代码时必须极其小心。在这里，对运行系统动态的完整而深刻的理解至关重要，或许比代码中的其他任何地方都更重要。它们丑陋、复杂，并且真的应该由硬件或某处隐藏起来，以免打扰操作系统开发人员。由于这不可能，操作系统开发人员所能做的最好事情就是将中断处理例程深藏在内核的深处，使得内核的其他任何部分都不必处理中断。这正是 Linux 内核所做的。

例如，Linux 设备驱动程序并不了解中断的概念；它们只是发出 I/O 请求，并让内核去处理由该 I/O 操作产生的中断。

作为一个很好的例子，查看定时器中断处理程序的源代码很有帮助。`定时器`就像你床边的闹钟。它被设置为一个微秒级的时间值，当该值倒计时归零时返回。

内核定时器中断处理程序是位于`kernel/timer.c`中的`do_timer()`：

```c
void do_timer(struct pt_regs * regs)
{
	(*(unsigned long *)&jiffies)++;
	lost_ticks++;
	mark_bh(TIMER_BH);
	if (!user_mode(regs))
		lost_ticks_system++;
	if (tq_timer)
		mark_bh(TQUEUE_BH);
}
```

这段代码首先将全局`jiffies`变量增加一，然后标记相应的定时器`下半部分处理程序`（bottom-half handler）以便运行。`Jiffie`是 Linux 中对执行单位的名词。在 IA32 (i386) 机器上，它通常是 10 毫秒。下半部分处理程序在 IRQ 例程返回后立即运行。下半部分处理程序是特殊的`软中断例程`，类似于 NT 的（延迟过程调用 DPC$^{4}$）概念。

定时器中断还处理`丢失的中断`。例如，如果定时器下半部分执行时间过长（例如，因为有非常高的中断负载到达系统），可能会出现新的定时器中断在定时器下半部分完成执行之前到达的情况。这在较快的机器上不会发生，但在较慢的系统上这是一种必须考虑的可能性。

定时器下半部分处理程序是实际执行时间和定时器处理任务的地方。函数`timer_bh()`实际上运行所有内核定时器及其回调函数：

```c
void timer_bh(void)
{
    update_times();
    run_old_timers();
    run_timer_list();
}
```

`update_times()`处理日时间计算、系统负载计算以及每个进程的时间和处理器使用率统计。

代码片段`run_old_timers()`只是古老的 Linux 代码；它可能会在 2.5 版本中被移除。它是一个简单的定时器实现，仍在少数地方使用。

实际的 Linux 定时器代码位于`run_timer_list()`中。

Linux 定时器具有高度可扩展性。在繁忙的互联网服务器上，可以同时运行超过 100,000 个定时器。Linux 定时器实现是一个非常巧妙的技巧，由 Arne Gangstad 编写，也被专有操作系统厂商复制。该技巧在于保持`指数`超时值，而不是`绝对`超时值。其实现代码位于定时器向量（kernel/timer.c）中，如下所示：

```c
struct timer_vec {
  int index;
  struct timer_list *vec[TVN_SIZE];
};

struct timer_vec_root {
  int index;
  struct timer_list *vec[TVR_SIZE];
};

static struct timer_vec tv5 = { 0 };
static struct timer_vec tv4 = { 0 };
static struct timer_vec tv3 = { 0 };
static struct timer_vec tv2 = { 0 };
static struct timer_vec_root tv1 = { 0 };
```

每个定时器向量都是定时器环形列表的数组。定时器根据相对于当前时间的超时值进行排序。短期定时器被放入`tv1`，具有较大超时的定时器被放入`tv2`、`tv3`等。定时器向量的寻址是指数的：超时值被划分为位段，最高阶非零位段显示使用哪个定时器向量。

现在到了精彩的部分。在每次定时器中断时，所有定时器都必须推进，因为它们的超时值减 1。显然，我们不想对比如说 100,000 个定时器都这样做，因此使用了以下技巧。定时器向量有一个当前指针（`index`），如果前一个时间向量溢出，则它增加 1。也就是说，`tv1`的索引从 0 推进到 255；一旦达到 256，我们将`tv2`推进 1，并将`tv1`的索引设置为 0。如果`tv2`溢出到 64，则`tv3`推进 1，且`tv2`索引设置为零。如果`tv3`溢出到 64，则`tv4`推进，以此类推。如您所见，`tv1`索引在每次定时器滴答（`jiffy`）时增加，`tv2`索引每 256 次滴答增加，`tv3`索引每 256×64 次滴答增加，`tv4`索引每 256×64×64 次滴答增加，以此类推。短期定时器非常常见，因此`tv1`被增加以容纳 256 个定时器列表项。

此外，如果当前索引（刚刚增加的那个）有一个非零项，则该项必须“过期”：
