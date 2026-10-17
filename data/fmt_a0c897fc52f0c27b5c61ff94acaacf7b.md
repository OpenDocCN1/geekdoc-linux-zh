
| SIGPWR | 19 | Ignore | 电源无故障 |
| SIGWINCH | 20 | Ignore | 窗口大小变化 |
| SIGURG | 21 | Ignore | 紧急情况 |
| SIGPOLL | 22 | Exit | 可轮询事件 |
| SIGIO | 22 | Exit | 信号完成 |
| SIGSTOP | 23 | Stop | 停止（不可被捕获或忽略） |
| SIGTSTP | 24 | Stop | 停止 – 作业控制 |
| SIGCONT | 25 | Stop | 继续 |
| SIGTTIN | 26 | Stop | 停止 – 输入（参考 `termio(7)`） |
| SIGTTO | 27 | Stop | 停止 – 输出（参考 `termio(7)`） |
| SIGALRM | 28 | Exit | 虚拟闹钟 – `setimer(2)` |
| SIGPROF | 29 | Exit | 分析闹钟 – `setimer(2)` |
| SIGCPU | 30 | Core | CPU 时间超出限制 |
| SIGXZ | 31 | Core | 文件超出限制 |
| SIGWAIT | 32 | Ignore | 并发信号 |
| SIGLWP | 33 | Ignore | LWP 间信号 |
| SIGFREE | 34 | Ignore | 检查点暂停 |
| SIGTHAW | 35 | Ignore | 检查点恢复 |
| SIGCANCEL | 36 | Ignore | 取消信号 |
| SIGLOST | 37 | Ignore | 资源丢失 |
| SIGRTMIN | 38 | Exit | 最高优先级实时信号 |
| SIGRTMAX | 45 | Exit | 最低优先级实时信号 |

# `psig(1)` 命令列出进程的信号动作

下面的示例导出了我们 `ksh` 进程的信号动作；为了节省空间，我们省略了一些行。

```
$ /usr/proc/bin/psig 448
448:
  -ksh
  HUP  caught RESTART
INT   caught RESTART
QUIT  caught RESTART
JLL   caught RESTART
TRAP  caught RESTART
ABRT  caught RESTART
EMT   caught RESTART
FPE   default
KILL  caught RESTART
BUS   default
SEGV  default
SYS   caught RESTART
PIPE  caught RESTART
ALRM  caught RESTART
TERM  ignored
USR1  caught RESTART
USR2  caught RESTART
CLO   default NOCLDSTOP
PWR   default
```

请记住，由于各种原因，信号可以源于几个不同的地方。`SIGHUP`、`SIGINT` 和 `SIGQUIT` 通常由来自控制终端的键盘输入（`SIGINT` 和 `SIGQUIT`）产生，或者在控制终端断开时产生 `SIGHUP`。请注意，使用 `nohup(1)` 命令通过将 `SIGHUP` 的处理设置为忽略，使进程对挂起产生“免疫”。与其他 I/O 相关的信号包括 `SIGSTOP`、`SIGT`、`SIGTOU` 和 `SIGSTPE`。对于源自键盘命令的信号，产生这些信号的实际键序列在终端会话的参数中定义，通常通过 `stty(1)`。`Control-C` 通常是中断键，会导致向进程发送 `SIGINT`，该信号的默认派发是强制进程退出。

执行期间期间遇到错误直接生成的信号从系统上的硬件陷阱开始。不同的处理器架构定义了各种陷阱，导致控制权立即转移到内核陷阱处理函数。Solaris 内核根据 Solaris 环境的架构规范构建一个表并在适当的位置插入陷阱处理例程序：SPARC V7（早期 sun4 架构）、SPARC V8（SuperSPARC—sun4m 和 sun4d 架构）、SPARC x86。（术语上这些程序称为中断描述表，或 IDTs。在 SPARC 上，它们被称为陷阱表）。内核安装的陷阱处理器最终会向导致陷阱的线程产生信号。硬件陷阱产生的信号包括 `SIGILL`、`SIGFPE`、`SIGSEV`、`SIGTRAP`、`SIGBUS` 和 `SIGEMT`。表 8-8 列出了 UltraSPARC 的陷阱和产生的信号。

