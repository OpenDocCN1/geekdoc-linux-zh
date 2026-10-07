
```
$ ./ptmr_sigev_thread 5:5 10:10
Timer ID: 134525024 (5:5)
Timer ID: 134525080 (10:10)
[13:06:22] Thread notify
timer ID=134525024
timer_getoverrun()=0
main(): count = 1
[13:06:27] Thread notify
timer ID=134525080
timer_getoverrun()=0
main(): count = 2
[13:06:27] Thread notify
timer ID=134525024
timer_getoverrun()=2
main(): count = 3
Type Control-Z to suspend the program
$ [1] Stopped /ptmr_sigev_thread 5:5 10:10
$ fg
/ptmr_sigev_thread 5:5 10:10
[13:06:45] Thread notify
timer ID=134525024
timer_getoverrun()=2
There were timer overruns
main(): count = 6
[13:06:45] Thread notify
timer ID=134525080
timer_getoverrun()=0
main(): count = 7
Type Control-C to kill the program
```

### 列表 23-7: 使用线程函数的 POSIX 定时器通知

```c
#include <signal.h>
#include <time.h>
#include <pthread.h>
#include "curr_time.h"
#include "tlpi_hdr.h"
#include "itimerspec_from_str.h"

/* Declaration of currTime() */
/* Declares itimerspecFromStr() */
static pthread_mutex_t mtx = PTHREAD_MUTEX_INITIALIZER;
static pthread_cond_t cond = PTHREAD_COND_INITIALIZER;

static int expire = 0; /* Number of expirations of all timers */

static void /* Thread notification function */
timerFunc(union sigval sv)
{
    timer_t *tidptr;
    int s;

    tidptr = sv.sival_ptr;

    printf("[%s] Timer notify\n", currTime("%T"));
    printf(" ID=%d\n", (long)tidptr);
    printf(" timer_getoverrun()=%d\n", timer_getoverrun(*tidptr));

    /* Increment counter variable shared with main thread and signal condition variable to notify main thread of the change. */
    s = pthread_mutex_lock(&mtx);
    if (s != 0)
        errExEN(s, "pthread_mutex_lock");

    expire += 1 + timer_getoverrun(*tidptr);

    s = pthread_mutex_unlock(&mtx);
    if (s != 0)
        errExEN(s, "pthread_mutex_unlock");

    s = pthread_cond_signal(&cond);
    if (s != 0)
        errExEN(s, "thread_cond_signal");
}

int main(int argc, char *argv[])
{
    struct sigevent sev;
    struct itimerspec ts;
    timer_t *tidlist;
    int s, j;

if (argc < 2) {
    usageErr("%s secs[/nsecs]:[int-secs]/[int-nsecs]]...\n", argv[0]);
}
tidlist = calloc(argc - 1, sizeof(timer_t));
if (tidlist == NULL)
    errExit("malloc");
```

- `sigsev.notify = SIGV_THREAD;` /* 通过线程通知 */
- `sigsev.notify_handler = threadFunc;` /* 线程启动函数 */

`sigsev.notify_attributes = NULL;` /* 可以是指指向 pthread_attr 结构的指针 */

```c
/* 为每个命令行参数创建并启动一个定时器 */
for (j = 0; j < argc - 1; j++) {
    itimerpecFromStr(argv[j + 1], &ts);
}
```

- `sigsev.value.sival_ptr = &tidlist[j];` /* 作为参数传递给 threadFunc() */

```c
if (timer_create(CLOCK_REALTIME, &sev, &tidlist[j]) == -1)
    errExit("timer_create");
printf("Timer ID: %ld (%s)\n", (long)tidlist[j], argv[j + 1]);
```

- `if (timer_settime(tidlist[j], 0, &ts) == -1)`
    `errExit("timer_settime");`

```c
/* 主线程等待条件变量，该变量在每次调用通知函数时被信号。我们打印消息以便看到发生了什么。 */
s = pthread_mutex_lock(&mtx);
if (s != 0)
    errExEN(s, "pthread_mutex_lock");
```

- `for (;;) {`
    `s = pthread_cond_wait(&cond, &mtx);`
    `if (s != 0)`
        `errExEN(s, "pthread_cond_wait");`
    `printf("main(): expireCnt = %d\n", expire);`

## 23.7 通过文件描述符通知的定时器：timerfd API

从内核 2.6.25 开始，Linux 提供了另一种创建定时器的 API。Linux 特有的 `timerfd` API 创建的定时器可以通过文件描述符读取过期通知。这是非常有用的，因为可以使用 `select()`、`poll()` 和 `epoll` 同时监控。在本章讨论的其他定时器 API 需要通过一组文件描述符来监控多个定时器。

此 API 中的三个系统调用操作与第 23.6 节描述的 `timer_create()`、`timer_settime()` 和 `timer_gettime()` 操作类似。第一个系统调用是 `timerfd_create()`，它创建一个新的定时器对象并返回指向对象的文件的描述符。

```c
#include <sys/timerfd.h>

int timerfd_create(int clockid, int flags);
```

成功时返回描述符，失败返回 -1。`clock` 的值可以是 `CLOCK_REALTIME` 或 `CLOCK_MONOTONIC`（见表 23-1）。在 `timerfd_create()` 的初始实现中，`flags` 参数预留以后使用并必须指定为 0。但从 Linux 2.6.27 开始，支持两个标志：

### TFD_CLEXEC

- 在新的文件描述符上设置执行时关闭标志 `FD_CLEXEC`。该标志的作用与第 4.3.1 节描述的 `open()` `O_CLOEXEC` 标志相同。

