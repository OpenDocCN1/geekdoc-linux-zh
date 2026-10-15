
第 1226–1229 行

在此代码块中，我们将任务的状态设置为 `TASK_STOPPED`。如果 `clone_flags` 中没有设置 `CLONE_STOPPED` 标志，我们将唤醒子进程；否则，我们将让它等待唤醒信号。

第 1231–1234 行

如果父进程上开启了跟踪（ptracing），我们将发送一个通知。

## 3.4 进程生命周期

第 1236–1239 行

如果这最初是对 `vfork()` 的调用，在这里我们设置父进程阻塞，并在启用跟踪的情况下向跟踪器发送通知。这是通过将父进程放入等待队列中，并保持在 `TASK_UNINTERRUPTIBLE` 状态下，直到子进程调用 `exit()` 或 `execve()` 实现的。

第 1248 行

我们在当前任务（父进程）中设置了 `need_resched`。这允许子进程先运行。

现在我们已经了解了进程是如何创建的，接下我们需要查看在其生命周期期间发生了什么。在此期间，进程可能会发现自己处于各种状态中。这些状态之间的转换取决于进程执行的操作以及发送给它的信号的性质。我们的示例程序处于过 `TASK_UNINTERRUPTIBLE` 状态，并且在退出之前（其当前状态）被设置为 `TASK_RUNNING` 状态。

进程第一个状态设置为 `TASK_UNINTERRUPTIBLE`。这发生在由 `do_fork()` 调用的 `copy_process()` 例程中的进程创建期间。进程发现的第二个个状态是 `TASK_RUNNING`，它是在退出 `do_fork()` 之前设置的。这两个状态保证了进程的存活。在这两个状态之后，许多变量开始发挥，决定了进程将处于何种状态。进程的最后一个状态被设置为 `TASK_ZOMBIE`，是在调用 `do_exit()` 期间。让我们看看进程状态以及从一个状态到下一个状态转换的方式。我们指出我们的进程是如何从一个状态变为另一个状态的。

### 3.4.1 进程状态

当进程运行时，意味着它的上下文已加载到 CPU 寄存器和内存中，并且定义此上下文的程序正在执行中。在任何特定时刻，进程可能由于多种原因无法运行。进程可能无法继续运行是因为它正在等待不存在的输入，或者调度程序可能认为它已经运行了所允许的最大时间单位，必须让给其他进程。当进程没有运行但能够运行（例如重新调度时）时，被认为是“就绪”；当等待输入时，被认为是“阻塞”。

图 3.10 显示了抽象进程状态，以及与每个抽象状态对应的底层 Linux 任务状态。表 3.5 概述了四种转换及其实现。表 3.6 将抽象状态与 Linux 内核用于识别这些状态的值相关起来。

![](img/6525157588f931c50a65c5a42af9a432_137_0.png)

图 3.10
进程状态转换

#### 表 3.5
转换总结

| 转换 | 转换代理者 |
|---|---|
| 就绪到运行 (A) | 由调度器选择 |
| 运行到就绪 (B) | 时间片结束（非活动） |
| 进程让出（活动） | |
| 阻塞到就绪 (C ) | 接收信号 |
| 资源变得可用 | |
| 运行到阻塞 (D) | 进程睡眠或等待某些内容 |

#### 表 3.6
抽象状态与 Linux 内核值的关联
| 抽象状态 | Linux 状态 |
|---|---|
| 就绪 | `TASK_RUNNING` |
| 运行 | `TASK_RUNNING` |
| 阻塞 | `TASK_INTERRUPTIBLE`, `TASK_UNINTERRUPTIBLE`, `TASK_ZOMBIE`, `TASK_STOPPED` |

> 注意：通过 `current->state=TASK_INTERRUPTIBLE` 这种方式设置进程状态。

### 3.4.2 进程状态转换

在进程生命周期期间，发生了导致进程状态转换的事件。我们现在查看导致进程从一个状态变为另一个状态的类型。抽象进程转换（参见表 3.5）包括从就绪状态到运行状态、从运行状态到就绪状态的转换，以及从运行状态到阻塞状态的转换。每个转换可能对应到多种状态，例如 `TASK_INTERRUPTIBLE`、`TASK_UNINTERRUPTIBLE`、`TASK_ZOMBIE` 或 `TASK_STOPPED` 到 `TASK_RUNNING`。图 3.11 和表 3.7 描述了这些转换。

