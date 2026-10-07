
`static void cleanupHandler(void *arg) { /* Free memory pointed to 'arg' */`

    `printf(1000);`

 /* cleanup: freeing memory */

    `free(arg);`

    `printf("cleanup: unlocking mutex\n");`

    `pthread_mutex_unlock(&mtx);`

}

`static void *threadFunc(void *arg) { /* Thread started thread */`

    `int s;`

    `void *buf = NULL; /* Buffer allocated by thread */`

    `buf = malloc(1000); /* Not a cancellation point */`

    `printf("thread: allocated memory at %p\n", buf);`

    `s = pthread_mutex_lock(&mtx); /* Not a cancellation point */`

    `if (s != 0)`

        `errExitIn(s, "pthread_mutex_lock");`

    `pthread_cleanup_push(cleanupHandler, buf);`

    `while (glob == 0) { /* Loop waiting for condition variable cond */`

        `s = pthread_cond_wait(&cond, &mtx); /* A cancellation point */`

        `if (s != 0)`

            `errExitIn(s, "pthread_cond_wait");`

    `}`

    `printf("thread: loop completed\n");`

    `pthread_cleanup_pop(1); /* Executes cleanup handler */`

    `return NULL;`

}

`int main(int argc, char *argv[]) {`

    `pthread_t thr;`

    `void *res;`

    `int s;`

    `s = pthread_create(&thr, NULL, threadFunc, NULL);`

    `if (s != 0)`

        `errExitIn(s, "thread_create");`

    `sleep(2); /* Give thread a chance to get started */`

    `if (argc == 1) { /* Cancel thread */`

        `printf("main: about to cancel thread\n");`

        `s = pthread_cancel(thr);`

        `if (s != 0)`

            `errExitIn(s, "pthread_cancel");`

    `} else { /* Signal condition variable */`

        `printf("main: about to signal condition variable\n");`

        `glob = 1;`

        `s = pthread_cond_signal(&cond);`

        `if (s != 0)`

            `errExitIn(s, "pthread_cond_signal");`

    `}`

    `s = pthread_join(thr, &res);`

    `if (s != 0)`

        `errExitIn(s, "pthread_join");`

    `if (res == PTHREAD_CANCELED)`

        `printf("main: thread was canceled\n");`

    `else`

        `printf("main: thread terminated normally\n");`

    `exit(EXIT_SUCCESS);`

}

| Case | Description |
| :--- | :--- |
| No command-line argument | The thread is canceled by `main()` ④. In this case, cancellation will occur at one of cancellation points shown in Table 32-1. The cleanup handler using `pthread_cleanup_push()` is invoked automatically. The associated global variable `glob` is first set to a nonzero value ⑤, which also causes the thread to call `pthread_cleanup_pop()` ⑥. The main program joins the terminated thread ⑦ and reports whether the thread was canceled or terminated normally. |
| Command-line argument | The thread terminates normally ⑧. |

## 32.6 异步可取消性

当一个线程被设置为异步可取消（取消类型为 `PTHREAD_CANCEL_ASYNCHRONOUS`）时，它可以在任何时间被取消（即在任何语言指令处）；取消信号的递送不会被延迟，直到该线程到达下一个取消点。

异步取消的问题在于，尽管清理处理程序（cleanup handlers）仍会被调用，但这些处理程序没有办法确定线程的状态。列表 32-2 中的程序采用了延迟可取消类型，该线程只有在执行 `pthread_cond_wait()` 调用时才可能被取消；到此时，我们已经知道 `buf` 已经初始化并指向一块分配的内存块，且互斥锁已锁定。然而，使用异步取消，线程可能在任何点被取消；例如，在 `malloc()` 调用之前、在加锁之间、以及在锁定互斥锁之后，清理处理程序无法知道是否发生了取消，或者具体需要哪些清理步骤。此外，线程还可能在 `malloc()` 调用期间被取消，这在执行时是一场灾难（第 7.1.3 节）。

作为一个通用原则，异步可取消的线程不能分配任何资源，也不能获取任何互斥锁、信号量或锁。这排除了大量库函数的使用，包括大多数 Pthreads 函数。Sys33 对 `pthread_cancel()`、`pthread_cancelstate()` 和 `pthread_canceltype()` 做了例外处理，这些函数被明确要求是异步取消安全的（即在该实现中，确保了从异步可取消的线程中调用它们是安全的）。换句话说，异步取消有用的情况很少。其中一种情况是取消一个处于计算密集型循环中的线程。

## 32.7 总结

`pthread_cancel()` 函数允许一个线程向另一个线程发送取消请求，该请求要求目标线程终止。

目标线程如何反应取决于它的取消状态和类型。如果取消取消状态当前被设置为禁用（disabled），则结果将保持挂起状态，直到取消状态被设置为启用（enabled）。如果启用了取消，则由取消类型决定目标线程何时响应请求。如果类型是延迟的（deferred），取消发生在线程下次调用 Sysv3 指定为取消点的函数之一时。如果类型是异步的（asynchronous），取消可能在任何时间发生（这很少用）。

