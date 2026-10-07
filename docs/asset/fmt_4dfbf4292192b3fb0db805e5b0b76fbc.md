
```c
struct iocb {
 void *data;        /* 在 io 完成事件中返回 */
 unsigned key;      /* 用于识别 io 请求 */

 short aio_lio_opcode;
 short aio_reqprio;
 int    aio_fildes;

 union {
struct iocb_common  c;
struct iocb_vector   v;
struct iocb_poll    poll;
struct iocb_sockaddr saddr;
 } u;

struct io_iocb_poll {
 int events;
}; /* 结果代码为结果标志集或 -ve errno */

struct io_iocb_sockaddr {
 struct sockaddr *addr;
 int    len;
}; /* 结果代码为 sockaddr 的长度，或 -ve errno */
```

## 15.3. LINUX 实现

```c
struct io_iocb_common {
    void            *buf;
    unsigned long nbytes;
    long long offset;
}; /* 结果码是读取字节数或负的 errno */
```

```c
struct io_iocb_vector {
    const struct iovec *vec;
    int nr;
    long long         offset;
}; /* 结果码是读取字节数或负的 errno */
```

虽然你可以仅通过这些函数和结构体完成工作，但在提交请求之前，在正确的位置插入所有正确的值可能会非常繁琐。头文件中有很多辅助函数，它们可以为你完成大部分工作。遗憾的是，手册页（man pages）并没有提到它们。你绝对想要用上的两个特定函数是：

```
void io_prep_pread (struct iocb *iocb, int fd, void *buf, size_t count, long long offset);
void io_prep_write (struct iocb *iocb, int fd, void *buf, size_t count, long long offset);
```

以显而易见的方式调用这些函数后，你只需调用 `io_submit()` 即可启动 I/O 操作。

最终，glibc 维护者会完成必要的封装，以允许使用 Posix API。到那个时候，如果需要移植性，那么使用 AIO 的原生 Linux 应该以一种直接的方式实现移植。

## 15.4 实验

### 实验 1：使用 POSIX 和 Linux API 测试异步 I/O

编写一个使用原生 Linux API 的程序。让它发送若干写入和读取请求并进行正确的同步。你可以使用一个临时文件。

我们还提供了一个使用 Posix API 实现应用程序的解决方案。

确保在编译时链接了正确的库；Linux API 使用 `-laio`，Posix API 使用 `-lrt`。（在任何情况下你都可以使用两者，因为它们不会冲突。）

# 第 16 章

# 信号 - Ⅰ

我们将学习 Linux 如何使用信号、有哪些可用信号，以及如何分发和处理它们。我们将学习闹钟、挂起和睡眠。我们将讨论信号集和 `sigaction()` 接口。

- 16.1 什么是信号？ ................................................................................................................................................. . . . . . . . . . . 123

- 16.2 可用信号 ................................................................................................................................... 124

- 16.3 分发信号 ................................................................................................................................... 125

- 16.4 闹钟、挂起和睡眠 .......................................................................................................................... 126

- 16.5 设置信号处理器 .......................................................................................................................... 127

- 16.6 信号集 ....................................................................................................................................... 129

- 16.7 sigaction() ................................................................................................................................... 131

- 16.8 实验 ....................................................................................................................................... 133

### 16.1 什么是信号？

信号是软件中断，提供了一种处理异步事件的方法。它们提供了一种进程间通信的基本方法，通信进程可能并不相关，在大多数情况下，发送的信息是信号类型。

## 第 16 章，信号 - Ⅰ

进程只能向具有相应权限的进程发送信号。信号可以用于通知进程采取某些操作或优雅地终止。对于大多数信号，如果进程接收到信号，执行将返回到备选位置。

使用 `setjmp()`、`longjmp()`、`siglongjmp()` 函数是可能的，以避免损坏。早期的 `signal()` 实现不可靠；因为无法保证信号不会丢失。在 Linux 下，使用了更可靠的 `sigaction()` 接口，它是 `signal()` 接口的封装。信号 API 追溯到 Unix 早期，特别是在多线程出现之前。它还包含了很多包袱，在某种意义上是过时的。如果你正在开发一个大量使用信号的新应用程序，你需要考虑设计模型是否合理，以及是否使用线程更好。

### 16.2 可用信号

`kill -1` 命令将列出可用信号，`man 7 signal` 提供更多文档。给出定义的文件是 `/usr/include/asm-x86_64/signal.h`。这是 x86 的信号列表，在其他架构上可能会不同：

| 信号 | 值 | 默认操作 | Posix? | 含义 |