![](img/6525157588f931c50a65c5a42af9a432_138_0.png)

图 3.11
任务转换

#### 表 3.7
转换总结

| 起任务状态 | 结束任务状态 | 转换代理者 |
|---|---|---|
| `TASK_RUNNING` | `TASK_INTERRUPTIBLE` | 进入等待队列 |
| `TASK_RUNNING` | `TASK_INTERRUPTIBLE` | 进入等待队列 |
| `TASK_RUNNING` | `TASK_STOPPED` | 正在跟踪 |
| `TASK_RUNNING` | `TASK_ZOMBIE` | 父进程未调用 `wait()` |
| `TASK_INTERRUPTIBLE` | `TASK_STOPPED` | 信号期间 |
| `TASK_UNINTERRUPTIBLE` | `TASK_STOPPED` | 唤醒期间 |
| `TASK_INTERRUPTIBLE` | `TASK_RUNNING` | 接收到等待的资源 |
| `TASK_INTERRUPTIBLE` | `TASK_RUNNING` | 接收到信号 |
| `TASK_RUNNING` | `TASK_RUNNING` | 调度器移动 |

### 3.4.2.1 就绪到运行

抽象进程转换“就绪到运行”并不对应实际的 Linux 任务转换，因为状态没有改变（保持为 `TASK_RUNNING`）。然而，进程从就绪任务队列（或运行队列）变为实际由 CPU 执行。

### 3.4.2.2 运行到就绪

在这种情况下，尽管任务发生了变化，但任务状态没有改变。抽象进程转换帮助我们理解发生的情况。正如之前提到的，当进程从由 CPU 执行变为被放入运行队列时，它从运行变为就绪。

### 3.4.2.3 运行到阻塞

当进程被阻塞时，它可能处于以下状态之一：`TASK_INTERRUPTIBLE`、`TASK_UNINTERRUPTIBLE`、`TASK_ZOMBIE` 或 `TASK_STOPPED`。我们现在描述如何从 `TASK_RUNNING` 进入这些状态中的一种，如表 3.7 所示。

设备已准备好可以访问数据。因此，驱动程序将包含如下代码：

```
while (1)
{
  if(resource_available)
    break();
  set_current_state(TASK_INTERRUPTIBLE);
    schedule();
  }
  set_current_state(TASK_RUNNING);
```

示例进程在执行 `open()` 调用时进入 `TASK_INTERRUPTIBLE` 状态。此时，它通过 `schedule()` 调用从运行进程列表中移除，队列选择的另一个进程成为运行进程。当资源可用后，该进程跳出循环并将进程状态设置为 `TASK_RUNNING`，这将其放回运行队列。它会一直等待直到调度器确定它是需要运行的进程。

下面的列表显示了函数 `interruptible_sleep_on()`，它可以将一个项设置为 `TASK_INTERRUPTIBLE` 状态：

```
kernel/sched.c
2504  void interruptible_sleep_on(wait_queue_head_t *q)
2505 {
2506    SLEEP_ON_VAR
2507
2508    current->state = TASK_INTERRUPTIBLE;
2509
2510    SLEEP_ON_HEAD
2511    schedule();
2512    SLEEP_ON_TAIL
2513  }
```

`SLEEP_ON_HEAD` 和 `SLEEP_ON_TAIL` 宏负责将任务从等待队列中添加和移除（参见本章的“等待队列”节）。`SLEEP_ON_VAR` 宏初始化任务的等待队列项以便将其加入等待队列。

## TASK_RUNNING 到 TASK_UNINTERRUPTIBLE

`TASK_UNINTERRUPTIBLE` 状态与 `TASK_INTERRUPTIBLE` 类似，不同在于进程在处于内核模式时不会忽略发入的信号。该状态也是任务在 `do_fork()` 创建期间初始化时被设置的默认状态。

## 3.4 进程生命周期

调用 `sleep_on()` 函数将任务设置为 `TASK_UNINTERRUPTIBLE` 状态。

```
kernel/sched.c
2545 long fastcall __sleep_on(wait_queue_head_t *q)
2546 {
2547     SLEEP_ON_VAR
2548
2549     current->state = TASK_UNINTERRUPTIBLE;
2550
```
