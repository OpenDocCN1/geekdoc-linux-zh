
## 注册你的处理程序

接下来，softirq 处理程序在运行时通过 `open_softirq()` 进行注册，该函数接收两个参数：softirq 的索引及其处理函数。例如，网络子系统在 `net/core/dev.c` 中这样注册其 softirqs：

```c
open_softirq(NET_TX_SOFTIRQ, net_tx_action);
open_softirq(NET_RX_SOFTIRQ, net_rx_action);
```

Softirq 处理程序在中断启用的情况下运行，并且不能睡眠。当处理程序运行时，当前处理器上的 softirq 会被禁用。然而，另一个处理器可以执行其他的 softirq。如果在某个 softirq 执行期间再次被触发，另一个处理器可以同时运行它。这意味着任何共享数据——即使仅用于 softirq 处理程序内部的全局数据——也需要适当的锁定（如下一章和下一章中讨论的那样）。这是一个重要的点，也是任务单元（tasklets）通常更受欢迎的原因。仅仅防止你的 softirqs 并发运行并不是理想的。如果一个 softirq 获取了一个锁以防止另一个实例同时运行，那么就没有理由使用 softirq 了。因此，大多数 softirq 处理程序采用每处理器数据（每个处理器独有的数据，因此不需要锁定）和其他技巧来避免显式锁定并提供出色的可扩展性。

Softirqs 的*根本目的*是**可扩展性**。如果你不需要扩展到无限多的处理器，那么请**使用**一个任务单元。任务单元本质上是一种 softirq，其中同一个处理程序的多个实例无法在多个处理器上并发运行。

## 触发你的 Softirq

在处理程序被添加到枚举列表并通过 `open_softirq()` 注册后，它就可以运行了。为了标记其待处理状态，以便在 `do_softirq()` 的下一次调用时运行它，调用 `raise_softirq()`。例如，网络子系统将调用 `raise_softirq(NET_TX_SOFTIRQ);`

这将触发 `NET_TX_SOFTIRQ` softirq。其处理程序 `net_tx_action()` 将在内核下次执行 softirqs 时运行。该函数在真正触发 softirq 之前禁用中断，然后将其恢复为之前的状态。如果中断已经关闭，可以使用函数 `raise_softirq_irqoff()` 作为一个小的优化。例如：

```c
/*
 * 中断必须已经关闭！
 */
raise_softirq_irqoff(NET_TX_SOFTIRQ);
```

Softirqs 通常是在中断处理程序内部触发的。在中断处理程序的情况下，中断处理程序执行基本的硬件相关工作，触发 softirq，然后退出。在处理中断时，内核调用 `do_softirq()`。然后 softirq 运行并从中断处理程序停止的地方继续执行。在这个例子中，“上半部”和“下半部”的命名应该变得有意义了。

# 任务单元（Tasklets）

任务单元是建立在 softirqs 之上的下半部机制。如前所述，它们与任务（tasks）没有任何关系。任务单元在性质和行为上与 softirqs 相似；然而，它们具有更简单的接口和更宽松的锁定规则。

作为设备驱动程序作者，决定是否使用 softirqs 还是任务单元很简单：你几乎总是希望使用任务单元。正如我们在上一节中看到的那样，你几乎可以用一只手的指头数出 softirqs 的用户数量。Softirqs 仅用于**高频**和**高度多线程**的使用场景。另一方面，任务单元被**大量使用**。任务单元在绝大多数情况下表现良好，并且非常容易使用。

## 实现任务单元

由于任务单元建立在 softirqs 之上，它们*就是* softirqs。如前所述，任务单元由两个 softirqs 表示：`HI_SOFTIRQ` 和 `TASKLET_SOFTIRQ`。这些类型之间的唯一区别是，基于 `HI_SOFTIRQ` 的任务单元优先于基于 `TASKLET_SOFTIRQ` 的任务单元运行。

## 任务单元结构体

任务单元由 `tasklet_struct` 结构体表示。每个结构体表示一个唯一的任务单元。该结构体在 `<linux/interrupt.h>` 中声明：

```c
struct tasklet_struct {
  struct tasklet_struct *next;    /* 列表中的下一个任务单元 */
  unsigned long state;            /* 任务单元的状态 */
  atomic_t count;                /* 引用计数器 */
  void (*func)(unsigned long);   /* 任务单元处理函数 */
  unsigned long data;            /* 传递给任务单元函数的参数 */
};
```

`func` 成员是任务单元处理程序（相当于 softirq 的 `action`），并接收 `data` 作为其唯一参数。

`state` 成员恰好是 `zero`、`TASKLET_STATE_SCHED` 或 `TASKLET_STATE_RUN`。`TASKLET_STATE_SCHED` 表示已调度运行但尚未执行的任务单元，而 `TASKLET_STATE_RUN` 表示正在运行的任务单元。作为一种优化，`TASKLET_STATE_RUN` 仅用于多处理器机器，因为单处理器机器总是知道任务单元是否正在运行。（它要么是当前正在执行的代码，要么不是。）

`count` 字段用作任务单元的引用计数。如果它不为零，任务单元被禁用且无法运行；如果为零，任务单元被启用，如果标记为待处理则可以运行。

## 调度任务单元