| :--- | :--- | :--- | :--- | :--- |

| SIGHUP | 1 | 终止 | 是 | 控制终端挂断或控制进程死亡 |

| SIGINT | 2 | 终止 | 是 | 键盘中断 |

| SIGQUIT | 3 | 核心转储 | 是 | 键盘退出 |

| SIGILL | 4 | 核心转储 | 是 | 非法指令 |

| SIGTRAP | 5 | 核心转储 | 是 | 调试跟踪/断点 |

| SIGABRT | 6 | 核心转储 | 是 | 异常终止 |

| SIGBUS | 7 | 核心转储 | 是 | 总线错误 |

| SIGFPE | 8 | 核心转储 | 是 | 浮点异常 |

| SIGKILL | 9 | 终止 | 否 | 杀死信号（无法捕获或忽略） |

| SIGUSR1 | 10 | 终止 | 是 | 用户定义信号 |

| SIGSEGV | 11 | 核心转储 | 是 | 无效内存引用 |

| SIGUSR2 | 12 | 终止 | 是 | 用户定义信号 |

| SIGPIPE | 13 | 终止 | 是 | 管道破：无读者写入 |

| SIGALRM | 14 | 终止 | 是 | 闹钟定时信号 |

| SIGTERM | 15 | 终止 | 是 | 进程终止 |

| SIGFLT | 16 | 终止 | 否 | 数学协处理器栈溢出 |

| SIGCHLD | 17 | 忽略 | 是 | 子进程停止或终止 |

| SIGCONT | 18 | 继续 | 是 | 停止后继续 |

| SIGSTOP | 19 | 停止 | 是 | 停止进程（无法捕获或忽略） |

| SIGUSP | 20 | 停止 | 是 | 在 tty 处停止 |

| SIGTTIN | 21 | 停止 | 是 | 后台进程需要 tty 输入 |

| SIGTOU | 22 | 停止 | 是 | 后台进程需要 tty 输出 |

| SIGURG | 23 | 忽略 | 否 | Socket 紧急情况 (4.2 BSD) |

| SIGXPCU | 24 | 核心转储 | 是 | CPU 时间超时 (4.2 BSD) |

| SIGXFSZ | 25 | 核心转储 | 是 | 文件大小限制超时 (4.2 BSD) |

| SIGVALRM | 26 | 终止 | 否 | 虚拟闹钟 (4.2 BSD) |

| SIGPROF | 27 | 终止 | 否 | 性能分析闹钟 (4.2 BSD) |

| WINCH | 28 | 忽略 | 否 | 窗口调整信号 (4.3 BSD, Sun) |

| SIGIO | 29 | 终止 | 否 | 现在支持 I/O (4.2 BSD) (System V) |

| SGPWR | 30 | 终止 | 否 | 故障 (System V) |

| SIGSYS | 31 | 终止 | 否 | 错误的系统调用。未使用信号 |

| SIGUNUSED | | | |

## 16.3 分发信号

分发（发送）信号很容易；正确处理（捕获）并避免竞态条件则较困难。有两个函数用于产生信号：

```c
#include <sys/types.h>
#include <signal.h>

int kill(pid_t pid, int sig);
int raise(int sig);
```

`kill()` 可以向任何进程组或进程发送任何信号。注意，发送进程必须具有向另一个进程发送信号的权限。

`raise()` 用于进程向自身发送信号；在单线程进程中，`raise(sig)` 等于 `kill(getpid(),sig)`。在多线程进程中，它只向当前线程发送信号。

`kill()` 的 `pid` 参数有多种用法：

## 表 16.2: kill() 进程选择

| Value | 含义 |

|---|--|

| pid > 0 | 信号发送给进程 ID 为 pid 的进程。 |

| pid = 0 | 信号发送给所有进程组 ID 与发送者相同且发送者对这些进程具有权限的进程。 |

| pid < -1 | 信号发送给所有进程组 ID 为 pid 绝对值且发送者对这些进程具有权限的进程。 |

| pid = -1 | 信号发送给进程表中第一个进程以外的所有进程，按照从进程表中从高到低的顺序。 |

这些函数在成功时返回 0，错误时返回 -1（并设置 errno）。可能的错误返回值为：

## 表 16.3: kill() 错误返回值

| Value | 含义 |

|---|--|

| EINVAL | 指定的信号值无效。 |

| ESRCH | pid 或进程组不存在。 |

| EPERM | 权限被拒绝 |

## 16.4 闹钟、暂停与睡眠

该函数：

```c
#include <unistd.h>
unsigned int alarm (unsigned int seconds);
```

