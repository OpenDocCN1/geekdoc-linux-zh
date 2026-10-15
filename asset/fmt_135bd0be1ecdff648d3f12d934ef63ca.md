
# 信号处理与 system 函数实现详解

## 信号掩码与同步

```c
/* 阻塞 SIGUSR1 和 SIGUSR2，保存当前信号掩码。*/
if (sigprocmask(SIG_BLOCK, &newmask, &oldmask) < 0)
    err_sys("SIG_BLOCK error");
}

void
TELL_PARENT(pid_t pid)
{
    kill(pid, SIGUSR2);      /* 告诉父进程已完成 */
}

void
WAIT_PARENT(void)
{
    while (sigflag == 0)
        sigsuspend(&zeromask); /* 并等待父进程 */
    sigflag = 0;
}

/* 重置信号掩码为原始值。*/
if (sigprocmask(SIG_SETMASK, NULL, &oldmask) < 0)
    err_sys("SIG_SETMASK error");
}

void
TELL_CHILD(pid_t pid)
{
    kill(pid, SIGUSR1);      /* 告诉子进程已完成 */
}

void
WAIT_CHILD(void)
{
    while (sigflag == 0)
        sigsuspend(&zeromask); /* 并等待子进程 */
    sigflag = 0;
}

/* 重置信号掩码为原始值。*/
if (sigprocmask(SIG_SETMASK, NULL, &oldmask) < 0)
    err_sys("SIG_SETMASK error");
```

如果我们想在等待信号发生时进入睡眠，`sigsuspend`函数很好用（正如我们在之前的示例所示）。

在没有线程的情况下，我们能做的是在信号发生时在信号处理程序中使用全局变量。例如，如果我们调用 `SIGINT` 和 `SIGALARM` 并使用 `signal_intr` 函数安装处理程序，信号将中断任何被阻塞的慢速系统调用。信号最发生在我们阻塞在 `select()` 调用中（第 14.5 节）等待来自慢速设备的输入时。（这对于 `SIGALRM` 尤为如此，因为我们设置了闹钟以防止无限等待输入。）

处理此情况的代码看起来如下：

```c
if (int_intr)      /* 由我们的 SIGINT 处理程序设置的标志 */
    handle_intr();
if (alarm_flag)     /* 由我们的 SIGALARM 处理程序设置的标志 */
    handle_alarm();

/* 信号在此最后发生 */
while (select(...) < 0) {
  if (errno == EINTR) {
    if (alarm_flag) {
      handle_alarm();
    } else if (int_flag) {
      handle_intr();
    }
  } else {
    /* 其他错误 */
  }
}
```

我们在调用 `select` 之前测试了每个全局标志，如果 `select` 返回中断的系统调用错误。如果信号在前两个语句和随后的 `select` 调用之间被捕获，就会出现问题。正如代码注释所示，在此处信号将会丢失。信号处理程序被调用并设置相应的全局变量，但 `select` 永远不会（除非有数据可以读取）。

我们希望能够执行以下步骤：

1. 阻塞 `SIGINT` 和 `SIGALARM`。
2. 测试两个全局变量以查看是否发生了信号，如果是，则处理条件。
3. 调用 `select`（或其他任何函数）然后取消阻塞。

`sigsuspend` 函数帮助我们避免这种竞态条件。

## 10.17. abort 函数

我们之前提到过 `abort()` 会导致异常终止。

```c
#include <stdlib.h>
void abort(void);
```

ISO C 规定 `abort()` 不返回。

POSIX-1 标准规定 `abort()` 向进程发送 `SIGABRT`。如果信号被捕获，处理程序必须调用 `exit()` 来终止进程。

```c
exit(1); /* 这不应该被执行 ... */
}
```

## 10.18. system 函数

在第 8.13 节中我们展示了 `system` 函数的实现。然而，该版本没有进行任何信号处理。POSIX.1 要求 `system` 忽略 `SIGINT`、`SIGQUIT` 和 `SIGCHLD`。在展示一个能够正确处理这些信号的版本之前，让我们先来看看为什么我们需要担心信号处理。

### 示例

图 10.26 所示的程序使用了第 8.13 节中的 `system` 版本来调用 `ed` (1) 编辑器。（该编辑器长期以来一直是 UNIX 系统的一部分。我们使用它是因为它是一个可以捕获中断和退出信号的交互式程序。我们从 shell 调用 `ed` 并输入中断，它会捕获中断并打印提示符。该程序还设置了退出信号的处置，使其被忽略。）图 10.26 中的程序捕获了 `SIGINT` 和 `SIGCHLD`。如果我们运行该程序，会得到：

