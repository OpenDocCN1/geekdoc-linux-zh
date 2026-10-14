
`new_value` 参数指定定时器的新设置。`old_value` 参数可以返回定时器之前的设置（见下文 `timerfd_gettime()` 的描述）。如果我们对之前的设置感兴趣，可以将 `old_value` 设置为 `NULL`。两者都是 `itimerspec` 结构，使用方式与 `timer_settime()` 相同（见第 23.6 节）。

`flags` 参数与 `timer_settime()` 的对应参数类似。它可能是 0，这意味着 `new_value.tv_value` 相对于调用 `timerfd_settime()` 时间进行解释；或者可以是 `TFD_TIMER_ABSTIME`，这意味着 `new_value.tv_value` 被解释为绝对时间（即从时钟零点测量）。

`timerfd_gettime()` 系统调用返回由文件描述符 `fd` 标识的定时器的间隔和剩余时间。

```c
#include <sys/timerfd.h>
int timerfd_gettime(int fd, struct timespec *curr_value);
```

成功返回 0，错误返回 -1。

与 `timer_gettime()` 类似，间隔和定时器下次过期的时间返回指向 `curr_value` 的 `timespec` 结构中。`curr_value->tv_value` 返回下次过期的时间，即使这是使用 `TFD_TIMER_ABSTIME` 确定的绝对时间。如果返回的 `curr_value->tv_value` 结构的两个字段都为 0，则定时器当前已开启。如果返回的 `curr_value->tv_interval` 结构为 0，则定时器仅过期一次，在 `curr_value->tv_value` 给出的时间过期。

## `timerfd` 与 `fork()` 和 `exec()` 的交互

在 `fork()` 期间，子进程继承 `timerfd_create()` 创建的文件描述符副本。这些文件描述符指向父进程相同的定时器对象，定时器过期可以在任何一个进程中读取。

由 `timerfd_create()` 创建的文件描述符在 `exec()` 之后保留（除非如第 27.4 节所述将标记标记为执行时关闭），且开启的定时器在 `exec()` 之后将继续产生过期。

## 示例程序

列表 23-8 演示了 `timerfd` API 的用法。该程序接受两个命令行参数。第一个参数是强制的，指定定时器的初始时间和间隔。（该参数使用列表 23-6 所示的 `timerspecFromStr` 函数解释。）第二个参数是可选的，指定了程序在终止之前应该等待的定时器最大到期次数；此参数的默认值为 1。

程序使用 `timerfd_create()` 创建定时器，并使用 `timerfd_settime()` 设置定时器。它会循环读取，从文件描述符中读取到期通知，直到达到指定的到期次数。在每次调用 `read()` 之后，程序都会显示自定时器启动以来经过的时间、到期次数以及到目前为止的到期总数。

在下面的会话日志中，命令行参数指定了一个初始值为 1 秒、间隔为 1 秒的定时器，且最多 100 次到期。

```
$ ./demo_timerfd 1:1 100
1.000: expirations read: 1; total=1
2.000: expirations read: 1; total=2
3.000: expirations read: 1; total=3
按下 Control-C 将程序挂起到后台运行几秒
[1] Stopped ./demo_timerfd 1:1 100
$ fg
  ./demo_timerfd 1:1 100 恢复程序
14.205: expirations read: 11; total=14 自上次 read() 之后发生了多次到期
15.000: expirations read: 1; total=15
16.000: expirations read: 1; total=16
按下 Control-C 终止程序
```

从上面的输出中看到，在程序挂起到后台期间发生了多次定时器到期，所有这些到期都在程序恢复执行后的第一次调用 `read()` 时返回。

### 列表 23-8：使用 `timerfd` API

```c
#include <sys/timerfd.h>
#include <time.h>
#include <stdint.h>
#include <itimerspec_from_str.h>
#include <tlpi_hdr.h>

/* uint64_t 的定义 */
/* 声明 itimerspecFromStr() */

int
main(int argc, char *argv[])
{
	struct timespec ts;
	struct timespec start, now;
	int maxExp, secs, nanosecs;
	uint64_t numExp, totalExp;
	size_t s;

	if (argc < 2 || strcmp(argv[1], "--help") == 0)
	usageError("%s secs[/nsecs]/[int-secs]] [max-exp]\n", argv[0]);

	itimerspecFromStr(argv[1], &ts);
	maxExp = (argc > 2) ? getInt(argv[2], GN_GT_0, "max-exp") : 1;

	fd = timerfd_create(CLOCK_REALTIME, 0);
	if (fd == -1)
	errExit("timerfd_create");

	if (timerfd_settime(fd, 0, &ts, NULL) == -1)
	errExit("timerfd_settime");

	if (clock_gettime(CLOCK_MONOTONIC, &start) == -1)
	errExit("clock_gettime");

	for(totalExp = 0; totalExp < maxExp;) {

  /* 读取定时器上的到期次数，然后显示
     自定时器启动以来经过的时间，随后是读取的
     到期次数以及目前为止的到期总数。 */

  s = read(fd, &numExp, sizeof(uint64_t));
  if (s != sizeof(uint64_t))
	errExit("read");

  totalExp += numExp;

  if (clock_gettime(CLOCK_MONOTONIC, &now) == -1)
	errExit("clock_gettime");

  secs = now.tv_sec - start.tv_sec;
  nanosecs = now.tv_nsec - start.tv_nsec;
  if (nanosecs < 0) {
    secs--;
    nanosecs += 1000000000;
  }

  printf("%03d: expirations read: %lu; total=%lu\n",
         secs, (nanosecs + 500000) / 1000000,
         (unsigned long long) numExp, (unsigned long long) totalExp);
	}

  exit(EXIT_SUCCESS);
}
```

## 23.8 总结

进程可以使用 `setimer()` 或 `alarm()` 来设置定时器，以便在经过指定的实际时间量后接收到一个信号。定时器的作用之一是为系统调用阻塞的时间设置一个上限。需要在指定时间间隔内暂停执行的应用可以使用各种睡眠函数来实现此目的。Linux 2.6 实现了 POSIX 扩展，这些扩展定义了高精度时钟和定时器的 API。POSIX 定时器相比传统的 `setimer()` 具有一系列优势：可以选择在定时器到期时递送的信号；检索自上次到期以来的溢出计数；以及选择通过执行而非通过递送信号来接收定时器通知。Linux 特有的 `timerfd` API 提供了一组创建定时器的接口，与 POSIX 定时器类似，但允许通过文件描述符读取定时器通知。该文件描述符可以使用 `select()`、`poll()` 进行监控。
