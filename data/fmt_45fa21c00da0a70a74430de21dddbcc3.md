
尽管 `sleep` 可以用 `alarm` 函数实现，这两个函数之间存在交互。POSIX.1 标准对所有这些交叉点均未规定。例如，如果我们执行 `alarm(10)` 并在 3 秒后执行 `sleep(5)`，会发生什么？`sleep` 将在 5 秒后返回（假设没有捕获到其他信号），但 2 秒后会产生另一个 `SIGALRM`。这些细节取决于具体实现。

> `FreeBSD` 8.0、`Linux` 3.2.0、`Mac OS X` 10.6 和 `Solaris` 10 使用 `nanosleep` 函数实现 `sleep`，这使得实现独立于信号和闹钟定时器。为了移植性，你不应该对 `sleep` 的实现做任何假设，但如果你打算将 `sleep` 调用与其他任何计时函数混合，你必须意识到可能的交互。

### 示例

10.29 显示了 POSIX.1 `sleep` 函数的实现。该函数是图 10.7 的修改，它可靠地处理信号，避免了早期实现中的竞态条件。我们仍然处理与之前设置的闹钟的任何交互。（如所述，这些交互在 POSIX.1 中是未定义的。）

```c
#include "apue.h"

static void
sig_alarm(int signo)
{
    /* 什么都不做，只需返回即可唤醒 sigsuspend() */
}

unsigned int
sleep(unsigned int seconds)
{
    struct sigaction newact, oldact;
    sigset_t newmask, oldmask, susmask;
    unsigned int unsplept;

    /* set our handler, save previous information */
    newact.sa_handler = sig_alarm;
    sigemptyset(&newact.sa_mask);
    newact.sa_flags = 0;
    sigaction(SIGALRM, &newact, &oldact);

    /* block SIGALRM and save current signal mask */
    sigemptyset(&newmask);
    sigaddset(&newmask, SIGALRM);
    sigprocmask(SIG_BLOCK, &newmask, &oldmask);

    alarm(seconds);
    susmask = oldmask;

    /* make sure SIGALRM isn't blocked */
    sigdelset(&susmask, SIGALRM);

    /* wait for any signal to be caught */
    sigsuspend(&susmask);

    /* some signal has been caught, SIGALRM is now blocked */
    unsplept = alarm(0);

    /* reset previous action */
    sigaction(SIGALRM, &oldact, NULL);

    /* reset signal mask, which unblocks SIGALRM */
    sigprocmask(SIG_SETMASK, &oldact, NULL);

    return(unsplept);
}
```

图 10.29 可靠的 `sleep` 实现

编写这个可靠的实现所需的代码比图 10.7 中显示的要多。我们没有使用在图 10.8 中使用的任何非局部分支，以避免 `alarm` 和 `pause` 之间的竞态条件，因此对于在处理 `SIGALRM` 时可能正在执行的其他信号处理程序没有影响。

`nanosleep` 函数与 `sleep` 函数相似，但它提供了纳秒级的粒度。

```c
#include <time.h>

int nanosleep(const struct timespec *reqtp, struct timespec *rem);
// 返回: 如果睡眠了请求的时间则返回 0，出错则返回 -1
```

该函数挂起调用进程，直到请求的时间通过或函数被信号中断。`reqtp` 参数指定了以秒和纳秒为单位的睡眠时间。如果睡眠间隔被信号中断且进程没有终止，则指向 `rem` 参数的 `timespec` 结构将被设置为睡眠间隔中剩余的时间。如果我们对剩余的时间不感兴趣，可以将此参数设置为 `NULL`。

如果系统不支持 `nanosleep` 粒度，请求的时间将向上取整。`nanosleep` 函数不涉及任何信号的产生，我们可以使用它而无须担心与其他函数的交互。

`nanosleep` 函数曾经属于单 `Unix` `UNIX` 规范中的 `Timer` 选项，但在 `Susv4` 中移动到了基础部分。

