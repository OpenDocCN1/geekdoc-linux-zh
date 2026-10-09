

EC_CLEANUP_BGN
  @exit(EXIT_FAILURE);
EC_CLEANUP_END
}

static void dummy_handler(int signum, siginfo_t *info, void *context)
{
}

请注意，在线程创建之前已经生成了四个信号，以证明它们会被排队。由于这些信号的编号低于 `MYSIG_STOP`，因此保证在线程处理 `MYSIG_STOP` 之前会先接受 `MYSIG_COUNT` 个信号。还要注意，信号是被阻塞的，并且保持阻塞状态。需要设置一个空处理器，因为必须设置 `SA_SIGINFO` 以启用排队功能。恰好的是，Solaris 无论如何都会对 `RTS` 信号进行排队，但在可移植程序中不能依赖这一点。

以下是输出结果，证明了信号已被排队：

Got MYSIG_COUNT: value: One
Got MYSIG_COUNT: value: Two
Got MYSIG_COUNT: value: Three
Got MYSIG_STOP: terminating thread

如果你只想等待有限的时间，可以使用 `sigtimedwait`，它在 `sigwaitinfo` 的基础上增加了一个超时参数：

![](img/41b4c8f6d6a5c349eee321a301703d97_660_0.png)

`sigtimedwait` 最多等待 `ts` 指定的纳秒数，以便 `set` 中的某个信号变为待处理状态并返回。如果时间周期过期，它会返回 −1，并将 `errno` 设置为 `EAGAIN`。不能将超时设置为 `NULL`。如果 `timespec` 的两个成员都为零且 `set` 中没有待处理的信号，`sigtimedwait` 会立即返回，但这并不是真正的特殊情况——只是超时了而已。

### 9.5.6 sigevent 结构与 SIGEV_THREAD

除了 sigqueue 之外的 RTS 生成函数在其他地方都有描述，如第 9.5.1 节所列，但它们都使用 sigevent 结构来指定要发送的信号和值。我在此仅解释 sigevent 结构。

![](img/41b4c8f6d6a5c349eee321a301703d97_661_0.png)

要发送的信号（例如 SIGRTMIN）放入 sigev_signo，伴随的值放入 sigev_value。与其他 RTS 特性一样，它保证只对 RTS 信号有效。sigev_notify 成员指定信号如何发送：

- **SIGEV_SIGNAL** 生成一个信号，就好像调用了 sigqueue 一样
- **SIGEV_THREAD** 启动一个线程，就好像调用了 pthread_create 一样
- **SIGEV_NONE** 不提供任何通知，这通常没有太大意义

SIGEV_THREAD 是最有趣的。当事件发生时，每次发生都会启动一个新线程，并且由 sigev_notify_function 指向的函数成为该线程的启动函数。通常，启动函数有一个指向 void 的指针参数；在这种情况下，它是一个指向 union sigval 的指针，这大致相同，因为联合体的一个成员是一个 void 指针。你可以使用 sigev_notify_attributes 成员来设置线程的属性，但不能使线程可连接（joinable）。如果该成员为 NULL，线程默认是分离的（detached），这与 pthread_create 的默认行为相反。

创建线程有很大的开销，因此显然，除非事件相当罕见和/或其生成相对于启动新线程的成本来说代表大量工作，否则你不应该指定 SIGEV_THREAD。例如，每次有输入到达时都启动一个新线程可能有点过头了。

如果你感到困惑，当本来可以生成信号时创建线程，与让线程在 `sigwait`（第 9.2.2 节）中等待是完全不同的。它们唯一的共同点是都使用线程。

## 9.6 全局跳转

通常，函数仅通过执行 return 语句返回到调用者，或者如果它是 `void` 函数，则通过流经其外层块的末尾（效果相同）。但是，可以使用标准 C 函数 `setjmp` 和 `longjmp` 跳转到程序中任意但预先计划好的点：

**setjmp**—设置跳转点

```c
#include <setjmp.h>
int setjmp(
    jmp_buf loc_info      /* 保存的位置信息 */
);
/* 如果直接调用则返回 0，如果从 longjmp 返回则返回非零值
   （没有错误返回） */
```

