

## 延迟执行

通常，内核代码（尤其是驱动程序）需要一种方法来延迟一段时间的执行，而不使用定时器或下半部机制。这通常是为了给硬件留出时间以完成特定任务。这段时间通常非常短。例如，某网络卡的规范中可能列明改变以太网模式所需时间为两微秒。在设置好所需速度后，驱动程序应至少等待两微秒再继续执行。

内核提供了多种解决方案，具体取决于延迟的语义。这些解决方案具有不同的特性。有些在延迟期间会占用处理器——实际上阻止了任何实质性工作的完成。其他解决方案不占用处理器，但无法保证代码会按精确所需的时间恢复执行。⁶

### 忙等待循环

最简单的实现方案（尽管很少是最优解）是*忙等待*或*忙循环*。这种技术仅在你想要延迟的时间是时钟频率（滴答率）的整数倍，或者精度不重要时有效。

其原理很简单：在循环中自旋，直到经过指定数量的时钟滴答。例如

```c
unsigned long timeout = jiffies + 10;            /* ten ticks */

while (time_before(jiffies, timeout))
    ;
```

循环持续进行，直到`jiffies`大于`delay`，这只有在经过10个时钟滴答后才会发生。在x86架构且HZ等于1,000的情况下，这将导致10毫秒的等待。类似地

```c
unsigned long delay = jiffies + 2*HZ;           /* two seconds */

while (time_before(jiffies, delay))
    ;
```

这将自旋直到经过2*HZ个时钟滴答，无论时钟速率如何，这总是两秒。

这种方式对系统其他部分并不友好。当你的代码等待时，处理器被无意义循环的自旋所占用——没有完成任何有用的工作！你很少希望采用这种笨拙的方法，这里展示它是因为它是一种清晰且简单的延迟执行方式。你也可能在他人不太优雅的代码中遇到它。

更好的解决方案是重新调度你的进程，允许处理器在你的代码等待时完成其他工作：

```c
unsigned long delay = jiffies + 5*HZ;

while (time_before(jiffies, delay))
    cond_resched();
```

`cond_resched()`调用会调度一个新进程，但仅当`need_resched`被设置时才执行。换句话说，该方案仅当存在更重要的任务需要运行时，才有条件地调用调度器。请注意，由于该方法调用了调度器，你无法在中断处理程序中使用它——只能在进程上下文中使用。所有这些方法最好在进程上下文中使用，因为中断处理程序应尽可能快地执行。（而且忙循环无助于实现这一目标！）此外，在持有锁或禁用中断期间，如果可能，应避免以任何方式延迟执行。

C语言爱好者可能会疑惑上述循环有何保证能正常工作。C编译器通常被允许仅执行一次给定的加载操作。通常，并没有保证循环条件语句中的`jiffies`变量在每次迭代中都被重新加载。然而，内核要求`jiffies`在每次迭代中被重新读取，因为其值在别处被递增：即在定时器中断中。事实上，这就是该变量在`<linux/jiffies.h>`中标记为`volatile`的原因。`volatile`关键字指示编译器每次访问变量时都从主存中重新加载，且永不将变量值别名至寄存器，从而保证上述循环按预期完成。

## 短延迟

有时，内核代码（再次，通常是驱动程序）需要短小（小于一个时钟滴答）且相当精确的延迟。这通常是为了与硬件同步，而硬件通常又列出了活动完成的最低时间——通常小于一毫秒。对于如此短的等待，使用基于`jiffies`的延迟（如前例）是不可能的。若定时器中断频率为100Hz，时钟滴答是相当大的10毫秒！即使使用1,000Hz的定时器中断，时钟滴答也仍是一毫秒。显然，对于更小、更精确的延迟需要另一种解决方案。

幸运的是，内核提供了三个分别用于微秒、纳秒和毫秒延迟的函数，定义在`<linux/delay.h>`和`<asm/delay.h>`中，它们不使用`jiffies`：

```c
void udelay(unsigned long usecs);
void ndelay(unsigned long nsecs);
void mdelay(unsigned long msecs);
```

