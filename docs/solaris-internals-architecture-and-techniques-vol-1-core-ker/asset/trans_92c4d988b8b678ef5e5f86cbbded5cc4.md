
SIGLOST 首次出现在 Solaris 2.6 版本中。2.5 和 2.5.1 版本没有此信号，它们的 SIGRTMIN 和 SIGRTMAX 信号号分别为 37 和 44。内核将 `MAXSIG`（在 `/usr/include/sys/signal.h` 中用户代码可用）定义为一个符号常量，用于内核支持代码中的多个处。在 Solaris 2.5 和 2.5.1 中，`MAXSIG` 为 44，在 Solaris 2.6 和 Solaris 7 中为 45。此外，SIGLLO 和 SIGIO 都定义为信号号 22。SIGIO 的产生是由于进程通过 `aioread(3)` 或 `aiowrite(3)` 发起异步读或写（或 POSIX 等效的 `aio_read(3)` 或 `aio_write(3)`），用于通知进程 I/O 完成或发生了错误。SIGLLP 是一个更通用的指示器，表示发生了可轮询事件。

信号的处置（disposition）可以从其默认值更改，进程可以安排捕获信号并调用自己的信号处理程序，也可以忽略那些默认处置非忽略的信号。唯一的例外是 SIGKILL 和 SIGSTOP——这两个信号的默认处置无法更改。定义和更改信号处置的接口是 `signal(3)`、`sigset(3)` 库以及 `sigaction(2)` 系统调用。

信号还可以被阻塞，这意味着进程或线程临时阻止了信号的传递。被阻塞信号的产生会导致信号对进程保持挂起（pending）状态，直到被显式取消阻塞或处置更改为忽略。用于阻塞信号的信号掩码存在于 kthread 内部和用户线程级；`t_hold` 结构（内核和用户线程均使用相同的名称）是一个 `sigset_t` 数据类型，使用设置位来表示被阻塞的信号。`sigprocmask(2)` 系统调用为调用的 kthread 设置或获取信号掩码。非线程进程有一对 LWP/kthread；因此，kthread 中的 `t_hold` 变成全进程范围的信号掩码。等效接口——`thr_setsigmask(3)` 和 `pthread_sigmask(3)`——在用户线程级设置和检索信号掩码（用户线程结构中的 `t_hold`）。

# Solaris 多线程进程架构

`psig(1)` 命令列出进程的信号动作。下面的示例输出了我们 ksh 进程的信号动作；为了节省空间省略了部分行。

```
$ /usr/proc/bin/psig 448
448:     -ksh
HUP      caught RESTART
INT      caught RESTART
QUIT     caught RESTART
ILL      caught RESTART
TRAP     caught RESTART
ABRT     caught RESTART
ENT      caught RESTART
PBRG     default
KILL     default
BUS      caught RESTART
SEGV     caught RESTART
SYS      caught RESTART
PIPE     caught RESTART
ALRM     ignored
TERM     USR1     caught RESTART
USR2     caught RESTART
CLD      default NOCLDSTOP
PWR      default
```

记住，信号可以源于几个不同的地方，通常出于多种原因。SIGHUP、SIGINT 和 SIGQUIT 通常由控制终端的键盘输入产生（SIGINT 和 SIGQUIT），或在控制终端断开时产生，注意使用 `nohup(1)` 命令通过将 SIGHUP 的处置设置为忽略来使进程变得“免疫”。其他与终端 I/O 相关的信号包括 SIGSTOP、SIGTIN、SIGTOU 和 SIGTSTP。对于源自键盘命令的信号，产生这些信号的实际键序列在终端会话参数中定义，通常通过 `stty(1)`。例如，^ (Control-C) 通常是中断键序列，并在发送给进程的 SIGINT 中，默认处置是强制进程退出。

作为指令执行期间遇到错误而直接产生的信号，从系统上的硬件陷阱（trap）开始。不同的处理器架构定义了各种陷阱，导致控制权立即转移到内核陷阱处理函数。Solaris 内核构建陷阱表，根据 Solaris 环境支持的处理器架构在适当的位置插入陷阱处理程序：SPARC V7 (sun 架构)、SPARC V8 (UltraSPARC 架构)、SPARC V9 (UltraSPARC) 和 Intel x86。术语上，这些程序被称为中断描述表，或 IDTs。在 SPARC 上，它们被称为陷阱表。内核安装的陷阱处理器通常向导致陷阱的线程产生一个信号。硬件产生的信号是 SIGILL、SIGFPE、SIGSEGV、SIGTRAP 和 SIGBUS。

