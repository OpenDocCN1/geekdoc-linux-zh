
我们声明了一个互斥锁 `counter_mutex`，线程在操作计数器变量之前必须锁定该互斥锁。当我们运行此程序时，输出始终是正确的：值单调递增，打印的最终值为 `10000`。
互斥锁锁定涉及多少开销？图 `26.17` 和 `26.18` 中的程序被修改为循环 `50,000` 次，并在输出重定向到 `/dev/null` 时进行了计时。不使用互斥锁的错误版本与使用互斥锁的正确版本之间的 CPU 时间差异为 `10%`。这告诉我们，互斥锁的开销并不大。

## 26.8 条件变量

互斥锁可以防止同时访问共享变量，但我们需要其他东西来进入睡眠并等待条件的发生。让我们通过一个例子来演示。我们回到 `26.6` 节中的 Web 客户端，将 Solaris 的 `thr_join` 替换为 `pthread_join`。但是，在我们声明一个跟踪已线程数的全局变量并用互斥锁保护它之前，我们无法知道 Pthread 函数已经终止。

```c

int ndone; /* 已终止线程数 */

pthread_mutex_t ndone_mutex = PTHREAD_MUTEX_INITIALIZER;

```

我们要求每个线程在终止时递增此计数器，并小心使用关联互斥锁。

```c

void *

do_get_read(void *vptr)

{

  ...

  pthread_mutex_lock(&ndone_mutex);

  ndone++;

  pthread_mutex_unlock(&ndone_mutex);

  return(fptr); /* 终止线程 */

}

while (nleftthread > 0) {

  while (nconn < maxconn && nleftthread > 0) {

    /* 找到要读取的文件 */

    ...

    if (ndone > 0) {

      for (i = 0; i < nfiles; i++) {

      if (file[i].f_flags & DONE) {

        pthread_join(file[i].f_tid, (** )fptr);

        /* 为终止线程更新 file[i] */

      }

    }

  }

  pthread_mutex_unlock(&ndone_mutex);

}

```

这样是可以的，但我们如何编写主循环呢？它需要不断锁定互斥锁并检查是否有线程已终止。虽然这样做可行，但这意味着主循环永远不会睡眠，只是不断检查 `ndone`。这被称为轮询，浪费了 CPU 时间。

我们希望有一种方法让主循环睡眠，直到某个线程通知它。条件变量配合互斥锁提供了这种机制。互斥锁提供互斥，条件变量提供信号机制。在线程中，条件变量是一个类型为 `pthread_cond_t` 的变量。它们配合以下函数使用：

```c

#include <pthread.h>

int pthread_cond_wait(pthread_cond_t *cptr, pthread_mutex_t *mptr);

int pthread_cond_signal(pthread_cond_t *cptr);

// 如果成功返回 0，出错时返回正值

```

第二个函数中的“signal”术语并不是 Unix 信号。解释这些函数的最好的方法是回到 Web 客户端示例，计数器 `ndone` 现在与条件变量和互斥锁关联。

```c

int ndone;

pthread_mutex_t ndone = PTHREAD_MUTEX_INITIALIZER;

pthread_cond_t ndone_cond = PTHREAD_COND_INITIALIZER;

```

线程在持有互斥锁时通过增加计数器并信号条件变量来通知主循环它正在终止。

```c

pthread_mutex_lock(&ndone_mutex);

ndone++;

pthread_cond_signal(&ndone_cond);

pthread_mutex_unlock(&ndone_mutex);

```

主循环随后调用 `pthread_cond_wait` 时阻塞，等待线程的信号。

```c

while (nleftthread > 0) {

  while (nconn < maxconn && nleftthread > 0) {

    /* 找到要读取的文件 */

    /* 等待线程终止 */

    pthread_mutex_lock(&ndone_mutex);

    while (ndone == 0)

      pthread_cond_wait(&ndone_cond, &ndone_mutex);

    for (i = 0; i < nfiles; i++) {

      if (file[i].flags & DONE) {

        pthread_join(file[i].f_tid, (void **)fptr);

        /* 为终止线程更新 file[i] */

      }

    }

    pthread_mutex_unlock(&ndone_mutex);

  }

}

```

注意变量 `ndone` 仅在持有互斥锁时被检查。然后，如果没有事情要做，就会调用 `pthread_cond_wait`。这会让调用线程睡眠并释放它持有的互斥锁。此外，当线程从 `pthread_cond_wait` 返回（其他线程发送信号后），它再次持有互斥锁。

为什么条件变量总是与互斥锁关联？条件”通常是线程共享的某个变量。需要互斥锁来允许不同的线程设置并测试该变量。例如，如果代码中没有互斥锁，主循环将如下测试它：

```c

/* 等待线程终止 */

while (ndone == 0)

    pthread_cond_wait(&ndone_cond, &ndone_mutex);

```

但是，可能最后一个线程在测试 `ndone == 0` 之后、调用 `pthread_cond_wait` 之前增加了 `ndone`。如果发生这种情况，这个“信号”就会丢失，主循环将永远等待永远不会发生的事情。

这就是 `pthread_cond_wait` 必须在关联的互斥锁锁定的情况下调用的原因，并且该函数以单一原子操作释放互斥锁并让线程睡眠。如果该函数在返回时不解锁互斥锁并锁定它，线程将必须锁定和解锁互斥锁，代码如下：

```c

/* 等待线程终止 */

pthread_mutex_lock(&ndone_mutex);

while (ndone == 0) {

    pthread_cond_unlock(&ndone_mutex);

    pthread_cond_wait(&ndone, &ndone_mutex);

}

pthread_mutex_unlock(&ndone_mutex);

```

但同样，可能最后一个线程在调用 `pthread_mutex_unlock` 和 `pthread_cond_wait` 之间终止并增加了 `ndone` 的值。

通常，`pthread_cond_signal` 唤醒一个等待条件变量的线程。在线程发现多个线程应该被唤醒的情况下，`pthread_cond_broadcast` 将唤醒所有在条件变量上的线程。

```c

#include <pthread.h>

int pthread_cond_broadcast(pthread_cond_t *cptr);

int pthread_cond_timedwait(pthread_cond_t *tspec, pthread_mutex_t *mtpr,

                           const struct timespec *abstime);

返回值：如果成功返回 0，出错时返回正 ETIMED 值

```

`pthread_cond_timedwait` 允许线程对其阻塞时间设置限制。`abstime` 是一个 `timespec`（如 `6.9` 节中 `pselect` 函数定义），指定了函数必须返回的时间，即使条件变量没有被信号。如果发生此超时，则返回 `ETIME`。

此值是绝对时间；而不是增量时间。也就是说，`abstime` 是系统时间——自 `1970` 年 `1` 月 `1` 日以来的秒数和纳秒——函数应该返回的时间。这与 `select` 和 `pselect` 不同，后者指定的是距离未来某个时间的秒数和微秒（pselect 为纳秒）。标准程序是调用 `gettimeofday` 获取当前时间（使用 `timeval` 类型！），并将其复制到

# Web 客户端与并发连接（继续）

一个 `timespec` 结构体，添加所需的时间限制。例如：

```
struct timeval tv;

struct timespec ts;

if (gettimeofday(&tv, NULL) < 0)

    err_sys("gettimeofday error");
```
