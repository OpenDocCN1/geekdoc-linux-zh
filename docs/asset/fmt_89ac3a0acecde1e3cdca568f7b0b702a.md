
首先，如果 `set` 不是空指针，则通过 `oset` 返回原来的信号掩码。其次，如果 `set` 不是空指针，则 `how` 参数指示如何修改信号掩码。图 10.13 描述了 `how` 的可能值。

| how | 描述 |
| :--- | :--- |
| `SIG_BLOCK` | 新的信号掩码是当前掩码与 `set` 指向集合的并集。注意 `SIGKILL` 和 `SIGSTOP` 不能被阻塞。 |
| `SIG_UNBLOCK` | 新的信号掩码是当前掩码与 `set` 指向集合的交集。`set` 包含了我们要解锁的信号。 |
| `SIG_SETMASK` | 新的信号掩码由 `set` 指向的值替换。 |

如果 `set` 是空指针，则信号掩码由 `how` 忽略。在调用 `sigprocmask` 之后，如果任何阻塞的信号是挂起的，这些信号将传递给进程。如果 `set` 为空指针，则信号掩码不改变。`sigprocmask` 函数仅为单线程进程定义。我们在 12.8 节讨论这一点。

### 示例

图 10.14 显示了一个打印信号掩码中信号名称的函数。

```c
#include "apue.h"

#include <errno.h>

void

pr_mask(const char *str)

{

    sigset_t sigset;

    int errno_save;

    errno_save = errno;    /* 可以被信号处理程序调用 */

    if (sigprocmask(0

```
（此处代码省略）

图 10.14 打印信号掩码

为了节省空间，没有测试信号掩码中的每个信号。（见练习 10.9）。

## 10.13 sigpending 函数

`sigpending` 函数返回对于调用进程被阻塞传递且当前挂起的信号集。该集合通过 `set` 参数返回。

```c
#include <signal.h>

int sigpending(sigset_t *scf);

返回：如果成功返回 0，错误返回 -1
```

### 示例

图 10.15 显示了我们描述的许多信号功能。

```c
#include "apue.h"

static void sig_quit(int)

int

main(void)

{

    sigset_t newmask, oldmask, pendmask;

    if (signal(SIGQUIT, sig_quit) == SIG_ERR)

        err_sys("can't catch SIGQUIT");

    /*

     * 阻塞 SIGQUIT 并保存当前信号掩码。

     */

    sigemptyset(&newmask);

    sigaddset(&newmask, SIGQUIT);

    if (sigprocmask(SIG_BLOCK, &newmask, &oldmask) < 0)

        err_sys("SIG_BLOCK error");

    sleep(5); /* SIGQUIT 在此处将保持挂起 */

    if (sigpending(&pendmask) < 0)

        err_sys("sigpending error");

    if (sigismember(&pendmask, SIGQUIT))

        printf("\nSIGQUIT pending\n");

    /*

     * 恢复解锁 SIGQUIT 的信号掩码。

     */

    if (sigprocmask(SIG_SETMASK, &oldmask, NULL) < 0)

        err_sys("SIG_SETMASK error");

    printf("SIGQUIT unblocked\n");

    sleep(5); /* SIGQUIT 在此处将导致终止并生成核心文件 */

    exit(0);

}

static void

sig_quit(int signo)

{

    printf("caught SIGQUIT\n");

    if (signal(SIGQUIT, SIG_DFL) == SIG_ERR)

        err_sys("can't reset SIGQUIT");

}
```

图 10.15 信号集和 `sigprocmask` 示例

进程阻塞了 `SIGQUIT`，保存了其当前信号（以便稍后恢复），然后进入 5 秒的睡眠。在此期间发生的任何退出信号都会被阻塞，并且在信号取消阻塞之前不会被递送。在 5 秒睡眠结束时，我们检查信号是否处于挂起（`pending`）状态并取消阻塞该信号。