线程可以建立一个清理处理程序栈，这些是程序员定义的函数，当线程被取消时会被自动调用以执行清理工作（例如恢复共享变量的状态或解锁互斥锁）。

## 更多信息

请参阅第 29.10 节列出的信息源。

## 33
## 线程：更多细节

本章提供了 POSIX 线程各个方面的更多详细信息。我们讨论了线程与传统 UNIX API 各部分的交互——特别是信号和进程控制原语 `fork()`、`exec()` 和 `exit()`。我们还概述了 Linux 上可用的两种 POSIX 线程实现——LinuxThreads 和 NPTL，并指出了这些实现在何处偏离了 SUSv3 的 Pthreads 规范。

### 33.1 线程栈

每个线程都有自己的栈大小，该大小在线程创建时是固定的。在 Linux/x86-32 上，除主线程外的所有线程，每个线程栈的默认大小为 2 MB。（在某些 64 位架构上，默认大小更高；例如在 IA-64 上为 32 MB）。主线程拥有更大的栈增长空间。

有时，更改线程栈的大小是有用的。`pthread_attr_setstacksize()` 函数设置一个线程属性，该属性决定使用线程属性对象创建的线程的栈大小。相关的 `pthread_attr_setstack()` 函数可以同时控制栈的大小和位置，但设置位置可能会降低程序的移植性。手册提供了这些函数的详细信息。

更改每个线程栈大小的原因之一是，为那些分配了大型自动变量或进行深度嵌套函数调用（可能是由于递归）的线程提供更大的栈。或者，应用程序可能想要减小每个线程栈的大小，以便在进程中容纳更多线程。例如，在 x86-32 上，用户可访问的虚拟地址空间为 3 GB，2 MB 的默认栈大小意味着我们最多可以创建大约 1500 个线程。（精确值取决于文本段、数据段、共享库等消耗了多少内存）。在特定架构上可以使用的最小栈可以通过调用 `syscall(SC_THREAD_MIN)` 来确定。对于 Linux/x86-32 上的 NPTL 实现，它返回值为 16384。

在 NPTL 线程实现下，如果栈大小限制（`RLIMIT_STACK`）被设置为无限（unlimited）以外的任何值，则它将作为创建新线程时的默认栈大小。此限制必须在程序执行之前设置，通常是在执行程序之前使用 `ulimit` 内置命令（在 C shell 中限制栈大小）。在主程序中使用 `setlimit()` 来设置限制是不够的，因为 NPTL 是在 `main()` 被调用之前的运行时初始化期间确定其默认栈大小的。

### 33.2 线程与信号

UNIX 信号模型的设计是考虑到 UNIX 进程模型的，并且其出现比 Pthreads 的出现早了几个十年。因此，信号模型和线程模型之间存在显著冲突。这些冲突主要源于信号模型和线程模型需要维护信号语义（即进程范围的操作）。由于信号模型和线程模型的差异，结合信号和线程是复杂的，但尽管如此，有时我们必须处理信号。在本节中，我们将讨论信号之间的交互并描述一些有用的函数。

#### 33.2.1 信号如何映射到线程

要理解 UNIX 信号如何映射到线程，需要区分哪些是进程范围的（即所有线程共享），哪些是特定的线程。以下列表总结了关键点：

- 信号动作是进程范围的。如果一个线程为 `SIGINT` 建立了处理程序，那么该处理程序将被所有线程共享。
- 信号处置是进程范围的。如果一个线程将信号设置为忽略（ignore），那么该信号对所有线程都忽略。
- 由其他机制生成的信号是定向的。例如使用 `kill()` 或 `sigqueue()` 允许向另一个线程发送信号。

信号可能定向到特定线程，如果：
- 它是执行硬件异常的直接结果（见第 22.4 节：`SIGBUS`、`SIGFPE`、`SIGILL`、`SIGGV`）；
- 它是写入管道时生成的 `SIGPIPE`；
- 它是通过 `pthread_kill()` 或 `pthread_sigqueue()` 发送的（见第 33.2.3 节）。

当信号递送到建立了处理程序的进程线程进程时，内核会主动选择一个线程并在其中调用处理程序。这种行为与维护传统的信号语义是一致的。对于同一个信号，让进程执行多次信号处理是没有意义的。

信号掩码是每个线程的（多线程进程中不存在控制所有线程的进程范围信号掩码）。线程独立地使用 `pthread_sigmask()`（由 Pthreads API 定义）来阻塞或取消信号。通过操作线程线程信号掩码，应用程序可以控制哪些线程可以处理指向整个进程的信号。

