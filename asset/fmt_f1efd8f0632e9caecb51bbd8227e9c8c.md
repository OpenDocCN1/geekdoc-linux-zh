
```c
#include <sys.h>

int getitimer(int which, struct itimerval *curr_value);

// 成功时返回 0，出错时返回 -1
```

`getitimer()` 系统调用通过 `curr_value` 指向的缓冲区获取当前定时器的当前状态。这与通过 `setitimer()` 的 `old_value` 参数返回的信息完全相同，区别在于我们不需要更改定时器设置即可获取这些信息。`curr_value.it_value` 子结构返回距离下次定时器到期的剩余时间。该值随着定时器的倒计时而变化，并且在设置定时器时指定了非零的 `it_interval` 值，则它会在定时器到期时重置。`curr_value.it_interval` 子结构返回该定时器的间隔；该值在下一次调用 `setitimer()` 之前保持不变。

使用 `setitimer()`（以及稍后讨论的 `alarm()`）建立的定时器在 `execute()` 时会保留，但不会被 `fork()` 的子进程继承。

SUSv4 将 `timer()` 和 `setitimer()` 标记为废弃，并建议使用 POSIX 定时 API（第 23.6 节）。

## 程序

列表 23-1 展示了 `setitimer()` 和 `getitimer()` 的用法。该程序执行以下步骤：

- 为 `SIGALRM` 信号建立处理程序。
- 使用命令行参数提供的值为实际定时器（`ITIM_REAL`）设置值字段和间隔字段。如果缺少这些参数，程序将设置一个仅在 2 秒后到期一次的定时器。
- 执行连续循环，消耗 CPU 时间并定期调用 `displayTimes()` 函数，该函数会显示自程序开始以来经过的实际时间，以及 `ITIM_REAL` 时间的当前状态。

每当定时器到期时，`SIGALRM` 处理程序被调用，它会设置一个全局标志 `gotAlarm`。每当此标志被设置时，主程序中的循环就会调用 `displayTimes()` 以显示处理程序被调用的时间以及定时器的状态。我们这样设计信号处理程序是为了避免从异步信号中调用异步信号。正如第 2 节所述，如果定时器具有非零间隔，在列表 23-1 中所示：

```c
#include <signal.h>
#include <time.h>
#include <unistd.h>
#include <stdio.h>

static volatile sig_t gotAlarm = 0;

static void sigalarmHandler(int sig) {
	gotAlarm = 1;
}

int main(int argc, char *argv[]) {
	struct itimerval itv;
	int maxSigs;
	int sigCnt;
	struct sigaction sa;
	/* 退出前捕获的信号数 */
	/* 已捕获的信号数 */

	if (argc > 1 && strcmp(argv[1], "--help") == 0)
		usageErr("%s [usecs] [int-secs] [int-usecs]\n", argv[0]);

	sigCnt = 0;
	sigemptyset(&sa.sa_mask);
	sa.sa_flags = 0;
	sa.sa_handler = sigalarmHandler;
	if (sigaction(SIGALRM, &sa, NULL) == -1)
		errExit("sigaction");

	/* 设置定时命令行参数 */
	itv.value.tv_sec = (argc > 1) ? strtol(argv[1], 0, "secs") : 2;
	itv.value.tv_usec = (argc > 2) ? strtol(argv[2], 0, "usecs") : 0;
	itv.interval.tv_sec = (argc > 3) ? strtol(argv[3], 0, "int-secs") : 0;
	itv.interval.tv_usec = (argc > 4) ? strtol(argv[4], 0, "int-usecs") : 0;

	/* 在 3 个信号后退出，或者在间隔为 0 时在第一个信号退出 */
	maxSigs = (itv.interval.tv_sec == 0 && itv.interval.tv_usec == 0) ? 1 : 3;

	while (sigCnt < maxSigs) {
		if (gotAlarm) {
			gotAlarm = 0;
			if (getitimer(ITIM_REAL, &itv) == -1) {
				errExit("getitimer");
			}
		}
		displayTimes("", 1);
		sleep(100);
	}
}

static void displayTimes(const char *msg, int includeTimer) {
	timeval curr;
	static timeval start;
	if (getitimer(ITIM_REAL, &curr) == -1) {
		errExit("getitimer");
	}
	printf("Elapsed %ld.%06ld %s", (long)(curr.tv_sec - start.tv_sec), (long)curr.tv_usec, msg);
	if (includeTimer) {
		printf("Interval: %ld.%06ld\n", (long)itv.interval.tv_sec, (long)itv.interval.tv_usec);
	}
}
```

*(注：由于原文文本在最后部分存在大量重复和乱码，上述译文部分根据逻辑重构了完整的代码示例逻辑结构)*

```c
displayTimes("START": FALSE);
if (setimer(ITIMER_REAL, &itv, 0) == -1)
  errExit("setimer");

prevClock = clock();
sigCnt = 0;
```

