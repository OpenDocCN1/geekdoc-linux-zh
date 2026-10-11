
### 表 4.2：跟踪的系统资源

| 资源 | 描述 |
| :----- | :----- |
| `ru_utime` | 执行用户模式（非内核）代码所花费的时间 |
| `ru_stime` | 执行内核代码（来自用户代码的系统服务请求）所花费的时间 |
| `ru_minflt` | 次要缺页中断的数量（未导致磁盘访问的内存访问） |
| `ru_majflt` | 主要缺页中断的数量（导致磁盘访问的内存访问） |
| `ru_nswap` | 因主要缺页中断而从磁盘读取的内存页数量 |

如表 4.2 所示，内存缺页中断分为两种类型：次要缺页中断和主要缺页中断。*次要缺页中断*发生在 CPU 必须访问主内存（RAM）时。这种缺页中断发生的原因是 CPU 所需的代码或数据不在其寄存器或缓存中。*主要缺页中断*发生在进程必须从磁盘读取数据时，因为所需的代码或数据不在 RAM 中。`ru_nswap` 成员存储了因主要缺页中断而从磁盘读取的内存页数量。

要获取这些信息，请使用在 `<sys/resource.h>` 中声明的 `getrusage` 调用。`ru_utime` 和 `ru_stime` 成员存储进程累积的用户 CPU 时间和系统 CPU 时间。`getrusage` 提供的新信息只有内存缺页中断的次数以及与缺页中断相关的磁盘访问次数。与 `times` 函数不同，如果要获取父进程和子进程两者的信息，必须调用两次 `getrusage`。`getrusage` 的原型如下：

```c
int getrusage(int who, struct rusage *usage);
```

`usage` 是函数填充的 `rusage` 结构的指针。`who` 参数确定返回的资源使用情况是调用进程的还是其子进程的。`who` 必须是 `RUSAGE_SELF` 或 `RUSAGE_CHILDREN`。如果 `getrusage` 成功，返回 0；如果发生错误，返回 -1。

![](img/be588b36b489136ce784030a08a1d3d4_105_0.png)

## 示例

此程序重写了之前的示例，使用 `getrusage` 代替 `times`：

```c
/*
 * resusg2.c - 获取进程时间和资源使用情况
 */
#include <stdio.h>
#include <stdlib.h>
#include <sys/times.h>
#include <sys/resource.h>
#include <time.h>
#include <unistd.h>

void err_quit(char *);
void doIt(char *, long);

int main(void)
{
    struct rusage usage;

    /* 重定向输出以防止屏幕杂乱 */
    system("grep the /usr/doc/*/* > /dev/null 2> /dev/null");

    /* 获取父进程的资源结构 */
    if((getrusage(RUSAGE_SELF, &usage)) == -1)
        err_quit("getrusage");

    puts("Parent times");
    doIt("\tuser CPU", usage.ru_utime.tv_sec);
    doIt("\tsys CPU", usage.ru_stime.tv_sec);

    fputs("Parent memory stats");
    doIt("\tminor faults", usage.ru_minflt);
    doIt("\tmajor faults", usage.ru_majflt);
    doIt("\tpage swaps", usage.ru_nswap);

    /* 获取子进程的资源结构 */
    if((getrusage(RUSAGE_CHILDREN, &usage)) == -1)
        err_quit("getrusage");

    puts("Child Times");
    doIt("\tuser CPU", usage.ru_utime.tv_sec);
    doIt("\tsys CPU", usage.ru_utime.tv_sec);

    puts("Child memory stats");
    doIt("\tminor faults", usage.ru_minflt);
    doIt("\tmajor faults", usage.ru_majflt);
    doIt("\tpage swaps", usage.ru_nswap);

    exit(EXIT_SUCCESS);
}

void doIt(char *str, long resval)
{
    printf("%s: %ld\n", str, resval);
}

void err_quit(char *str)
{
    perror(str);
    exit(EXIT_FAILURE);
}
```

此程序执行与之前相同的 `grep` 命令。但是，除了计时信息外，它还显示父进程和子进程的内存使用情况。一次示例运行产生了以下输出：

![](img/be588b36b489136ce784030a08a1d3d4_107_0.png)

