
`rmset` 的行为与上一个示例相反，它创建了一个完整的信号集，其中包含所有信号。然后它移除了`SIGALRM`。同样，`sigismember` 调用确认被移除的信号确实被移除了，而其他信号未被移除。

## 注册处理器

然而，仅仅创建一个信号集并添加或删除信号，并不能创建信号处理器，也不能让你捕获或阻止信号。还需要采取更多步骤。首先，你必须使用`sigprocmask` 来设置或修改（或两者兼有）当前的信号掩码——如果尚未设置信号掩码，所有信号都将具有其默认处置方式。一旦设置了信号掩码，你需要使用`sigaction` 为你想要捕获的信号或信号注册一个信号处理器。

正如你可能已经预料的那样，`sigaction` 和`sigprocmask` 在`<signal.h>` 中声明了原型。它们的原型如下：

```c
int sigprocmask(int how, const sigset_t *set, sigset_t *oldset);
```

`sigprocmask` 根据`how` 的值设置或检查当前的信号掩码，`how` 可以是以下值之一：

*   `SIG_BLOCK` — 集合包含要阻止的附加信号
*   `SIG_UNBLOCK` — 集合包含要解除阻止的信号
*   `SIG_SETMASK` — 集合包含新的信号掩码

如果`how` 为`NULL`，则忽略它。如果`set` 为`NULL`，当前掩码存储在`oldset` 中；如果`oldset` 为`NULL`，则忽略它。`sigprocmask` 成功时返回 0，出错时返回 -1。

```c
int sigaction(int signum, const struct sigaction *act, struct sigaction *oldact);
```

`sigaction` 为`signum` 中指定的信号设置信号处理器。结构体`struct sigaction` 描述了信号的处置方式。其完整定义来自`<signal.h>`，如下所示：

```c
struct sigaction {
    void (*sa_handler)(int);
    sigset_t sa_mask;
    int sa_flags;
    void (*sa_restorer)(void);
};
```

`sa_handler` 是一个指向函数的指针，该函数指定了在生成`signum` 信号时调用的处理器或函数。该函数必须被定义为返回类型`void` 并接受一个`int` 参数。或者，`sa_handler` 参数也可以是`SIG_DFL`，这将导致`signum` 的默认动作发生，或者是`SIG_IGN`，这将导致此信号被忽略。

在信号处理器执行期间，触发该处理器的信号会被阻止。`sa_mask` 定义了处理器执行期间应被阻止的一组附加信号的信号掩码。`sa_flags` 是一个掩码，用于修改`sa_handler` 的行为。它可以是以下选项的一个或多个：

*   `SA_NOCLDSTOP` — 进程将忽略子进程生成的任何`SIGSTOP`、`SIGTSTP`、`SIGTTIN` 和`SIGTTOU` 信号。
*   `SA_ONESHOT` 或`SA_RESETHAND` — 注册的自定义信号处理器只执行一次。执行后，信号的默认动作将被恢复。
*   `SA_RESTART` — 启用可重启的系统调用。
*   `SA_NOMASK` 或`SA_NODEFER` — 不防止在其自身的处理器中接收该信号。

请忽略`sa_restorer` 元素；它已过时，不应使用。

综上所述，`sigprocmask` 操作你想要阻止的信号集合并查询当前的信号掩码。函数`sigaction` 为内核注册一个或多个信号的信号处理器，并设置处理器的确切行为。

## 示例

![](img/be588b36b489136ce784030a08a1d3d4_142_0.png)

### 示例 1

第一个示例仅阻止`SIGALRM` 和`SIGTERM`，而无需安装处理器来采取特殊操作。

```c
/*
 * blkset.c - 创建信号集
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
    /* 添加 SIGTERM 和 SIGALRM */
    if((sigaddset(&newset, SIGTERM)) < 0)
        err_quit("sigaddset:SIGTERM");
    if((sigaddset(&newset, SIGALRM)) < 0)
        err_quit("sigaddset:SIGALRM");

    /* 阻止信号而不处理它们 */
    if((sigprocmask(SIG_BLOCK, &newset, NULL)) < 0)
        err_quit("sigprocmask");

    /* 等待信号 */
    pause();

    exit(EXIT_SUCCESS);
}

void err_quit(char *msg)
{
    perror(msg);
    exit(EXIT_FAILURE);
}
```

![](img/be588b36b489136ce784030a08a1d3d4_143_0.png)

#### 输出

此程序的测试产生了以下输出。该程序在一个窗口中运行，并使用`kill` 命令从另一个窗口发送信号（从第二个窗口发送的命令用括号表示）。

```bash
$ ./block
[$ kill -TERM $(pidof ./block)]
[$ kill -ALRM $(pidof ./block)]
[$ kill -QUIT $(pidof ./block)]
Quit (core dumped)
```

你可以从输出中看到，向进程发送`SIGTERM` 和`SIGALRM` 没有产生任何影响，尽管这两个信号的默认动作都是终止进程。命令`pidof ./block` 返回与`./block` 关联的 PID，而`$( . . . )` 构造用于替换命令的结果并将其传递给`kill` 命令。当进程接收到`SIGQUIT` 时，它退出，如输出所示。请注意，因为程序阻止了`SIGTERM` 和`SIGALRM`，所以进程不会接收到信号，`pause` 永远不会返回。

![](img/be588b36b489136ce784030a08a1d3d4_143_1.png)

### 示例 2

此程序为`SIGUSR1` 建立了一个处理器。`SIGUSR1` 的默认动作是终止进程。自定义处理器只是说明它被调用了。

```c
/*
 * blkusr.c - SIGUSR1 的自定义处理器
 */
#include <unistd.h>
#include <signal.h>
#include <stdio.h>
#include <stdlib.h>

void err_quit(char *);  /* 错误处理函数 */
void hndl_usr1(int);    /* 信号处理器 */

int main(void)
{
    struct sigaction action;

    /* 设置处理程序 */
    action.sa_handler = hndl_usr1;
    sigemptyset(&action.sa_mask);
    action.sa_flags = SA_NOCLDSTOP;

    /* 注册处理程序 */
    if((sigaction(SIGUSR1, &action, NULL)) < 0)
        err_quit("sigaction");

    /* 预留足够的时间以发送信号 */
    sleep(60);
    exit(EXIT_SUCCESS);
}

void err_quit(char *msg)
{
    perror(msg);
    exit(EXIT_FAILURE);
}

void hndl_usr1(int signum)
{
    if(signum == SIGUSR1)
        puts("caught USR1");
    else
        printf("caught %d\n", signum);
}
```
