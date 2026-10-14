
| `SIGTTOU` | 27 | 停止 | 已停止 – tty 输出（参见 `termio(7I)`） |
| `SIGVTALRM` | 28 | 退出 | 闹钟 – `setitimer(2)`、`ITIMER_VIRTUAL` |
| `SIGPROF` | 29 | 退出 | 性能分析闹钟 – `setitimer(2)`、`ITIMER_PROF` 和 `ITIMER_REALPROF` |
| `SIGXCPU` | 30 | 核心转储 | 超出 CPU 时间限制（参见 `getrlimit(2)`） |
| `SIGXFSZ` | 31 | 核心转储 | 超出文件大小限制（参见 `getrlimit(2)`） |
| `SIGWAITING` | 32 | 忽略 | 线程库使用的并发信号 |
| `SIGLWP` | 33 | 忽略 | 线程库使用的 LWP 间信号 |
| `SIGFREEZE` | 34 | 忽略 | 检查点挂起 |
| `SIGTHAW` | 35 | 忽略 | 检查点恢复 |
| `SIGCANCEL` | 36 | 忽略 | 线程库使用的取消信号 |
| `SIGLOST` | 37 | 忽略 | 资源丢失 |
| `SIGRTMIN` | 38 | 退出 | 最高优先级实时信号 |
| `SIGRTMAX` | 45 | 退出 | 最低优先级实时信号 |

`SIGLOST` 首次出现在 Solaris 2.6 中。2.5 和 2.5.1 版本未定义此信号，其 `SIGRTMIN` 和 `SIGRTMAX` 分别位于信号编号 37 和 44。内核将 `MAXSIG`（用户代码可在 `/usr/include/sys/signal.h` 中使用）定义为符号常量，用于内核信号支持代码的多个位置。`MAXSIG` 在 Solaris 2.5 和 2.5.1 中为 44，在 Solaris 2.6 和 Solaris 7 中为 45。另外，`SIGPOLL` 和 `SIGIO` 都被定义为信号编号 22。`SIGIO` 是进程通过 `aio_read(3)` 或 `aio_write(3)`（或 POSIX 等效的 `aio_read(3R)` 或 `aio_write(3R)`）发出异步读或写时产生的，用于通知进程 I/O 已完成或发生错误。`SIGPOLL` 是一个更通用的指示符，表示已发生可轮询事件。

信号的处理方式可以从其默认值更改，进程可以安排捕获信号并调用自己的信号处理例程，或者忽略其默认处理方式并非忽略的信号。唯一的例外是 `SIGKILL` 和 `SIGSTOP`——这两个信号的默认处理方式无法更改。定义和更改信号处理方式的接口是 `signal(3C)` 和 `sigset(3C)` 库以及 `sigaction(2)` 系统调用。

信号也可以被阻塞，这意味着进程或线程暂时阻止了信号的传递。已阻塞信号的产生会导致该信号在进程中保持挂起（pending）状态，直到显式解除阻塞或处理方式被更改为忽略。用于阻塞信号的信号掩码存在于线程内和用户线程级别；`t_hold` 结构成员（内核和用户线程中使用相同名称）是 `sigset_t` 数据类型，使用置位来表示被阻塞的信号。`sigprocmask(2)` 系统调用为调用它的 kthread 设置或获取信号掩码。非线程进程有一个 LWP/kthread 对；因此，kthread 中的 `t_hold` 就成了进程级的信号掩码。一个等效的接口——`thr_setsigmask(3T)` 和 `pthread_sigmask(3T)`——在用户线程级别设置和获取信号掩码（用户线程结构中的 `t_hold`）。

`psig(1)` 命令列出进程的信号动作。下面的示例转储了我们的 ksh 进程的信号动作；为节省篇幅，我们省略了一些行。

