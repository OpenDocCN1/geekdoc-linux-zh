

[SUS2002] 仅规定了前两个成员。更新的 BSD 系统，包括 FreeBSD，支持所有成员。Solaris 8（至少在 Intel 架构上）仅支持标准成员；Linux 2.4 支持标准成员以及 `ru_minflt`、`ru_majflt` 和 `ru_nswap`。有关这些成员含义的详细信息，请查阅你系统的 `getrusage` 手册页；若要了解全貌，如果有条件，请在基于 BSD 的系统中运行它。

返回的两个时间类似于 `times` 返回的时间（第 1.7.2 节），但分辨率更高，因为 `timeval`（第 1.7.1 节）是以微秒为单位的。

## 5.17 线程简介

本节将非常简要地介绍线程，内容仅足以展示一些有趣的示例程序。我的目标是解释它们是什么，帮助你判断应用设计是否可能从中受益，并提醒你如果不小心使用它们可能会遇到的危险。

若要了解线程的全部真相（管理它们需要大约一百个系统调用），你不得不找一本相关书籍，例如 [Norl997] 或 [But1997]。

### 5.17.1 线程创建

在之前的示例中，我们创建（通过 `fork`）的进程只有一个控制流，或*线程*。执行从一条指令顺序进行到下一条指令，在一个单一序列中，堆栈、全局数据和系统资源会被各种指令修改，其中一些指令可能执行了系统调用。

借助 UNIX 的 POSIX 线程功能，一个进程可以拥有多个线程，每个线程都有自己的控制流（自己的指令计数器和 CPU 时钟）以及自己的堆栈。除了这些，关于该进程的一切，包括全局数据和资源（如打开的文件或当前目录），都是共享的。<sup>18</sup>以下代码说明了我的意思。

- 18. 线程还可以安排拥有一些线程特定数据；有关详情，请参阅 [SUS2002] 或所引用的任何一本参考书。

```c
static long x = 0;

static void *thread_func(void *arg)
{
    while (true) {
        printf("Thread 2 says %ld\n", ++x);
        sleep(1);
    }
}

int main(void)
{
    pthread_t tid;

    ec_rv( pthread_create(&tid, NULL, thread_func, NULL) )
    while (x < 10) {
        printf("Thread 1 says %ld\n", ++x);
        sleep(2);
    }
    return EXIT_SUCCESS;

EC_CLEANUP_BGN
    return EXIT_FAILURE;
EC_CLEANUP_END
}
```

线程打印的顺序是不可预测的；这是我们碰巧得到的输出：

```
Thread 2 says 1
Thread 1 says 2
Thread 2 says 3
Thread 1 says 4
Thread 2 says 5
Thread 2 says 6
Thread 1 says 7
Thread 2 says 8
Thread 2 says 9
Thread 1 says 10
Thread 2 says 11
Thread 2 says 12
```

因此你可以看到，两个线程——main 中的那个和 thread_func 中的那个——都访问了同一个全局变量 x。这存在一些我在第 5.17.3 节中会讨论的问题。

初始线程——包含 main 的那个——通过 pthread_create 系统调用启动了第二个线程：

```c
pthread_create—创建线程

#include <pthread.h>

int pthread_create(
    pthread_t *thread_id,      /* 新线程的 ID */
    const pthread_attr_t *attr, /* 属性（或 NULL） */
    void *(*start_fcn)(void *), /* 启动函数 */
    void *arg                 /* 传递给启动函数的参数 */
);
/* 成功时返回 0，出错时返回错误号 */
```

新线程从调用在 `pthread_create` 调用中指定的启动函数开始，该函数必须具有如下原型：

```c
pthread 启动函数

void *start_fcn(
    void *arg
);
/* 返回退出状态 */
```

你传递给 `pthread_create` 的第四个参数将直接传递给启动函数。为了通用性，它是一个 `void` 指针，通常它确实是指向某些数据的指针。由于线程共享同一地址空间，该指针对两个线程都有效。如果你愿意，也可以传入整型数据，但必须将其强制转换为 `void` 指针。并且，为了安全起见，你应该检查（例如使用 `assert`）你使用的整型大小是否适合放在 `void` 指针中，使用类似下面这样的代码，你会在随后的某些示例中看到：

