
一旦启用了微状态统计，内核在进程状态切换时记录 LWP 的微状态。这反映了 LWP 状态。

# Profs — 进程文件系统

在初始化期间设置，并在每次通过 `new_state()` 时都会重置，标记新状态转换的开始时间。对应于上一个微状态的 `ms_acct[]` 数组位置将被更新，以反映在该状态下流逝的时间。由于时间值是累加的，`ms_acct[]` 中的当前值将与新计算出的流逝时间相加。因此 `ms_acct[]` 数组包含了各种微状态下的流逝时间，并在状态发生变化时动态更新。最后，内核线程的 `t_mstate` 被设置为以反映新的微状态。

针对受跟踪的微状态对 `new_mstate()` 的调用来自内核的几个区域。表 8-6 出了出了针对特定状态变化调用 `new_mstate()` 的内核函数。

## 表 8-6 调用到 `new_mstate()` 的微状态变化调用

| 新状态 | 调用来源 |
| --- | --- |
| LMS_USER | 系统处理程序，在从系统调用返回时。 |
| LMS_SYSTEM | 系统处理程序，在进入系统调用时。 |
| LMS_TRAP | 异常处理程序，当发生异常时（包括浮点异常）。 |
| LMS_TFAULT | 异常处理程序（文本页异常）。 |
| LMS_FAULT | 异常处理程序（数据页异常）。 |
| LMS_KFAULT | 异常处理程序（内核页异常）。 |
| LMS_USER_LOCK | LWP 支持代码，当获取互斥锁时。 |
| LMS_SLEEP | 闸门代码，当 LWP/kthread 将阻塞时。 |
| LMS_WAIT_CPU | 调度器代码。未在 `new_mstate()` 中更新，但在 `restore_mstate()` 中更新（见下文）。 |
| LMS_STOPPED | 信号代码，当发送作业控制信号时。 |

最后讨论关于微状态计数的函数是 `restore_mstate()`，它从调度器代码中的几处调用，用于恢复仅供执行的 LWP 的微状态。`restore_mstate()` 使用与 `new_mstate()` 函数描述相同的相同算法，计算在上一个状态（通常是睡眠）中消耗的微状态时间值，并从 `ms_prev` 字段（`lwp_state` 结构）恢复上一个状态。

当 LWP/kthreads 终止时，`ms_acct[]` 数组中的微状态数据以及资源使用计数器会被添加到 `proc` 结构中对应位置的值中。同样，进程级资源计数器和微状态数据反映了进程中所有的 LWP/kthreads。

## 8.7 信号

信号是进程或线程通知特定事件的手段。信号通常与硬件中断相比较，当硬件子系统（如磁盘 I/O 接口，例如 SCSI 硬盘适配器）由于 I/O 完成而向处理器产生中断时。中断会导致处理器进入中断处理程序，从而根据中断的来源和原因在操作系统中进行后续处理。硬件中断的类比很好地映射了信号的本质。同样，当信号被发送给进程或线程时，可能会进入信号处理程序（取决于信号的当前处置），这与系统在接收到中断后进入中断处理程序是模拟的。

信号承载着深厚的历史，以及在各种 UNIX 实现中信号代码的设计变更。这些实现和信号接口的变化在部分由于早期信号实现的某些缺陷，以及在不同版本的 UNIX（主要是 BSD UNIX 和 AT&T System V）上进行的并行开发工作。这段历史在 [25] 和 [10] 中进行了总结，不再重复。

值得提到的是，早期的信号实现被认为是不可靠的。不可靠性源于过去，如果进程捕获了信号并调用了自己的处理程序，内核会将信号处理程序重置为默认值，但内核的重置在进程处理程序被调用之前就已经发生了。在用户代码中通过连续发生相同信号来解决此问题的尝试会导致竞态条件，不仅没有解决问题，反而会在用户定义的处理程序安装之前调用默认操作。对于默认动动为终止进程的信号，这种行为产生了一些问题。这个问题（以及其他一些问题）在 20 世纪 80 年代中期 4.BSD UNIX 和 SVR3 中得到了解决。可靠信号实现——即安装的信号处理程序保持持久且不被内核重置——POSIX 标准为代码中使用信号提供了一组相当定义良好的接口，如今 Solaris 的信号实现完全符合 POSIX 标准。请注意，可靠信号需要使用较新的 `sigaction(2)` 接口，而不是传统的 `signal(3)` 调用。`signal(3)` 库不保持处理程序的持久性，导致了不可靠的信号行为。

信号的发生对于进程或线程可能是同步或异步的，取决于信号的来源以及底层的原因或引起。同步信号是执行指令流的直接结果，其中不可恢复的错误（如非法指令或非法地址引用）需要立即终止进程。此类信号指向导致错误的执行流的线程。由于此类类型的错误会导致进入内核异常处理程序，同步信号有时被称为陷阱（traps）。

异步信号正如其名所示，是外部的（在某些情况下与当前执行上下文无关的）。一个明显的例子是进程或线程通过 `kill(2)`、`lwp_kill(2)` 或 `sigsend(2)` 向另一个进程发送信号。

