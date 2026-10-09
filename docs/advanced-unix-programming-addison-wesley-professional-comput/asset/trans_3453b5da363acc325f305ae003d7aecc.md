

default:
    printf("Other signal\n");
}

将这段代码与本章的第一个示例进行对比，你会发现为调用 `sigaction` 做准备时的差异：设置了 `SA_SIGINFO` 标志，且处理函数的成员是 `sa_sigaction` 而不是 `sa_handler`。我将在下一节介绍信号 `SIGRTMIN`；在此之前，如果将其视为 `SIGUSR2` 有助于你理解代码，那就请这样认为。

尽管 `printf` 函数并非异步信号安全（async-signal-safe），但我们在信号处理函数中调用它是合法的，因为该信号是由一个异步信号安全的系统调用产生的：`kill` 或 `sigqueue`（我们稍后将在第 9.5.4 节中介绍）。

以下是我获得的输出：

signal number: 10
sending process ID: 29501
real user ID of sending process: 500
Signal from user
signal number: 32
sending process ID: 29501
real user ID of sending process: 500
Signal from sigqueue; value = 1234

信号处理函数的第三个参数 `context` 是指向 `ucontext_t` 类型对象的指针，它描述了接收进程在被中断时的上下文。之所以是指向 `void` 的指针而不是 `ucontext_t`，是因为在引入此原型时，该新类型尚未标准化。此指针并不总是被实现，也很少被使用。更多信息请参阅 [SUS2002] 或你系统的文档。

### 9.5.2 RTS 信号

RTS 引入了一组新信号，其编号范围从 `SIGRTMIN` 到 `SIGRTMAX`，至少提供 `RTSIG_MAX` 个信号。你可以在运行时通过 `sysconf`（第 1.5.5 节）获取实际数量，但它始终至少为 8。（事实上，在我的 Solaris 版本上就是如此；在 Linux 上则是 32。）

对于 RTS 生成函数（定义于第 9.5 节开头），你可以指定想要使用的信号，且应选择其中一个 RTS 信号；是否可以使用经典信号则取决于实现。

除了第一个和最后一个信号外，其他 RTS 信号没有对应的符号，因此你需要引用 `SIGRTMIN`、`SIGRTMIN + 1`，依此类推，直到 `SIGRTMAX`。当然，你会希望定义自己的宏，例如：

```c
#define DB_IO_DONE SIGRTMIN + 4
```

遗憾的是，两个库使用相同信号的问题并未由 POSIX.4 组解决，因此请小心。

`SIGRTMIN` 和 `SIGRTMAX` 不一定是常量整型表达式，因此你不能可移植地将其用作 case 标签或在预处理器表达式中（例如在 #ifs 中）使用。

如果有一个以上的 RTS 信号（SIGRTMIN 至 SIGRTMAX）处于挂起状态，编号最小的信号将首先被递送。因此，你可以将它们视为按优先级排序，在将它们分配给不同的应用目的时可能需要考虑这一点。所有 RTS 信号的默认操作都是终止。

### 9.5.3 排队信号

通常情况下，当同类型的信号已处于挂起状态时，如果生成了该信号，你不能指望会发生什么。如果实现不具备排队信号的能力，例如每种信号只保留一个标志，那么它会直接忽略第二个信号。你绝不应将信号用于计数目的——例如，用来跟踪 SIGUSR1 被发送的次数。

然而，对于 RTS，如果通过 sigaction 为该信号设置了 `SA_SIGINFO` 标志，由 RTS 生成函数（定义于第 9.5 节开头）发送的 RTS 信号（SIGRTMIN 至 SIGRTMAX）将被排队。经典信号是否也支持排队取决于实现，因此不要依赖这一点。许多系统即使你不设置 `SA_SIGINFO` 标志也会将 RTS 信号排队，这是完全合法的，但为了可移植性，你应该设置该标志。

如果你希望排队但不希望有信号处理函数，因为例如你打算使用 sigwait（第 9.2.2 节），似乎可以将 sigaction 结构体的 `sa_sigaction` 成员设置为 `SIG_DFL`，但 SUS 在此点上并不明确。为了安全起见，编码一个空的处理函数，并将操作指向该函数。

进程的队列长度最大至少为 32；你可以使用 sysconf（第 1.5.5 节）查找实际数量。

### 9.5.4 sigqueue

sigqueue—为进程生成信号

```c
#include <signal.h>
int sigqueue(
    pid_t pid,                   /* process ID */
    int signum,                 /* signal */
    const union sigval value
);
/* Returns 0 on success or -1 on error (sets errno) */
```

我们已经在第 9.5.1 节的示例中看到了 sigqueue 的使用。前两个参数与 kill 的参数类似，但 pid 只能是一个进程 ID——kill 的广播功能（例如，发送给所有进程）在这里不起作用。此外，你可以传递一个值，如果设置了 SA_SIGINFO 标志且信号处理函数使用第 9.5.1 节描述的三参数形式，该值即可被接收。你自己决定是要使用联合体中的 int 成员还是指针成员；处理函数必须知道使用哪一个，因为不会传递关于你使用了哪一个的信息。

