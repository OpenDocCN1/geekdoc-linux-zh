
The `add_timer()` call sets up a specified function to be executed at a given time (given in jiffies). The chosen function will be executed at the specified time unless the timer is canceled. If the event for which the process is waiting occurs normally, then the interrupt service routine can cancel the timer (with `del_timer()`). If the interrupt fails to occur for any reason, then the timer will expire and call the specified function. This will usually flag that the error has taken place and `wake_up()` the sleeping process to deal with it.

`add_timer()` 调用设置一个指定的函数在给定时间（以 jiffies 为单位）执行。所选函数将在指定时间执行，除非定时器被取消。如果进程等待的事件正常发生，则中断服务例程可以取消定时器（使用 `del_timer()`）。如果由于任何原因中断未能发生，则定时器将到期并调用指定的函数。这通常会标记错误已发生并唤醒正在睡眠的进程以处理它。

# Part V INTERNALS

## Process Scheduling

In a multi-tasking operating system, one of the most fundamental operations is process scheduling. In any system where you would like to be able to run multiple processes concurrently on a machine with a single processor, some form of process scheduling must take place. This is obvious when you consider that, at any particular instant, the CPU can only be executing a single instruction, and that on behalf of a single process. For several processes to be making progress on the machine together, the CPU time must be shared between the processes that are ready to run. The task of the scheduler, then, is to choose which of the processes that are ready to run should be allocated the CPU next.

在多任务操作系统中，最基本的操作之一是进程调度。在任何希望在单处理器机器上并发运行多个进程的系统中，都必须进行某种形式的进程调度。这很明显，因为在任何特定瞬间，CPU 只能执行一条指令，并且代表单个进程执行。为了使多个进程在机器上共同取得进展，CPU 时间必须在准备运行的进程之间共享。因此，调度程序的任务是选择下一个应分配 CPU 的准备运行的进程。

### 28.1 Background

In trying to perform its task, the scheduler has various objectives that it must try to achieve. And, as we shall see, several of these objectives will make demands on the scheduler that will pull in opposite directions. Among the more important objectives are:

在执行其任务时，调度程序有各种需要尝试实现的目标。而且，正如我们将看到的，其中几个目标会对调度程序提出相互冲突的要求。更重要的目标包括：

- Give each process a fair share of the CPU.

  为每个进程提供公平的 CPU 份额。

- Minimize the CPU idle time (i.e. keep the CPU busy).

  最小化 CPU 空闲时间（即保持 CPU 忙碌）。

- Maximize throughput. This means maximizing the number of processes completed in a given time.

  最大化吞吐量。这意味着在给定时间内最大化完成的进程数量。

- Minimize the time the system takes to respond to user requests.

  最小化系统响应用户请求所需的时间。

An obvious way in which these objectives conflict is with regard to user requests. Here, it seems as though user requests should be favored in some way, though this obviously conflicts with the idea of giving all processes a fair share of the CPU.

这些目标冲突的明显方式是关于用户请求。在这里，似乎用户请求应该以某种方式得到优先考虑，尽管这显然与给所有进程公平 CPU 份额的想法相冲突。

One problem that the scheduler faces immediately is that, in general, very little is known about a process when it starts up. In particular, such things as how long the process will use the CPU on average before it has to stop to wait for some I/O to take place, and how long on average the process must wait for an I/O event to take place once it is requested, are unknown.

调度程序立即面临的一个问题是，通常在进程启动时对其知之甚少。特别是，诸如进程在平均需要停止等待某些 I/O 发生之前将使用 CPU 多长时间，以及一旦请求后进程平均需要等待 I/O 事件发生多长时间等，都未知。

Another question is what to do with a process which uses a very large amount of CPU time before it does any I/O; can it be allowed just to go on hogging the processor? Well, obviously it can't, otherwise such a process could virtually stop all the other processes from making any progress.

另一个问题是，对于在进行任何 I/O 之前使用大量 CPU 时间的进程该怎么办；可以允许它继续占用处理器吗？嗯，显然不行，否则这样的进程几乎会阻止所有其他进程取得进展。

This implies that there needs to be some mechanism for switching the CPU to another process when the current process has had long enough. But where is the decision to do this taken and how?

这意味着需要某种机制在当前进程已运行足够长时间时切换 CPU 到另一个进程。但这一决定的做出位置和方式在哪里？

In general, there are two possibilities here, the first is to allow the processes themselves to release control of the CPU voluntarily when they have had a reasonable time on the CPU, and the second is to find some mechanism to force a process to release its CPU control. The first of these is called non-preemptive scheduling and the second is called preemptive scheduling.

一般来说，这里有两种可能性，第一种是允许进程本身在 CPU 上运行合理时间后自愿释放 CPU 控制权，第二种是找到某种机制强制进程释放其 CPU 控制权。前者称为非抢占式调度，后者称为抢占式调度。

As we shall see when we look at threads, it is perfectly feasible to run a system of co-operating pieces of code that use non-preemptive scheduling to switch between them. However, for process scheduling in a multi-user environment, it is usually safer to assume that the processes may be, at best, unaware of each other's existence or, at worst, positively antagonistic towards each other in terms of their CPU use.

