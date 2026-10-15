

在任何一个 UNIX 系统中，你可能会发现其中一种解决方案被采用，而其他方案则没有，完全没有一致性。POSIX 标准在 sigaction() 接口中引入了一种统一的解决方案来解决这个问题。

## 5.3.11 The sigaction() call

sigaction() 系统调用允许一个进程安装信号处理程序并指定它将如何响应多个到达的信号。其原型为

```
#include <signal.h>
int (sigaction (int signum, const struct sigaction *act,
struct sigaction *oldaction);
```

其中

- signum 是要处理的信号的值
- act 是指向 sigaction 结构的指针，该结构指定了信号的处理程序、掩码和标志
- oldact 是指向结构的指针，用于保存当前活动的 sigaction 数据。

我们将首先检查 sigaction 结构，以了解此接口的灵活性。请注意，函数名与传递给它的结构地址的名称相同，就像 stat() 函数和 stat 结构一样。

## 5.3.12 The sigaction struct

sigaction 结构在 <signal.h> 中定义。该定义不寻常，因为它有两个成员（sa_handler 和 sa_sigaction），它们在内存中允许重叠并且必须互斥使用。最简单的方式是将其呈现为同一结构的两种不同的重载定义：

```
struct sigaction        // backward-compatible, old-style handler
{
    void (*sa_handler) (int); // the action to take
    sigset_t sa_mask;         // additional signals to block
                            // during handling of the signal
    int sa_flags;             // flags that affect behavior
};
```

或

```
struct sigaction        // POSIX compliant, new-style handler
{
void (*sa_sigaction) (int, siginfo_t *, void *);
sigset_t sa_mask;                 // pointer to signal handler
                                   // additional signals to block
int sa_flags;                       // during handling of the signal
};                                  // flags that affect behavior
```

换句话说，sigaction 结构有两种不同的形式。第一种使用旧式的处理程序，第二种使用更新的 POSIX 兼容方法。结构体在其他方面是相同的。

### Notes

在旧式中，sa_handler 成员不一定是指向函数的指针。它也可以是 SIG_IGN 或 SIG_DFL 两个标志之一。如果是 SIG_IGN，则忽略该信号；如果是 SIG_DFL，则执行默认操作。如果提供了指向处理程序的指针，则该处理程序将被运行。处理程序必须有一个整数参数。

在新样式中，sa_handler 被替换为指向具有三个参数的函数的指针，如下所示：

- 一个 sa_mask，它定义了在处理程序处理信号时应阻塞哪些信号。默认情况下，导致处理程序运行的信号将始终被阻塞。将信号添加到 SA_MASK 是一种阻塞其他信号的方式。

- sa_flags 是一个标志集合，可用于控制与导致处理程序运行的信号相同类型的后续信号如何被处理。例如，如果处理程序正在处理 SIGINT 信号，而在进程仍在处理程序中时又到达另一个 SIGINT，则 sa_flags 将决定如何处理第二个 SIGINT。它对其他到达的信号没有影响。标志决定了在处理程序被调用后到达的信号如何被处理。所有标志都是独立的，sa_flags 是它们的按位或。最重要的标志是：

SA_RESETHAND  如果设置了此位，则信号操作将被重置为 SIG_DFL。这意味着一旦信号被传递，默认操作就会发生。此标志隐含 SA_NODEFER 标志；信号不会被阻塞，而是导致进程采取该类型信号的默认操作。目的是使处理程序的行为类似于旧式的 signal() 处理程序，因为在第一个之后到达的任何信号都会导致默认行为。

SA_NODEFER  如果设置了此位，内核将不会在捕获信号时自动阻塞该信号。这意味着到达的信号将导致处理程序本身被中断并重新进入第二个信号。这是非自愿的递归。

SA_RESTART  如果设置了此位，则某些在信号在执行期间被传递时本应终止的系统调用将被自动重启。此位允许 BSD 风格的处理。

SA_SIGINFO  如果设置了此位，则向信号捕获函数传递两个额外的参数。如果第二个参数不为 NULL，则它指向一个 siginfo_t 结构，其中包含生成信号的原因；第三个参数指向一个 ucontext_t 结构，其中包含信号被传递时接收进程的上下文。

