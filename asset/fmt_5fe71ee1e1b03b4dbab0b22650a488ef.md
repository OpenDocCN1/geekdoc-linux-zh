
# 表 9.1 Linux 跟踪的进程资源

| 类型 | 字段 | 描述 |
|---|---|---|
| structval | ru_utime | 执行用户模式代码的总时间。这包括在应用程序中运行指令的所有时间，但不包括内核满足请求花费的时间。 |
| structval | ru_stime | 执行内核模式代码的总时间。 |
| long | ru_maxrss | 最大驻留内存大小（内存 中的内存）。 |
| long | ru_ixrss | 最大共享驻留内存大小。 |
| long | ru_idrss | 最大数据驻留内存大小。 |
| long | ru_isrss | 最大栈驻留内存大小。 |
| long | ru_minflt | 软缺页次数。 |
| long | ru_majflt | 软缺页次数。 |
| long | ru_nswap | 交换次数。 |
| long | ru_inblock | 从磁盘读取的块。 |
| long | ru_oublock | 输出磁盘的块。 |
| long | ru_msgsnd | 发送的消息数。 |
| long | ru_msggrcv | 接收的消息数。 |
| long | ru_signals | 信号数。 |
| long | ru_nvcsw | 自愿上下文切换次数。 |
| long | ru_nivcsw | 非自愿上下文切换次数。 |

### 9.3.3 建立限制

为了防止异常进程破坏系统性能，Unix 跟踪了进程使用的许多资源，并允许系统管理员和用户自身对其可以使用的资源设置限制。

限制分为两类：硬限制（hard limits）和软限制（soft limits）。硬限制可以被任何进程降低，但只有超级用户可以提高。硬限制在启动时通常设置为 `RLIM INFINITY`，这意味着没有限制。唯一的例外是 `RLIMIT_CORE`（核心转储的最大大小），Linux 将其初始化为 0 以防止意外的核心转储生成。然而，许多发行版在启动时会重置此限制（关于什么是核心转储见117页）。软限制是内核实际执行的限制。任何进程都可以将资源的软限制设置为小于或等于该资源硬限制的值。

# 表 9.2 资源限制

| 值 | 限制 |
| --- | --- |
| RLIMIT_CPU | 总 CPU 时间（秒） |
| RLIMIT_SIZE | 打开文件的最大大小（写入时检查） |
| RLIMIT_DATA | 数据内存最大大小（字节） |
| RLIMIT_STACK | 栈内存最大大小（字节） |
| RLIMIT_CORE | 内核生成的转储文件最大大小（如果核心文件太大，则不创建） |
| RLIMIT_RSS | 任何时间使用的最大内存量（超过此限制会导致分页）。这被称为进程的驻留内存大小。 |
| RLIMIT_NPROC | 进程可以创建的子进程最大数。这仅限制了它同时拥有的子进程数量。它不限制它可以拥有多少后代——最多拥有 RLIMIT_NPROC 个子进程 |
| RLIMIT_NOFILE | 最大打开文件数 |
| RLIMIT_MEMLOCK | 可以使用 `mlock()` 锁定的最大内存 |

可以设置的各种限制列在表 9.2 中，并定义在 `<sys/resource.h>`。`getrlimit()` 和 `setrlimit()` 系统调用获取并设置单个资源的限制。

这两个函数都使用了 `struct rlimit`，其定义如下：

```c
#include <sys/resource.h>

struct rlimit {
  long int rlim_cur;    /* 软限制 */
  long int rlim_max;    /* 硬限制 */
};
```

第一个字段 `rlim_max` 表示资源参数所指限制的硬限制，而 `rlim_cur` 包含软限制。这些是通过 `ulimit` 和 `limit` 命令操作的同一组限制，其中其中一个（或两者）被内置在大多数 shell 中。

## 9.4 进程原语

尽管描述一个进程需要较长的讨论，但在 Linux 中创建和销毁进程是非常简单的。

### 9.4.1 产生孩子

Linux 有两个创建新进程的系统调用：`fork()` 和 `clone()`。如前所述，`clone()` 用于创建线程，将在本章稍后部分进行讨论。目前，我们将重点关注 `fork()`，它是最常用的进程创建方法。