### TFD_NONBLOCK

- 在底层文件描述符上设置 `O_NONBLOCK` 标志，以便未来的读取是非阻塞的。这为了达到相同结果所需的额外的 `fcntl()` 调用。

当我们完成 `timerfd_create()` 创建的定时器时，应该 `close()` 关联的文件描述符，以便内核释放与定时器相关的资源。`timerfd_settime()` 系统调用启动（开启）或停止（取消）文件描述符指向的定时器。

```c
#include <sys/timerfd.h>

int timerfd_settime(int fd, int flags, struct itimerspec *new_value,
                    struct itimerspec *old_value);
```

成功时返回 0，失败返回 -1。`new_value` 参数指定定时器的设置。`old_value` 参数可用于返回定时器的设置（详情见下文 `timerfd_gettime()`）。如果我们对设置感兴趣，可以将 `old_value` 指定为 NULL。这两个参数都是 `timespec` 结构，其使用方式与 `timer_settime()` 相同（见第 23.6.2 节）。`flags` 参数与 `timer_settime()` 对应的参数类似。它可能是 0，意味着 `new_value->it_value` 相对于调用 `timerfd_settime()` 的时间解释；也可以 `TFD_TIMER_ABSTIME`，意味着 `new_value.it_value` 被解释为绝对时间（即从时钟零点开始测量）。

`timerfd_gettime()` 系统调用返回由文件描述符 `fd` 指定的定时器的间隔和剩余时间。

```c
#include <sys/timerfd.h>

int timerfd_gettime(int fd, struct timespec *curr_value);
```

成功时返回 0，失败返回 -1。与 `timer_gettime()` 一样，间隔和定时器到期时间返回在由 `curr_value` 指向的 `timespec` 结构中。即使此定时器使用 `TFD_TIMER_ABSTIME` 设置为绝对时间，`curr_value.it_value` 也返回到下一次过期的时间。如果返回的 `curr_value.it_value` 结构字段均为 0，则定时器当前已开启。如果返回的 `curr_value.it_interval` 字段均为 0，则定时器过期一次。

## timerfd 与 fork() 和 exec() 的交互

在 `fork()` 期间，子进程继承由 `timerfd_create()` 创建的文件描述符。这些描述符指向父进程中对应描述符相同的定时器对象，可以在可以在进程中读取定时器过期。

`timerfd_create()` 创建的文件描述符在 `exec()` 之后会被保留（除非标记为执行时关闭，见第 27.4 节），且开启的定时器将在 `exec()` 之后继续产生过期。

## 示例程序

列表 23-8 演示了 `timerfd` API 的用法。该程序接受两个命令行参数。第一个参数是强制性的，指定定时器的初始时间和间隔。（该参数使用列表 23-6 中所示 `itimerpecFromStr()` 函数进行解释。）第二个参数是可选的，指定

程序应等待定时器终止的最多到期次数；此参数的默认值为 1。

程序使用 `timerfd_create()` 创建一个定时器，并使用 `timerfd_settime()` 为其设置定时。它进入循环，从描述符中读取到期通知，直到达到指定的到期次数。在每次 `read()` 之后，程序都会显示自定时器启动以来经过的时间、到期次数，以及到目前为止的到期总数。

在接下来的 shell 会话日志中，命令行参数指定了一个数值为 1 秒、间隔为 1 秒的定时器，最多允许 100 次到期。

```
$ ./timerfd 1 1 100

1000: expirations read: 1; total=1

2000: expirations read: 1; total=2

3000: expirations read: 1; total=3

输入 Control-C 将程序在后台暂停几秒

[1] Stopped ./timerfd 1 1 100

$ fg

./timerfd 1 1 100 在前台恢复程序

14205: expirations read: 11; total=14 (上次读取后发生了多次到期)

15000: expirations read: 1; total=15

16000: expirations read: 1; total=16

输入 Control-C 终止程序
```

# 列表 23-8：使用 timerfd API

```c
timers/demo_timerfd.c

#include <sys/timerfd.h>
#include <time.h>
#include <stdint.h>
#include "itimerspec_from_str.h"   /* uint64_t 的定义 */
#include <tlpi_hdr.h>               /* 声明 itimerspecFromStr() */

int
main(int argc, char *argv[])
{
    struct itimerspec ts;
    struct timespec start, now;
    int maxExp, fd, decsecs, nanosecs;
    uint64_t numExp, totalExp;
    ssize_t s;

    if (argc < 2 || strcmp(argv[1], "--help") == 0)
        usageErr("%s %secs/%nanosecs]:[int-secs/int-nanosecs] [max-exp]\n", argv[0]);

    itimerspecFromStr(argv[1], &ts);
    maxExp = (argc > 2) ? getInt(argv[2], GN_GT_0, "max-exp") : 1;

    fd = timerfd_create(CLOCK_REALTIME, 0);
    if (fd == -1)
        errExit("timerfd_create");

    if (timerfd_settime(fd, 0, &ts, NULL) == -1)
        errExit("timerfd_settime");

    if (clock_gettime(CLOCK_MONOTONIC, &start) == -1)
        errExit("clock_gettime");

    for (totalExp = 0; totalExp < maxExp;) {
        /* 读取定时器上的到期次数，然后显示
           自定时器启动以来经过的时间，随后是到期次数和到目前为止读取的到期次数。 */
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
        printf("%.03d: expirations read: %lu; total=%lu\n",
               secs, (nanosecs + 500000) / 1000000,
               (unsigned long) numExp, (unsigned long) totalExp);
    }
    exit(EXIT_SUCCESS);
}
```
