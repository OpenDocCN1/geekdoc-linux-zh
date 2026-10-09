
```c
long snums[NUMNUM];

pthread_barrier_t b;

#ifdef SOLARIS

#define heapsort qsort

#else

extern int heapsort(void *, size_t, size_t,
int (*)(const void *, const void *));

#endif
/*
* 比较两个长整数（堆排序的辅助函数）
*/
int
complong(const void *arg1, const void *arg2)
{
    long l1 = *(long*)arg1;
    long l2 = *(long*)arg2;

    if (l1 == l2)
        return 0;
    else if (l1 < l2)
        return -1;
    else
        return 1;
}

/*
* 用于对数字部分进行排序的工作线程。
*/
void thr_fn(void *arg)
{
    long idx = (long)arg;
    heapsort(&nums[idx], TNUM, sizeof(long), complong);
    pthread_barrier_wait(&barrier);
    /*
    * 去执行更多工作 ...
    */
    return((void *)0);
}

/*
* 合并各个排序范围的结果。
*/
void merge()
{
    long idx[NTHR];
    long minid, sidx, num;

    for (i = 0; i < NTHR; i++)
        idx[i] = i * TNUM;
    for (sidx = 0; sidx < TNUM; sidx++) {
        num = LONG_MAX;
        for (i = 0; i < NTHR; i++) {
            if ((idx[i] < (i+1)*TNUM && nums[idx[i]] < num) {
                num = nums[idx[i]];
                minid = i;
            }
        }
        nums[sidx] = nums[idx[minid]];
        idx[minid]++;
    }
}

int main() {
    unsigned long i;
    long long start, end;
    double elapsed;
    int err;
    pthread_t tid;
    
    /*
     * 创建需要排序的初始数字集。
     */
    srand(1);
    for (i = 0; i < NUMNUM; i++)
        nums[i] = random();

    /*
     * 创建 8 个线程来对数字排序。
     */
    gettimeofday(&start, NULL);
    pthread_barrier_init(&b, NULL, NTHR+1);
    for (i = 0; i < NTHR; i++) {
        err = pthread_create(&tid, NULL, thr_fn, (void *)(i * TNUM));
        if (err != 0)
            err_exit(err, "cannot create thread");
    }
    pthread_barrier_wait(&b);
    merge();
    gettimeofday(&end, NULL);

    /*
     * 打印排序后的列表。
     */
    long long startusec = start.tv_sec * 1000000 + start.tv_usec;
    long long endusec = end.tv_sec * 1000000 + end.tv_usec;
    elapsed = (double)(endusec - startusec) / 1000000;
    printf("sort took %.4f seconds\n", elapsed);
    for (i = 0; i < NUMNUM; i++)
        printf("%ld\n", nums[i]);
    exit(0);
}
```

**图 11.16** 使用屏障

本章展示了在简化情况下`pthread_barrier_t`的使用，在这种简化情况下，线程只执行一项任务。在更实际的情况下，工作线程在调用`pthread_barrier_wait()`返回后将继续执行其他活动。

在示例中，我们使用 8 个线程来分担排序 800 万个数字的任务。每个线程使用堆排序算法排序 100 万个数字（详情请参见 Knuth [1998]）。主线程调用一个函数来合并结果。

我们不需要使用`pthread_barrier_wait()`的返回值`PTHREAD_BARRIER_SERIAL`来决定由哪个线程合并结果，因为我们使用主线程来完成工作。这就是为什么屏障计数比工作线程数多一个；主线程算作一个等待者。

如果我们写一个使用单线程排序 800 万个数字的程序，在与图 11.16 中的程序比较时，我们会看到性能的提升。在具有 8 核的系统上，单线程程序排序 800 万个数字花费了 12.4 秒。在同一系统上，使用 8 个线程并行以及一个线程合并结果，同样的 800 万个数字仅用 1.9 秒就完成了排序，速度快了 6 倍。

## 1 总结

在本章中，我们引入了线程的概念，并讨论了创建和销毁它们的 POSIX 原语。我们还引入了线程同步问题。我们讨论了五种基本机制——互斥锁、读写锁、条件变量、自旋锁和屏障以及如何使用它们来保护共享。

## 练习题

- 1.1 修改图 11.4 所示的代码，以便在线程之间正确传递结构体。
- 1.2 在图 11.14 所示的示例代码中，需要哪些额外的同步（如果有），允许主线程更改与挂起线程关联的线程 ID？这将如何影响`pthread_detach()`函数？
- 1.3 应用图 11.11 所示的技术，在图 11.15 中所示的线程中，可能会遇到哪些困难？
- 1.4 哪种顺序是正确的？
    1. `pthread_mutex_lock()`。
    2. 信号`condition`。
    3. `pthread_cond_broadcast()`。
    4. `pthread_mutex_unlock()`。
