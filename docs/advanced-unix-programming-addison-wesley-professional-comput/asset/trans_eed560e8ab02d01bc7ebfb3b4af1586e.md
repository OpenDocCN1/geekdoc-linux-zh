
## **usleep** — 以微秒为单位挂起执行，或直到收到信号

```c
#include <unistd.h>

int usleep(
unsigned long usecs
/* 要睡眠的微秒数 */
);
/* 成功时返回 0，出错时返回 -1（设置 errno） */
```

usleep 几乎与 sleep 相同，区别在于：如果试图使用它睡眠整整一秒或更长时间，则被视为错误。也就是说，usecs 必须小于一百万。如果你知道系统具有定时器选项（_POSIX_TIMERS），那么 nanosleep 更精确，且没有这种限制：

## **nanosleep** — 以纳秒为单位挂起执行，或直到收到信号

```c
#include <time.h>

int nanosleep(
const struct timespec *req,
struct timespec *rem
/* 返回时：未使用的剩余时间，或为 NULL */
);
/* 成功时返回 0，出错时返回 -1（设置 errno） */
```

nanosleep 接受一个 timespec 结构，该结构在第 1.7.2 节中定义。回顾一下，它包含一个用于秒的 tv_sec 成员和一个用于纳秒的 tv_nsec 成员。

如果该函数被中断，它会像往常一样返回 -1 并将 errno 设置为 EINTR，同时将其指针 rem 所指向的内存设置为剩余时间。如果返回值为零，或者 remain 为 NULL，则它不会通过参数返回任何内容。

第 9.7.5 节中还有另一个名为 clock_nanosleep 的睡眠函数。

## 9.7.4 基本区间定时器系统调用

alarm 系统调用（第 9.7.1 节）使用一个进程范围内的区间定时器，存在于所有 UNIX 版本中。所有符合 SUS 标准的系统，以及一些其他系统，还提供另外三个你可以独立使用的区间定时器：

- *ITIMER_REAL* 在真实时间内递减；到期时产生 SIGALRM。
- *ITIMER_VIRTUAL* 在进程虚拟时间内递减；到期时产生 SIGVTALRM。
- *ITIMER_PROF* 在进程虚拟时间以及系统代表该进程运行期间同时递减；到期时产生 SIGPROF。它旨在供性能分析器使用，帮助通过指示程序在哪里耗费时间来进行调优。

在接下来的两个系统调用中，which 参数必须是上述列出的三个宏之一：

**getitimer** — 获取区间定时器的值

```c
#include <sys/time.h>

int getitimer(
	int which,	/* 要获取的定时器 */
	struct itimerval *val	/* 返回的值 */
);
/* 成功时返回 0，出错时返回 -1（设置 errno） */
```

**setitimer** — 设置区间定时器的值

```c
#include <sys/time.h>

int setitimer(
	int which,	/* 要设置的定时器 */
	const struct itimerval *val,	/* 要设置的值 */
	struct itimerval *oval	/* 返回的旧值 */
);
/* 成功时返回 0，出错时返回 -1（设置 errno） */
```

**struct itimerval** — 用于 getitimer 和 setitimer 的结构体

```c
struct itimerval {
	struct timeval it_interval;	/* 重置值 */
	struct timeval it_value;	/* 当前值 */
};
```

在 itimerval 结构中，it_interval 是定时器到期时重置定时器所用的时间，it_value 是当前区间的值。也就是说，与只触发一次的 alarm 不同，这些定时器可以在触发时自动重置。如果你调用 setitimer 时 it_value 成员为零，它会立即停止定时器。如果你调用 setitimer 时 it_interval 成员为零，它会在当前区间到期后停止定时器。在第 1.7.1 节中定义的 timeval 结构有两个成员：tv_sec 用于秒，tv_usec 用于微秒。

如果 setitimer 的 oval 参数非 NULL，它会获取旧值。示例如下：

```c
/* 3.5 秒定时器，仅触发一次 */
itv.it_interval.tv_sec = 0;
itv.it_interval.tv_usec = 0;
itv.it_value.tv_sec = 3;
itv.it_value.tv_usec = 500000;
ec_negl( setitimer(TIMER_REAL, &itv, NULL) )
```

```c
/* 3.5 秒定时器，然后重复 2.25 秒的定时器 */
itv.it_interval.tv_sec = 2;
itv.it_interval.tv_usec = 250000;
itv.it_value.tv_sec = 3;
itv.it_value.tv_usec = 500000;
ec_neg!(setitimer(TIMER_REAL, &itv, NULL))

/* 立即停止定时器；区间并不重要 */
itv.it_value.tv_sec = 0;
itv.it_value.tv_usec = 0;
ec_neg!(setitimer(TIMER_REAL, &itv, NULL))
```

在中间的示例中，定时器将在 3.5 秒时触发，然后在 5.75 秒再次触发，接着在 8 秒触发，依此类推，之后每隔 2.25 秒触发一次，直到停止。

下面是一个示例，它每 2 秒（真实/“墙上时钟”时间）显示一个 X。请注意，一旦设置好定时器，程序其余部分就可以自由执行其任务，在此示例中，该任务只是从终端读取数据并回显所读取的内容：

