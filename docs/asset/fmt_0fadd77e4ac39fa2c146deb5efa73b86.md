
我们可以使用 `pthread_mutexattr_getrobust` 函数获取健壮互斥锁属性的值。要设置健壮互斥锁属性的值，我们可以调用 `pthread_mutexattr_setrobust` 函数。

```c
#include <pthread.h>

int pthread_mutexattr_getrobust(const pthread_mutexattr_t *attr,
                                               int *restrict robust);

int pthread_mutexattr_setrobust(pthread_mutexattr_t *attr,
                                               int robust);
```

两者均返回：0 表示成功，否则失败返回错误。

健壮属性有两个可能的值。默认是 `PTHREAD_MUTEX_STALLED`，这意味着当进程在持有互斥锁时终止时不会采取任何特殊操作。在这种情况下，互斥锁可能会导致未定义的行为，等待其解锁的应用程序实际上会“停滞”。另一个值是 `PTHREAD_MUTEX_ROBUST`。该值会导致当另一个持有锁的进程在未解锁的情况下终止时，阻塞在 `pthread_mutex_lock` 调用中的线程能够获取该锁，但 `pthread_mutex_lock` 的回传值将是 `EROWNDEAD` 而不是 0。应用程序可以使用此返回值作为指示，表明它们需要恢复互斥锁的状态（关于受保护的内容以及如何恢复的细节在许多应用程序中各有所异）。请注意，在这种情况下返回 `EROWNDEAD` 并不是真正的错误，因为调用者将拥有该锁。

使用健壮互斥锁会改变我们使用 `pthread_mutex_lock` 的方式，因为我们现在必须检查三个返回值，而不是：成功（无需恢复）、成功和失败。然而，如果我们不使用健壮互斥锁，可以继续检查成功和失败。

在本文涵盖的四个平台中，Linux 3.2 目前支持健壮 pthread 互斥锁。Solaris 10 仅在 Solaris 库中支持健壮互斥锁（更多信息请参阅 Solaris 手页 `mutex_init(3C)`）。然而，Solaris 11 支持健壮互斥锁。

如果无法恢复应用程序状态，在线程解锁互斥锁后，该锁将处于永久不可用的状态。为了防止这个问题，线程可以调用 `pthread_mutex_consistent` 函数，在解锁互斥锁之前指示与互斥锁的状态是一致的。

```c
#include <pthread.h>
int pthread_mutex_consistent(pthread_mutex_t * mutex);
```

返回：0 表示成功，失败返回错误号

如果线程在没有先调用 `pthread_mutex_consistent` 的情况下解锁互斥锁，那么在尝试获取互斥锁时阻塞的其他线程将看到 `ENOTRECOVER` 返回。如果发生这种情况，互斥锁将不再可用。

类型属性控制互斥锁的锁定特性，POSIX 定义了四种类型：

- `PTHREAD_MUTEX_NORMAL`：一种不进行任何错误检查的标准互斥锁类型。
- `PTHREAD_MUTEX_ERRORCHECK`：一种提供错误检查的互斥锁类型。
- `PTHREAD_MUTEX_RECURIVE`：允许同一线程多次锁定的互斥锁类型。
- `PTHREAD_MUTEX_DEFAULT`：提供默认特性的互斥锁类型。

例如，Linux 3.2 映射到普通锁，而 FreeBSD 8.0 映射到错误检查类型。四种类型的行为如图 12.5 所示。

| 互斥锁类型 | 未解锁重锁？ | 已拥有时解锁？ | 已解锁时解锁？ |
| :--- | :--- | :--- | :--- |
| `PTHREAD_MUTEX_NORMAL` | 死锁 | 未定义 | 未定义 |
| `PTHREAD_MUTEX_ERRORCHECK` | 错误 | 未定义 | 错误 |
| `PTHREAD_MUTEX_RECURIVE` | 允许 | 错误 | 错误 |
| `PTHREAD_MUTEX_DEFAULT` | 未定义 | 未定义 | 未定义 |

我们可以使用 `pthread_mutexattr_gettype` 函数获取互斥锁属性。要更改属性，可以使用 `pthread_mutexattr_settype` 函数。

```c
#include <pthread.h>
int pthread_mutexattr_gettype(const pthread_mutexattr_t *restrict attr, int *type);
int pthread_mutexattr_settype(pthread_mutexattr_t *attr, int type);
```

两者均返回：0 表示成功，失败返回错误号

从 11.6.6 回忆，互斥锁用于保护与条件变量相关的条件。在阻塞线程之前，`pthread_cond_wait` 和 `pthread_cond_timedwait` 会释放互斥锁。这允许其他线程获取互斥锁、更改条件、释放锁并信号变量。由于更改条件需要持有互斥锁，使用递归互斥锁不是好主意。如果递归互斥锁被多次锁定并在 `pthread_cond_wait` 中使用，条件永远无法满足，因为 `pthread_cond_wait` 不会释放锁。

