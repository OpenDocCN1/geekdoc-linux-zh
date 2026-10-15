
成功时返回 `0`，出错时返回正错误号

要锁定互斥锁，我们在调用 `pthread_mutex_lock` 时指定该互斥锁。如果互斥锁当前未锁定，则此调用将锁定互斥锁并立即返回。如果互斥锁当前被另一个线程锁定，则 `pthread_mutex_lock()` 将阻塞，直到互斥锁被解锁，此时它将锁定互斥锁并返回。

如果调用线程已经锁定了传递给 `pthread_mutex_lock()` 的互斥锁，那么对于默认类型的互斥锁，可能会产生两种实现定义的可能结果之一：线程阻塞并尝试锁定它已经锁定的互斥锁，或者调用失败并返回错误 `EDEADLOCK`。在 Linux 上，线程默认会发生死锁。（我们在查看 `30.1.7` 节中的互斥锁类型时会描述其他其他行为）。

`pthread_mutex_unlock()` 函数解锁之前由调用线程锁定的互斥锁。解锁一个当前未锁定的互斥锁，或解锁一个被另一个线程锁定的互斥锁，都是错误。

如果有多个线程等待获取由调用 `pthread_mutex_unlock()` 解锁的互斥锁，则无法确定哪个线程将成功获取它。

# 示例程序

列表 `30-2` 是列表 `30-1` 中程序的修改版本。它使用一个互斥锁来保护对全局变量 `glob` 的访问。当我们使用之前讨论过的类似命令行运行此程序时，`glob` 总是能够可靠地递增：

```
$ ./thread_incr_mutex 1000000

glob = 2000000
```

列表 `30-2`：使用互斥锁保护对全局变量的访问 `threads/thread_incr_mutex.c`

```cc
#include <pthread.h>
#include <tlpi_hdr.h>
static int glob = 0;
static pthread_mutex_t mtx = PTHREAD_MUTEX_INITIALIZER;
static void *
/* 循环 'arg' 线程增加 'glob' */
threadfunc(void *arg)
{
    int loops = *((int *)arg);
    int loc, j, s;
    for (j = 0; j < loops; j++) {
        s = pthread_mutex_lock(&mtx);
        if (s != 0)
            errExitEN(s, "pthread_mutex_lock");
        loc = glob;
        loc++;
        glob = loc;
        s = pthread_mutex_unlock(&mtx);
        if (s != 0)
            errExitEN(s, "pthread_mutex_unlock");
    }
    return NULL;
}
int
main(int argc, char *argv[])
{
    pthread_t t1, t2;
    int loops;
    loops = (argc > 1) ? getInt(argv[1], GN_GT_0, "num-loops") : 10000000;
    s = pthread_create(&t1, NULL, threadFunc, &loops);
    if (s != 0)
        errExitEN(s, "pthread_create");
    s = pthread_create(&t2, NULL, threadFunc, &loops);
    if (s != 0)
        errExitEN(s, "pthread_create");
    s = pthread_join(t1, NULL);
    if (s != 0)
        errExitEN(s, "pthread_join");
    s = pthread_join(t2, NULL);
    if (s != 0)
        errExitEN(s, "pthread_join");
    printf("glob = %d\n", glob);
    exit(EXIT_SUCCESS);
}
```

> `threads/thread_incr_mutex.c`

# `pthread_mutex_trylock()` 和 `pthread_mutex_timedlock()`

Threads API 提供了 `pthread_mutex_lock()` 函数的两个变体：`pthread_mutex_trylock()` 和 `pthread_mutex_timedlock()`。（这些函数的原型请参阅手册页。）

`pthread_mutex_trylock()` 函数与 `pthread_mutex_lock()` 相同，不同在于如果互斥锁当前已被锁定，`pthread_mutex_trylock()` 将失败并返回错误 `EBUSY`。