设置一个定时器在 seconds 秒后过期并引发 SIGALRM 信号。如果 seconds = 0，任何待处理的请求都会被取消。

每个进程只能有一个闹钟；如果之前已注册了闹钟，则返回剩余的秒数，并将定时器重置为新值。成功时，新闹钟的返回值为 0。

暂停和睡眠通过以下函数完成：

```c
#include <unistd.h>
int pause (void);
unsigned int sleep (unsigned int seconds);
```

### 设置信号处理程序

pause() 使进程进入睡眠，直到接收到信号。只有当执行信号处理程序且该程序返回时，函数才会返回。在这种情况下，pause() 返回 -1 并设置 errno 为 EINTR。

sleep() 让当前进程睡眠，直到通过秒数或到达未被忽略的信号。如果请求的时间已过去，函数返回 0，否则返回剩余的睡眠秒数。

为了对睡眠间隔进行更精细的控制，可以使用以下函数：

```c
#include <unistd.h>
void usleep(usec);

#include <time.h>
int nanosleep(const timespec *req, struct timespec *rem);

struct timespec {
    time_t tv_sec;
    long tv_nsec;
```

其中 usleep() 挂起执行指定的微秒，而 nanosleep() 则挂起 tv_sec 秒和 tv_nsec 纳秒。请查看 man 页面以获取其参数的完整描述以及对精度的讨论（该精度可能小于请求的值）。

还可以使用带有 `NULL` 文件描述符集合的 `select()` 函数来请求微秒级的睡眠：

```c
select(1, NULL, NULL, NULL, struct timeval *timeout);
struct timeval {
    long tv_sec;
    long tv_usec
}
```

## 16.5 设置信号处理程序

signal() 函数是处理信号的最简单方法；正如我们将看到的，sigaction() 更好，并且在 Linux 下，signal() 底层实际上也是使用它。

```c
#include <signal.h>
void (*signal(int signum, void (*handler)(int)))(int);
```

signal() 系统调用为编号为 signum 的信号安装一个新的信号处理程序。信号处理程序被设置为 handler()，它可以是一个用户指定的函数，也可以是以下之一：

## 表 16.4: 默认信号处理程序

| Value | 含义 |

|---|---|

| SIG_IGN | 忽略信号。 |

| SIG_DFL | 将信号重置为默认行为 |

传递给信号处理例程的整数参数是信号值。这使得使用一个信号处理程序处理多个信号成为可能。

无法为 SIGKILL 或 SIGSTOP 设置信号处理程序。

信号处理程序不能为 SIGKILL 或 SIGSTOP 设置。原型具有误导性。在实践中，它的原型看起来像：

```c
typedef void (*sighler_t)(int);
sighler_t signal (int signum, sighler_t handler);
```

signal() 返回处理程序的值，错误时返回 SIG_ERR。

根据 man 页面，当信号被阻塞时，signal() 会返回不同的值。实际上，如果想重置为默认行为，需要调用 signal() 并传入 SIG_DFL。当信号被阻塞时，signal() 实际上被调用。如果想确保信号被重置，需要调用 signal()

当信号被阻塞时，signal() 实际上被调用。如果想确保信号被重置，需要调用 signal()

以下是信号用例：

```c
#include <signal.h>
#include <stdio.h>
#include <unistd.h>

void ouch (int sig)
{
    printf("OUCH! %d\n", sig);
}

int main (int argc, char *argv[])
{
    signal(SIGINT, ouch);
    while (1) {
        sleep(1);
    }
}
```

### 16.6 信号集

可以使用带有 `NULL` 文件描述符集合的 `select()` 函数来请求微秒级睡眠。以下三个函数允许对信号集进行复杂的操作：

```c
#include <signal.h>

int sigempty(sigset_t *set);
int sigfillset(sigset_t *set);
int sigaddset(sigset_t *set, int sig);
int sigdelset(sigset_t *set, int sig);
int sigismember(const sigset_t *set, int sig);
```

sigprocmask() 更改阻塞信号列表，取决于 how 的值：

## 表 16.5: 信号掩码选择

| Value | 含义 |

|---|---|

| SIG_BLOCK | 阻塞信号集为当前集与 set 参数的并；即 set 是要阻塞的额外信号。 |

| SIG_UNBLOCK | 阻塞信号集为当前集与 set 参数补集的交集；即 set 中指定的信号从当前集中移除。 |

| SIG_SETMASK | 阻塞信号集设置为参数。 |

如果 offset 不为 `NULL`，之前的信号集值将检索到其中。