图 12.6 展示了一个递归互斥锁似乎解决并发问题的情况。假设 `func1` 和 `func2` 是库中的现有函数，其接口无法更改，因为应用程序调用了它们且这些应用程序无法更改。

为了保持接口相同，我们将互斥锁嵌入数据结构中，结构地址 `x` 作为参数传递。这只有在我们为结构提供了分配器时才是可能的，这样应用程序就不知道它的大小（假设我们在添加互斥锁时必须增加其大小）。

如果我们最初定义结构时预留了足够的填充，以便将某些字段替换为互斥锁，这也是可能的。不幸的是，大多数程序员都不擅长预测未来，因此这不是常见的做法。

如果 `func1` 和 `func2` 必须操作该结构且可能同时从多个线程访问，那么 `func1` 和 `func2` 在操作结构之前必须锁定互斥锁。如果 `func1` 必须调用 `func2`，如果互斥锁类型不是递归的，我们将死锁。如果我们能够释放，就可以避免使用递归互斥锁。

## 第 12.4 同步属性 435

```text
main
```

`func1(x)`

```text
func1
```

`pthread_mutex_lock(x->lock)`

`func2(x)`

`pthread_mutex_unlock(x->lock)`

```text
func2
```

`func2(x)`

`pthread_mutex_lock(x->lock)`

`pthread_mutex_unlock(x->lock)`

![](img/5dc46842acde5fbcadfab4612cdecbbc_468_0.png)

在调用 `func2` 之前锁定互斥锁，并在 `func2` 返回后重新获取，但这种方法打开了一个窗口，使得另一个线程可能夺取互斥锁的控制权，并在 `func1` 执行期间更改数据结构。这取决于互斥锁旨在提供的保护，可能是不可接受的。

12.7 显示了在这种情况下使用递归互斥锁的替代方案。我们可以保持 `func1` 和 `func2` 的接口不变，通过提供 `func2` 的私有版本（命名为 `func2_locked`）来避免使用递归互斥锁。要调用 `func2_locked`，我们必须持有嵌入在作为参数传递的数据结构中的互斥锁。`func2_locked` 的主体包含 `func2` 的拷贝，而 `func2_now` 则简单地获取互斥锁、调用 `func2_locked`，然后释放互斥锁。

如果我们不需要保持库的接口不变，可以为每个函数添加第二个参数，以指示结构体是否被调用者锁定。然而，如果可以，通常保持接口不变更好，而不是用实现产物来污染它们。

提供函数的锁定版本和未锁定版本的策略通常适用于简单的情况。在更复杂的情况下，例如当库需要调用库外部的函数，而该函数可能会回调库时，我们需要依赖递归锁。

# 线程控制

## 第 12 章

![](img/5dc46842acde5fbcadfab4612cdecbbc_469_0.png)

图 12.7 避免递归锁的机会

### 示例

图 12.8 中的程序说明了另一种需要递归互斥锁的情况。在这里，我们有一个“超时”（`timeout`）函数，它允许我们在并在未来的任何时间调度另一个函数的运行。假设线程是廉价的资源，我们可以为每个待处理的超时创建一个线程。该线程等待直到时间到达，然后调用我们请求的函数。

当我们无法创建线程或者调度运行函数的时间已经过去时，问题就会出现。在这种情况下，我们直接从当前持有锁的地方调用请求的函数，除非锁是递归的，否则将发生死锁。