```c
pid_t fork(void);
```

该系统调用有一个不寻常的：每次调用并不只返回一次，而是返回两次：一次在父进程中，一次在子进程中。注意，我们没有说“首先在父进程中”——编写对两个进程按确定顺序执行做出任何假设的代码都是非常糟糕的主意。

每次从 `fork()` 系统调用返回都会返回不同的值。在父进程中，系统调用返回新创建的子进程的 `pid`；在子进程中，调用返回 0。

返回值的差异是进程之间唯一可见的差异。它们都具有相同的内存映像、凭据、打开的文件和信号处理程序。这里创建一个子进程程序的简单示例。

```c
#include <sys/types.h>
#include <stdio.h>
#include <unistd.h>
int main(void) {
    pid_t child;
    if (!child = fork())) {
        printf("in child\n");
        exit(0);
    }
    printf("in parent -- child is %d\n", child);
    return 0;
}
```

### 9.4.2 监视你的孩子的死亡

收集子进程的退出状态被称为“等待进程”（waiting on the process）。有四种方法可以实现这一点，尽管只有一个调用是由内核提供的。另外三种方法是在标准库中实现的。由于内核系统调用接受四个参数，因此它被称为 `wait4()`。

```c
pid_t wait4(pid_t pid, int *status, int options, struct rusage *rusage);
```

第一个参数 `pid` 是应该返回其退出代码的进程。它可以取多个特殊值。

- `-1` 等待任何 pgid 与 `pid` 绝对值相同的子进程。
- `-1` 等待任何子进程终止。
- `0` 等待当前进程所在进程组中的孩子。
- `0` 等待进程 `pid` 退出。

关于父进程和子进程打开的文件之间关系的详细信息，请参阅第 182 页。

第二个参数是一个指向整数的指针，该整数将被设置为导致 `wait4()` 返回的进程（我们以后将其称为被检查的进程）的退出状态。返回状态的格式非常复杂，提供了一组宏来使其具有意义。

有三个事件会导致 `wait4()` 返回被检查进程的状态：该进程可能已经退出、可能被 `kill()` 终止（发送了致命信号）、或者可能由于某种原因被停止。你可以通过以下宏找出发生了哪种情况，每个宏都接受 `wait4()` 返回的状态作为唯一参数。

- `WIFEXITED(status)` 返回进程是否正常退出。当程序的 `main()` 函数返回或程序调用 `exit()` 时，进程正常退出。如果 `WIFEXITED()` 为真，则 `WEXITSTATUS(status)` 将返回进程的退出状态。
- `WIFSIGNALED(status)` 如果进程由于信号而终止，则返回真（这是通过 `kill()` 终止的进程所发生的情况）。如果是如此，`WTERMSIG(status)` 返回终止进程的信号号。
- `WIFSTOPPED(status)` 如果进程被信号停止，`WIFSTOPPED()` 将返回真，`WSTOPSIG(status)` 返回停止进程的信号。只有在作为选项中指定了 `WTRACED` 时，`wait4()` 才会返回关于停止进程的信息。

`options` 参数控制调用的行为。`WNOHANG` 导致调用立即返回。如果没有进程准备好报告其状态，调用将返回 0 而不是有效的 `pid`。`WTRACED` 让 `wait4()` 在适当的孩子被停止时返回。关于停止进程的更多信息，请参见第 14 章。这两种行为都可以通过逻辑或将两个值结合来指定。

6. 参见第 14 章了解可能发生这种情况的原因。

`wait4()` 的最后一个参数是一个指向 `struct rusage` 的指针，它将填充被检查进程及其所有子进程的资源使用情况。有关这包含哪些内容，请参阅第 105–106 页关于 `getrusage()` 和 `RUSAGE_BOTH` 的讨论。如果此参数为 `NULL`，则不返回状态信息。

`wait4()` 有其他三个接口，都提供了其功能的子集。以下是替代接口的总结。

```c
pid_t wait(int *status)
```

`wait()` 的唯一参数是一个指向存储已终止进程返回代码位置的指针。该函数始终阻塞直到子进程终止。

```c
pid_t waitpid(pid_t pid, int *status, int options)
```