- 1.5 哪些同步原语可以实现屏障？`pthread_barrier_wait()`。

# 12 线程控制

## 12.1 引言

在 11 章中，我们学习了线程的基础。在本章中，我们将学习控制线程的细节。通过设置与每个对象关联的属性，线程接口可以调和同步对象。线程属性。属性属性。属性线程线程属性。

属性 线程线程线程的属性，， 111中中的的的属性。

## 12.2 线程限制

我们讨论了 2.5 节中的`sysconf()`函数。POSIX 标准定义了与线程相关的若干限制。1 1.. 总结了这些限制。

12.2 显示了书中描述的四种实现的线程限制。如果实现的限制是不定的，则列出“无限制”。然而，这并不意味着该值是无限的。

> 注意，尽管实现可能无法对这些限制进行访问，但这并不意味着限制并不存在。这意味着实现没有提供通过`sysconf`获取它们的方法。

| 限制名称 | 描述 | 参数 |
| :--- | :--- | :--- |
| `PTHREAD_DESTRUCTOR_ITERATIONS` | 线程退出时销毁线程特定数据的最大次数（12.6节） | `SC_THREAD_DESTRUCTOR_ITERATIONS` |
| `PTHREAD_KEYS_MAX` | 进程可以创建的键数（12.6节） | `SC_KEYS_MAX` |
| `PTHREAD_STACK_MIN` | 线程栈所需的最小字节数（12.3节） | `SC_STACK_MIN` |
| `PTHREAD_THREADS_MAX` | 进程允许的最大线程数（12.3节） | `SC_THREADS_MAX` |

**图 12.2** `sysconf` 的限制和参数

## 12.3 线程属性

线程接口允许我们通过设置与每个对象关联的属性，微调线程和同步对象的行为。通常，管理这些属性的函数遵循相同的模式：

- 每个对象都与其对应类型的属性对象关联（线程关联线程属性，互斥锁关联互斥锁属性）。属性对象可以表示多个属性。属性对象对应用程序是不透明的。这意味着应用程序不应该知道其内部结构。相反，提供了函数来管理属性对象。
- 有一个初始化函数用于将属性设置为默认值。
- 有另一个函数用于销毁属性对象。如果初始化函数分配了任何与属性对象相关的资源，销毁函数将释放这些资源。
- 每个属性都有一个用于获取属性对象值的函数。由于该函数在成功时返回 0，失败时返回错误号，因此值通过存储在参数之一指定的内存位置返回给调用者。
- 每个属性都有一个用于设置属性值的函数。在这种情况下，值是按值作为参数传递的。

在第 11 章中调用`pthread_create()`的所有示例中，我们传递了一个空指针而不是传递一个`pthread_attr_t`结构。我们可以使用`pthread_attr_t`来修改默认属性，并将这些属性与我们创建的线程关联。我们使用`pthread_attr_init()`来初始化`pthread_attr_t`结构。在调用`pthread_attr_init()`后，`pthread_attr_t`结构包含了实现支持的所有线程属性的默认值。

```c
#include <pthread.h>
int pthread_attr_init(pthread_attr_t *attr);
int pthread_attr_destroy(pthread_attr_t *attr);
```

两者均返回：成功返回 0，失败返回错误号

要取消初始化`pthread_attr_t`结构，我们调用`pthread_attr_destroy()`。如果`pthread_attr_init()`的实现为属性对象分配了任何动态内存，`pthread_attr_destroy()`将释放该内存。此外，`pthread_attr_destroy()`将用无效值初始化属性对象，因此如果误用，`pthread_attr_create()`将返回错误代码。

POSIX.1 定义的线程属性总结在图 12.3 中。POSIX.1 在线程执行调度中定义了额外的属性，旨在支持实时应用程序，但我们在这里不讨论它们。在图 12.3 中，我们展示了哪些平台支持每个属性。

| 名称 | 描述 | FreeBSD 8.0 | Linux 3.2.0 | Mac OS X 10.6.8 | Solaris 10 |
|---|---|---|---|---|---|
| `detachstate` | 离分离线程属性 | | | | |
| `guardsize` | 线程栈末端的缓冲区大小（字节） | | | | |
| `stackaddr` | 线程栈的最低地址 | | | | |
| `stacksize` | 线程栈的最小大小（字节） | | | | |

**图 12.3** POSIX.1 线程属性

在第 11.5 节中，我们引入了离分离线程的概念。如果我们不再感兴趣现有线程的终止状态，可以使用`pthread_detach()`允许操作系统在线程退出时回收该线程的资源。

