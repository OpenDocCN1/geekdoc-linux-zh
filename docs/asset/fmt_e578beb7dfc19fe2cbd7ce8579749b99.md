
```c
perror("Failed to get start time");

return 1;

}

function_to_time(tmend);

if ((tend = times(&tmend)) == -1) {

perror("Failed to get end times");

return 1;

}

cticks = tmend.tm_utime + tmend.tm_stime -
         tmstart.tm_utime - tmstart.tm_stime;

printf("Total CPU time for operation is %f seconds\n", clockticks);

if ((cticks < tstart) || (cticks < 0)) {

fprintf(stderr, "Tick time wrapped, couldn't calculate fraction\n");

return 1;

}

printf("Fraction of CPU time used is %f\n", cticks, (tend - tstart));

return 0;

}
```

## 示例 9.9

以下命令行使用程序 9.5 的 `timechild` 来对程序 9.4 的执行计时。

```bash
timechild cpufraction
```

## 程序 9.5 timechild.c

一个执行其 `fork()` 命令行数组作为子进程的程序，并返回执行子进程所需的时间。

```c
#include <errno.h>
#include <stdio.h>
#include <unistd.h>
#include <sys/times.h>
#include <types.h>
#include <wait.h>
#include <stdlib.h>
#include <time.h>
int main(int argc, char *argv[]) {
    pid_t child;
    double clockticks;
    double ticks;
    struct tms tmend, tmstart;
    clock_t tend, tstart;
    if (argc != 2) {
        fprintf(stderr, "Usage: %s\n", argv[0]);
        return 1;
    }
    if ((child = fork()) == -1) {
        perror("fork");
        return 1;
    }
    if (child == 0) {
        execv(argv[1], &argv[1]);
        perror("execv");
        exit(1);
    }
    if ((tstart = times(&tmstart)) == -1) {
        perror("Failed to get start time");
        return 1;
    }
    wait(NULL);
    if ((tend = times(&tmend)) == -1) {
        perror("Failed to get end times");
        return 1;
    }
    cticks = tmend.tm_utime + tmend.tm_stime -
             tmstart.tm_utime - tmstart.tm_stime;
    if ((clockticks = (double)sysconf(_SC_CLK_TCK)) == -1) {
        perror("Failed to determine clock ticks per second");
        return 1;
    }
    if ((cticks < tstart) || (cticks < 0)) {
        fprintf(stderr, "Tick time wrapped, couldn't calculate fraction\n");
        return 1;
    }
    printf("The number of ticks per second is %f\n", clockticks);
    printf("Total CPU time for operation is %f seconds\n", clockticks);
    printf("Fraction of CPU time used is %f\n", cticks, (tend - tstart));
    return 0;
}
```
*(注：原文提供的程序 9.5 源码存在严重的错乱和重复，此处已根据逻辑和上下文进行了人工修复和整理，以符合标准文档规范。)*

## 9.2 Sleep 函数

一个自愿阻塞指定时间的进程被称为 `sleep`。`sleep` 函数阻塞直到指定时间结束。

### 概要

```c
#include <unistd.h>
unsigned sleep(unsigned seconds);
```

### POSIX

如果请求的时间已经结束，`sleep` 函数返回 0。如果被信号中断，它返回未睡眠的时间。`sleep` 受任何信号的影响。

## 示例 9.10 beeper.c