正如我们在查看线程时将看到的，运行一个使用非抢占式调度在它们之间切换的协作代码系统是完全可行的。然而，对于多用户环境中的进程调度，通常更安全地假设进程在最好情况下彼此不知情，在最坏情况下在 CPU 使用方面彼此积极敌对。

Consequently, in a multi-user environment, preemptive scheduling is used almost without exception – and Linux is no exception.

因此，在多用户环境中，抢占式调度几乎无一例外地被使用——Linux 也不例外。

The way that this is achieved is that each process is given a maximum length of time it will be allowed to have on the CPU without a break. In addition, the system will generate fairly rapid and periodic clock timer interrupts, which will be counted and used to determine when the process has had its allocated time slice.

实现这一点的办法是为每个进程分配一个最大时间长度，允许其在不中断的情况下使用 CPU。此外，系统会产生相当快速且周期性的时钟定时器中断，这些中断会被计数并用于确定进程是否已用完其分配的时间片。

When the time slice of the current process has elapsed, the scheduler will be forced to run to determine if there is another process ready to run and more eligible to run than the process whose time slice on the CPU has just expired. If there is, then it will be run in place of the current process. If there is not, then the current process can be allowed to continue.

当当前进程的时间片用完时，调度程序将被迫运行以确定是否存在另一个准备运行且比刚用完 CPU 时间片的进程更适合运行的进程。如果有，则它将取代当前进程运行。如果没有，则允许当前进程继续运行。

Obviously, from the previous discussion, there are several states in which a process may find itself and several transitions between states that can occur in response to various events. Figure 28.1 shows a greatly simplified state transition diagram for processes under the control of the CPU scheduler and labels six transitions between the states which occur in the following circumstances:

显然，从之前的讨论可以看出，进程可能处于几种状态，并且在各种事件响应下可能发生几种状态之间的转换。图 28.1 显示了 CPU 调度程序控制下进程的极度简化的状态转换图，并标记了在以下情况下发生的六种状态之间的转换：

1. When a process is first started (by `fork()` in Linux) it is not given control of the CPU straight away. Instead, it joins a list of other processes that are in the position that they can proceed immediately, as soon as they have time on the CPU. This, then, is the starting transition which puts the process into the runnable state.

   当进程首次启动时（在 Linux 中由 `fork()` 启动），它不会立即获得 CPU 控制权。相反，它加入到其他可以立即进行的进程列表中，只要它们有 CPU 时间即可。这就是将进程置于可运行状态的起始转换。

2. Eventually, a process that is runnable will be selected by the scheduler to execute for a time on the CPU. Transition 2 takes the process from the runnable list and starts it running.

   最终，可运行的进程将被调度程序选中在 CPU 上执行一段时间。转换 2 将进程从可运行列表中取出并开始运行。

![](img/ad36c2db45661d7b3b68db09c8eea0a1_430_0.png)

**图 28.1 CPU 调度器的简化状态转换图。**

3. 进程从“在 CPU 上”状态转移有几种方式。转换 3 是将当前正在运行的进程放回可运行列表的那一种。这发生在进程用完了在处理器上分配的时间片，必须被抢占以给其他进程运行机会时。

4. 进程失去对处理器的控制的另一个主要方式是当它请求某个 I/O 操作，该操作会涉及机器硬件响应请求时的时延。在此 I/O 等待期间，即使处理器完全空闲，进程也无法运行。因此，当进程以这种方式阻塞等待 I/O 时，它不能被放回可运行列表，因为它根本不可运行。它因此通过转换 4 转移到等待其 I/O 请求完成的阻塞状态。

5. 当被阻塞进程等待的 I/O 事件发生时，进程再次变得有资格运行。然而，进程不会立即获得 CPU 时间来处理其 I/O，而是只被放回可运行列表以再次等待调度程序选择。这就是转换 5。

6. 在此简化图中所示的失去对处理器控制的最后一种方式是当正在运行的进程终止时。转换 6 显示导致进程终止的事件。

也许令人惊讶的是，无论 CPU 调度程序用来确定下一个应运行哪个进程的实际算法如何，此状态转换图通常都适用。

可以用于 CPU 调度的算法有很多，包括大量关于在各种情况下哪种算法最好的理论。然而，与其在这里进行调度算法的一般讨论，我们将只集中于 Linux 调度算法本身的细节。

### 28.2 细节

在其生命周期中，Linux 进程可能处于几种状态之一，主要的有：

`TASK_RUNNING` 只有当进程处于此状态时，调度程序才会考虑其运行。这相当于图 28.1 中的“可运行”状态。

`TASK_INTERRUPTIBLE` 处于此状态的进程正在睡眠，但如果收到信号将被设置为 `TASK_RUNNING`，以便处理它。这相当于图 28.1 中的“阻塞”状态。

`TASK_UNINTERRUPTIBLE` 这与前一状态类似，只是信号对进程状态没有影响。重启睡眠进程的通常方式是使用 `wake_up()`。使用 `wake_up()` 是进程从图 28.1 进行转换 5 的通常方式。

Linux 中每个进程在内部由一个 `struct task_struct` 表示，其中包含进程执行环境的大部分细节。此结构在文件中声明：