已调度的任务单元（相当于已触发的 softirqs[^5]）存储在两个每处理器结构中：`tasklet_vec`（用于常规任务单元）和 `tasklet_hi_vec`（用于高优先级任务单元）。这两个结构都是 `tasklet_struct` 结构体的链表。列表中的每个 `tasklet_struct` 结构体代表一个不同的任务单元。

任务单元通过 `tasklet_schedule()` 和 `tasklet_hi_schedule()` 函数进行调度，这些函数将任务单元的 `tasklet_struct` 指针作为其唯一参数。每个函数确保提供的任务单元尚未被调度，然后适当调用 `__tasklet_schedule()` 和 `__tasklet_hi_schedule()`。这两个函数是相似的。（区别在于一个使用 `TASKLET_SOFTIRQ`，另一个使用 `HI_SOFTIRQ`。）下一节将介绍任务单元的编写和使用。现在，让我们看看 `tasklet_schedule()` 执行的步骤：

-   1. 检查任务单元的 `state` 是否为 `TASKLET_STATE_SCHED`。如果是，则任务单元已被调度运行，该函数可以立即返回。
-   2. 调用 `__tasklet_schedule()`。
-   3. 保存中断系统的状态，然后禁用本地中断。这确保在 `tasklet_schedule()` 操作任务单元时，此处理器上的任何进程不会干扰任务单元代码。
-   4. 将待调度的任务单元添加到 `tasklet_vec` 或 `tasklet_hi_vec` 链表的头部，该链表对系统中的每个处理器都是唯一的。
-   5. 触发 `TASKLET_SOFTIRQ` 或 `HI_SOFTIRQ` softirq，以便 `do_softirq()` 在近期执行此任务单元。
-   6. 将中断恢复为之前的状态并返回。

在最合适的时机，`do_softirq()` 如前节所述被执行。由于大多数任务单元和 softirqs 在中断处理程序中被标记为待处理，`do_softirq()` 很可能在最后一个中断返回时运行。由于现在 `TASKLET_SOFTIRQ` 或 `HI_SOFTIRQ` 已被触发，`do_softirq()` 执行相关的处理程序。这些处理程序，`tasklet_action()` 和 `tasklet_hi_action()`，是任务单元处理的核心。让我们看看这些处理程序执行的步骤：

-   1. 禁用本地中断递送（这里无需先保存其状态，因为代码在此处始终作为 softirq 处理程序被调用，且中断始终处于启用状态）并检索此处理器的 `tasklet_vec` 或 `tasklet_hi_vec` 列表。
-   2. 通过将列表设置为 `NULL` 来清除此处理器的列表。
-   3. 启用本地中断递送。同样，无需将其恢复为之前的状态，因为该函数知道它们最初始终是启用的。
-   4. 循环遍历检索到的列表中每个待处理的任务单元。
-   5. 如果这是一台多处理机器，通过检查 `TASKLET_STATE_RUN` 标志来检查该任务单元是否正在另一个处理器上运行。如果它当前正在运行，则不要现在执行它，并跳过下一个待处理的任务单元。（回忆一下，给定类型的任务单元只允许一个并发运行。）
-   6. 如果任务单元当前未运行，设置 `TASKLET_STATE_RUN` 标志，以便另一个处理器不会运行它。
-   7. 检查计数值是否为零，以确保任务单元未被禁用。如果任务单元被禁用，则跳过它并转到下一个待处理的任务单元。
-   8. 现在我们已知任务单元不在其他位置运行，已标记为运行状态以防止其在其他位置启动，且计数值为零。运行任务单元处理程序。
-   9. 任务单元运行后，清除任务单元状态字段中的 `TASKLET_STATE_RUN` 标志。
-   10. 对下一个待处理的任务单元重复此过程，直到没有更多已调度的任务单元等待运行。

任务单元的实现很简单，但相当巧妙。如你所见，所有任务单元都复用在两个 softirqs 之上，即 `HI_SOFTIRQ` 和 `TASKLET_SOFTIRQ`。当任务单元被调度时，内核触发这些 softirqs 中的一个。这些 softirqs 随后由特殊函数处理，这些函数运行任何已调度的任务单元。这些特殊函数确保给定类型的任务单元在同一时间只有一个在运行。（但其他任务单元可以同时运行。）所有这些复杂性都隐藏在一个简洁简单的接口背后。

# 使用任务单元

在大多数情况下，任务单元是实现正常硬件设备下半部的首选机制。任务单元是动态创建的，易于使用且快速。此外，虽然它们的名称令人困惑至极，但你很快就会习惯起来：它很可爱。

## 声明你的任务单元

你可以静态或动态创建任务单元。你选择哪种选项取决于你是否（或是否想要）对任务单元有直接或间接引用。如果你要静态创建任务单元（因此对它有直接引用），请使用 `<linux/interrupt.h>` 中的两个宏之一：

```c
DECLARE_TASKLET(name, func, data)
DECLARE_TASKLET_DISABLED(name, func, data);
```

这两个宏静态创建一个名为 name 的 struct tasklet_struct。当任务单元被调度时，给定的函数 func 被执行并传递参数 data。

[^5]: 这是这里令人困惑的命名方案的又一个例子。为什么 softirqs 是被“触发”（raised）的，而任务单元是被“调度”（scheduled）的？谁知道呢？这两个术语都意味着将该下半部标记为待处理，以便其尽快执行。