```c
#include "apue.h"
#include <pthread.h>
#include <time.h>
#include <sys/time.h>

extern int makethread(void (*)(void *), void *);

struct to_info {
    void (*to_fn)(void *); /* 函数指针 */
    void *to_arg;               /* 参数 */
    struct timespec to_wait;      /* 等待时间 */

#define NANONOSEC 1000000000      /* 秒到纳秒 */
#if defined(CLOCK_REALTIME) || defined(BSD)
#define clock_nanosleep(ID, FL, REQ, REM)  nanosleep((REQ), (REM))
#endif

#ifdef CLOCK_REALTIME
#define CLOCK_REALTIME 0
#define USECNOSEC 1000               /* 微秒到纳秒 */
void
clock_gettime(int id, struct timespec *tsp)
{
    struct timeval tv;

    gettimeofday(&tv, NULL);
    tsp->tv_sec = tv.tv_sec;
    tsp->tv_nsec = tv.tv_usec * USECNOSEC;
}
#endif
void *
timeout_helper(void *arg)
{
    struct to_info *tip;          /* 参数 */
    tip = (struct to_info *)arg;
    clock_nanosleep(CLOCK_REALTIME, 0, &tip->to_wait, NULL);
    (*tip->to_fn)(tip->to_arg);
    free(arg);
    return(0);
}
void
timeout(const struct timespec *when, void (*func)(void *), void *arg)
{
    struct timespec now;
    struct to_info *tip;
    int err;

    clock_gettime(CLOCK_REALTIME, &now);
    if ((when->tv_sec > now.tv_sec) ||
        (when->tv_sec == now.tv_sec && when->tv_nsec > now.tv_nsec)) {
        tip = malloc(sizeof(struct_info));
        if (tip != NULL) {
            tip->to_fn = func;
            tip->to_arg = arg;
            tip->to_wait.tv_sec = when->tv_sec - now.tv_sec;
            if (when->tv_nsec >= now.tv_nsec) {
                tip->to_wait.tv_nsec = when->tv_nsec - now.tv_nsec;
            } else {
                tip->to_wait.tv_sec--;
                tip->to_wait.tv_nsec = NANONOSEC + when->tv_nsec - now.tv_nsec;
            }
            err = makethread(timeout_helper, (void *)tip);
            if (err == 0) {
                return;
            } else {
                free(tip);
            }
            /* 如果满足 (a) <= now，或者 (b) malloc 失败，或者 (c) 我们无法创建线程，则直接调用函数。 */
            (*func)(arg);
        }
    }
}

pthread_mutexattr_t attr;
pthread_mutex_t mutex;
void retry(void *arg)
{
    pthread_mutex_lock(&mutex);
    /* 执行重试 */
    pthread_mutex_unlock(&mutex);
}

int main(void)
{
    int err, condition;
    struct timespec when;
    if ((err = pthread_mutexattr_init(&attr)))
        err_exit(err, "mutexattr_init 失败");
    if ((err = pthread_mutexattr_settype(&attr, THREAD_MUTEX_RECURIVE)) != 0)
        err_exit(err, "无法设置递归类型");
    if ((err = pthread_mutex_init(&mutex, &attr)) != 0)
        err_exit(err, "无法创建递归互斥锁");

    /* 继续处理 */
    pthread_mutex_lock(&mutex);
    /* 在锁的保护下检查条件，
     * 使得检查和调用 timeout 是原子的。
     */
    if (condition) {
        /* 计算我们想要重试的绝对时间。 */
        clock_gettime(CLOCK_REALTIME, &when);
        when.tv_sec += 10; /* 现在 10 秒后 */
        timeout(&when, retry, (void*)arg);
    }
    pthread_mutex_unlock(&mutex);
    /* 继续处理 */
    exit(0);
}
```

图 12.8 使用递归互斥锁

我们使用图 12.4 中的 `makethread` 函数创建一个分离状态（detached）的线程。因为传递给 `timeout` 的函数将在将来运行，所以我们不想等待它完成。我们可以调用 `sleep` 等待超时过期，但这只能提供秒粒度。如果我们想等待非整数秒的时间，需要使用 `nanosleep` 或 `clock_nanosleep`，它们允许我们以更高的分辨率进行睡眠。

在没有定义 `CLOCK_REALTIME` 的系统中，我们通过 `select` 定义 `nanosleep`。然而，FreeBSD 8.0 定义了该符号以支持 `clock_gettime` 和 `clock_settime`，但不支持 `clock_nanosleep`（Linux 3.2 和 Solaris 10 目前支持 `clock_nanosleep`）。

此外，在没有定义 `CLOCK_REALTIME` 的系统中，我们提供了自己的 `clock_gettime` 实现，它调用 `gettimeofday` 并微秒转换为纳秒。

`timeout` 的调用者持有互斥锁以检查条件并原子地调度重试函数。重试函数将尝试锁定同一个互斥锁。除非互斥锁是递归的，否则 `timeout` 函数直接调用 `retry` 会导致死锁。

### 12.4.2 读写锁属性

读写锁也有属性，类似于互斥锁。我们使用 `pthread_rwlockattr_init` 初始化 `pthread_rwlockattr_t` 结构体，并使用 `pthread_rwlockattr_destroy` 反初始化结构体。

```c
#include <pthread.h>

int pthread_rwlockattr_init(pthread_rwlockattr_t *attr);
int pthread_rwlockattr_destroy(pthread_rwlockattr_t *attr);
```

两者返回：0 表示 OK，失败时返回错误码

读写锁支持的唯一属性是进程共享属性（process-shared）。它与互斥锁的进程共享属性相同。与互斥锁的进程共享属性一样，提供一对函数来获取和设置读写锁的进程共享属性。

```c
#include <pthread.h>

int pthread_rwlockattr_getpshared(const pthread_rwlockattr_t *restrict attr,
int *restrict pshared);

int pthread_rwlockattr_setpshared(pthread_rwlockattr_t *attr, int pshared);
```

两者返回：0 表示 OK，失败时返回错误码

尽管 POSIX 只定义了一个读写锁属性，实现可以定义额外的标准属性。