随着多个系统时钟的引入（回顾第 6.10 节），我们需要一种方法使用特定时钟的延迟时间来挂起调用线程。`clock_nanosleep` 函数为提供了这种能力。

```c
#include <time.h>

int clock_nanosleep(clock_t clock_id, int flags,
                    const struct timespec *reqtp, struct timespec *rem);
// 返回: 如果睡眠了请求的时间则返回 0，失败则返回错误
```

`clock_id` 参数指定了评估时间延迟的时钟。时钟的标识符列在图 6.8 中。`flags` 参数用于控制延迟是绝对的还是相对的。当 `flags` 设置为 0 时，睡眠时间是相对的（即我们想要睡眠多久）。当它被设置为 `TIMER_ABSTIME` 时，睡眠时间是绝对的（即我们想要睡眠直到时钟到达指定的时间）。

其他参数 `reqptim` 和 `rem` 与 `nanosleep` 函数中的参数相同。然而，`rem` 参数是未使用的，它是不需要的；我们可以对 `reqptim` 参数重用相同的值进行对 `clock_nanosleep` 的后续调用，直到时钟达到指定的绝对时间值。

注意，对于错误，该调用

```c
clock_nanosleep(CLOCK_REALTIME, 0, reqptim, rem);
```

的效果与调用

```c
nanosleep(reqptim, rem);
```

相同。

使用相对睡眠的问题是，某些应用程序对睡眠时长有精确要求，而相对时间可能会导致时间比预期的更长。例如，如果一个应用程序需要定期执行某个任务，它必须获取当前时间，计算到下次执行任务所需的时间，然后调用 `nanosleep`。在获取时间到调用 `nanosleep` 之间，处理器的调度和抢占可能会导致相对睡眠时间超出预期的间隔。使用绝对时间可以提高精确度，尽管分时处理器调度器无法保证我们的任务会在我们的睡眠时间结束后立即执行。

在旧版本的单 `Unix` `UNIX` 规范中，`nanosleep` 函数属于 `Clock Selection` 选项。在 `Susv4` 中，它被移动到了基础部分。

## 10.20 sigqueue

在第 10.8 节中，我们提到 `UNIX` 系统不队列信号。随着 POSIX.1 实时扩展的引入，某些系统开始支持信号队列。在 `SUSv4`，队列信号功能已从实时扩展移动到了基础规范。

通常，一个信号携带一个位的信息：信号本身。除了队列信号外，这些扩展还允许应用程序在递送时传递更多信息（回顾第 10.14 节）。这些信息嵌入在 `siginfo` 结构中。除了系统提供的信息外，应用程序还可以向信号处理程序传递整数或指向包含更多信息的缓冲区指针。

要使用队列信号，我们必须执行以下操作：

1. 在使用 `sigaction` 函数安装信号处理程序时，指定 `SA_SIGINFO` 标志。如果我们不指定此标志，信号将被发布，当信号被队列化时由实现决定。

2. 在 `sigaction` 结构的 `sa_sigaction` 成员中提供信号处理程序，而不是使用通常的 `sa_handler` 字段。实现允许我们使用 `sa_handler` 字段，但我们将无法获得通过 `sigqueue` 函数发送的额外信息。

3. 使用 `sigqueue` 函数发送信号。

```c
#include <signal.h>

int sigqueue(pid_t pid, int sig, const union sigval value);
// 返回: 如果正常则返回 0，出错则返回 -1
```

`sigqueue` 函数与 `kill` 函数相似，但我们只能向单个进程发送直接信号。

使用相对睡眠的问题是，某些应用程序对睡眠时长有精确要求，而相对时间可能会导致时间比预期的更长。例如，如果一个应用程序需要定期执行某个任务，它必须获取当前时间，计算到下次执行任务所需的时间，然后调用 `nanosleep`。在获取时间到调用 `nanosleep` 之间，处理器的调度和抢占可能会导致相对睡眠时间超出预期的间隔。使用绝对时间可以提高精确度，尽管分时处理器调度器无法保证我们的任务会在我们的睡眠时间结束后立即执行。

