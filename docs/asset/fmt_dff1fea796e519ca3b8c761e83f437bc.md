
只有当进程捕获了信号时，`pause` 才返回到调用进程。如果交付的信号调用了处理程序，该处理程序将在 `pause` 返回之前执行。`pause` 总是返回 `-1`，并将 `errno` 设置为 `EINTR`。

## 示例

![](img/be588b36b489136ce784030a08a1d3d4_136_0.png)

这个简单的程序只是等待信号被交付，然后退出。

```c
/*
 * pause.c - Pause then exit
 */
#include <unistd.h>
#include <stdlib.h>

int main(void)
{
    pause();
    exit(EXIT_SUCCESS);
}
```

![](img/be588b36b489136ce784030a08a1d3d4_136_1.png)

### 输出

```bash
$ ./pause
[Ctrl+z]
[1]+  Stopped              ./pause
fg
./pause
[Ctrl+\]
Quit (core dumped)
$ ./pause
User defined signal 1
```

在第一次运行中，`pause` 只是进入了一种永恒的挂起状态。首先，`Ctrl+Z`（从键盘输入）挂起程序；`fg` 命令再次将其带回前台，此时 `Ctrl+\`（`SIGQUIT`）将其终止并导致转储核心文件。如果你没有终止它，它将在 `pause` 中继续，直到接收到另一个信号或系统重启。

在第二次运行中，程序在一个窗口中运行。在第二个窗口中，使用 `ps` 获取了 PID，然后发出 `kill -USR1 <PID>`。由于没有为 `SIGUSR1` 信号建立信号处理程序，其默认操作——终止——发生了。

## 定义信号处理程序

在某些情况下，信号的默认操作是期望的行为。在其他情况下，可能大多数情况下，你希望改变该行为或执行额外的任务。在这些情况下，你必须定义并安装一个自定义的信号处理程序以覆盖默认操作。

考虑一个生成多个子进程的父进程的情况。当子进程终止时，父进程接收 `SIGCHLD` 信号。为了跟踪其子进程并监控它们的退出状态，父进程可以在生成每个子进程后立即调用 `wait`，或者更有效地，建立一个信号处理程序，每次接收到 `SIGCHLD` 时都调用 `wait`（或 `waitpid`）。

POSIX 定义了一组用于创建和操作信号的函数。一般程序是创建信号集，设置你想要捕获的信号，在内核中注册信号处理程序，并等待捕获信号。

## 信号处理 API

要创建、设置和查询信号集，请使用以下五个函数，它们都定义在 `<signal.h>` 中：

- `int sigemptyset(sigset_t *set);`

- `int sigfillset(sigset_t *set);`

- `int sigaddset(sigset_t *set, int signum);`

- `int sigdelset(sigset_t *set, int signum);`

- `int sigismember(const sigset_t *set, int signum);`

`set` 是类型 `sigset_t` 的信号集，如章节开头所解释的那样。`sigemptyset` 初始化信号集 `set`，使所有信号都排除在该集合之外。相反，`sigfillset` 初始化 `set`，使所有信号都包含在内。`sigaddset` 将信号 `signum` 添加到 `set` 中。`sigdelset` 从 `set` 中删除 `signum`。

这四个函数成功时返回 `0`，发生错误时返回 `-1`。最后，`sigismember` 测试 `signum` 是否在 `set` 中，如果在则返回 `1`（真），如果不在则返回 `0`（假）。

## 创建信号集

因此，要创建信号集，请使用 `sigemptyset` 或 `sigfillset` 来初始化一个信号集。如果创建一个空的信号集，您需要使用 `sigaddset` 添加感兴趣的信号。如果创建一个完整的信号集，请使用 `sigdelset` 从信号掩码中移除信号。

## 示例

![](img/be588b36b489136ce784030a08a1d3d4_138_0.png)

1. 此程序向空信号集中添加一个信号，然后使用 `sigismember` 确认该信号在集合中。

```c
/*
 * mkset.c -- 创建一个信号集
 */
#include <signal.h>
#include <stdlib.h>
#include <stdio.h>

void err_quit(char *);

int main(void)
{
    sigset_t newset;

    /* 创建集合 */
    if((sigemptyset(&newset)) < 0)
        err_quit("sigemptyset");
    /* 向集合中添加 SIGCHLD */
    if((sigaddset(&newset, SIGCHLD)) < 0)
        err_quit("sigaddset");

    /* 检查信号掩码 */
    if(sigismember(&newset, SIGCHLD))
        puts("SIGCHLD is in signal mask");
    else
        puts("SIGCHLD not in signal mask");
    /* SIGTERM 不应该存在 */
    if(sigismember(&newset, SIGTERM))
        puts("SIGTERM in signal mask");
    else
        puts("SIGTERM not in signal mask");

    exit(EXIT_SUCCESS);
}

void err_quit(char *msg)
{
    perror(msg);
    exit(EXIT_FAILURE);
}
```

![](img/be588b36b489136ce784030a08a1d3d4_139_0.png)

### 输出

```bash
$ ./mkset
SIGCHLD is in signal mask
SIGTERM not in signal mask
```

`mkset` 首先创建一个空的信号集，将 `sigset_t` 结构的地址传递给 `sigemptyset`。接下来，它向进程的 `信号掩码` 中添加 `SIGCHLD`。最后，使用 `sigismember`，它确认 `SIGCHLD` 是集合的一部分，而 `SIGTERM` `不是` 掩码的一部分。

![](img/be588b36b489136ce784030a08a1d3d4_139_1.png)

## 示例

2. 此示例演示了从进程的信号掩码中移除信号的过程。

```c
/*
 * rmset.c - 从集合中移除信号
 */
#include <signal.h>
#include <stdlib.h>
#include <stdio.h>

void err_quit(char *);

int main(void)
{
    sigset_t newset;

    /* 创建集合 */
    if((sigfillset(&newset)) < 0)
        err_quit("sigfillset");
    /* 从集合中移除 SIGALRM */
    if((sigdelset(&newset, SIGALRM)) < 0)
        err_quit("sigdelset");

    /* SIGALRM 应该已经不存在了 */
    if(sigismember(&newset, SIGALRM))
        puts("SIGALRM is in signal mask");
    else
        puts("SIGALRM not in signal mask");
    /* SIGTERM 应该仍然在那里 */
    if(sigismember(&newset, SIGTERM))
        puts("SIGTERM in signal mask");
    else
        puts("SIGTERM not in signal mask");

    exit(EXIT_SUCCESS);
}

void err_quit(char *msg)
{
    perror(msg);
    exit(EXIT_FAILURE);
}
```

![](img/be588b36b489136ce784030a08a1d3d4_140_0.png)

### 输出

```bash
$ ./rmset
SIGALRM not in signal mask
SIGTERM in signal mask
```