我们在阻塞信号时记录了旧的掩码（`old mask`）。为了解锁信号，我们使用该旧掩码的 `SIG_SETMASK`。或者，我们使用 `SIG_UNBLOCK` 仅解锁我们阻塞的那个信号。请注意，如果我们写了一个可以被他人调用的函数，并且在函数中需要阻塞某个信号，我们就不能使用 `SIG_UNBLOCK` 来解锁信号。在这种情况下，我们必须使用 `SIG_SETMASK` 将信号掩码恢复到先前的值，因为调用者在调用我们的函数之前可能特意阻塞了该信号。我们将在 10.18 的系统函数中看到此示例。

如果我们在这个睡眠期间生成了退出信号，该信号现在处于挂起状态且未被阻塞，因此它会在 `sigprocmask` 返回之前被递送。我们将看到这一点，因为信号处理程序中的 `printf` 输出将先于 `sigprocmask` 调用之后的 `printf`。

进程再次睡眠 5 秒。如果我们在这个睡眠期间生成了退出信号，该信号应该终止进程，因为我们在捕获到它时将该信号的处理重置为了默认值。在以下输出中，当我们输入 `Control-backslash`（终端字符）时，终端会打印 `'`：

```text
$ /a.out	生成一次信号（在 5 秒结束前）

SIGQUIT pending	从睡眠中返回后

caught SIGQUIT	信号处理程序中的信号

SIGQUIT unblocked	从 sigprocmask 返回后

'Quit(coredump)	再次生成信号

$ /a.out

'\\\\\\\\\\\\\\\\\\'	生成 10 次信号（在 5 秒结束前）

SIGQUIT pending	仅生成一次信号

caught SIGQUIT

SIGQUIT unblocked

'Quit(coredump)	再次生成信号
```

当子进程异常终止时，shell 会打印 `quit(coredump)` 消息。注意，当我们第二次运行程序，在进程睡眠时生成了 10 次退出信号，但在信号取消阻塞时，只向进程递送了一次。这证明了信号在此并不队列。

## 10.14 sigaction 函数

`sigaction` 函数允许我们检查或修改与特定信号相关的动作。该函数取代了早期 UNIX 系统的信号处理函数。在本节末尾，我们将展示 `sigaction` 的实现。

```c
#include <signal.h>

int sigaction(int signo, const struct sigaction *restrict act,
               struct sigaction *restrict oact);

```

返回 0

参数是我们正在检查或修改的信号号。如果 `act` 指针不为空，则我们正在修改动作。如果 `oact` 指针不为空，系统通过 `oact` 返回信号之前的动作。此函数使用以下结构：

```c
struct sigaction {
    void    (*sa_handler)(int);    /* 信号处理函数地址， */
                             /* 或 SIG_IGN, SIG_DFL */

    sigset_t sa_mask;               /* 要阻塞的其他信号 */

    int      sa_flags;              /* 信号选项，图 10.16 */

};
```

在更改信号动作时，如果 `sa_handler` 字段包含信号处理函数的地址（而不是 `SIG_IGN` 或 `SIG_DFL` 常量），`sa_mask` 字段指定了调用信号处理函数之前添加到进程信号掩码的信号。当信号处理函数返回时，进程的信号掩码恢复到之前的值。通过这种方式，我们在调用信号处理程序时可以阻塞某些信号。操作系统允许在处理信号期间返回到 10.8 节，相同信号的后续发生通常不会队列。如果信号在阻塞时发生了五次，该信号的处理函数将仅调用一次（这一特性在之前的示例中已有说明）。

一旦为信号安装了动作，它将一直保持直到通过调用 `sigaction` 进行显式更改。与不可靠的早期系统不同，POSIX.1 要求处理器保持直到被显式更改。

`act` 结构的 `sa_flags` 字段指定了该信号处理器的各种选项。图 10.16 详细说明了设置这些选项时的含义。如果标志是 POSIX.1 规范的一部分，则包含 SUS；如果是 XSI 选项的一部分，则包含 XSI。