内核维护进程挂起的信号记录，同时也维护每个线程挂起的信号记录。`sigpending()` 调用返回进程挂起信号和调用线程挂起信号的并集。在新创建的线程中，挂起信号集最初为空。线程定向可以递送到目标线程。如果线程阻塞了信号，它将一直保持直到线程取消信号（或终止）。

如果信号处理程序中断了 `pthread_mutex_lock()` 调用，则它会自动重启。如果信号处理程序中断了 `pthread_cond_wait()` 调用，则该调用会自动重启（这是 Linux 的做法）或返回 0 表示发生了虚假唤醒（在这种情况下，良好的应用程序将重新检查相应的变量并重启调用，见第 30.2.3 节），这要求这两个函数按照此处描述的方式运行。

- 备用栈是每个线程的（参见第 21.3 节中对 `signalstack()` 的描述）。新创建的线程不会从其创建者处继承备用信号栈。

#### 33.2.2 操作线程信号掩码

当创建一个新线程时，它会继承创建它的线程的信号掩码副本。线程可以使用 `pthread_sigmask()` 来更改其信号掩码、获取现有的掩码，或两者兼顾。

```c
#include <signal.h>

int pthread_sigmask(int how, const sigset_t *set, sigset_t *oldset);

// 成功返回 0，错误返回正错误数
```

除了操作对象是线程信号掩码外，`pthread_sigmask()` 的用法与 `sigprocmask()`（第 20.10 节）相同。

> SUSv 注意，在多线程程序中使用 `sigprocmask()` 的行为是不指定的。我们不能在多线程程序中使用 `sigprocmask()`。在实践，包括 Linux 在内的许多实现中，`sigprocmask()` 和 `pthread_sigmask()` 是相同的。

#### 33.2.3 向线程发送信号

`pthread_kill()` 函数向同一进程中的另一个线程发送信号 `sig`。目标线程通过参数 `thread` 标识。

```c
#include <signal.h>

int pthread_kill(pthread_t thread, int sig);

// 成功返回 0，错误返回正错误数
```

由于线程 ID 仅保证在进程内是唯一的（第 29.5 节），我们无法使用 `pthread_kill()` 向另一个进程中的线程发送信号。

`pthread_kill()` 是使用 Linux 特有的 `tgkill(tid, tid, sig)` 系统调用实现的，该调用向由 `tid` 标识的线程组内由 `tid` 标识的线程（由 `gettid()` 返回类型的内核 ID）发送信号 `sig`。更多细节参见 `tgkill(2)` 手页。

Linux 特有的 `pthread_sigqueue()` 结合了 `pthread_kill()` 和 `sigqueue()`（第 22.8.1 节）的功能：它向同一进程中的另一个线程发送带有数据的信号。

```c
#define _GNU_SOURCE
#include <signal.h>

int pthread_sigqueue(pthread_t thread, int sig, union sigval value);

// 成功返回 0，错误返回正错误数
```

与 `pthread_kill` 类似，`sig` 指定要发送的信号，`thread` 标识目标线程。`value` 参数指定随信号发送的数据，其用法与 `sigqueue()` 的等效参数相同。

`pthread_sigqueue` 函数在 glibc 2.11 版本中加入，并需要内核的支持。这种支持由在 Linux 2.6.31 中引入的 `rt_sigqueueinfo()` 系统调用提供。

#### 3.2.4 安全地处理异步信号

在第 20 到 22 节中，我们讨论了各种因素——例如重入性问题、重启系统调用的需要，以及避免竞态条件——这些因素使得通过信号处理程序处理异步生成的信号变得复杂。此外，Pthreads API 中的所有函数都不属于可以从信号处理程序安全调用的异步信号安全（async-signal-safe）函数集（第 21.1.2 节）。由于这些原因，必须处理异步生成信号的多线程程序通常不应使用信号处理程序作为接收信号传递通知的机制。推荐的方法如下：

- 所有线程都阻塞进程可能接收的所有异步信号。此的最简单的方法是在创建任何其他线程之前在主线程中阻塞信号。随后创建的每个线程都将继承主线程信号掩码的副本。
- 创建一个小型专用线程，使用 `sigwaitinfo()`、`sigtimedwait()` 或 `sigwait()` 接收传入信号。我们在第 22.10 节中描述了 `sigwaitinfo()` 和 `sigtimedwait()`。我们在下方描述 `sigwait()`。

这种方法的优点是异步生成的信号是同步接收的。由于它是同步接收的，该专用线程可以安全地修改变量（在互斥锁控制下）并调用所有非异步安全的函数。它还可以指示条件变量，并采用其他的线程和进程间通信及同步机制。

`sigwait()` 函数等待 `set` 所指向的集合中某个信号的传递，接收该信号并将其返回到 `sig`。

```c
#include <signal.h>

int sigwait(const sigset_t *set, int *sig);

// 成功返回 0，错误返回正错误数
```
