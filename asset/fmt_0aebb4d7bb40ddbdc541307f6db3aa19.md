
一两个僵尸进程不是问题，但如果程序不断`fork`和`exec`且未能收集退出状态，进程表最终会填满，从而阻碍性能并导致系统需要重启——这在任务关键的生产环境中并不是一种理想的情况！

另一方面，`*孤儿进程*`是指在其父进程调用`wait`或`waitpid`之前终止的子进程。在这种情况下，`init`进程成为该子进程的父进程并收集退出状态，从而防止僵尸进程的产生。

要收集子进程的退出状态，请使用`wait`或`waitpid`调用。你必须包含头文件`<sys/types.h>`和`<sys/wait.h>`。它们的原型如下：

```c
pid_t wait(int *status);
pid_t waitpid(pid_t pid, int *status, int options);
```

`status`参数存储子进程的退出状态。`pid`是你想要等待的进程的 PID。它可以取表 4.3 中列出的四个值之一。

### 表 4.3：`*`pid*`的可能值`

| 值 | 描述 |
| :--- | :--- |
| `< -1` | 等待任何 `PGID` 等于 `PID` 绝对值的子进程 |
| `-1` | 等待任何子进程 |
| `0` | 等待任何 `PGID` 等于调用进程 `PGID` 的子进程 |
| `> 0` | 等待 `PID` 等于 `pid` 的子进程 |

`options` 指定了 `wait` 调用应该如何行为。它可以是 `WNOHANG`，这会导致 `waitpid` 在没有子进程退出的情况下立即返回；`WUNTRACED`，这意味着它应该为那些状态尚未报告的子进程返回；或者你可以对它们进行逻辑或运算以获得两种行为（即，将 `WNOHANG | WUNTRACED` 作为 `options` 参数传递）。

## 示例

![](img/be588b36b489136ce784030a08a1d3d4_117_0.png)

`waiter.c` 演示了如何使用 `waitpid`。

```c
/*
 * waiter.c - 简单的 wait 用法
 */
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    pid_t child;
    int status;

    if((child = fork()) == -1) {
        perror("fork");
        exit(EXIT_FAILURE);
    } else if(child == 0) {
        puts("in child");
        printf("\tchild pid = %d\n", getpid());
        printf("\tchild ppid = %d\n", getppid());
        exit(EXIT_SUCCESS);
    } else {
        waitpid(child, &status, 0);
        puts("in parent");
        printf("\tparent pid = %d\n", getpid());
        printf("\tparent ppid = %d\n", getppid());
        printf("\tchild exited with %d\n", status);
    }
    exit(EXIT_SUCCESS);
}
```

一次示例运行产生了以下输出：

![](img/be588b36b489136ce784030a08a1d3d4_118_0.png)

### 输出

```
$ ./waiter
in child
    child pid = 4502
    child ppid = 4501
in parent
    parent pid = 4501
    parent ppid = 4429
    child exited with 0
```

该程序与之前的 `child.c` 类似，只是增加了一条 `waitpid` 语句。它专门等待由 `child` 指定的子进程返回，并显示该子进程的退出状态。请注意，父进程和子进程的输出不再像 `child.c` 中那样混合在一起。父进程的执行会停止，直到子进程退出。`waitpid`（和 `wait`）返回已退出的子进程的 PID，如果 `options` 中指定了 `WNOHANG` 则返回 0，如果发生错误则返回 -1。

## 终止进程

进程终止的原因有五种：

- 其 `main` 函数调用 `return`
- 它调用 `exit`
- 它调用 `_exit`
- 它调用 `abort`
- 它被信号终止

前三种原因是正常终止，后两种是非正常终止。尽管进程终止的原因可能不同，但最终执行的内核代码是相同的，它会关闭打开的文件，释放内存资源，并执行其他必要的清理工作。由于本书假定读者具备 C 编程能力，因此希望 `return` 函数无需过多解释。

## `exit` 函数

你已经见过 `exit` 函数，它是 C 标准库的一部分，在本章的程序中都有使用。而不是提供另一个示例，下面列出了它的原型，如 `<stdlib.h>` 中声明的那样：

```c
int exit(int status);
```

`exit` 导致程序正常终止并向父进程返回 `status`。通过 `atexit` 注册的函数将被执行。

`_exit` 函数在 `<unistd.h>` 中声明。它立即终止调用进程；通过 `atexit` 注册的函数不会执行。

## 使用 `abort`

如果需要非正常终止程序，请使用 `abort` 函数。在 Linux 下，`abort` 还有额外的副作用，即导致程序转储核心文件（core dump），大多数调试器使用核心文件来分析程序崩溃时的状态。尽管任何打开的文件都会被关闭，但 `abort` 是一个严厉的调用，应该仅在最后手段时才调用，例如当你遇到无法以编程方式处理的错误时，如严重的内存短缺。`abort` 也是一个标准库函数（在 `<stdlib.h>` 中声明）。其原型是

```c
void abort(void);
```

![](img/be588b36b489136ce784030a08a1d3d4_119_0.png)

## 示例

以下程序展示了 `abort` 函数的行为：

```c
/*
 * abort.c - 演示 abort 系统调用
 */
#include <stdlib.h>
#include <stdio.h>

int main(void)
{
    abort();

    /* 不应该到达这里 */
    exit(EXIT_SUCCESS);
}
```

![](img/be588b36b489136ce784030a08a1d3d4_119_1.png)

### 输出

```
$ ./abort
Aborted
$ ulimit -c unlimited
$ ./abort
Aborted (core dumped)
```

请注意，你的系统可能不会生成核心文件。如果没有，请使用 shell 的 `ulimit` 命令，如输出中所示。核心文件在调试程序时非常有用。

> 有关使用核心文件调试的更多信息，请参阅第 426 页的 “Starting gdb”。

### 使用 `kill` 函数

前两节关注的是进程如何终止自身。那么，一个进程如何终止另一个进程？使用 `kill` 函数，其原型如下：

```c
int kill(pid_t pid, int sig);
```

要使用它，你必须在程序中包含 `<sys/types.h>` 和 `<signal.h>`。`pid` 参数指定你要终止的进程，`sig` 是你想要发送的信号。由于本节涉及终止进程，目前你只需要关心 `SIGKILL` 信号。第 5 章将扩展对信号的讨论。现在，请暂且相信这一点。

![](img/be588b36b489136ce784030a08a1d3d4_120_0.png)

## 示例

该程序展示了如何终止一个进程：