`sa_sigaction` 字段是在使用 `SA_SIGINFO` 标志配合 `sigaction` 时使用的替代信号处理函数。实现可能会对 `sa_sigaction` 字段和 `sa_handler` 字段使用相同的存储，因此应用程序一次只能使用这些字段之一。

## 第 10.14 节 sigaction 函数 351

| 选项 | SUS | FreeBSD 8.0 | Linux 3.2.0 | Mac OS X 10.6.8 | Solaris 10 |  |
|---|---|---|---|---|---|
| `SA_SIGINFO` | | | | | 如果设置 `SA_SIGINFO` 标志，信号处理程序作为 `void handler(int signo, siginfo_t *info, void *context)` 调用。 |
| `SA_SIGINFO` | | | | | 如果设置 `SA_SIGINFO` 标志，信号处理程序作为 `void handler(int signo, siginfo_t *info, void *context)` 调用。 |
| `SA_STOP` | | | | | 如果设置 `SA_SIGINFO` 标志，信号处理程序作为 `void handler(int signo, ...)` 调用。 |
| `SA_NOCLD` | | | | | 如果信号是 `SIGCHLD`，则 `si_pid`、`si_status` 和 `si_uid` 字段将被设置。 |
| `SA_LDWAIT` | | | | | 如果信号是 `SIGCHLD`，系统将等待子进程。 |
| `SA_NODEFER` | | | | | 如果信号在阻塞时发生，则不进入队列。 |
| `SA_ONSTACK` | | | | | 信号处理程序在用户提供的栈上执行。 |
| `SA_RESTART` | | | | | 如果信号被中断，系统调用将自动重启。 |

图 10.16 每个信号的选项 (`sa_flags`)

## 352 信号 第 10 节

通常，处理程序作为 `void handler(int signo)` 调用；如果设置了 `SA_SIGINFO` 标志，信号处理程序作为 `void handler(int signo, siginfo_t *info, void *context)` 调用；它包含了关于生成信号的信息。所有符合 POSIX 的实现必须至少包含以下内容：

```c
struct siginfo {
    int si_signo;          /* 信号号 */
    int si_errno;          /* 如果非零，来自 errno 的错误号 */
    int si_code;           /* 附加信息（取决于信号） */
    pid_t si_pid;          /* 发送进程 ID */
    uid_t si_uid;          /* 发送进程真实 ID */
    void *si_addr;         /* 导致故障的地址 */
    int si_status;         /* 退出值或信号号 */
    union sig_value;      /* 特定的值 */
    /* 可能还有其他字段 */
};
```
信号联合包含以下字段：

```c
int sival_int;
void *sival_ptr;
```

在递送信号时，应用程序在 `si_value.sival_int` 中传递整数值，或在 `si_value.sival_ptr` 中传递指针值。图 10.7 显示了单 Unix 规范定义的各种信号的 `si_code`。如果信号是 `SIGCHLD`，`si_pid`、`si_status` 和 `si_uid` 字段将被设置。如果信号是 `SIGBUS`、`SIGILL`、`SIGFPE` 或 `SIGSEGV`，`si_addr` 包含负责故障的地址，尽管地址可能并不准确。`si_errno` 字段包含导致生成信号的情况对应的错误号，尽管其用途由实现定义。信号处理程序的上下文是一个类型指针，可以转换为 `ucontext_t` 结构，用于标识信号递送时的进程上下文。该结构至少包含以下内容：

```c
ucontext_t *uc_link;      /* 指向此上下文返回时恢复的上下文的指针 */
sigset_t uc_sigmask;        /* 此上下文阻塞的信号掩码 */
                            /* 激活状态 */
stack_t uc_stack;           /* 此上下文使用的栈 */
mcontext_t uc_mcontext;    /* 保存上下文的机器特定表示 */
```