前两个函数通过忙循环延迟执行指定的*微秒*数。最后一个函数延迟执行指定的*毫秒*数。

请记住一秒等于1,000毫秒，而1,000毫秒等于1,000,000微秒。用法很简单：

```c
udelay(150); /* delay for 150 µs */
```

udelay()函数实现为一个知道在给定时间内能执行多少迭代的循环。mdelay()函数则基于udelay()实现。因为内核知道处理器在一秒内能完成多少循环（参见BogoMIPS侧栏），udelay()函数只需将该值缩放为给定延迟所需的正确循环迭代次数。

### 我的BogoMIPS比你的大！

BogoMIPS值一直是混淆和幽默的来源。实际上，BogoMIPS的计算与计算机性能关系不大，主要仅用于udelay()和mdelay()函数。其名称是bogus（即虚假的）和MIPS（百万条指令每秒）的缩写。每个人都熟悉类似以下的启动信息（这是在2.4 GHz的7300系列Intel Xeon处理器上）：

```text
Detected 2400.131 MHz processor.
Calibrating delay loop... 4799.56 BogoMIPS
```

BogoMIPS值是处理器在给定时期内能执行的忙循环迭代次数。实际上，BogoMIPS是衡量处理器能多快地“什么都不做”的指标。该值存储在loops_per_jiffy变量中，并可从/proc/cpuinfo读取。延迟循环函数使用loops_per_jiffy值来计算（相当精确地）需要执行多少次忙循环迭代以提供所需的延迟。

内核在启动时通过init/main.c中的calibrate_delay()计算loops_per_jiffy。

udelay()函数仅应用于小延迟，因为在快速机器上较大的延迟可能导致溢出。作为规则，不要对超过一微秒时长的延迟使用udelay()。对于较长的时长，mdelay()工作得很好。与其他忙等待的延迟执行解决方案类似，这两个函数（尤其是用于长延迟的mdelay()）不应在绝对不需要时使用。请记住，在持有锁或禁用中断时进行忙循环是不礼貌的，因为这会对系统响应和性能产生不利影响。然而，如果你需要精确的延迟，这些调用是你最佳的选择。这些忙等待函数的典型用途是延迟一小段时间，通常在微秒范围内。

## schedule_timeout()

延迟执行更优化的方法是使用schedule_timeout()。该调用将你的任务置于睡眠状态，直到至少经过指定时间。没有保证睡眠时长会精确等于指定时间——只保证时长至少等于指定值。当指定时间经过后，内核唤醒任务并将其放回运行队列。用法很简单：

```c
/* set task's state to interruptible sleep */
set_current_state(TASK_INTERRUPTIBLE);

/* take a nap and wake up in "s" seconds */
schedule_timeout(s * HZ);
```

唯一的参数是以jiffies为单位的期望相对超时时间。此示例将任务置为可中断睡眠s秒。由于任务被标记为`TASK_INTERRUPTIBLE`，若收到信号它会提前唤醒。如果代码不想处理信号，可以使用`TASK_UNINTERRUPTIBLE`代替。在调用`schedule_timeout()`之前，任务必须处于这两种状态之一，否则任务将不会进入睡眠。

请注意，由于`schedule_timeout()`调用调度器，调用它的代码必须能够睡眠。有关原子性和睡眠的讨论参见第8章和第9章。简而言之，你必须处于进程上下文中，且不得持有锁。

## schedule_timeout() 实现

`schedule_timeout()`函数相当直截了当。事实上，它是内核定时器的简单应用，让我们来看看它的代码：

```c
signed long schedule_timeout(signed long timeout)
{
    timer_t timer;
    unsigned long expire;

    switch (timeout) {
    case MAX_SCHEDULE_TIMEOUT:
        schedule();
        goto out;
    default:
        if (timeout < 0)
        {
            printk(KERN_ERR "schedule_timeout: wrong timeout "
                    "value %lx from %p\n", timeout,
                    __builtin_return_address(0));
            current->state = TASK_RUNNING;
            goto out;
        }
    }

    expire = timeout + jiffies;

    init_timer(&timer);
}
```