```c
for (;;) {
  /* 内循环消耗至少 0.5 秒 CPU 时间 */
while (((clock) - prevClock) * 10 / CLOCKS_PER_SEC) < 5) {
  if (getAlarm) {
    /* 我们收到了信号吗？ */
    getAlarm = 0;
    displayTimes("ALARM", TRUE);

sigCnt++;
if (sigCnt >= maxSigs) {
  printf("That's all folks\n");
  exit(EXIT_SUCCESS);
}
  }
}
```

```
timers/real_timer.c
```

## 一个更简单的定时器接口：alarm()

`alarm()` 系统调用为建立一次性的实时定时器提供了一个简单的接口，该定时器过期后不会重复间隔。（从历史角度，`alarm()` 是设置定时器的原始 UNIX API。）

```c
#include <unistd.h>

unsigned int alarm(unsigned int seconds)
  /* 总是成功，返回之前设置的任何定时器的剩余秒数，如果之前没有设置定时器则返回 0 */
```

`seconds` 参数指定了定时器在未来过期的秒数。到那时时，一个 `SIGALRM` 信号将传递给调用进程。

使用 `alarm()` 设置定时器会覆盖之前设置的任何定时器。我们可以通过调用 `alarm()` 来禁用现有定时器。

作为返回值，`alarm()` 给我们之前设置的任何定时器到期前的剩余秒数，如果没有设置定时器，则返回 0。

`alarm()` 的使用示例见第 23.3 节。

在本书后的的一些示例程序中，我们使用 `alarm()` 启动定时器而不建立相应的 `SIGALRM` 处理器，这是一种确保进程在没有被其他终止的情况下被杀死的技术。

## settimer() 和 alarm() 之间的交互

在 Linux 上，`alarm()` 和 `settimer()` 共享同一个进程级实时定时器，这意味着使用其中一个函数设置定时器会更改之前由任何一个函数设置的任何定时器。在其他 UNIX 实现中情况可能并非如此（即这些函数可能控制独立的定时器）。SysV 显式地未说明 `settimer()` 和 `alarm()` 之间的交互，以及这些函数与第 23.4.1 节描述的 `sleep()` 函数之间的交互。为了最大的可移植性，我们应该确保应用程序只使用 `settimer()` 和 `alarm()` 之一来设置实时定时器。

## 23.2 定时器的调度与准确性

取决于系统负载和进程调度，进程可能在定时器实际过期后一短时间内（即通常是几分之一秒的一小部分）才被调度运行。尽管如此，通过 `settimer()` 或本章描述的其他接口设置的周期性定时器的过期将保持保持规律。例如，如果设置一个实时定时器每 2 秒过期一次，那么单个定时器事件的传递可能会受到上述延迟的影响，但后续事件的调度永远不会是精确的 2 秒间隔。换句话说，定时器不受累积误差的影响。

虽然 `settimer()` 使用的定时器允许微秒级精度，但定时器的准确性传统上受到软件时钟频率（第 10.6 节）的限制。如果定时器值与软件时钟颗粒度的整数不匹配，则定时器值将向上舍入。这意味着，例如，如果我们指定一个间隔定时器每 19,190 微秒运行一次（即仅 199 毫秒），假设 jiffy 值为 4 毫秒，我们实际上得到的定时器是每 20 毫秒过期一次。

## 高分辨率定时器

在 Linux 内核上，上述关于定时器分辨率受软件时钟频率限制的说法不再成立。从内核 2.6.21 开始，Linux 可选地支持高分辨率定时器。如果启用了此支持（通过 `CONFIG_HIGH_RES_TIMERS` 内核配置），我们在本章描述的定时器和 sleep 接口的准确性不再受内核 jiffy 大小的限制。相反，准确性可以达到底层硬件允许的程度。在现代硬件上，准确到微秒是常态的。

可以通过检查第 23.5.1 节描述的 `clock_gettime()` 返回的时钟来确定高分辨率定时器的可用性。

## 为阻塞操作设置超时

实时定时器的一个用途是为阻塞系统调用保持阻塞状态的时间设定上限。例如，如果用户在一定时间内没有输入行输入，我们希望取消来自终端的 `read()`。我们可以按照以下方法实现：

- 调用 `sigaction()` 为 `SIGALRM` 建立处理器，忽略 `SA_RESTART` 标志，这样系统调用就不会被重启（参见第 21.5 节）。
- 调用 `alarm()` 或 `setitimer()` 建立一个定时器，指定我们希望系统调用的时间上限。
- 执行阻塞系统调用。
- 系统调用返回后，再次调用 `alarm()` 或 `setitimer()` 来禁用定时器（以防系统调用在定时器过期前已完成）。
- 检查阻塞系统调用是否因 `errno` 被设置为 `EINTR`（中断的系统调用）。

列表 23-2 展示了这种用于 `read()` 的技术，使用 `alarm()` 建立定时器。

列表 23-2：带有超时的 `read()` 执行