## 第 10.14 节 sigaction 函数 353

`uc_stack` 字段描述了当前上下文所使用的栈。它至少包含以下成员：

```c
void *ss_sp;           /* 栈基地址或指针 */
size_t ss_size;        /* 栈大小 */
int   ss_flags;        /* 标志 */
```

当实现支持实时信号扩展时，使用 `SA_SIGINFO` 标志位建立的信号处理程序将导致信号可靠地队列。有一组独立的保留信号编号可供实时应用程序使用。可以使用 `sigqueue` 函数（第 10.20 节）通过信号传递信息。

| 信号 | 操作码 | 原因 |
|---|---|---|
| `SIGILL` | `ILL_ILLOPC` | 非法操作数 |
| | `ILL_ILLOWN` | 非法寻址 |
| | `ILL_LLADR` | 非法陷阱 |
| | `ILL_LTR` | 特权操作码 |
| | `ILL_PRREG` | 特权寄存器 |
| | `ILL_COPROC` | 协处理器错误 |
| | `ILL_BADSTK` | 内部栈错误 |
| `SIGFPE` | `FPE_INTDIV` | 整数除零 |
| | `FPE_INTDIVV` | 浮点数除零 |
| | `FPE_FLTOV` | 浮点溢出 |
| | `FPE_FLUND` | 浮点数不精确 |
| | `FPE_FLRES` | 无效浮点操作 |
| | `FPE_FLTIN` | 下标越界 |
| | `FPE_FLSUB` | |
| `SIGSEGV` | `SEGV_MAPERR` | 地址未映射到对象 |
| | `SEGV_ACC` | 映射对象的权限无效 |
| `SIGBUS` | `BUS_ADRLN` | 无效的对齐 |
| | `BUS_ADDR` | 非驻留物理地址 |
| | `BUS_OBJERR` | 对象特定的硬件错误 |
| `SIGTRAP` | `TRAP_BRKT` | 进程断陷阱 |
| | `TRAP_TRACE` | 进程跟踪陷阱 |
| `SIGCHLD` | `CLD_EXITED` | 子进程退出 |
| | `CLD_KILLED` | 子进程异常终止（无核心转储） |
| | `CLD_DUMPED` | 子进程带核心转储异常终止 |
| | `CLD_TRAPPED` | 被跟踪的子进程发生陷阱 |
| | `CLD_STOPPED` | 子进程已停止 |
| | `CLD_CONTINUED` | 已停止的子进程已继续 |
| Any | `SI_USER` | `kill` 发送的信号 |
| | `SI_QUEUE` | `sigqueue` 发送的信号 |
| | `SI_TIMER` | `timer_settime` 设置的定时器超时 |
| | `SI_ASYNC` | 异步 I/O 请求完成 |
| | `SI_MESQ` | 消息队列到达（实时扩展） |

图 10.17 `siginfo_t` 代码值

## 信号函数

示例 – 现在使用 `sigaction` 实现 `signal` 函数。这是许多平台所采用的方法（POSIX.1 理由性说明中的注释也指出这是 POSIX 的意图）。另一方面，具有二进制限制的系统可能会提供一个支持旧的、不可靠信号语义的 `signal` 函数。除非你明确需要这些旧的、不可靠的语义（为了向后兼容），否则你应该使用以下 `signal` 实现或直接调用 `signal`。（正如你可能猜到的，使用旧语义实现的 `signal` 可能导致 `sigaction` 无法指定 `SA_RESETHAND` 和 `SA_NODEFERR`）本文中的所有示例都调用了图 10.18 所示的 `signal` 函数。

```c
#include "apue.h"

/* signal() 的可靠版本，使用 POSIX sigaction()。 */

Sigfunc *

signal(int signo, Sigfunc *func)

{

    struct sigaction act, oact;

    act.sa_handler = func;

    sigemptyset(&act.sa_mask);

    act.sa_flags = 0;
```