## 表 8-8 UltraSPARC 陷阱及产生的信号

| 陷阱名称 | 信号 |
| :--- | :--- |
| instruction_access_exception | SIGSEGV, SIGBUS |
| instruction_access_MMU miss | SIGSEGV |
| instruction_access_error | SIGBUS |
| illegal_instruction | SIGILL |
| privileged_opcode | SIGILL |
| fp_disabled | SIGILL |
| fp_exception_ie7 | SIGFPE |
| fp_exception_other | SIGFPE |
| tag_overflow | SIGBUS |
| division_by_zero | SIGFPE |
| data_access_exception | SIGSEGV, SIGBUS |
| data_access_MMU miss | SIGSEGV |
| data_access_error | SIGBUS |
| data_access_protection | SIGSEGV |
| mem_address_not_aligned | SIGBUS |
| privileged_action | SIGILL |
| async_data_error | SIGBUS |

信号可以源于终端 I/O 和错误条件以外的源；进程引发（例如 SIGXFS）和外部事件（kill()）也可以产生信号。例如：

- 应用程序可以创建用户自定义信号，作为定义 SIGUSR1 或 SIGUSR2 进程间通信处理器的粗略形式，并在进程之间发送这些信号。如果进程超过其处理器时间限制，内核会发送 SIGCPU；如果文件写入超过大小限制，则发送 SIGXFS。调用 `abort(3)` 库后会发送 SIGABRT。如果进程正在写入管道而读取器已终止，则产生 SIGPIPE。
- `kill(2)`,`sigsend(2)` 或 `thr_kill(3)` 是显式的程序化发送。`kill(1)` 命令从命令行向进程发送信号；`sigsend(2)` 和程序化地向进程或进程组发送信号。内核通过 SIGCHLD 通知父进程子进程的状态变化。`alarm(2)` 系统调用在定时器过期时发送 SIGALRM。

完整列表可以在任何关于 UNIX 编程的书中找到（参见 [3]）。

在实际实现方面，信号表示为数据结构中的一个位（二进制数字）（实际上是几个数据结构，正如我们将看到的那样）。更准确地说，内核发布信号会导致进程级或线程级结构成员中的一个位被设置。由于每个信号都有唯一的信号号，我们使用足够宽的结构成员，以便通过简单地设置与要发布的信号信号号相对应的位来表示每个信号。例如，设置第 17 位以发布信号 17，SIGUSR1（实际上是第 16 位，因为它们从 0 开始，信号从 1 开始）。

由于 Solaris 环境中现在可能超过 32 个信号，`long` 或 `int` 类型宽度不足以将每个可能的信号表示为唯一的位，因此我们需要数据结构。在 64 位 Solaris 7 中，`long` 是一种 64 位数据类型，但信号代码是在实现 64 位数据类型之前开发的（使用 `k_sigset_t`）。多个数据结构使用了 `/usr/include/signal.h` 中定义的 `k_sigset_t` 结构来存储发布的位。`k_sigset_t` 是两个无符号类型的数组（成员 0 和 1），提供了 64 位的宽度，如图 8.21 所示。定义在 `signal.h` 中的 `sigset_t` 在本质上与 `k_sigset_t` 相同，只是大小是两倍（`sigset_t` 使用数组，而 `k_sigset_t` 使用两个）。

```
typedef struct {
    unsigned long _sigbits[2];
} k_sigset_;
```

通过设置对应信号号的位发布信号

| _sigbits[1] | _sigbits[0] |
| :--- | :--- |
| 32 | |

图 8.21 k_sigset_t 类型中的信号表示

# 8.7.1 信号实现

对 Solaris 实现的讨论反映了 Solaris 2.5 中的代码。该讨论适用于 Solaris 2.5 到 Solaris 7 的所有版本。

Solaris 多线程架构为开发符合 POSIX 等行业标准的 UNIX 信号语义带来了一些有趣的挑战。信号通过两个定义的阶段：产生和传递。信号产生是信号的起点——发送阶段。当为忽略信号建立处置时，则认为信号已传递。如果信号被阻塞（即推迟传递），则被视为挂起（pending）。

Solaris 环境中的用户线程（通过显式调用 `thr_create(3)` 或 `pthread_create(3)` 创建）每个都有自己的信号掩码。线程可以独立于同一进程中的其他线程选择阻塞信号；因此，在进程执行的不同期间，不同的线程可能用于传递不同的信号。线程库（POSIX 和