## 表 8-8 UltraSPARC 陷阱及产生的信号

| 陷阱名称 | 信号 |
|--- |--- |
| instruction_access_exception | SIGSEGV, SIGBUS |
| instruction_access_MMU_miss | SIGSEGV |
| instruction_access_error | SIGBUS |
| illegal_instruction | SIGILL |
| privileged_opcode | SIGILL |
| fp_disabled | SIGILL |
| fp_exception_754 | SIGFPE |
| fp_exception_other | SIGFPE |
| tag_overflow | SIGEMT |
| division_by_zero | SIGFPE |
| data_access_exception | SIGSEGV, SIGBUS |
| data_access_MMU_miss | SIGSEGV |
| data_access_error | SIGBUS |
| data_access_protection | SIGSEGV |
| mem_address_not_aligned | SIGBUS |
| privileged_action | SIGILL |
| async_data_error | SIGBUS |

信号可以源于终端 I/O 和错误条件以外的源；进程引发（例如 `SIGXFSZ`）和外部事件（`kill()`）也可以产生信号。例如：

- 应用程序可以通过定义 `SIGUSR1` 或 `SIGUSR2` 的处理程序并在进程之间发送这些信号，作为一种粗略的进程间通信形式创建用户自定义信号。当进程超过其处理器时间资源限制时，内核会发送 `SIGCPU`，或者发送 `SIGFSZ`。

# 表 8-9 `sigqueue` 结构（续）

| 字段名称 | 数据类型 | 说明 |
| --- | --- | --- |
| `sq_func` | pointer | 函数指针—引用析构函数指针 |
| `sq_backptr` | pointer | 指向与上述相关的数据结构 |

`sigqueue` 结构为 `siginfo` 结构形成的链表提供了一个框架，该链表在进程级别维护，对于多线程进程，则在 LWP/线程级别维护。`siginfo` 为许多不同类型的信号存储了各种位信息。该结构内部包含几个联合体（在某些情况下是嵌套联合体），因此可用数据取决于运行时结构是如何实例化的的。出于可读性考虑，此处未显示所有的联合体声明。

![](img/6356e5c1a4c2ea1083732d1b35e8cf75_373_0.png)

图 8.22 信号相关的结构

`siginfo` 数据对于需要了解更多信号生成原因的进程（准确来说是程序）可用。`sigaction(2)` 系统调用以程序方式提供了这些信息。`sigaction` 结构中 `sa_flags` 字段中可选的 `SA_SIGINFO` 标志会导致向信号处理程序传递两个额外的参数（当然，假设信号位置必须被捕获）。第一个参数总是信号号。第二个参数不为 NULL 则指向 `siginfo` 结构的指针，第三个参数是指向 `ucontext_t` 结构的指针，它包含了信号递送时接收进程的硬件信息（栈指针、信号掩码和寄存器内容）。当产生陷阱（trap）时，`siginfo` 数据对于调试非常有用；例如，在 `SIGSE` 或 `SIGFPE` 的情况下，在准备发送信号时，可以从内核池到 `siginfo` 的数据中获取有关陷阱底层原因的更具体信息。（参见 `sigaction(2)`、`siginfo(5)` 和 `ucontext(5)` 手页。）

# 表 8-10 `siginfo` 结构

| 结构或联合体 | 字段名称 | 数据类型 | 说明 |
|---|---|---|---|
| struct siginfo | `si_sign` | 整数 | 信号号 |
| | `si_code` | 整数 | 与信号相关的代码 |
| | `si_errno` | 整数 | 系统调用 errno |
| union _proc | `pid` | `pid_t` | 在 `kill(2)`、SIGLD 和 `sigqueue()` 中发起的进程 ID |
| | `status` | int | 子进程退出状态 |
| | `stime` | `clock_t` | 子进程系统时间 |
| | `utime` | `clock_t` | 子进程用户时间 |
| | `uid` | `uid_t` | UID |
| | `value` | int | |