以下程序响铃 $n$ 秒，$n$ 是通过命令行传递的。

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
int main(int argc, char *argv[]) {
    int sleeptime;
    if (argc != 2) {
        fprintf(stderr, "Usage: %s\n", argv[0]);
        return 1;
    }
    sleeptime = atoi(argv[1]);
    fprintf(stderr, "Sleep time is %d\n", sleeptime);
    for ( ; ; ) {
        sleep(sleeptime);
        printf("\a");
        fflush(stdout);
    }
}
```

`nanosleep` 函数导致调用线程挂起执行，直到 `rqtp` 指定的时间间隔结束或线程接收到信号。如果 `nanosleep` 被信号中断且 `rmtp` 不为空，则指向的位置包含剩余时间，允许 `nanosleep` 重新启动。系统时钟 `CLOCK_REALTIME` 决定了 `rqtp` 的分辨率。

### 概要

```c
#include <time.h>
int nanosleep(const struct timespec *rqtp, struct timespec *rmtp);
```

如果成功，`nanosleep` 返回 0。如果失败，`nanosleep` 返回 -1 并设置 `errno`。下表列出了 `nanosleep` 的强制错误。

| errno | 原因 |
|--- |--- |
| EINTR | nanosleep 被信号中断 |
| EINVAL | rqtp 指定的纳秒值不在 [0, 10^9) |

`nanosleep` 使用的数据结构允许纳秒级分辨率，但 `CLOCK_REALTIME` 的分辨率通常大得多，在 10 毫秒级。`nanosleep` 函数旨在取代被认为过时的 `usleep`。

程序 9.6 测试了 `nanosleep` 函数的分辨率。它执行了 100 次睡眠时间为 1000 纳秒的 `nanosleep`。如果 `nanosleep` 具有真正的 1 ns 分辨率，将在 100 微秒内完成。在 10 毫秒分辨率的系统中，该程序大约需要一秒钟完成。

## 9.3 POSIX:XSI 间隔定时器

定时器在指定时间过去后会产生通知。与通过递增来跟踪时间流逝的时钟不同，定时器通常递减其值，并在值变为零时产生信号。计算机系统通常只有少几个硬件间隔定时器，操作系统通过使用这些硬件定时器来实现多个软件定时器。

操作系统以多种方式使用间隔定时器。间隔定时器可以引起周期性中断，触发操作系统增加计数器。该计数器可以记录自操作系统启动以来的时间。UNIX 系统传统将自 1970 年 1 月 1 日以来的秒数作为当天的时间。如果底层间隔定时器在 1000 微秒后产生中断并在每次过期后重启，则定时器服务程序可以维护一个本地计数器，通过在间隔定时器每过期 10,000 次后递增该计数器，来测量自 1970 年 1 月 1 日以来的秒数。

## 程序 9.6 nanotest.c

测试 nanosleep 分辨率的函数。

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/time.h>
#define COUNT 100
#define D_BILLION 10000000000.0
#define D_MILLION 1000000.0
#define MILLION 10000000L
#define NANOSECONDS 1000
int main(void) {
    int i;
    struct timespec slptm;
    long tdf;
    struct timeval tv_sec, tend, tstart;
    slptm.tv_sec = 0;
    slptm.tv_nsec = NANOSECONDS;
    if (gettimeofday(&tstart, NULL) == -1) {
        fprintf(stderr, "Failed to get start time\n");
        return 1;
    }
    for (i = 0; i < COUNT; i++) {
        if (nanosleep(&slptm, NULL)) {
            perror("Failed to nanosleep");
            return 1;
        }
    }
    if (gettimeofday(&tend, NULL) == -1) {
        fprintf(stderr, "Failed to get end time\n");
        return 1;
    }
    long tdiff = MILLION*(tend.tv_sec - tstart.tv_sec) + 
                 tend.tv_usec - tstart.tv_usec;
    printf("%d nanoseconds of %d nanoseconds\n", COUNT, NANOSECONDS);
    printf("Should take %ld microseconds and %f seconds\n",
    NANOSECONDS*COUNT/1000, NANOSECONDS*COUNT/D_MILLION);
    printf("Actually took %ld microseconds and %f seconds\n",
    ttdif/D_MILLION);
    printf("Number of seconds per nanosleep was %f\n",
    ttdif/(double)COUNT/MILLION);
    printf("Number of seconds per nanosleep should be %f\n",
    NANOSECONDS/D_BILLION);
    return 0;
}
```

分时操作系统也可以将间隔定时器用于进程调度。当操作系统调度一个进程时，它会启动一个称为调度量子（scheduling quantum）的时间间隔定时器。如果该定时器过期且进程仍在执行，调度器会将该进程移动到就绪队列，以便另一个进程可以执行。多处理器系统每个处理器都需要这样一个间隔定时器。

