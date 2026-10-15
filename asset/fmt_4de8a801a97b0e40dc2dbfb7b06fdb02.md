
```
for(i=0; i<N; i++) {

  waitTime = rand();

  for(j=0; j<waitTime; j++) { // 模拟运行

    // process

  }

  request(r[i%M], ...); // 请求 k < c[i%M] 个单元

  waitTime = rand();

  for(j=0; j<waitTime; j++) { // 模拟运行

    // process

  }

  release(r[i%M], ...); // 释放资源

}
```

更全面的测试程序将导致进程同时持有超过一种类型的资源。如果你有时间，让你的测试驱动程序检查这些更复杂的情况。

尝试不同的小值 `$N=8, M<10$` 和 `$c_p$`。进程运行的随机时间应保持尽可能小，以确保你的测试不会花费过长时间。确保你的测试用例会导致进程因不可用资源而阻塞。提交你的资源管理器和测试平台的列表，连同一次测试会话中状态转换的追踪（少于五页）。

# 内核定时器

此作业可以在大多数版本的 UNIX 上完成。

设计并实现使用 `ITIM_REAL`、`ITIM_VIRTUAL` 和 `ITIM_PROF` 间隔定时器的软件，以测量进程的使用情况。准备一份报告，提供实时（使用 `ITIM_REAL` 定器）执行时间、处理器时间（进程实际上在用户空间和内核空间中都在运行）、用户空间时间和内核空间时间。你可以通过调用 `gettimeofday()` 来检查你的墙钟（实际）时间的准确性。所有时间都应具有毫秒精度。尽管如此，设计代码时仍假设代码具有毫秒精度。使用通用的信号处理程序来跟踪实际、虚拟和分析时间的秒数（你应该配置这三个定时器，使其每秒产生一次信号）。通过测量一个父进程和两个子进程的性能来演示你的解决方案，每个进程执行包含在“解决问题”实验中的斐波那契程序。针对 `N = 20, 30` 和 `36` 的斐波那契序列。

# 背景

时间是相对于某个重要纪元（epoch）给出的。例如，美国的时间是使用格里哥利历计算的，该历法选择零点约为 2000 年前。当你向 shell 输入 `date` 命令时，该命令将引发一个内核变量来确定时间，例如“Mon Jun 21 09:01:28 MDT 2002”，你可能会将其解释为自纪元开始以来已经过去了 2002 年。

由于 UNIX 系统在 1970 年之前不存在，它们简单地避免表示 1970 年之前的时间。1970 年 1 月 1 日（格林尼治标准时间 00:00:00）。注意，在 30 年后（或 2000 年 1 月 1 日），自 UNIX 纪元开始以来过去了 946,080,000 秒。

用于保存时间的内核数据结构是：

```c
struct timeval {
  long tv_sec;
  long tv_usec;
};
```

OS 如何知道何时更新时间？每台现代计算机都包含一个非常可编程的定时器。该设备并不是真的用于 I/O，而是为了在精确的间隔产生中断（例如，Linux 系统设置定时器每秒产生 100 次中断）。OS 可以使用该设备保持准确时间：当 OS 初始化时，它将定时器变量设置为零。每当中断发生时，处理程序就会增加定时器变量。也就是说，如果中断每 10 ms 发生。

当前时间由 UNIX 内核管理，用户通过系统调用访问：

```c
#include <sys/time.h>
...
struct timeval theTime;
...
gettimeday(&theTime, NULL);
```

当代码段完成后，`timeval` 结构将 `tv_sec` 设置为自 1970 年 1 月 1 日以来过的整数秒数，而 `tv_usec` 是一个 `long` 类型变量，提供自上一秒开始以来过的微秒数。当 OS 初始化时，自纪元开始的秒数保存在内核变量中。`gettimeday()` 函数通过加上已过去的时间返回当前时间。

定时器处理程序维护的 OS 时钟值也用于确定何时将当前运行的进程从 CPU 中移除以便其他进程使用，跟踪进程在用户模式或内核模式下执行的时间（使用问题说明中提到的 ITER 值），等等。

# 进程定时器

内核积累时间并为每个进程管理各种定时器。例如，调度策略取决于每个进程都有其自使用 CPU 以来积累的 CPU 时间。内核还相对于每个进程跟踪三种不同的时间间隔：

- `TIMER REAL`：反映真实时间的经过，通过 `it_real_value` 和 `it_real_incr` 字段实现。
- `TIMER VIRTUAL`：反映虚拟时间的经过，这意味着此时间仅在相应进程在用户模式下执行时才会增加。
- `TIMER_PROF`：反映进程活跃期间的经过（虚拟时间）加上内核代表相应进程执行操作的时间（例如，执行系统调用）。

## 第六章 进程、线程与资源的实现

这些定时器都是倒计时器，这意味着它们会被周期地初始化为某个规定的值，然后通过向零倒计时来反映时间的流逝。当定时器达到零时，它会发出一个信号，通知系统的其他部分（操作系统或用户空间程序）计数器已零。然后它会重置周期并再次开始倒计时。

每个定时器通过 `setitimer()` 系统调用进行初始化：

```c
#include <sys/time.h>
...
setitimer(
    int timerType,
    const struct timerval *value,
    struct timerval *oldValue
);
```

`struct timerval` 包含以下字段：

```c
struct timerval {
    struct timeval it_interval;
    struct timeval it_value;
};
```

你可以通过阅读 `setitimer()` 的 man 页来获取参数的详细信息。基本思路是 `timerType` 参数被设置为 `ITIMER_REAL`、`ITIMER_VIRTUAL` 或 `ITIMER_PROF` 之一（这些是在 `sys/time.h` 头文件中定义的常量）。`value` 参数用于初始化给定定时器的秒和微秒；`it_value` 字段定义了定时器的值，而 `it_interval` 字段定义了当定时器达到零时应用于重置定时器的值。

定时器的值可以通过 `getitimer()` 系统调用读取：

```c
#include <sys/time.h>
...
getitimer(
    int timerType,
    const struct timerval *value,
);
```

在这种情况下，`value` 参数用于返回内核时钟的值。以下代码段设置了 `ITIMER_REAL` 然后对其进行了读取：

```c
#include <sys/time.h>
...
struct timerval v;
...
v.it_interval.tv_sec = 9;
v.it_interval.tv_usec = 999999;
v.it_value.tv_sec = 9;
v.it_value.tv_usec = 999999;
setitimer(ITIMER_REAL, &v, NULL);
...
getitimer(ITIMER_REAL, &v);
```

```c
printf("... %ld seconds, %ld microseconds ...");
...
v.it_value.tv_sec,
v.it_value.tv_usec,
...);
```