```c
void timer_try(void)
{
    struct sigaction act;
    struct itimerval itv;
    char buf[100];
    ssize_t nread;

    memset(&act, 0, sizeof(act));
    act.sa_handler = handler;
    ec_neg!(sigaction(SIGALRM, &act, NULL))
    memset(&itv, 0, sizeof(itv));
    itv.it_interval.tv_sec = 2;
    itv.it_value.tv_sec = 2;
    ec_neg!(setitimer(TIMER_REAL, &itv, NULL))
    while (true) {
        switch (nread = read(STDIN_FILENO, buf, sizeof(buf) - 1)) {
        case -1:
            EC_FAIL
        case 0:
            printf("EOF\n");
            break;
        default:
            if (nread > 0) {
                buf[nread] = '\0';
                ec_neg!(write(STDOUT_FILENO, buf, strlen(buf)))
            }
            continue;
        }
        break;
    }
    return;

EC_CLEANUP_BGN
    EC_FLUSH("timer_try1")
EC_CLEANUP_END
}

void handler(int signum)
{
    write(STDOUT_FILENO, "\nX\n", 3);
}
```

输出如下所示：

```text
X
ERROR:  0: tml [/aup/c9/tmr.c:26] 0
    *** EINTR (4: "Interrupted system call") ***
```

发生的情况是，第一个 X 在 2 秒后正常输出，但 SIGALRM 信号中断了处于阻塞状态的 read。解决方法是设置 SA_RESTART 标志，以便系统调用不被中断：

```c
    memset(&act, 0, sizeof(act));
    act.sa_handler = handler;
    act.sa_flags = SA_RESTART;
    ec_neg1( sigaction(SIGALRM, &act, NULL) )
```

现在的输出如下，显示输入了 “hello” 并被回显，同时每 2 秒显示一个 X：

```text
X
x
hello
X
hello
X
...
```

还有一个名为 ualarm 的区间定时器系统调用，但它已被弃用。

## 9.7.5 实时时钟

所有 UNIX 系统都有一个基本时钟，你可以使用 time 和 gettimeofday 系统调用（第 1.7.1 节）读取其值，但带来 nanosleep（第 9.7.3 节）的同一 Timers 选项（_POSIX_TIMERS）还包括一个或多个额外的时钟，具体取决于软件和硬件支持的数量。要访问其中一个，需通过其时钟 ID 进行引用。

所有具有 Timers 选项的系统都支持一个 ID，即 CLOCK_REALTIME，它记录时间（time of day）。是否存在其他时钟、它们的宏是什么，以及它们是系统范围内的还是进程私有的，取决于具体实现。例如，Solaris 还支持一个系统范围内的 CLOCK_HIGHRES 时钟，它从过去的某个点开始计数。读取它不能得到当天的时间，因为你不知道它是如何设置的，但它非常适合比较两个不同时刻的读数。

调用 clock_gettime 可以在返回的 timespec 结构中获取纳秒级的时间（第 1.7.2 节和第 9.7.3 节）：

**clock_gettime** — 从时钟获取时间

```c
#include <time.h>

int clock_gettime(
    clockid_t clock_id,          /* 时钟 ID（如 CLOCK_REALTIME） */
    struct timespec *tp          /* 时间 */
);
/* 成功时返回 0，出错时返回 -1（设置 errno） */
```

使用 clock_getres 可以获取时钟的纳秒级分辨率：

**clock_getres** — 获取时钟分辨率

```c
#include <time.h>

int clock_getres(
    clockid_t clock_id,          /* 时钟 ID */
    struct timespec *res         /* 分辨率 */
);
/* 成功时返回 0，出错时返回 -1（设置 errno） */
```

此外，在具有适当权限的情况下（对于 CLOCK_REALTIME 为超级用户权限），你可以设置时钟：

**clock_settime** — 设置时钟

```c
#include <time.h>

int clock_settime(
    clockid_t clock_id,          /* 时钟 ID */
    const struct timespec *tp     /* 时间 */
);
/* 成功时返回 0，出错时返回 -1（设置 errno） */
```

下面是一个函数，它从时钟获取时间和分辨率并显示出来，同时显示 time 系统调用（第 1.7.1 节）以秒为单位的时间：

```c
void clocks(void)
{
    struct timespec ts;
    time_t tm;

    ec_negl( time(&tm) )
    printf("time() Time: %ld secs.\n", (long)tm);
    printf("CLOCK_REALTIME:\n");
    ec_negl( clock_gettime(CLOCK_REALTIME, &ts) )
    printf("Time: %1d.%09ld secs.\n", (long)ts.tv_sec, (long)ts.tv_nsec);
    ec_negl( clock_getres(CLOCK_REALTIME, &ts) )
    printf("Res.: %1d.%09ld secs.\n", (long)ts.tv_sec, (long)ts.tv_nsec);
    return;

EC_CLEANUP_BGN
    EC_FLUSH("clocks")
EC_CLEANUP_END
}
```

在 FreeBSD 系统上的输出为：

```text
time() Time: 1051646878 secs.
CLOCK_REALTIME:
Time: 1051646878.568628061 secs.
Res.: 0.000000838 secs.
```

这表明分辨率略小于一微秒。在不同的硬件上，Solaris 系统的输出为：

```text
time() Time: 1051646409 secs.
CLOCK_REALTIME:
Time: 1051646409.686869683 secs.
Res.: 0.010000000 secs.
```

那里的分辨率仅为百分之一秒。显示小数点后 9 位时间具有误导性——最好将显示限制在分辨率所能达到的精度。然而，这些时钟并非用于显示目的。它们用于计时。

有一个使用特定时钟的 nanosleep 版本（第 9.7.3 节）：