（注：原文中存在部分重复段落，已按要求完成翻译并保持逻辑一致）

```c
#include "apue.h"
#define BUFFSIZE 1024

static void
sig_tstp(int signo) /* signal handler SIGTSTP */
{
    sigset_t mask;
    /* ... move cursor to lower left corner, reset tty mode ... */
    /*
      Unblock SIGTST, since it's blocked while we're handling it.
     */
    sigsetempty(&mask);
    sigaddset(&mask, SIGTST);
    sigprocmask(SIG_UNBLOCK, &mask, NULL);
    signal(SIGTST, SIG_DFL); /* reset disposition to default */
    kill(getpid(), SIGTST); /* and send the signal to ourselves */
    /* we won't return from the kill until we're continued */
    signal(SIGTST, sig_tstp); /* reablish signal handler */
    /* ... reset tty mode, redraw screen ... */
}

int
main(void)
{
    int n;
    char buf[BUFFERSIZE];

    /* Only catch SIGTST if we're running with a job-control shell. */
    if (signal(SIGTST, SIG_IGN) == SIG_DFL)
        signal(SIGTST, sig_tstp);

    while ((n = read(STDIN_FILENO, buf, BUFFSIZE)) > 0)
        if (write(STDOUT_FILENO, buf, n) != n)
            err_sys("write error");

    if (n < 0)
        err_sys("read error");

    exit(0);
}
```

图 10.31 如何处理 `SIGTST`

当图 10.31 中的程序启动时，它安排仅在信号的处置（disposition）为 `SIG_DFL` 时捕获 `SIGTST` 信号。原因是，当程序由一个不支持作业控制的 `shell`（例如 `/bin/sh`）启动时，信号的处置应该设置为 `SIG_IGN`。事实上，该 `shell` 并没有显式地忽略这个信号；`init` 将三个作业控制信号（`SIGTSTP`, `SIGTTIN`, `SIGTTO`）的处置设置为 `SIG_IGN`。这种处置被所有登录 `shell` 继承。作业控制 `shell` 应该将这三个信号的处置重置为 `SIG_DFL`。

当挂起（suspend）被调用时，进程接收到 `SIGTSTP` 信号并调用信号处理器。此时，进行任何与终端相关的处理：将光标移动到左下角、恢复终端模式等。然后，在将其处置重置为默认值（停止进程）并解锁信号后，恢复相同的信号 `SIGTSTP`。我们取消了阻塞（unblock），是因为我们正在处理该信号，而系统在信号被捕获时会自动阻塞它。此时，系统停止该进程。只有当进程收到 `SIGCONT` 信号（通常是来自作业控制 `shell` 响应交互式 `fg` 命令）时，它才会继续运行。我们无法捕获 `SIGCONT`。它的默认处置是继续执行停止的进程；当这种情况发生时，程序继续执行，就像从 `kill` 函数返回一样。当程序继续运行时，我们重置 `SIGTSTP` 信号的处置以及我们需要的任何终端处理（例如我们可以重绘屏幕）。

## 10.22 信号名称和编号

在本节中，我们描述了如何在信号编号和名称之间进行映射。某些系统提供了数组

```c
extern char *siglist();
```

索引是信号编号，返回一个指向信号名称字符串的指针。

`FreeBSD` 8.0、`Linux` 3.2 和 `Mac OS` 10.6.8 都提供了这个信号名称数组。`Solaris` 10 也提供，但它内部使用的是名称 *`siglist`*。

为了以可移植的方式打印与信号编号对应的字符串，我们可以使用 `psignal` 函数。

```c
#include <signal.h>

void psignal(int sig, const char *msg);
```

字符串 `msg`（通常包含程序名称）被输出到标准错误。