**longjmp**—跳转到跳转点

```c
#include <setjmp.h>
void longjmp(
    jmp_buf loc_info,     /* 保存的位置信息 */
    int val               /* setjmp 返回的值 */
);
```

你通过调用 `setjmp` 来标记想要跳转的位置——可以说这是标签——它保存所需的位置信息（例如当前栈指针、机器地址）到其参数中，该参数看起来不像可以接收信息的指针，但实际上是。然后，从任何函数内部，无论嵌套多深，你执行 `longjmp` 并使用相同的参数，效果就好像 `setjmp` 返回了 `val`，而 `val` 不能为零；如果为零，`setjmp` 返回 1。

由于调用包含 `longjmp` 的函数可能向栈中压入了数据，`longjmp` 会自动将所有这些数据弹出。包含 `setjmp` 的函数没有被“调用”，返回时没有递归，尽管在调用 `longjmp` 的路径上可能存在递归。

这是一个例子。如果你以前从未见过 `setjmp` 和 `longjmp`，你会觉得它相当奇怪：

```c
static jmp_buf loc_info;

static void fcn2(void)
{
    printf("In fcn2\n");
    longjmp(loc_info, 1234);
    printf("Leaving fcn2\n");
}

static void fcn1(void)
{
    printf("In fcn1\n");
    fcn2();
    printf("Leaving fcn1\n");
}

int main(void)
{
    int rtn;

    rtn = setjmp(loc_info);
    printf("setjmp returned %d\n", rtn);
    if (rtn == 0)
        fcn1();
    printf("Exiting\n");
    exit(EXIT_SUCCESS);
}
```

以下是输出结果：

```
setjmp returned 0
In fcn1
In fcn2
setjmp returned 1234
Exiting
```

因此，你可以看到 setjmp 被调用了一次但返回了两次，并且跳转直接从 fcn2 的中间跳回到 main 的中间；两行“leaving”语句没有被打印出来。

如果你没有完全理解，不用担心，因为我接下来要说的是：永远不要使用 longjmp。原因如下：

- 虽然栈被清理了，但其他很少（例如，分配的内存、打开的文件）不会。
- 关于在哪里可以使用 setjmp 和 longjmp 有一些限制，如果你忘记了它们，就会陷入麻烦。
- 有些人（包括我）甚至不喜欢在函数 _内部_ 使用 `goto`。他们更不喜欢 `longjmp`。它使程序非常难以理解和维护。
- `longjmp` 的主要用途是从信号处理器中调用，但它不是异步信号安全的，因此你不能在那里使用它，除非你能保证信号处理器是由异步信号安全函数调用的，例如从同一进程内部执行的 `kill`（第 9.1.7 节）。

如果你认为需要 `longjmp`，那可能是因为你没有足够好地设计你的函数，使它们能够返回到调用者，也许带有一个错误或异常状态的指示。努力一点，你会想出办法的。

`longjmp` 可能会也可能不会恢复信号掩码。如果你想强制恢复它，有 `setjmp`/`longjmp` 的变体，它们是完全相同的，除了它们可以保存和恢复信号掩码：

**sigsetjmp**—设置跳转点

```c
#include <setjmp.h>
int sigsetjmp(
    sigjmp_buf loc_info,    /* 保存的位置信息 */
    int savemask             /* 非零以保存信号掩码 */
);
/* 如果直接调用则返回 0，如果从 siglongjmp 返回则返回非零值（没有错误返回） */
```

**siglongjmp**—跳转到跳转点，如果已保存则恢复信号掩码

```c
#include <setjmp.h>
void siglongjmp(
    sigjmp_buf loc_info,    /* 保存的位置信息 */
    int val                  /* sigsetjmp 返回的值 */
);
```

恢复的信号掩码是在调用 `sigsetjmp` 时生效的那个。如果 `siglongjmp` 在信号处理器内部被调用（这是它的设计目的），这可能不同于信号处理器如果允许正常返回时会恢复的掩码。

由于 `siglongjmp` 与 `longjmp` 一样不是异步信号安全的，它通常不能用于信号处理器中，因此其额外的恢复信号掩码的功能几乎无用。

