
进入文件描述时设置 `O_NONBLOCK` 标志，以便未来的读取将是非阻塞的。这节省了为了实现相同结果而额外调用 `fcntl()`。

创建文件描述符后，我们可以使用 `read()` 从读取信号。提供的缓冲区必须足够大，至少能容纳一个 `signfd_siginfo` 结构体，该结构在 `<sys/signalfd.h>` 中的定义如下：

```c
struct signalfd_siginfo {
    uint32_t ssi_sign; /* 信号号 */
    int32_t ssi_errno; /* 错误号（通常未使用） */
    uint32_t ssi_code; /* 信号代码 */
    uint32_t ssi_pid; /* 发送进程的 PID */
    uint32_t ssi_uid; /* 发送者的真实 UID */
    int32_t ssi_fd; /* 文件描述符 (SIGPOLL/SIGIO) */
    uint32_t ssi_tid; /* 内核定时器 ID (POSIX 定时器) */
    uint32_t ssi_band; /* 带宽事件 (SIGPOLL/SIGIO) */
    uint32_t ssi_tid; /* (内核内部) 定器 ID (POSIX 定时器) */
    uint32_t ssi_utime; /* 溢计数 (POSIX 定时器) */
    uint32_t ssi_trapno; /* 陷阱号 */
    int32_t ssi_status; /* 退出状态或信号 (SIGCHLD) */
    int32_t ssi_int; /* 由 sigqueue() 设置的整数 */
    uint64_t ssi_ptr; /* 由 sigqueue() 设置的指针 */
    uint64_t ssi_stime; /* 用户 CPU 时间 (SIGCHLD) */
    uint64_t ssi_stime; /* 系统 CPU 时间 (SIGCHLD) */
    uint64_t ssi_addr; /* 产生信号的地址（硬件生成的信号） */
};
```

该结构中的字段返回的信息与传统 `siginfo_t` 结构（第 21.4 节）中同名的字段相同。

每次调用 `read()` 都会根据提供的缓冲区中待处理和等待的信号数量，返回相应数量的 `signfd_siginfo` 结构体。如果在调用时没有待处理信号，则 `read` 将阻塞直到信号到达。我们还可以使用 `fcntl()` 的 `F_SETFL` 操作（第 5.3 节）为文件描述符设置 `O_NONBLOCK` 标志，使得读取是非阻塞的，并在没有待处理信号时将以错误 `EAGAIN` 失败。

当从 `signalfd` 文件描述符读取信号时，该信号会被消费，不再对进程处于待处理状态。

### 列表 22-7: 使用 `signalfd()` 读取信号

```c
#include <sys/signalfd.h>
#include <signal.h>
#include <tlpi_hdr.h>

int
main(int argc, char *argv[])
{
    sigset_t mask;
    int sfd, j;
    struct signalfd_siginfo info;
    ssize_t s;

    if (argc < 2 || strcmp(argv[1], "-help") == 0)
        usageErr("%s sig-num...\n", argv[0]);

    printf("%s: PID = %ld\n", argv[0], (long) getpid());

    sigemptyset(&mask);
    for (j = 1; j < argc; j++)
        sigaddset(&mask, atoi(argv[j]));

    if (sigprocmask(SIG_BLOCK, &mask, NULL) == -1)
        errExit("sigprocmask");

    sfd = signalfd(-1, &mask, 0);
    if (sfd == -1)
        errExit("signalfd");

    for (;;) {
        s = read(sfd, &info, sizeof(struct signalfd_siginfo));
        if (s < 0)
            errExit("read");

        printf("%s: got signal %d\n", argv[0], info.ssi_sign);
        if (info.ssi_code == SIGINFO) {
            printf("%s: queued signal = %d, value = %d\n", argv[0], info.ssi_sign, info.ssi_int);
        }
    }
}
```

忽略的倾向。`sigpause()` 函数与 `sigsuspend()` 类似，它在挂起进程之前从进程信号掩码中移除仅一个信号，直到信号的到达。

## BSD 信号 API

POSIX 信号 API 很大程度上借鉴了 4.2BSD API，因此 BSD 函数是 POSIX 中函数的直接类比物。结合上述描述的 System V 信号 API 中的函数，我们现在给出 BSD 信号 API 中函数的原型，并简要解释每个函数的操作。再次重申，手册页提供了更详尽的细节。

```c
#define BSD_SOURCE
#include <signal.h>

int sigvec(int sig, struct sigvec *vec, struct sigvec *ovec);
// 成功时返回 0，出错时返回 -1
```

`sigvec()` 函数类似于 `sigaction()`。`vec` 和 `ovec` 参数是指向以下类型结构体的指针：

- `struct sigvec` {
    void (*sv_handler)();
    int sv_mask;
    int sv_flags;
};

`sigvec` 结构体的字段与 `sigaction` 结构的字段紧密对应。第一个显著区别是 `sv_mask` 字段（`sa_mask` 的类比）是一个整数而非 `sigset_t`，这意味着在 32 位架构上，最多有 31 种不同的信号。另一个区别是在 `sv_flags` 字段（`sa_flags` 的类比）使用了 `SV_INTERRUPT` 标志。在 4.2BSD 中，系统调用启动是默认的，该标志用于指定慢系统调用应被信号处理器中断。（这与 POSIX API 形成对比，在 POSIX 中，我们必须在使用 `sigaction()` 建立信号处理程序时显式指定 `SA_RESTART` 以启用系统调用重启。）

```c
#define BSD_SOURCE
#include <signal.h>

int sigblock(int mask);
int sigsetmask(int mask);

int sigpause(int sigmask);
// 都返回之前的信号掩码

// 始终返回 -1 并设置 errno 为 EINTR

int sigmask(sig);
// 返回带有位 sig 的信号掩码值
```

`sigblock` 函数向进程掩码添加一组信号。它类似于 `sigprocmask()` 的 `SIG_BLOCK` 操作。`sigsetmask()` 调用信号掩码的绝对值。它类似于 `sigprocmask()` 的 `SIG_SETMASK` 操作。

`sigpause()` 函数类似于 `sigsuspend()`。注意，该函数在 System V 和 BSD API 中具有相同的调用签名定义。除非我们在编译程序时指定了 `BSD_SOURCE` 特性测试，否则 GNU C 库默认提供 System V 版本。

`sigmask()` 宏将信号值转换为相应的 32 位掩码值。这些位可以进行位或（OR）操作以创建一个信号集，如下所示：

```c
sigblock(sigmask(SIGINT) | sigmask(SIGQUIT));
```

## 22.14 总结

某些信号会导致进程创建核心转储（core dump）并终止。核心转储包含调试器可以用于检查进程终止时进程状态的信息。默认情况下，核心转储文件命名为 `core`，但 Linux 提供了 `/proc/sys/kernel/core_pattern` 文件来控制核心转储的名称。

信号可以是异步或同步生成的。当信号由内核或另一个进程发送时，就会发生异步生成。进程无法精确预测异步生成的信号何时被递送。（我们注意到，异步信号通常在接收进程下次从内核模式切换到用户模式时被递送。）当进程本身执行直接生成信号的代码时，就会发生同步生成——例如，通过执行导致硬件异常的指令或调用 `raise()`。同步生成的信号的递送是精确可预测的（它立即发生）。
