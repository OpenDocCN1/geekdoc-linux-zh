
![](img/ad36c2db45661d7b3b68db09c8eea0a1_430_0.png)

## 图 28.1 CPU 调度器的简化状态转换图。

3. 进程从“在 CPU 上”状态转移有几种方式。转换 3 是将当前正在运行的进程放回可运行列表的那一种。这发生在进程用完了在处理器上分配的时间片，必须被抢占以给其他进程运行机会时。

4. 进程失去对处理器的控制的另一个主要方式是当它请求某个 I/O 操作，该操作会涉及机器硬件响应请求时的时延。在此 I/O 等待期间，即使处理器完全空闲，进程也无法运行。因此，当进程以这种方式阻塞等待 I/O 时，它不能被放回可运行列表，因为它根本不可运行。它因此通过转换 4 转移到等待其 I/O 请求完成的阻塞状态。

5. 当被阻塞进程等待的 I/O 事件发生时，进程再次变得有资格运行。然而，进程不会立即获得 CPU 时间来处理其 I/O，而是只被放回可运行列表以再次等待调度程序选择。这就是转换 5。

6. 在此简化图中所示的失去对处理器控制的最后一种方式是当正在运行的进程终止时。转换 6 显示导致进程终止的事件。

也许令人惊讶的是，无论 CPU 调度程序用来确定下一个应运行哪个进程的实际算法如何，此状态转换图通常都适用。

可以用于 CPU 调度的算法有很多，包括大量关于在各种情况下哪种算法最好的理论。然而，与其在这里进行调度算法的一般讨论，我们将只集中于 Linux 调度算法本身的细节。

## 28.2 细节

在其生命周期中，Linux 进程可能处于几种状态之一，主要的有：

**TASK_RUNNING** 只有当进程处于此状态时，调度程序才会考虑其运行。这相当于图 28.1 中的“可运行”状态。

**TASK_INTERRUPTIBLE** 处于此状态的进程正在睡眠，但如果收到信号将被设置为 TASK_RUNNING，以便处理它。这相当于图 28.1 中的“阻塞”状态。

**TASK_UNINTERRUPTIBLE** 这与前一状态类似，只是信号对进程状态没有影响。重启睡眠进程的通常方式是使用 wake_up()。使用 wake_up() 是进程从图 28.1 进行转换 5 的通常方式。

Linux 中每个进程在内部由一个 struct task_struct 表示，其中包含进程执行环境的大部分细节。此结构在文件中声明：

```
/usr/src/linux/include/linux/sched.h
```

并且该结构在进程首次创建时在 do_fork() 内核函数中动态分配给进程。do_fork() 函数包含在文件中：

```
/usr/src/linux/kernel/fork.c
```

task_struct 的成员之一称为 counter，我们将看到它在进程调度中发挥重要作用。TASK_RUNNING 进程中 counter 的值越高，下次调度程序执行时被选为运行的可能性就越大。counter 的值通常在 0 到 70 范围内，尽管在某些情况下，超出此范围的值也是可能的。

在 CPU 上执行的进程需要在四种主要情况下放弃它，以便其他进程轮流运行：

- 1. 当进程请求代表其执行某些 I/O 操作（例如磁盘访问操作）并且该操作需要一些时间才能完成时。在这种情况下，即使只有几毫秒的时延也足以证明重新调度是合理的。
- 2. 各种与信号相关的活动可能导致重新调度，例如调用 pause() 或 sigsuspend() 系统调用，或在 ptrace() 打开时接收信号。
- 3. 当在某些硬件事件上发生中断并唤醒在该事件上睡眠的进程时。如果被唤醒的进程的 counter 值明显高于当前进程的 counter 值，则会请求重新调度。
- 4. 如果进程没有以其他方式停止，那么最终它将用完其 CPU 时间分配，这将导致重新调度发生。task_struct 中的 counter 值是进程 CPU 时间分配中剩余的 jiffies（10 ms 定时器中断）的计数。

从概念上讲，Linux 调度程序自早期以来几乎没有变化，尽管 1.3 内核版本已多次清理代码，并增加了对多处理器系统的支持。对于单处理器，调度程序的操作相当直接，我们将详细检查它。

调度任务本身由内核中的一个名为 schedule() 的函数执行。该函数包含在文件中：

```
/usr/src/linux/kernel/sched.c
```

以下伪代码程序详细说明了单处理器版本的 schedule() 内核函数所采取的步骤：

```
Execute any functions on the scheduler task queue

FOR each process
    IF the process has a real time interval timer running
        IF the interval timer has expired
            Send a SIGALRM to the process
            Restart the interval timer if required
        END_IF
    END_IF

    IF the process state is TASK_INTERRUPTIBLE
        IF process has had a signal or has an expired timeout
            Set process state to TASK_RUNNING
        END_IF
    END_IF
END_FOR

FOR each process
    IF process state is TASK_RUNNING
        Remember the process with the highest counter value
    END_IF
END_FOR

IF all runnable processes have a counter value of zero
    FOR each process
        Recalculate process counter value from its priority
    END_FOR
END_IF
```

切换到记住的“最高 counter”进程的上下文

正如你所见，这是一个非常简单的调度算法，很大程度上依赖于 counter 值来确定进程运行的可能性以及运行时的时间片大小。

在可以支持多处理器的内核中，用于选择下一个运行进程的 counter 值的使用方式有一个简单的修改。除了单独使用 counter 外，还添加了额外的项，以给同一处理器上的进程一些优势，并给当前进程一点优势。

有了这些说明和一份 Linux 内核调度程序源代码，你应该能够相当容易地浏览代码并弄清其工作原理。

## 微线程 – 案例研究

你已经看到在 Linux 中并发的主要单位是进程。为了在执行一个进程和下一个进程之间切换，需要做很多工作。这种上下文切换开销是必要的，因为通常 Linux 需要确保任何一对进程都不会相互干扰，特别是当你考虑到进程可能甚至不属于同一用户时。

然而，很 often 你会想要编写彼此 aware 存在并且可以为了共同目标而合作的程序。解决此问题的标准方案是进程间通信机制。

无论你选择使用哪种 IPC 机制，只要普通进程需要协同工作，就仍需应对上下文切换开销。

克服这一问题的方法是使用线程的概念。每个 Linux 进程都有自己的文本、数据和系统内存区域和数据结构，以及处理器上的自己的时间片，以便每个进程可以按自己的节奏独立进行。线程背后的想法是，每个进程可以将其处理器时间片在几个并发线程之间共享，每个线程也共享其所属进程的内存和数据结构。

在单个进程内两个协作线程之间进行上下文切换所涉及的工作量远小于在两个进程之间切换的工作量。这主要是因为进程内的线程都共享相同的文本、数据和系统内存区域和数据结构，因此无需花费精力重新排列这些东西。

由于线程专门设计为协作而不是对抗，内核无需做任何事情来保护单个进程内的线程彼此不受干扰。

因此，线程可以被视为轻量级进程；与进程相比，在它们之间进行上下文切换所需的工作量很小