如果你向另一个进程发送信号，你可能无法使用指针，因为该指针对于另一个进程没有意义。唯一有效的情况是，两个进程共享位于相同地址的内存，并且该指针指向该共享内存。

正如我在上一节中所述，如果设置了 SA_SIGINFO 标志且接收进程已有 signum 信号挂起，则新信号将被排队。

你只能对 RTS 信号（第 9.5.2 节）依赖排队和传递值的机制。

正如上一节所解释的，你只能排队有限数量的信号。如果新信号无法排队，sigqueue 返回 -1 并将 errno 设置为 EAGAIN。下一节中有一个使用 sigqueue 的另一个示例。

### 9.5.5 sigwaitinfo 和 sigtimedwait

第 9.2.2 节中的 sigwait 系统调用不是 RTS 的一部分，但它对 RTS 信号运行良好，即使在排队时也是如此。它接受一个挂起信号并返回它；如果仍有该类型的信号挂起，它们保持排队状态。与信号处理函数一样，如果有一个以上的 RTS 信号（SIGRTMIN 至 SIGRTMAX）挂起，最高优先级（编号最小）的信号将首先被接受。

但 `sigsuspend` 的问题是，你无法获取 `siginfo_t` 信息，包括 value，而这可能是 RTS 最重要的功能。因此，有一个略微增强的系统调用名为 `sigwaitinfo`：

`sigwaitinfo`—等待信号

```c
#include <signal.h>

int sigwaitinfo(
    const sigset_t *set,    /* signals to wait for */
    siginfo_t *info          /* returned info */
);                     /* Returns signal number or -1 on error (sets errno) */
```

如果 `info` 为 NULL，则不会返回信息，且 `sigwaitinfo` 与 `sigsuspend` 完全相同，区别在于信号编号作为函数返回值而不是通过参数返回。如果 `info` 非 NULL，它将接收与 `SA_SIGINFO` 风格信号处理函数相同的结构体，如第 9.5.1 节所述。与 `sigsuspend` 一样，请确保 `set` 中的信号被阻塞；否则，当其中一个信号被递送时将发生不可预测的行为。

这是一个使用排队信号的示例。首先，这是我们将使用的两个 RTS 信号的定义：

```c
#define MYSIG_COUNT  SIGRTMIN
#define MYSIG_STOP  SIGRTMIN + 1
```

以下是等待信号的线程的函数，如果它是 `MYSIG_COUNT` 则将其值显示为字符串，如果它是 `MYSIG_STOP` 则返回（终止线程）：

```c
static void *sig_thread(void *arg)
{
    int signum;
    siginfo_t info;

    do {
        signum = sigwaitinfo((sigset_t *)arg, &info);
        if (signum == MYSIG_COUNT)
            printf("Got MYSIG_COUNT; value: %s\n",
                   (char *)info.si_value.sival_ptr);
        else if (signum == MYSIG_STOP) {
            printf("Got MYSIG_STOP; terminating thread\n");
            return (void *)true;
        }
        else
            printf("Got %d\n", signum);
    } while (signum != -1 || errno == EINTR);
    EC_FAIL;

    EC_CLEANUP_BGN;
    EC_FLUSH("sig_thread");
    return (void *)false;
    EC_CLEANUP_END;
}
```

请注意，我们不能使用 switch 语句，因为如第 9.5.2 节所述，MYSIG_COUNT 和 MYSIG_STOP 可能是非常量整型表达式。

下面是主函数：

```c
int main(void)
{
    sigset_t set;
    struct sigaction act;
    union sigval value;
    pthread_t tid;

    ec_negl( sigemptyset(&set) )
    ec_negl( sigaddset(&set, MYSIG_COUNT) )
    ec_negl( sigaddset(&set, MYSIG_STOP) )
    ec_rv( pthread_sigmask(SIG_SETMASK, &set, NULL) )
    memset(&act, 0, sizeof(act));
    act.sa_flags = SA_SIGINFO;
    act.sa_sigaction = &dummy_handler;
    ec_negl( sigaction(MYSIG_COUNT, &act, NULL) )
    ec_negl( sigaction(MYSIG_STOP, &act, NULL) )
    value.sival_ptr = "One";
    ec_negl( sigqueue(getpid(), MYSIG_COUNT, value) )
    value.sival_ptr = "Two";
    ec_negl( sigqueue(getpid(), MYSIG_COUNT, value) )
    value.sival_ptr = "Three";
    ec_negl( sigqueue(getpid(), MYSIG_COUNT, value) )
    value.sival_ptr = NULL;
    ec_negl( sigqueue(getpid(), MYSIG_STOP, value) )
    ec_rv( pthread_create(&tid, NULL, sig_thread, &set) )
    ec_rv( pthread_join(tid, NULL) )
    exit(EXIT_SUCCESS);
}