`pthread_mutex_timedlock()` 函数与 `pthread_mutex_lock()` 相同，不同在于调用者可以指定一个额外的参数 `abstime`，该参数限制了线程在等待获取互斥锁时的睡眠时间。如果 `abstime` 指定的时间间隔过期而调用者未成为互斥锁的所有者，`pthread_mutex_timedlock()` 将返回错误 `ETIMEDOUT`。

`pthread_mutex_lock()` 和 `pthread_mutex_timedlock()` 函数的使用频率远低于 `pthread_mutex_lock()`。在大多数设计良好的应用程序中，线程应该持有互斥锁很短的时间，以防止其他线程无法并行执行。这保证了在互斥锁上阻塞的其他线程将很快获得锁。使用 `pthread_mutex_trylock()` 轮询互斥锁以检查是否可以锁定的线程，面临由于互斥锁访问的风险，而队列中的线程却通过 `pthread_mutex_trylock()` 成功获得了互斥锁访问。

# 30.13 互斥锁的性能

使用互斥锁的代价是什么？我们展示了两个增加共享变量的程序。当我们使用之前讨论过的类似命令行运行此程序时，`glob` 总是能够可靠地递增：

```
$ ./thread_incr_mutex 1000000

glob = 2000000
```

列表 `30-2`：使用互斥锁保护对全局变量的访问 `threads/thread_incr_mutex.c`

```c
#include <pthread.h>
#include <tlpi_hdr.h>
static int glob = 0;
static pthread_mutex_t mtx = PTHREAD_MUTEX_INITIALIZER;
static void *
/* 循环 'arg' 线程增加 'glob' */
threadfunc(void *arg)
{
    int loops = *((int *)arg);
    int loc, j, s;
    for (j = 0; j < loops; j++) {
        s = pthread_mutex_lock(&mtx);
        if (s != 0)
            errExitEN(s, "pthread_mutex_lock");
        loc = glob;
        loc++;
        glob = loc;
        s = pthread_mutex_unlock(&mtx);
        if (s != 0)
            errExitEN(s, "pthread_mutex_unlock");
    }
    return NULL;
}
int
main(int argc, char *argv[])
{
    pthread_t t1, t2;
    int loops;
    loops = (argc > 1) ? getInt(argv[1], GN_GT_0, "num-loops") : 10000000;
    s = pthread_create(&t1, NULL, threadFunc, &loops);
    if (s != 0)
        errExitEN(s, "pthread_create");
    s = pthread_create(&t2, NULL, threadFunc, &loops);
    if (s != 0)
        errExitEN(s, "pthread_create");
    s = pthread_join(t1, NULL);
    if (s != 0)
        errExitEN(s, "pthread_join");
    s = pthread_join(t2, NULL);
    if (s != 0)
        errExitEN(s, "pthread_join");
    printf("glob = %d\n", glob);
    exit(EXIT_SUCCESS);
}
```

> `threads/thread_incr_mutex.c`

# `pthread_mutex_trylock()` 和 `pthread_mutex_timedlock()`

Threads API 提供了 `pthread_mutex_lock()` 函数的两个变体：`pthread_mutex_trylock()` 和 `pthread_mutex_timedlock()`。（这些函数的原型请参阅手册页。）

`pthread_mutex_trylock()` 函数与 `pthread_mutex_lock()` 相同，不同在于如果互斥锁当前已被锁定，`pthread_mutex_trylock()` 将失败并返回错误 `EBUSY`。

`pthread_mutex_timedlock()` 函数与 `pthread_mutex_lock()` 相同，不同在于调用者可以指定一个额外的参数 `abstime`，该参数限制了线程在等待获取互斥锁时的睡眠时间。如果指定的时间间隔过期而调用者未成为互斥锁的所有者，`pthread_mutex_timedlock()` 将返回错误 `ETIMEDOUT`。

