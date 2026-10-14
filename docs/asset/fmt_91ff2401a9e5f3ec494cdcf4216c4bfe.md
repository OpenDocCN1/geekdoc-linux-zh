
> 图 18.20 向后兼容

- 689 此函数通过更改参数顺序和 `priv` 的类型（从 `int` 为 `void`）升级了 `send_sig()`。如果 `priv` 为 0，意味着信号从用户模式发送，则 `(priv != 0)` 结果为假 (0)，并作为 `void` 指针返回。对于 `priv` 的任何其他值（内核模式），返回 1。`send_sig_info()` 函数在第 18.1.1 节中描述。
- 695 生成了一个新参数，强制转换为 `void` 指针。这意味着信号是从内核的某处发送的。`force_sig_info()` 函数在第 18.2.1 节中描述。
- 701 `priv` 参数从 `int` 转换为 `void` 指针，如第 689 行所示。`kill_pgid_info()` 函数在第 18.2.2 节中描述。
- 705 `sess` 参数标识一个会话。信号将发送给该会话的首目。
- 707 此更改了参数顺序并转换了 `priv`，如第 689 行所示。`kill_sl_info()` 函数在第 18.2.3 节中描述。
- 713 此更改了参数顺序并转换了 `priv`，如第 689 行所示。`kill_proc_info()` 函数在第 18.2.4 节中描述。

## 18.3. 挂起信号

之前的章节检查了信号是如何发送到进程的。在 `send_sig_info()` 函数运行后，代表目标进程的数据结构反映了信号已发送给该进程的事实。内核在某个特定点检查这些数据结构——系统调用的返回路径。在那个阶段，它安排进程采取任何适当的操作。该机制的设计是本章剩余部分的主题。我们首先检查检查信号是否挂起给某个进程的函数。

### 18.3.1 检查 `sigpending` 字段

当信号挂起给某个进程时，其任务中的 `sigpending` 字段被设置为 1。见第 18.3.2 节。图 18.21 所示的由 `<linux/sched.h>` 的简单函数检查指定进程的此字段并返回真或假。

```c
static inline signal_pending(struct task_struct *p)
{
  return (p->sigpending != 0);
}
```

图 18.21 检查 sigpending 字段

### 18.3.2 设置 `sigpending` 字段

图 18.22 显示的函数来自 `<linux/sched.h>` 设置了 `sigpending` 字段的值。每当阻塞位图（blocked bitmap）变化时，都需要重新评估。所有调用者都应该持有 `sigmask_lock`。

```c
static inline void recalc_sigpending(struct task_struct *t)
{
  t->sigpending = has_pending_signals(&t->pending.signal, &t->blocked);
}
```

图 18.22 评估进程的信号状态

因此它只是提取出信号和阻塞字段并将它们传递给 `has_pending_signals()`（见第 18.3.3 节）。`sigpending` 字段根据该函数返回的值（`TRUE` 或 `FALSE`）设置。

### 18.3.3 重新计算信号状态

图 18.23 显示的函数来自 `<linux/sched.h>`，根据待处理信号和阻塞信号的集合重新计算进程的信号状态。

```c
static inline int has_pending_signals(sigset_t *signal, sigset_t *blocked)
{
  unsigned long ready;
  long i;

  switch (_NSIG_WORDS) {
    default:
      for (i=_NSIG_WORDS, ready=0; i>= 0; )
        ready |= signal->sig[i] & ~blocked->sig[i];
      break;

    case 4: 
      ready= signal->sig[3] & ~blocked->sig[3];
      ready |= signal->sig[2] & ~blocked->sig[2];
      ready |= signal->sig[1] & ~blocked->sig[1];
      ready |= signal->sig[0] & ~blocked->sig[0];
      break;

    case 2: 
      ready=signal->sig[1] & blocked->sig[1];
      ready |= signal->sig[0] & blocked->sig[0];
      break;

    case 1: 
      ready=signal->sig[0] & blocked->sig[0];
      break;
  }
  return ready != 0;
}
```

图 18.23 重新计算待处理状态

- 第一个参数指向待处理信号位图的指针；第二个参数指向阻塞信号位图的指针（两者都在进程的 `task_struct` 中）。

- 646–663：由于这些位图在不同架构上的长度可能不同，因此对一个、两个或多个字（words）采取了单独的处理。

- 647–650：这是为了非常长的信号掩码，大于四个字。

- 648：循环的每次迭代都会检查位图中的一个 `unsigned long` 掩码。注意 `ready` 的初始化只执行一次；它是 `for` 循环初始化的一部分。

- 649：`signal` 当前元素中设置位而在 `blocked` 对应元素中被清除的任何位都会设置在 `ready` 中。循环的连续迭代中同一个位可能会在 `ready` 中被多次设置，但这并不重要——该函数只检查 `signal` 中是否存在未掩码的位。

- 652–656：对于四字信号掩码，这段代码比在之前的情况下使用 `long` 更快。每一行检查位图中的一个字，并在 `ready` 中设置任何相关位。与之前一样，这可能意味着某些位被多次设置。

- 658–659：这是针对双字情况经过优化的，例如 i386 架构。

- 662：这适用于仅使用 `unsigned long` 位图的架构。

- 664：如果 `ready` 中设置了一个位，则返回 `TRUE`；否则返回 `FALSE`。

## 18.4 递送待处理信号

待处理信号实际上是在系统服务调用返回路径上处理的（见第 10.6.3 节），该路径将控制权交给 `arch/i386/kernel/signal.c` 中的 `do_signal()` 函数。该例程执行一些初步检查和丢弃。当它找到需要处理的信号时，会将其传递给 `handle_signal()`，见第 19.1 节。所有这些都是特定于架构的代码。本节描述了 `do_signal()`。由于它是一个很长的函数，讨论将分为几个功能部分。

### 18.4.1 识别待处理信号

图 18.24 显示了 `do_signal()` 函数的开头。基本上，它所做的只是从队列中取出第一个信号。

```c
int do_signal(struct pt_regs *regs, sigset_t *oldset)
{
    siginfo_t tinfo;
    struct k_sigaction *ka;

    if ((regs->xcs & 3) != 3)
        return 1;

    if (oldset)
        oldset = &current->blocked;

    for (;;) {
        unsigned long signr;

        spin_lock(&current->sigmask_lock);
        signr = dequeue_signal(current->blocked, &info);
        spin_unlock(&current->sigmask_lock);

        if (!signr)
            break;
```

图 18.24 识别待处理信号

- 参数是进入内核时保存的待处理信号位图的指针，以及当前进程阻塞集合的指针。

- 这通常从中断路径被调用。它在检查中断发生时进程是否运行在用户模式。`pt_regs` 字段中的两个低位表示权限级别。如果这两个位都设置了，则说明中断发生时进程运行在用户模式。

- 如果中断发生时进程运行在内核模式，则不处理信号。此函数返回 1 表示操作成功（未遇到错误）。

- 如果 `oldset` 参数传递的是 `NULL` 指针，则使用当前进程的位图。这本就应该是这样使用的。

- 这开始了一个无限循环，跳转到该行（见图 18.24 到 18.28）。每次循环处理一个信号。有时信号由于某种原因被忽略，使用 `continue` 发生短路循环。如果没有进一步的队列信号，则在某处跳出循环。如果找到了需要处理的信号，我们进行处理并从函数返回。
