
```c
#define POSIX_C_SOURCE 199309
#include <time.h>

int clock_gettime(clock_t clock, struct timespec *tp);

int clock_getres(clock_t clock, struct timespec *res);

成功时返回 0，失败时返回 -1
```

`clock_gettime()` 返回 `timespec` 结构中的时间。`clock_getres()` 返回时钟的分辨率。

表 23-1 POSIX 时钟类型

| Clock ID | 描述 |
| :--- | :--- |
| `CLOCK_REALTIME` | 可设置系统时钟 |
| `CLOCK_MONOTONIC` | 不设置单调时钟 |
| `CLOCK_PROCESS_CPUTIME_ID` | 进程 CPU 时间（Linux 2.6 起） |
| `CLOCK_THREAD_CPUTIME_ID` | 线程 CPU 时间（Linux 2.6 起） |

`CLOCK_REALTIME` 测量墙上钟时间。与 `CLOCK_MONOTONIC` 相比，该时钟设置可以更改。具有权限的进程（`CAP_SYS_TIME`）可以设置 `CLOCK_REALTIME`。该时钟的初始值通常为自 Epoch 以来的时间。表 23-1 中的其他时钟均不可修改。

根据规定，实现允许设置 `CLOCK_PROCESS_CPUTIME_ID` 和 `CLOCK_THREAD_CPUTIME_ID` 时钟。在 Linux 上，这些时钟是只读的。

Linux 2.6.28 在表 23-1 中增加了一个时钟 `CLOCK_MONOTON_RAW`。这是一个类似于 `CLOCK_MONOTONIC` 的时钟，但它提供了不受 NTP 调整的硬件时间。该非标准时钟用于特殊的同步应用程序。

Linux 2.6.32 在表 23-1 中增加了两个时钟：`CLOCK_REALTIME_COARSE` 和 `CLOCK_MONOTONIC_COARSE`。它们类似于 `CLOCK_REALTIME` 和 `CLOCK_MONOTONIC`，但旨在用于以最小成本获取低分辨率时间戳的应用。这些非标准时钟不会访问硬件时钟（对于某些硬件时钟访问代价很大），且返回值的分辨率是 jiffy 值（第 10.6 节）。

### 23.5.2 设置时钟值：`clock_settime()`

`clock_settime()` 系统调用根据 `tp` 指向的缓冲区设置由 `clockid` 指定的时钟。

```c
#define POSIX_C_SOURCE 199309
#include <time.h>

int clock_settime(clock_t clockid, const timespec *tp);

成功时返回 0，失败时返回 -1
```

如果 `tp` 指定的时间不是 `clock_gettime()` 返回的时钟分辨率的倍数，则将向下取整。

具有权限的进程（`CAP_SYS_TIME`）可以设置 `CLOCK_REALTIME` 时钟。表 23-1 中的其他时钟均不可修改。

## 23.5.3 获取特定进程或线程的时钟 ID

本节描述的函数允许我们获取测量特定进程或线程消耗 CPU 时间的时钟 ID。我们可以在调用 `clock_gettime()` 时使用返回的 clock ID，以便查找进程或线程消耗的 CPU 时间。

`clock_getcpuclockid()` 在 `clockid` 指向的缓冲区返回进程 `pid` 的 CPU 时间时钟的标识符。

```
#include <time.h>
int clock_getcpuclockid(pid_t pid, clockid_t *clockid);
成功时返回 0，错误时返回正数
```

如果 `pid` 为 0，`clock_getcpuclockid()` 返回调用进程的 ID。

`thread_getcpuclockid()` 函数是 `clock_getcpuclockid()` 函数在 POSIX 线程中的对应物。它返回测量调用进程中特定线程消耗的 CPU 时间的时钟的标识符。

```
#include <pthread.h>
#include <time.h>
int thread_getcpuclockid(pthread_t thread, clockid_t *clockid);
成功时返回 0，错误时返回正数
```