`pthread_mutex_lock()` 和 `pthread_mutex_timedlock()` 函数的使用频率远低于 `pthread_mutex_lock()`。在大多数设计良好的应用程序中，线程应该持有互斥锁很短的时间，以防止其他线程无法并行执行。这保证了在互斥锁上阻塞的其他线程将很快获得锁。使用 `pthread_mutex_trylock()` 轮询互斥锁以检查是否可以锁定的线程，面临由于互斥锁访问的风险，而队列中的线程却通过 `pthread_mutex_trylock()` 成功获得了互斥锁访问。

# 30.14 互斥死锁

有时，线程需要同时访问两个或多个共享资源，每个资源都由一个独立的互斥锁管理。当多个线程锁定同一组互斥锁时，就会出现死锁情况。图 `30-3` 显示了一个示例，每个线程都成功锁定了一个互斥锁，然后尝试锁定另一个线程已经锁定的互斥锁。两个线程将保持阻塞。

线程 A          线程 B

- 1. `pthread_mutex_lock(mutex1);`
- 2. `pthread_mutex_lock(mutex2);`

- 1. `pthread_mutex_lock(mutex2);`
- 2. `pthread_mutex_lock(mutex1);`

**图 30-3:** 两个线程锁互斥锁时的死锁

避免此类死锁的最方法是定义互斥锁层次。当线程锁定同一组互斥锁时，它们应该始终以相同的顺序锁定。例如，在图 `30-3` 的场景中，如果两个线程按照 `mutex1` 后 `mutex2` 的顺序锁定，则可以避免死锁。有时，存在逻辑上明显的互斥锁层次。然而，即使不存在，也可能设计出所有线程都遵循的任意顺序。

另一种较少使用的策略是线程使用 `pthread_mutex_lock()` 锁定第一个互斥锁，然后使用 `pthread_mutex_trylock()` 锁定剩余的互斥锁。如果任何 `pthread_mutex_trylock()` 调用失败（`EBUSY`），则线程释放所有互斥锁，然后再次尝试，可能在一段延迟之后。这种方法比锁层次效率低，因为可能需要多次迭代。

# 30.15 动态初始化互斥锁

静态初始化器 `PTHREAD_MUTEX_INITIALIZER` 只能用于初始化静态分配互斥锁。在所有其他情况下，我们必须使用 `pthread_mutex_init()` 动态初始化互斥锁。

```c
#include <pthread.h>
int pthread_mutex_init(pthread_mutex_t *mutex, const pthread_mutexattr_t *attr);
```

成功时返回 `0`，出错时返回正错误号

`mutex` 参数标识要初始化的互斥锁。`attr` 参数是一个指向 `pthread_mutexattr_t` 对象的指针，该对象之前已初始化以定义互斥锁的属性。（我们将在下一节中更多地介绍互斥锁属性。）如果 `attr` 指定为 `NULL`，则互斥锁将被分配各种默认属性。

SUSv3 规定，初始化一个已经初始化的互斥锁会导致未定义行为；我们不应该这样做。

在必须使用 `pthread_mutex_init()` 而不是静态初始化器的情况下，有以下几种情况：

- 互斥锁是在堆上动态分配的。例如，假设我们创建了一个动态分配的结构链表，列表中的每个结构都包含一个 `pthread_mutex_t` 字段，该字段包含一个用于保护对结构访问的互斥锁。
- 互斥锁是分配在栈上的自动变量。
- 我们希望使用除默认属性以外的属性来初始化静态分配的互斥锁。

当自动或动态分配的互斥锁不再需要时，应该使用 `pthread_mutex_destroy()` 将其销毁。（对于使用 `PTHREAD_MUTEX_INITIALIZER` 静态初始化的互斥锁，没有调用 `pthread_mutex_destroy()`）。

```c
#include <pthread.h>
int pthread_mutex_destroy(pthread_mutex_t *mutex);
```

成功时返回 `0`，错误时返回正错误数

只有当互斥锁处于未锁定状态且后续没有线程将锁定它时，销毁互斥锁才是安全的。如果互斥锁位于动态分配内存中，则应在释放该内存区域之前销毁。自动分配的互斥锁必须在函数返回之前销毁。
被 `pthread_mutex_destroy()` 销毁的互斥锁随后可以通过 `pthread_mutex_init()` 重新初始化。