每个信号都有唯一的名称：`SIGINT`, `SIGQUIT`, `SIGHUP`, `SIGILL`, `SIGTRAP`, `SIGABRT`, `SIGBUS`, `SIGFPE`, `SIGKILL`, `SIGTERM`, `SIGSEGV`, `SIGSYS`, `SIGALRM`, `SIGUSR1`, `SIGUSR2`, `SIGCHLD`, `SIGPWR`, `SIGWINCH`, `SIGURG`, `SIGPOLL`, `SIGIO`, `SIGSTOP`, `SIGTSTP`, `SIGCONT`, `SIGTTIN`, `SIGTTO`, `SIGVALTRM`, `SIGPROF`, `SIGXCPU`, `SIGFSZ`, `SIGWAITING`, `SIGLWP`, `SIGFREE`, `SIGTHAW`, `SIGCANCEL`, `SIGLOST`, `SIGRTMIN` 和 `SIGRTMAX`。异步信号也称为中断。

| 名称 | 编号 | 默认操作 |
| --- | --- | --- |
| SIGHUP | 1 | |
| SIGINT | 2 | |
| SIGQUIT | 3 | |
| SIGILL | 4 | |
| SIGTRAP | 5 | |
| SIGABRT | 6 | |
| SIGBUS | 7 | |
| SIGFPE | 8 | |
| SIGKILL | 9 | 不可捕获或忽略 |
| SIGTERM | 10 | |
| SIGSEGV | 11 | |
| SIGSYS | 12 | |
| SIGALRM | 13 | |
| SIGUSR1 | 14 | |
| SIGUSR2 | 15 | |
| SIGCHLD | 16 | |
| SIGPWR | 17 | |
| SIGWINCH | 18 | |
| SIGURG | 19 | |
| SIGPOLL | 20 | |
| SIGIO | 21 | |
| SIGSTOP | 22 | 不可捕获或忽略 |
| SIGTSTP | 23 | 停止 |
| SIGCONT | 24 | 停止 |
| SIGTTIN | 25 | 停止 |
| SIGTTO | 26 | 停止 |
| SIGVALTRM | 27 | |
| SIGPROF | 28 | |
| SIGXCPU | 29 | |
| SIGFSZ | 30 | |
| SIGWAITING | 31 | 忽略 |
| SIGLWP | 32 | 忽略 |
| SIGFREE | 33 | 忽略 |
| SIGTHAW | 34 | 忽略 |
| SIGCANCEL | 35 | 忽略 |
| SIGLOST | 36 | 忽略 |
| SIGRTMIN | 38 | |
| SIGRTMAX | 45 | |

`SIGLOST` 首次出现在 Solaris 2.6 版本中。2.5 和 2.5.1 版本没有此信号，它们的 `SIGRTMIN` 和 `SIGRTMAX` 信号号分别为 37 和 44。内核将 `MAXSIG`（在 `/usr/include/sys/signal.h` 中用户代码可用）定义为一个符号常量，用于内核支持代码中的多个处。在 Solaris 2.5 和 2.5.1 中，`MAXSIG` 为 44，在 Solaris 2.6 和 Solaris 7 中为 45。此外，`SIGLLO` 和 `SIGIO` 都定义为信号号 22。`SIGIO` 的产生是由于进程通过 `aioread(3)` 或 `aiowrite(3)` 发起异步读或写（或 POSIX 等效的 `aio_read(3)` 或 `aio_write(3)`），用于通知进程 I/O 完成或发生了错误。`SIGLLP` 是一个更通用的指示器，表示发生了可轮询事件。

信号的处置（disposition）可以从其默认值更改，进程可以安排捕获信号并调用自己的信号处理程序，也可以忽略那些默认处置非忽略的信号。唯一的例外是 `SIGKILL` 和 `SIGSTOP`——这两个信号的默认处置无法更改。定义和更改信号处置的接口是 `signal(3)`、`sigset(3)` 库以及 `sigaction(2)` 系统调用。

信号还可以被阻塞，这意味着进程或线程临时阻止了信号的传递。被阻塞信号的产生会导致信号对进程保持挂起（pending）状态，直到被显式取消阻塞或处置更改为忽略。用于阻塞信号的信号掩码存在于 kthread 内部和用户线程级；`t_hold` 结构（内核和用户线程均使用相同的名称）是一个 `sigset_t` 数据类型，使用设置位来表示被阻塞的信号。`sigprocmask(2)` 系统调用为调用的 kthread 设置或获取信号掩码。非线程进程有一对 LWP/kthread；因此，kthread 中的 `t_hold` 变成全进程范围的信号掩码。等效接口——`thr_setsigmask(3)` 和 `pthread_sigmask(3)`——在用户线程级设置和检索信号掩码（用户线程结构中的 `t_hold`）。

# Solaris 多线程进程架构

`psig(1)` 命令列出进程的信号动作。下面的示例输出了我们 ksh 进程的信号动作；为了节省空间省略了部分行。