## 输出

```
$ ./resusg2
Parent times
    user CPU: 0
    sys CPU: 0
Parent memory stats
    minor faults: 18
    major faults: 66
    page swaps: 0
Child Times
    user CPU: 2
    sys CPU: 2
Child memory stats
    minor faults: 2585
    major faults: 21412
    page swaps: 0
```

正如示例运行的输出所示，`getrusage` 产生的计时信息不如 `times` 产生的精确。另一方面，使用 `getrusage` 可以获得对进程内存使用情况的非常清晰的视图。实际上，示例运行中主要缺页中断的数量证实了之前关于程序所需磁盘 I/O 量的讨论。进程从磁盘读取了 21,412 次，因为必要的数据不在内存中。然而，没有发生页面交换。

## 会话和进程组

在某些情况下，简单的父/子模型不足以描述进程之间的关系。例如，考虑一个打开的 xterm 窗口。假设你在 xterm 中单独执行三条命令：ls、cat 和 vi。是 xterm 还是运行在 xterm 中的 shell 是父进程？显然，这三条命令彼此相关，但不是作为父子关系。相反，它们都是同一个会话的一部分。

另一个例子是在管道中执行的命令集，例如 `ls -1 | sort | more`。同样，这些命令彼此相关，不是作为父子关系，而是作为同一个进程组的成员。图 4.1 说明了进程、会话和进程组之间的关系。

![](img/be588b36b489136ce784030a08a1d3d4_108_0.png)

### 进程组

进程组是一组相关进程，通常是管道中的一系列命令。进程组中的所有进程具有相同的进程组 ID（PGID）。进程组的目的是方便作业控制。例如，假设你运行命令管道 `ls -1 /usr/include | sort | wc -1`。如果它在执行过程中被杀死（使用 Ctrl+C），shell 必须能够终止所有进程。它通过杀死进程组而不是每个单独的进程来实现这一点。

### 会话

会话由一个或多个进程组组成。会话领导者是创建该会话的进程。每个会话都有一个唯一的标识符，称为*会话 ID*，它仅仅是会话领导者的 PID。会话对于进程组的作用与进程组对于单个进程的作用相同。

假设你在后台执行之前提到的同一管道命令（即 `ls -l /usr/include | sort | wc -l &`），并在前台执行其他命令。现在，如果你正在 X Window 终端中运行这些命令，并在所有这些进程运行时关闭终端窗口，内核会向控制进程（会话领导者）发送信号，进而如上一段所述，杀死每个进程组。

操作进程组和会话是一个高级主题，超出了本书的范围。然而，理解这些概念和术语很重要，因为它们对第 5 章“信号”中涵盖的信号有重要影响。

## 操作进程

本节讨论创建新进程、终止现有进程以及对进程进行等待和监控。`system`、`fork` 和 `exec` 调用创建新进程。`kill` 函数可用于终止其他进程，进程可以调用 `exit` 或 `abort` 来终止自身。良好的资源管理要求父进程等待其子进程终止。各种 `wait` 函数处理这一要求。

### 创建进程

程序员经常需要在其程序内部创建新进程。例如，假设你创建了一个管理 CD-ROM 标题数据库的程序。你希望使用 `sort` 程序来完成排序工作，而不是自己创建排序例程。Linux 提供了三种方法来实现这一点。由标准 C 库提供的 `system` 调用是一种方法。然而，`fork` 和 `exec` 调用是“Linux 的方式”。本节查看这三种调用。

### 使用 system

`system` 函数执行传入的 shell 命令。其原型声明在 `<stdlib.h>` 中，如下所示：

```c
int system(const char *string);
```

`system` 通过将 `string` 传递给 `/bin/sh` 来执行 shell 命令，并在命令完成后返回。前面的示例已经展示了它的使用。如果由于某种原因，`system` 无法调用 `/bin/sh`，它返回 `127`。如果发生其他错误，`system` 返回 `-1`。`system` 的常规返回值是在 `string` 中传入的命令的退出代码。如果 `string` 为 `NULL`，如果 `/bin/sh` 可用，`system` 返回 0；如果不可用，则返回非零值。