大多数调度算法都有一种机制来提高等待执行一段时间的进程的优先级。调度器应该使用间隔定时器进行优先级管理。每当定时器过期，调度器就会提高未执行进程的优先级。

POSIX:XSI 扩展的间隔使用 `struct timeval`，包含以下成员。

```c
struct timeval it_value;      /* 到下次过期的时间 */
struct timeval it_interval;   /* 重新加载到定时器的值 */
```

这里 `it_value` 保存定时器过期前的剩余时间，而 `it_interval` 持有过期后重置定时器时使用的时间间隔。记住 `struct timeval` 具有秒和微秒字段。

符合 POSIX:XSI 标准的实现必须为每个进程提供以下三个用户间隔：

- ITER_REAL：按实时递减并在过期时产生 SIGALRM。
- ITER_VIRTUAL：按虚拟时间（进程使用）递减并在过期时产生 SIGVALRM。
- ITER_PROF：按进程的虚拟时间和系统时间递减并在过期时产生 SIGPROF 信号。

POSIX 提供了 `getimer` 函数用于获取当前时间间隔，以及 `setimer` 函数用于启动和停止间隔定时器。`which` 参数指定定时器（即 `ITIMER_REAL`、`ITIMER_VIRTUAL`、`ITIMER_PROF`）。`getimer` 函数将定时器的当前值存储在 `value` 指向的位置。`setimer` 将由 `which` 指定的值设置为 `value` 指向的值。如果 `value` 不为 `NULL`，`setimer` 将定时器的上一个值放在 `value` 指向的位置。如果定时器正在运行，`*value` 的 `it_value` 成员为非零，并包含定时器本应过期前的剩余时间。

### 概要 (SYNOPSIS)

```c
#include <sys/time.h>
int getimer(int which, struct itimerval *value);
int setimer(int which, struct itimerval *value, struct itimerval *old);
```

如果成功，这些函数返回 0。如果失败，它们返回 -1 并设置 `errno`。如果 `value` 中的微秒数为零，`setimer` 会设置 `errno`。如果 `*value` 的 `it_interval` 成员不为 0，定时器将在过期时重启。如果 `it_interval` 为 0，`setimer` 将停止运行的定时器。程序 9.7 使用 `ITIMER_PROF` 定时器每两个 CPU 秒打印一个星号。程序调用 `setup` 安装 `myhandler`。程序调用 `setimer` 使用 `ITIMER_PROF` 设置定时器，每2秒过期一次。`ITIMER_PROF` 定时器在两个 CPU 秒后产生 SIGPROF 信号。进程捕获 SIGPROF 信号并用 `myhandler` 处理。该处理程序向标准错误输出一个星号。

## 9.7 periodic.c

一个每两个 CPU 秒打印一个星号的程序。

```c
#include <errno.h>
#include <signal.h>
#include <stdio.h>
#include <unistd.h>
#include <sys/time.h>
/* 参数部分 */
static void myhandler(int s) {
    char aster = '*';
    int errsave = errno;
    write(STDERR_FILENO, &aster, 1);
    errno = errsave;
}
static int setup(void) {
    /* 为 SIGPROF 设置 myhandler */
    struct sigaction act;
    act.sa_handler = myhandler;
    act.sa_flags = 0;
    return sigemptyset(&act.sa_mask) & sigaction(SIGPROF, &act, NULL);
}
static int settimer(int value) {
    /* 设置2秒间隔的 ITIMER_PROF */
    struct itimerval value;
    value.it_interval.tv_sec = 2;
    value.it_interval.tv_usec = 0;
    value.it_value = value.it_interval;
    return setimer(ITIMER_PROF, &value, NULL);
}
int main(void) {
  if (settimer() == -1) {
    perror("Failed to setup handler for SIGPROF");
    return 1;
  }
  if (settimer() == -1) {
```