```c
assert(sizeof(long) <= sizeof(void *));
```

影响新线程的属性不仅仅是一些标志，而是一个类型为 `pthread_attr_t` 的对象，你必须使用诸如 `pthread_attr_setscope` 和 `pthread_attr_setstacksize` 这样的调用对其进行设置，这里我不展开讨论。（但也许你已经开始理解为什么有一百个线程相关的调用了。）在我们的示例中，我们只使用默认属性，因此我们传递给 `pthread_create` 的第二个参数将是 NULL。

“pthread” 函数统一在成功时返回 0，失败时返回错误码，而不是设置 errno。我们有一个特殊的“ec”宏用于此目的，`ec_rv`，它接收错误码（如果有的话），并将其视为一个 `errno` 值，因为它确实是一个 `errno` 值。<sup>19</sup>

> 19. 错误检查包中的各个函数已修改为线程安全，但本书未展示相关代码。不过，你可以在网站上看到。

### 5.17.2 等待线程终止

线程可以等待另一个线程终止并获取其退出状态，使用 `pthread_join`（类似于 wait 及其变体）。

```c
pthread_join—等待线程终止
#include <pthread.h>
int pthread_join(
    pthread_t thread_id,   /* 要加入的线程 ID */
    void **status_ptr      /* 返回的退出状态（如果参数不为 NULL） */
);
/* 成功时返回 0，出错时返回错误号 */
```

以下是我修改后的小示例，使得线程 1 将限制传递给线程 2，然后线程 2 将 x 的值报告回线程 1：

```c
static long x = 0;

static void *thread_func(void *arg)
{
    while (x < (long)arg) {
        printf("Thread 2 says %ld\n", ++x);
        sleep(1);
    }
    return (void *)x;
}

int main(void)
{
    pthread_t tid;
    void *status;

    assert(sizeof(long) <= sizeof(void *));
    ec_rv( pthread_create(&tid, NULL, thread_func, (void *)6) )
    while (x < 10) {
        printf("Thread 1 says %ld\n", ++x);
        sleep(2);
    }
    ec_rv( pthread_join(tid, &status) )
    printf("Thread 2’s exit status is %ld\n", (long)status);
    return EXIT_SUCCESS;

EC_CLEANUP_BGN
    return EXIT_FAILURE;
EC_CLEANUP_END
}
```

输出如下：

```
Thread 1 says 1
Thread 2 says 2
Thread 2 says 3
Thread 1 says 4
Thread 2 says 5
Thread 2 says 6
Thread 1 says 7
Thread 1 says 8
Thread 1 says 9
Thread 1 says 10
Thread 2's exit status is 7
```

### 5.17.3 线程同步（互斥锁）

正如我们将在接下来的几章中看到的那样，在 UNIX 上处理多进程（可能跨越网络）的挑战是允许它们共享数据。对于线程来说情况恰恰相反——挑战在于保持其自然的数据共享是分离的。实际上，我展示的两个线程示例都有缺陷，因为两个线程都可能同时访问相同的数据，即变量 x。虽然简单的自增运算符似乎是一个原子操作，但没有保证它一定是。实际上，线程 1 可能在更新 32 位 x 的一半时，线程 2 读取了整个 32 位，得到一个混合体而不是有效的整数。<sup>20</sup> 对于更复杂的共享数据结构——这是一个更现实的情况——问题严重得多。我们希望访问共享数据是原子的。这意味着以下两个示例：

- 如果更新数据结构使其暂时处于不一致状态，除了正在更新的那个线程外，其他线程不应看到这种状态，并且
- 如果一个线程必须读取数据、计算结果并写回，其他线程不应修改数据，直到整个序列完成。否则，其他线程的修改将丢失。

一些简单的系统调用提供了这些需求，它们实现互斥对象，简称为互斥锁（mutexes）。线程使用它们来保护临界区，以免其他线程看到不一致的数据或干扰更新。主要的互斥锁系统调用是 pthread_mutex_lock 和 pthread_mutex_unlock：

> 20. 而这只是可能出错的一件事。另一件事是编译器优化可能会将整数留在寄存器中。你真的永远不能让线程在未加保护的情况下同时访问数据。