```text
$/a.out

a append text 在编辑器的缓冲区中追加文本

Here is one line of text
.
period 独占一行停止模式

1,$p  打印缓冲区从第一行到最后一行的内容以查看内容
Here is one line of text
w temp.foo  将缓冲区写入文件
25  editor 说它写入了 25 字节

q  并离开编辑器
捕获到 SIGCHLD
```

当编辑器终止时（系统会向 `a.out` 进程发送 `SIGCHLD` 信号）。我们在信号处理程序中捕获并返回。如果是捕获到 `SIGCHLD`，父进程也应该这样做，因为它创建了自己的子进程，这样它就能知道子进程何时终止。在 `system` 函数执行期间，应该阻塞父进程中该信号的递送。事实上，这就是 POSIX.1 规定的。否则，当子进程创建时，它会欺骗 `system` 的调用者，让其认为自己的子进程已终止。调用者将使用 `wait` 函数之一获取子进程的终止状态，从而防止 `system` 函数能够捕获子进程的状态作为其返回值。

如果我们再次运行该程序，这次编辑器接收到了中断信号，我们会得到：

```text
$/a.out

a append text 在编辑器的缓冲区中追加文本

hello, world
.
period 独占一行停止追加模式

1,$p 打印从第一行到最后一行的内容以查看内容

hello, world

w temp.foo 将缓冲区写入文件

13 editor 说它写入了 13 字节

^? 输入中断字符

编辑器捕获到信号，打印问号

捕获到 SIGINT，父进程也是如此

q 离开编辑器

捕获到 SIGCHLD
```

回想第 9.6 节，输入中断字符会导致中断信号发送到前台进程组中的所有进程。图 10.27 显示了进程的布局。当编辑器运行时，`a.out` 进程和编辑器都捕获了信号。当我们使用 `system` 函数运行另一个程序时，我们不应该让父进程和子进程都捕获这两个终端生成的信号：中断和退出。这些信号应该发送给正在运行的进程；即子进程。由于是由交互式命令执行的子进程（也是示例中的程序），并且 `system` 的调用者放弃了对程序的控制权并等待其完成，调用者 `system` 不应该接收这两个终端生成的信号。这就是为什么 POSIX.1 规定 `system` 函数在等待完成时应该忽略这两个信号的原因。

## 10.26. 使用 system 调用 ed 编辑器

```c
#include <signal.h>

static void
sig_int(int signo)
{
    printf("caught SIGINT\n");
}

static void
sig_child(int signo)
{
    printf("caught SIGCHLD\n");
}

int
main(void)
{
    if (signal(SIGINT, sig_int) == SIG_ERR)
        err_sys("SIGINT error");

    if (signal(SIGCHLD, sig_child) == SIG_ERR)
        err_sys("SIGCHLD error");

    if (system("/bin/ed") < 0)
        err_sys("system error");

    exit(0);
}
```

## 图 10.27. 图 10.26 的前台和后台进程组

![](img/902515e97eef28cac8083866e00a6f4c_492_0.png)

### 示例

图 10.28 展示了带有信号处理的 `system` 函数实现。

如果我们将图 10.26 中的程序与此 `system` 函数实现链接，生成的二进制文件与上一个（最终）有以下不同：

- 当我们使用中断或退出处理程序时，不会向进程发送信号。
- 当 `ed` 命令退出时，`SIGCHLD` 不会发送给进程。相反，它会被阻塞，直到我们在 `sigprocmask` 的最后一次调用中解锁，系统函数通过调用 `waitpid` 获取子进程状态。

POSIX.1 规定，`wait` 或 `waitpid` 在 `SIGCHLD` 挂起时返回子进程的状态；当另一个子进程的状态也可用时，`SIGCHLD` 不应递给该进程。书中讨论的几个实现中没有一个是符合语义的。当系统函数调用并在信号解锁后，`SIGCHLD` 保持挂起状态，并被递给调用者。如果在图 10.26 的 `sig_child` 函数中调用 `wait`，它将返回 1。许多文本展示了如下所示：

