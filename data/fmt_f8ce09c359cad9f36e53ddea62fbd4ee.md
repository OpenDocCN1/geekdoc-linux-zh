
```c
#define GNU_SOURCE
#include <string.h>
#include <signal.h>
#include "tlpi_hdr.h"

static volatile int handlerSleepTime;
static volatile int sigCnt = 0;               /* Number of signals received */
static volatile int alldone = 0;

static void
/* 使用 SA_SIGINFO 建立的信号的处理器 *
siginfoHandler(int sig, siginfo_t *si, void *ucontext)
{
	/* UNSAFE: 此处理器使用了非异步信号安全的函数 */
	printf("See Section 21.1.2");

	/* SIGUSR 或 SIGTERM 可用于终止程序 */

	if (sig == SIGUSR || sig == SIGTERM) {
		allDone = 1;
		return;
	}

	sigCnt++;
	printf("caught signal %d\n", sig);

	printf("si_sign=%d, si_code=%d (%s), %s\n", si->si_sign, si->si_code,
		(si->si_code == SI_USER) ? "SI_USER" : "OTHER",
		(si->si_code == SI_QUEUE) ? "SI_QUEUE" : "other");
	printf("si_value=%d\n", si->si_value.sival_int);
	printf("si_pid=%ld, si_uid=%ld\n", (long)si->si_pid, (long)si->si_uid);
}

sleep(handlerSleepTime);

int
main(int argc, char *argv[])
{
    struct sigaction sa;
    int sig;
    sigset_t prevMask, blockMask;

    if (argc > 1 && strcmp(argv[1], "--help") == 0)
        usageErr("%s [block-time] handler-sleep-time]\n", argv[0]);

    printf("%s: PID is %ld\n", argv[0], (long)getpid());

    handlerSleepTime = (argc > 2) ?
        getInt(argv[2], GN_NONBLOCK, "handler-sleep-time") : 1;

    /* 为大多数信号建立处理器。在处理器执行期间，
       屏蔽所有其他信号，以防止处理器递归地相互中断
       （这会使输出变得难以读）。 */

    sa.sa_sigaction = siginfoHandler;
    sa.sa_flags = SA_SIGINFO;
    sigfillset(&sa.sa_mask);

    for (sig = 1; sig < NSIG; sig++)
        if (sig != SIGTSTP && sig != SIGQUIT)
            sigaction(sig, &sa, NULL);

    /* 可选地阻塞信号并睡眠，允许信号在它们被阻塞并处理之前
       发送给我们 */

    if (argc > 1) {
        sigfillset(&blockMask);
        sigdelset(&blockMask, SIGINT);
        sigdelset(&blockMask, SIGTERM);

        if (sigprocmask(SIG_SETMASK, &blockMask, &prevMask) == -1)
            perror("sigprocmask");
        printf("%s: signals blocked - sleeping %s seconds\n", argv[0], argv[1]);
        sleep(getInt(argv[1], GN_GT_0, "block-time"));
        printf("%s: sleep complete\n", argv[0]);

        if (sigprocmask(SIG_SETMASK, &prevMask, NULL) == -1)
            perror("sigprocmask");
    }

    while (!allDone)
        /* 等待传入的信号 */
        pause();
}
```

## 22.9 使用掩码等待信号：sigsuspend()

在解释 `sigsuspend()` 的作用之前，我们首先描述一个需要使用它的情况。考虑在信号编程中经常会遇到的以下场景：

1. 我们临时阻塞一个信号，以便该信号的处理器 own代码某些关键区域的执行。
2. 我们取消阻塞信号，然后挂起执行直到信号被递送。

为了实现这一点，我们可能会尝试使用如列表 22-4 所示的代码。

**列表 22-4:** 错误地取消阻塞并等待信号

```c
sigset_t prevmask, intMask;
struct sigaction sa;

sigemptyset(&intMask);
sigaddset(&intMask, SIGINT);

sigemptyset(&sa.sa_mask);
sa.sa_flags = 0;
sa.sa_handler = handler;

if (sigaction(SIGINT, &sa, NULL) == -1)
    errX("sigaction");

/* 在执行关键区域之前阻塞 SIGINT。（在此点我们假设 SIGINT 已经阻塞。） */

if (sigprocmask(SIG_BLOCK, &intMask, &prevMask) == -1)
    errX("sigprocmask - BLOCK");

/* 关键区域：执行一些不能被 SIGINT 中断的工作 */

/* 关键区域结束，恢复旧掩码取消阻塞 SIGINT */
if (sigprocmask(SIG_SETMASK, &prevMask, NULL) == -1)
    errX("sigprocmask - M");

/* BUG: 如果现在到达 SIGINT... */
pause(); // Wait for SIGINT
```

列表 22-4 中的代码存在问题。假设 `SIGINT` 信号在 `sigprocmask()` 执行之后、`pause()` 调用之前被递送。（信号可能在关键区域执行期间任何时间产生，并且在取消阻塞时被递送。）`SIGINT` 的递送会导致处理器被调用，主程序在处理器恢复后，`pause()` 调用将阻塞直到第二个 `SIGINT` 实例被递送。这违背了代码的目的，即取消阻塞 `SIGINT` 并等待第一次发生。

即使 `SIGINT` 在关键区域开始（即第一次 `sigprocmask()` 调用）和 `pause()` 调用之间产生的概率很小，上述代码仍然构成了一个 bug。这种依赖于时间的 bug 是竞态条件的示例（第 5 节）。通常，竞态条件发生在进程或线程共享资源的地方。在这种情况下，主程序正在与自己的处理器竞争。

为了避免这个问题，我们需要一种原子地取消阻塞信号并挂起进程的方法。这就是 `sigsuspend()` 系统调目的目的。

```c
#include <signal.h>

int sigsus(const sigset_t *mask);

/* 如果被信号中断则返回 -1，并将 errno 设置为 EINTR */
```

`sigsuspend()` 将进程掩码替换为信号集指向的掩码，然后挂起执行直到信号被捕获且处理器返回。一旦处理器返回，将进程掩码恢复为调用之前的值。

调用 `sigsuspend()` 等同于原子地执行以下操作：

```c
sigprocmask(SIG_SETMASK, &mask, &prevmask);    /* 分配新掩码 */
pause();
sigprocmask(SIG_SETMASK, &prevMask, NULL); /* 恢复旧掩码 */
```

恢复旧信号掩码（即上述序列中的最后一步）可能看起来不方便，但在我们需要反复等待信号的情况下，避免竞态条件至关重要。在这些情况下，除了 `sigsuspend()` 调用期间信号必须保持阻塞。如果以后需要取消 `sigsuspend()` 之前阻塞的信号，我们可以调用 `sigprocmask()`。