`thread` 参数是一个 POSIX 线程 ID，用于标识我们想要获取其 CPU 时间时钟 ID 的线程。该 ID 返回在 `clockid` 指向的缓冲区。

## 23.5.4 改进的高分辨率睡眠：`clock_nanosleep()`

与 `nanosleep()` 类似，Linux 特有的 `clock_nanosleep()` 系统调用会阻塞调用进程，直到指定的时间间隔通过或信号到达。在本节中，我们将描述区分 `clock_nanosleep()` 和 `nanosleep()` 的特性能。

```
#include <time.h>
int clock_nanosleep(clockid_t clockid, int flags, struct timespec *request, struct timespec *rem);
成功完成睡眠返回 0，错误或睡眠被中断时返回正数
```

`request` 和 `remain` 参数的作用与 `nanosleep()` 的对应参数类似。

默认情况下（即如果 `flags` 为 0），`request` 中指定的睡眠间隔是相对的（类似于 `nanosleep()`）。然而，如果我们在 `flags` 中指定 `TIMER_ABSTIME`（如列表 23-4 所示），则 `request` 指定一个由时钟测量的绝对时间。这一特性对于 `nanosleep` 累积到特定时间至关重要。如果我们尝试先获取当前时间、计算与目标时间的差值并使用相对睡眠，那么进程可能会在这些步骤中间被抢占，导致睡眠时间比预期的长。

正如 23.4.2 所述的，这种“过度睡眠”问题对于使用被信号处理程序中断的睡眠来重启进程来说尤为显著。如果信号以高频率递送，相对睡眠（由 `nanosleep()` 执行的类型）会导致进程花费睡眠的时间不准确。我们可以通过初始调用 `clock_gettime()` 来获取时间，在该时间基础上加上所需的时间量，然后带有 `ABSTIME` 标志调用 `clock_nanosleep()`，从而避免过度睡眠（如果被信号处理程序中断，则重新启动系统调用）。

当设置了 `ABSTIME` 标志时，`remain` 参数不被使用（它是没必要的）。如果 `clock_nanosleep()` 调用被信号处理程序中断，可以通过重复调用具有相同的 `request` 参数来重启睡眠。

另一个区分 `clock_nanosleep()` 和 `nanosleep()` 的特性是，我们可以选择用于测量睡眠间隔的时钟。我们在 `clockid` 中指定所需的时钟：`CLOCK_REALTIME`、`CLOCK_MONOTONIC` 或 `CLOCK_PROCESS_CPUTIME`。请见表 23-1 对这些时钟的描述。

列表 23-4 展示了如何使用 `clock_nanosleep()` 使用绝对时间值相对于 `CLOCK_REALTIME` 时钟睡眠 20 秒。

# 列表 23-4：使用 timespec request；

```
/* 获取 CLOCK_REALTIME 时钟的当前值 */

if (clock_gettime(CLOCK_REALTIME, &request) == -1)
	exit("clock_gettime");

request.tv_sec += 20;                /* 从现在起睡眠 20 秒 */

s = clock_nanosleep(CLOCK_REALTIME, TIMER_ABSTIME, &request, NULL);
if (s != 0) {
	if (s == EINTR)
		printf("interrupted by signal\n");
}
```

## 23.6 POSIX 间隔定时器

经典的间隔定时器存在许多局限性：

- 我们每种类型只能设置一个定时器：`ITIMER_REAL`、`ITIMER_VIRTUAL` 和 `ITIMER_PROF`。
- 唯一的通知方式是通过信号。
- 定时器的精度限于微秒；然而，某些系统具有更细的精度。
- POSIX 定时器不会被进程继承，并在 `exec()` 执行或进程终止时被删除。

### 23.6.1 创建定时器：`timer_create()`

`timer_create()` 函数使用 `clockid` 指定的时钟创建一个新的定时器。