```c
/* 10.28. 正确的 system 实现 */
#include <signal.h>
#include <sys/wait.h>
#include <errno.h>
#include <unistd.h>
#include <stdio.h>
#include <stdlib.h>

int
system(const char *command)
{
    pid_t pid;
    int status;
    sigset_t set, oldset;

    /* 阻塞 SIGINT SIG SIG 和 SIGCHLD */
    sigemptyset(&set);
    sigaddset(&set, SIGINT);
    sigaddset(&set, SIGQUIT);
    sigaddset(&set, SIGCHLD);

    if (sigprocmask(SIG_BLOCK, &set, &oldset) < 0)
        err_sys("sigprocmask");

    pid = fork();

    if (pid < 0)
        err_sys("fork");

    if (pid == 0) {
        /* 子进程 */
        if (sigprocmask(SIG_SETMASK, &oldset, NULL) < 0)
            err_sys("sigprocmask");

        signal(SIGINT, SIG_IGN);
        signal(SIGQUIT, SIG_IGN);
        signal(SIGCHLD, SIG_IGN);

        if (execcl("/bin/sh", "sh", "-c", command, (char *)NULL) < 0)
            err_sys("execcl");

        exit(1);
    }

    /* 父进程 */
    while (waitpid(pid, &status, 0) < 0) {
        if (errno != EINTR)
            err_sys("waitpid");
        if (errno == ECHILD) {
            /* 这里的逻辑其实是多余的 */
            break;
        }
    }

    if (sigprocmask(SIG_SETMASK, &oldset, NULL) < 0)
        err_sys("sigprocmask");

    if (WIFEXITED(status))
        status = WEXITSTATUS(status);
    else if (WIFSIGNALED(status))
        status = WTERMSIG(status);

    return status;
}
```

POSIX.1 规定，`wait` 或 `waitpid` 在 `SIGCHLD` 挂起时返回子进程的状态；当另一个子进程的状态也可用时，`SIGCHLD` 不应递给该进程。书中讨论的几个实现中没有一个是符合语义的。当系统函数调用并在信号解锁后，`SIGCHLD` 保持挂起状态，并递给调用者。如果在图 10.26 的 `sig_child` 函数中调用 `wait`，它将返回 1。许多文本展示了如下所示：

```c
/* 10.26. 错误的 system 实现 */
static void
sig_int(int signo)
{
    printf("caught SIGINT\n");
}

static void
sig_child(int signo)
{
    printf("caught SIGCHLD\n");
    wait(NULL); // 错误：这里使用了 wait
}

int
main(void)
{
    if (signal(SIGINT, sig_int) == SIG_ERR)
        err_sys("SIGINT error");

    if (signal(SIGCHLD, sig_child) == SIG_ERR)
        err_sys("SIGCHLD error");

    if (system("/bin/ed") < 0)
        err_sys("system error");

    exit(0);
}
```

这种代码的逻辑在于，我们在中断或退出处理程序时，不会向进程发送信号。当 `ed` 命令退出时，`SIGCHLD` 不会发送给进程。相反，它会被阻塞，直到我们在 `sigprocmask` 的最后一次调用中解锁，系统函数通过调用 `waitpid` 获取子进程状态。

```c
/* 10.28. 带有信号处理的 system 实现 */
#include <signal.h>
#include <sys/wait.h>
#include <errno.h>
#include <unistd.h>
#include <stdio.h>
#include <stdlib.h>

int
system(const char *command)
{
    pid_t pid;
    int status;
    sigset_t set, oldset;

    /* 阻塞 SIGINT SIG QUIT 和 SIGCHLD */
    sigemptyset(&set);
    sigaddset(&set, SIGINT);
    sigaddset(&set, SIGQUIT);
    sigaddset(&set, SIGCHLD);

    if (sigprocmask(SIG_BLOCK, &set, &oldset) < 0)
        err_sys("sigprocmask");

    pid = fork();

    if (pid < 0)
        err_sys("fork");

    if (pid == 0) {
        /* 子进程 */
        if (sigprocmask(SIG_SETMASK, &oldset, NULL) < 0)
            err_sys("sigprocmask");

        signal(SIGINT, SIG_IGN);
        signal(SIGQUIT, SIG_IGN);
        signal(SIGCHLD, SIG_IGN);

        if (execcl("/bin/sh", "sh", "-c", command, (char *)NULL) < 0)
            err_sys("execcl");

        exit(1);
    }

    /* 父进程 */
    while (waitpid(pid, &status, 0) < 0) {
        if (errno != EINTR)
            err_sys("waitpid");
        if (errno == ECHILD) {
            break;
        }
    }

    if (sigprocmask(SIG_SETMASK, &oldset, NULL) < 0)
        err_sys("sigprocmask");

    if (WIFEXITED(status))
        status = WEXITSTATUS(status);

    else if (WIFSIGNALED(status))
        status = WTERMSIG(status);

    return status;
}
```
