
| `union _fault` | `addr` | `caddr_t` | 用于 SEGV, BUS, ILL, TRAP, FPE 的陷阱联合体 |

| | `trapno` | `int` | 陷阱号 |

| | `pc` | `caddr_t` | 程序计数器 |

| `union _file` | `fd` | `int` | 用于 POLL, XFSZ 的文件联合体 |

| | `band` | `int` | 文件描述符带 |

| `union _prof` | `faddr` | `caddr_t` | 上一个陷阱地址 |

| | `tstamp` | `timestamp` | 时间戳 |

| | `syscall` | `short` | 系统调用号 |

# 索拉里斯多线程进程架构

## 表 8-10 siginfo 结构（续）

| 结构或联合体 | 字段名称 | 数据类型 | 说明 |
|---|---|---|---|

| | `nsysarg` | `char` | 系统调用参数数量 |

| | `fault` | `char` | 上一个陷阱代码 |

在进程级别，有三个 `k_sigset_t` 结构（参见第332页的图 8.22）：

- `p_sig` 字段为进程的每个挂起信号设置位。
- `p_ignore` 代表设置为忽略的信号。
- `p_siginfo` 表示 `siginfo` 结构中关于该信号的信息。

`siginfo` 数据结构嵌入在 `sigqueue` 中，其链表根于进程 `p_sigqueue` 指针，用于任何队列到进程的信号。`sigqueue` 结构从指向 `p_sighdr` 的池中分配。当进程执行 `sigqueue(2)` 系统调用时，会分配 32 个（默认）`sigqueue` 结构形成可用池。对于 `signotify` 调用，在 `p_sighdr` 处请求一个额外的池。`sigsignify` 系统调用在索拉里斯中没有显式暴露为 API（内部用于 POSIX 消息队列）。到达通知阶段的已生成但尚未递送的信号表示在 `p_notifs` 字段中，用于 lw 与进程之间的同步。

在嵌入的 `uarea` 中，维护了几个位图用于标记信号事件或强制特定行为，可以通过 `sigac(2)` 系统调用设置。一个指向状态的指针数组：`u_signal[MAXSIG]`，每个信号包含一个项。数组中的项可能表示信号被忽略（`SIG_IGN`）或设置了默认操作（`SIG_DEF`）。如果需要调用由 `signal(3)` 或 `sigaction(2)` 安装的处理程序，则数组位置指向信号递送时被调用的函数。`uarea` 信号字段如下。当字段中设置了对应的位时，会发生描述的行为。

- `u_sigstack` 标记用于处理信号的备用栈。假设已调用 `sigstack(2)` 设置了备用栈。如果没有设置，将在默认栈上处理。通过 `sigaction(2)` 及其 `sigaction` 结构 `sa_flags` 字段中的 `SA_ONSTACK` 标志实现。
- `u_sigresethand` 当信号的处理程序被删除时，将状态重置为默认（`SIG_DEF`）。处理程序被删除时信号不会被阻塞。如上，通过 `sa_flags` 中的 `SA_RESETHAND` 实现。
- `u_sigstart` 如果在接收信号时处于系统调用内部，则重启系统调用。此行为不适用于所有系统调用，仅适用于可能是“慢”的系统调用（例如 I/O 型系统调用——`read(2)`、`write(2)` 等）。中断的系统调用通常会导致错误，由 `sa_flags` 中的 `SA_RESTART` 设置 `errno`。
- `u_signodefer` 不阻塞已捕获信号的后续发生。当信号递送并执行处理程序时，正常信号会被阻塞。通过 `sa_flags` 中的 `SA_NODEFER` 实现。
- `u_sigmask[]` 已捕获并正持有的信号。
- `u_signal` 信号状态。

LWP 在 `lwp_curinfo` 中存储当前信号，并在 `lwp_curinfo` 中存储当前信号的信号队列指针，这用于信号递送阶段。其他字段包括如果通过调用 `sigstack(2)` 设置了备用栈 `lwp_sigstack` 时的栈指针。根据内核栈的默认用法，程序通过自己的栈管理在备用栈上处理信号是理想的。内核维护两个 `k_sigset_t` 成员：`t_sig` 和 `t_hold`。`t_sig` 的意义与进程级别的 `p_sig` 相同，是挂起信号的掩码；`t_hold` 是位掩码。

此外，`t_sigqueue` 指向信号数据的 `sigqueue`。`siginfo` 结构将位于进程 `p_sigqueue` 或线程 `t_sigqueue` 上。内核线程 `t_sigqueue` 用于内核代码传递了非空内核指针的情况，这指示定向信号，适用于具有多个 LWP 的多线程进程。

最后，对于多线程进程，用户线程（`t_psig`）、跳跃信号（`t_bsig`——稍后讨论跳跃信号）以及要的信号（`t_hold`）。还有一个延迟信号的 `siginfo`，引用为。

显然，在进程上下文中各种实体的信号结构成员中似乎存在一些冗余。这种冗余是由于对多线程模型的需求，以及根据信号本身和源将信号发布到不同位置的事实。之前的讨论中，我们提供了几个为什么发送某些信号及其起源的示例。异步信号可以从内核的一个或多个位置产生。从用户态发送的信号（例如 `kill(1)`、`kill(2)`、`sigqueue(2)`）发送到进程。源自内核的信号指向特定的 LWP/kthread；例如，内核时钟中断处理程序可能会发送

将 `SIGPROF` 或 `SIGVTALRM` 直接发送到 LWP/kthread。`pthread_kill(3T)` 和 `thr_kill(3T)` 线程库接口提供了向特定用户线程发送异步信号的功能。STREAMS 子系统在适当的情况下向进程发送 `SIGPOLL` 和 `SIGURG`（例如，发生轮询事件或接收到紧急带外消息）。

无论信号的来源是什么，通过操作系统完成的最终递送机制是内核的 `sigtopproc()` 函数，它接受多多四个参数：一个进程指针、一个内核线程指针、信号号以及一个来自用户的可选标志，该标志指示信号源是内核还是用户态。应该指向 kthread/LWP 的信号会调用带有有效 kthread 指针的 `sigtopproc()`。一个为 `NULL` 的 kthread 指针表示信号应该被投递到进程。让我们来看 `sigtopproc()` 的代码流。