```text
$ /usr/proc/bin/psig 448
448:       -ksh
HUP       caught  RESTART
INT       caught  RESTART
QUIT      caught  RESTART
ILL       caught  RESTART
TRAP      caught  RESTART
ABRT      caught  RESTART
EMT       caught  RESTART
FPE       caught  RESTART
KILL      default
BUS       caught  RESTART
SEGV      default
SYS       caught  RESTART
PIPE      caught  RESTART
ALRM      caught  RESTART
TERM      ignored
USR1      caught  RESTART
USR2      caught  RESTART
CLD       default NOCLDSTOP
PWR       default
          .
          .
          .
RTMAX     default
```

回顾一下，信号可以出于多种原因源自多个不同地方。`SIGHUP`、`SIGINT` 和 `SIGQUIT` 通常由控制终端的键盘输入（`SIGINT` 和 `SIGQUIT`）产生，或者如果控制终端断开连接，则产生 `SIGHUP`。注意，使用 `nohup(1)` 命令可以将 `SIGHUP` 的处理方式设置为忽略，从而使进程“免疫”挂断。其他与终端 I/O 相关的信号包括 `SIGTSTP`、`SIGTTIN`、`SIGTTOU` 和 `SIGSTOP`。对于源自键盘命令的信号，导致这些信号产生的实际键序列在终端会话的参数中定义，通常由 `stty(1)` 设置。例如，^C [Control-C] 通常是中断键序列，会导致 `SIGINT` 发送到进程，该信号的默认处理方式是强制进程退出。

在指令执行期间遇到错误而直接产生的信号，首先会触发系统上的硬件陷阱。不同的处理器架构定义了各种陷阱，这些陷阱会导致控制立即以向量方式转移给内核陷阱处理函数。Solaris 内核会根据 Solaris 环境所支持的处理器架构规范来构建陷阱表，并在相应位置插入陷阱处理例程：SPARC V7（早期 sun4 架构）、SPARC V8（SuperSPARC——sun4m 和 sun4d 架构）、SPARC V9（UltraSPARC——sun4u 架构）以及 Intel x86。（在 Intel 术语中，这些例程称为中断描述符表，即 IDT；在 SPARC 上，它们称为陷阱表。）内核安装的陷阱处理程序最终会向导致陷阱的线程产生一个信号。由硬件陷阱产生的信号包括 `SIGILL`、`SIGFPE`、`SIGSEGV`、`SIGTRAP`、`SIGBUS` 和 `SIGEMT`。表 8-8 列出了 UltraSPARC 的陷阱和信号。

### 表 8-8 *UltraSPARC 陷阱及产生的信号*

| 陷阱名称 | 信号 |
|---|---|
| `instruction_access_exception` | `SIGSEGV, SIGBUS` |
| `instruction_access_MMU_miss` | `SIGSEGV` |
| `instruction_access_error` | `SIGBUS` |
| `illegal_instruction` | `SIGILL` |
| `privileged_opcode` | `SIGILL` |
| `fp_disabled` | `SIGILL` |
| `fp_exception_ieee_754` | `SIGFPE` |
| `fp_exception_other` | `SIGFPE` |
| `tag_overflow` | `SIGEMT` |
| `division_by_zero` | `SIGFPE` |
| `data_access_exception` | `SIGSEGV, SIGBUS` |
| `data_access_MMU_miss` | `SIGSEGV` |
| `data_access_error` | `SIGBUS` |
| `data_access_protection` | `SIGSEGV` |
| `mem_address_not_aligned` | `SIGBUS` |
| `privileged_action` | `SIGILL` |
| `async_data_error` | `SIGBUS` |

信号也可能源于终端 I/O 和错误陷阱条件以外的来源；进程引起的（例如 `SIGXFSZ`）和外部事件（`kill(2)`）也能产生信号。例如：

- 应用程序可以通过定义 `SIGUSR1` 或 `SIGUSR2` 的处理程序并在进程之间发送这些信号，创建用户自定义信号作为一种略显粗糙的进程间通信形式。如果进程超过其处理器时间资源限制，内核会发送 `SIGXCPU`；如果文件写入超过文件大小资源限制，则发送 `SIGXFSZ`。调用 `abort(3C)` 库函数会产生 `SIGABRT`。如果进程正在向管道写入数据，而读取方已终止，则会产生 `SIGPIPE`。