```c
#include <signal.h>
#include <unistd.h>
#include <string.h>

#define BUF_SIZE 200

/* SIGALRM 处理器：中断系统调用 */
static void handler(int sig)
{
    printf("Caught signal\n"); /* 不安全 (见 21.1 节) */
}

int main(int argc, char *argv[])
{
    struct sigaction sa;
    char buf[BUF_SIZE];
    ssize_t numRead;
    int savedErrno;

    if (argc > 1 && strcmp(argv[1], "--help") == 0)
        usage("%s [num-secs]\n", argv[0]);

    /* 为 SIGALRM 设置处理器。除非提供了命令行参数，否则允许系统调用中断 */
    sa.sa_flags = (argc > 2) ? SA_RESTART : 0;
    sigemptyset(&sa.sa_mask);
    sa.sa_handler = handler;
    if (sigaction(SIGALRM, &sa, NULL) == -1)
        errExit("sigaction");

    alarm(argc > 1) ? alarm(atoi(argv[1])) : 0;

    numRead = read(STDIN_FILENO, buf, BUF_SIZE - 1);
    savedErrno = errno; /* 以防 alarm() 改变它 */
    alarm(0); /* 关闭定时器 */
    errno = savedErrno;

    /* 确定 read() 的结果 */
    if (numRead == -1) {
        if (errno == EINTR)
            printf("Read timed out\n");
        else
            errExit("read");
    } else {
        printf("Successful read (%ld bytes): %s", (long)numRead, buf);
    }
    exit(EXIT_SUCCESS);
}
```

注意列表 23-2 中的程序存在理论上的竞态条件。如果定时器在调用 `alarm()` 之后但在 `read()` 调用之前过期，`read()` 调用将被中断。由于在这种情况下使用的超时值很大（至少几秒），这种情况极不可能发生，因此在实践中这是一个可行的技术。[Stevens & Rago, 2005] 建议使用 `longjmp()`。处理 I/O 的另一种方法是使用 `select()` 或 `poll()` 系统调用的超时功能（第 6 章），它们允许我们同时等待多个描述符的 I/O。

## 23.4 按固定间隔暂停执行（睡眠）

我们希望让进程暂停一段固定时间。虽然可以使用 `sigsuspend()` 和已描述的定时器函数来实现这一点，但使用 `sleep` 函数之一更为简单。

### 23.4.1 低分辨率睡眠：sleep()

`sleep()` 函数根据 `seconds` 参数指定的秒数暂停调用进程，直到捕获信号（从而中断调用）。

```c
#include <unistd.h>

unsigned int sleep(unsigned int seconds);

/* 正常完成返回 0，如果提前终止则返回剩余秒数 */
```

如果睡眠完成，`sleep()` 返回 0。如果睡眠被信号中断，`sleep()` 返回剩余的（未睡眠）秒数。使用 `alarm()` 和 `setitimer()` 设置定时器时，系统负载可能会导致进程在 `sleep` 调用完成后一段（通常很短）后才重新调度。USv3 未规定 `sleep()` 与 `alarm()` 和 `setitimer()` 的交互。在 Linux 上，`sleep()` 实现为对 `nanosleep()`（第 23.4.2 节）的调用，结果是 `sleep()` 与定时器函数之间没有交互。然而，在许多实现中（尤其是旧版本），`sleep()` 是使用 `alarm()` 和 `SIGALRM` 处理器实现的。为了可移植性，避免将 `sleep()` 与 `alarm()` 和 `setitimer()` 使用。

## 高分辨率睡眠：nanosleep()

`nanosleep()` 函数类似于 `sleep()`，但提供了许多优势，包括在指定睡眠间隔时具有更精细的分辨率。

```c
#define _POSIX_C_SOURCE 199309
#include <time.h>

int nanosleep(const struct timespec *request, struct timespec *remain);

/* 成功完成睡眠返回 0，出错或睡眠中断返回 -1 */
```

`request` 参数指定睡眠间隔的持续时间，指向如下结构的指针：

```c
struct timespec {
    time_t tv_sec;      /* 秒 */
    long tv_nsec;       /* 纳秒 */
};
```

`tv_nsec` 字段指定纳秒值。它必须是 0 到 999,999,999 范围内的数字。

`nanosleep()` 的另一个优势是 USv3 明确规定它不应该使用信号实现。这意味着，与 `sleep()` 的情况不同，我们可以可移植地将 `nanosleep()` 调用与 `alarm()` 或 `setitimer()` 调用混合使用。

尽管不是使用信号实现的，`nanosleep()` 仍然可能被信号处理器中断。在这种情况下，`nanosleep()` 返回 -1，`errno` 为通常的 `EINTR`，且 `remain` 参数不为空，缓冲区用于返回剩余的未睡眠时间。如果需要，可以使用返回值来重启系统调用级完成的睡眠。这在列表 23-3 中得到演示。

该程序为 `nanosleep()` 期望秒和纳秒值。程序会循环执行 `nanosleep()`，直到总的睡眠间隔结束。如果 `nanosleep()` 被 `SIGINT` 处理器程序（通过输入 Control-C 生成）中断，则将使用 `remain` 返回的值重新启动调用。当我们运行此程序时，会看到以下内容：