如果我们在创建线程时知道我们不需要线程的终止状态，可以通过修改`pthread_attr_t`结构中的分离线程属性，安排让线程以离分离状态启动。我们可以使用`pthread_attr_setdetachstate()`函数将分离线程属性设置为两个合法值之一：`PTHREAD_CREATE_DETACHED`或`PTHREAD_CREATE_JOINABLE`，分别以离分离状态启动线程，或通过`PTHREAD_CREATE_JOINABLE`正常方式启动线程，以便应用程序可以检索其终止状态。

```c
#include <pthread.h>
int pthread_attr_getdetachstate(const pthread_attr_t *restrict attr,
                               int *detach);
int pthread_attr_setdetachstate(pthread_attr_t *attr, int detach);
// 两均返回：成功返回 0，失败返回错误号
```

我们可以调用`pthread_attr_getdetachstate()`获取当前分离状态属性。第二个参数指向的整数是`PTHREAD_CREATE_DETACHED`或`PTHREAD_CREATE_JOINABLE`，取决于给定`pthread_attr_t`结构中属性的运行值。

### 示例

图 12.4 展示了一个可以用于以分离状态创建线程的函数。

```c
#include "apue.h"
#include <pthread.h>

int
makethread(void (*fn)(void *), void *arg)
{
    int
        err;
        pthread_t tid;
        pthread_attr_t attr;

    err = pthread_attr_init(&attr);
    if (err != 0)
        return(err);
    err = pthread_attr_setdetachstate(&attr, PTHREAD_CREATE_DETACHED);
    if (err == 0) {
        err = pthread_create(&tid, &attr, fn, arg);
    }
    pthread_attr_destroy(&attr);
    return(err);
}
```

**图 12.4** 以分离状态创建线程

注意，我们忽略了`pthread_attr_destroy()`调用的返回值。在这种情况下，我们正确初始化了线程属性，因此`pthread_attr_destroy()`没有失败。然而，如果它失败了，清理工作将变得困难：我们必须销毁刚刚创建的线程，该线程可能已经在运行，且是异步于此函数的执行的。

使用`PTHREAD_MUTEX_INITIALIZER`常量或调用`pthread_mutex_init()`函数并将指向互斥锁属性结构的参数设置为空指针。

在处理非默认属性时，我们使用`pthread_mutexattr_init()`初始化一个`pthread_mutexattr_t`结构，并使用`pthread_mutexattr_destroy()`销毁它。

```c
#include <pthread.h>

int pthread_mutexattr_init(pthread_mutexattr_t *attr);
int pthread_mutexattr_destroy(pthread_mutexattr_t *attr);
```

两者均返回：0 表示成功，失败时返回错误。

`pthread_mutexattr_init()`函数将使用默认属性初始化`pthread_mutex_t`结构。共有三个属性：进程共享属性（process-shared）、健壮性属性（robust）和类型属性（type）。在 POSIX.1 中，进程共享属性是可选的；你可以通过检查传递`sysconf()`函数的`SC_THREAD_PROCESS_SHARED`符号参数来测试平台是否支持它。虽然 POSIX 标准的操作系统不要求提供此选项，但单 UNIX 规范（Single UNIX Specification）要求符合 XSI 标准的操作系统支持它。

在一个进程中，多个线程可以访问同一个同步对象。这是默认行为，正如我们在第 11 章所看到的。在这种情况下，进程共享互斥锁属性设置为`PTHREAD_PROCESS_PRIVATE`。

正如我们在第 14 和第 15 章中将看到的，某些机制允许独立进程将相同的内存映射到它们独立的地址空间中。多个进程对共享数据的访问通常需要同步，就像多个线程对共享数据的访问一样。如果进程共享互斥锁设置为`PTHREAD_PROCESS_SHARED`，则从进程间的内存区域分配的互斥锁可以被这些进程用于同步。

我们可以使用`pthread_mutexattr_getpshared()`函数查询`pthread_mutexattr_t`结构获取进程共享属性。我们可以使用`pthread_mutexattr_setpshared()`函数修改进程共享属性。

```c
#include <pthread.h>

int pthread_mutexattr_getpshared(const pthread_mutexattr_t *restrict attr, int *pshared);
int pthread_mutexattr_setpshared(pthread_mutexattr_t *attr, int pshared);
```

两者均返回：0 表示成功，失败时返回错误。

当属性设置为`PTHREAD_PROCESS_PRIVATE`时，进程共享属性允许库提供更高效的互斥锁实现，这是多线程应用程序的默认情况。线程库随后可以将开销较大的实现限制在互斥锁在进程间共享的情况下。

健壮性属性（robust）与多个进程间共享的互斥锁有关。它旨在解决进程在持有互斥锁时终止导致的互斥锁恢复问题。当这种情况发生时，互斥锁将处于锁定状态，且难以恢复。其他进程中阻塞在锁上的线程将无限期阻塞。