## 30.1.6 互斥锁属性

如所述，可以使用 `pthread_mutexattr_init()` 属性指定一个 `pthread_mutexattr_t` 对象，该对象定义了互斥锁的属性。可以使用各种 Pthreads 函数来初始化和检索 `pthread_mutexattr_t` 对象中的属性。我们不会深入探讨互斥锁属性的所有细节，也不会展示用于初始化 `pthread_mutexattr_t` 对象中属性的各种函数的原型。然而，我们将描述可以为互斥锁设置的属性之一：类型。

## 30.1.7 互斥锁类型

在前面的页面中，我们对互斥锁的行为做了一些陈述：

- 单个线程可能多次锁定同一个互斥锁。
- 线程不能解锁它当前不拥有的互斥锁（即它没有锁定的互斥锁）。
- 线程不能解锁一个当前未锁定的互斥锁。

在这些情况下具体发生了什么，取决于互斥锁的类型。SUSv3 定义了以下互斥锁类型：

### `PTHREAD_MUTEX_NORMAL`

此类类型的互斥锁不提供（自）死锁检测。如果一个线程尝试锁定它已经锁定的互斥锁，会导致死锁。解锁一个未锁定的互斥锁或被另一个线程锁定的互斥锁产生未定义的结果。（在 Linux 上，这两种操作对于该类型的互斥锁都是执行成功的。）

### `PTHREAD_MUTEX_ERRORCHECK`

对所有操作都执行错误检查。上述所有三种场景都会导致相关的 Pthreads 函数返回错误。这种类型的互斥锁通常比普通互斥锁慢，但可以作为调试工具，发现应用程序在何处违反了关于互斥锁使用方法的规则。

### `PTHREAD_MUTEX_RECURSIVE`

递归互斥锁维护一个锁定计数。当线程首次获取互斥锁时，锁定计数设置为 `1`。同一线程的后续每个操作都会增加锁定计数，每个解锁操作都会减少计数。只有当锁定计数降到 `0` 时，互斥锁才释放（即允许其他线程获取）。解锁一个未锁定的互斥锁会失败，另一个线程解锁也是如此。

Linux 实现为每种互斥锁类型提供了非标准的静态初始化器（例如 `PTHREAD_RECURSIVE_MUTEX_INITIALIZER_NP`），因此对于静态分配的互斥锁，不需要使用 `pthread_mutex_init()` 来初始化这些类型。然而，可移植的应用程序应避免使用这些初始化器。

除了互斥锁类型外，SUSv3 还定义了 `PTHREAD_MUTEX_DEFAULT`，如果你使用 `PTHREAD_INITIALIZER` 或在 `pthread_mutex_init()` 中将 `attr` 为 `NULL`，它是互斥锁的默认类型。这种类型互斥锁在本节开头描述的三种场景中的行为都是未定义的，这为高效实现互斥锁提供了最大的灵活性。在 Linux 上，`PTHREAD_MUTEX_DEFAULT` 互斥锁的行为类似于 `PTHREAD_MUTEX_NORMAL` 互斥锁。

`30-3` 所示的代码演示了如何设置互斥锁的类型，在本例中是创建一个错误检查互斥锁。

### 列表 30-3: 设置互斥锁类型

```c
pthread_mutex_t mtx;
pthread_mutexattr_t mtxAttr;
int s, type;
s = pthread_mutexattr_init(&mtxAttr);
if (s != 0)
    errExitEN("pthread_mutexattr_init");
```

```c
s = pthread_mutexattr_settype(&mtx, PTHREAD_MUTEX_ERRORCHECK);
if (s != 0)
    errExITEN(s, "pthread_mutexattr_settype");
```

```c
s = pthread_mutex_init(&mtx, &mtxAttr);
if (s != 0)
    errExITEN(s, "pthread_mutex_init");
```