如果你有一个来自替代 `sigaction` 信号处理器的 `siginfo` 结构，可以使用 `psinfo` 函数打印信号信息。

```c
#include <signal.h>

void psinfo(const siginfo_t *info, const char *msg);
```

它的工作方式与 `psignal` 函数类似。虽然此函数可以获取比仅信号编号更多的信息，但不同平台打印的具体额外信息有所不同。

如果你只需要信号的字符串描述，且调用者不希望将其写入标准错误（例如你可能想将其写入日志文件），可以使用 `strsignal` 函数。该函数类似于 `strerror`（在 1.7 节中描述）。

```c
#include <signal.h>

char *strsignal(int signal);
// 返回：一个指向描述信号的字符串的指针
```

给定信号编号，`strsignal` 将返回一个描述该信号的字符串。应用程序可以使用此字符串打印有关收到的信号的错误信息。

书中讨论的所有平台都提供了 `psignal` 和 `strsignal` 函数，但存在差异。在 `Solaris` 10 上，如果信号编号无效，`strsignal` 将返回空指针，而 `FreeBSD` 8.0、`Linux` 3.2.0 和 `Mac OS X` 10.6.8 则返回一个指示该数字未定义的字符串。

只有 `Linux` 3.2 和 `Solaris` 10 支持 `psiginfo` 函数。

`Solaris` 提供了几个将信号编号映射到信号名称以及反之的函数。

```c
#include <signal.h>

int sig2str(int sign, char *str);
int str2sig(const char *str, int *sign);
// 成功返回 0，错误返回 -1
```

这些函数在编写需要信号名称和编号的交互式程序时非常有用。`sig2str` 将信号编号转换为字符串并存储在 `str` 指向的内存中。调用者必须确保内存足够容纳最长字符串。`Solaris` 在 `<signal.h>` 中定义了常量 `SIGSTR_MAX` 来定义字符串长度。字符串不包含 `SIG` 前缀。例如，翻译 `SIGKILL` 会导致缓冲区中存储 "KILL"。

`str2sig` 将名称转换为信号编号。信号编号存储在整数 `sign` 中。

注意 `sig2str` 和 `str2sig` 不设置 `errno`。

## 10.23 总结

信号用于大多数应用程序。理解信号处理的原理和方法对于高级系统编程至关重要。本章详细介绍了 `Unix` 信号。我们从观察以前实现中的缺陷及其表现开始。然后讨论了 POSIX 可靠信号概念以及所有相关函数。在涵盖这些细节后，我们提供了 `abort`、`system` 和 `sleep` 函数的实现。我们最后查看了作业控制信号以及转换名称与编号的方法。

## 练习

- 10.1 在图 10.2 中，删除 `for` 循环语句。会发生什么？为什么？
- 10.2 实现 10.22 节描述的 `sig2str` 函数。
- 10.3 画出运行图 10.9 程序时的栈帧。
- 10.4 在图 10.11 中，我们展示了使用 `setjmp` 和 `longjmp` 为 I/O 设置超时的技术。以下代码也有：

```c
signal(SIGALRM, sig_alarm);
alarm(60);
if (setjmp(env_alarm) != 0) {
    /* 处理超时 */
}
```

代码有什么问题？

- 10.5 使用单个定时器（`alarm` 或高精度定时器），提供一组允许进程设置任意数量定时器的函数。
- 10.6 编写以下程序以测试图 10.24 中的父子同步函数。程序创建一个文件并写入 0。进程 `fork` 后，父进程和子进程交替增加文件中的计数器。每次增加时，打印是哪个进程（父进程或子进程）在进行增加。
- 10.7 在图 10.25 所示函数中，如果调用者捕获 `SIGABRT` 并从信号处理器返回，我们是否会费力将处置重置为默认并再次调用，而不是直接调用 `_exit`？
- 10.8 你是否认为 10.14 节中的 `siginfo` 结构在 `si_uid` 字段中包含实际用户 ID 而不是有效用户 ID？
