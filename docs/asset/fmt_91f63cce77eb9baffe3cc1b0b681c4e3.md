
POSIX:CX

`difftime` 没有定义任何错误。

## 示例 9.2 simpletiming.c

以下程序计算了执行 `function_to_time` 所需的墙钟时间。

```
# include <stdio.h>
# include <time.h>
void function_to_time(void);
int main(void) {
    time_t tstart;
    tstart = time(NULL);
    function_to_time(elapsed);
    printf("function_to_time took %f seconds of elapsed time\n", difftime(NULL, tstart));
    return 0;
}
```

示例 9.2 使用了一秒的分辨，除非 `function_to_time` 涉及大量的计算或等待，否则这可能不够准确。此外， `time` 函数测量的是墙钟时间或流逝时间，这可以反映 CPU 时间的使用量。第 9.1.5 节介绍了代码计时的其他替代方法。

## 9.1.2 显示日期和时间

`time_t` 类型便于需要时间差的计算，但对于打印日期来说很麻烦。此外，程序应该调整日期并考虑时区、夏令时间和闰秒等因素。

`localtime` 函数接收一个自纪元以来的秒数作为参数，并返回一个结构，其中时间组件（如日、月、年）已根据本地需求进行了调整。`asctime` 函数将 `localtime` 返回的结构转换为字符串。`ctime` 函数等同于 `asctime(localtime(clock))`。`gmtime` 函数接收一个代表自纪元以来的秒数的参数并返回一个结构。

概要

```
#include <time.h>
char *asctime(const struct tm *timeptr);
char *ctime(const time_t *clock);
struct tm *gmtime(const time_t *timer);
struct tm *localtime(const time_t *timer);
```

POSIX:CX

`localtime` 函数接收自纪元以来的秒数作为参数，并返回一个根据本地需求调整了时间组件（如日、月、年）的结构。`asctime` 函数将 `localtime` 返回的结构转换为字符串。`ctime` 函数等同于 `asctime(localtime(clock))`。`gmtime` 函数接收一个代表自纪元以来的秒数的参数并返回一个结构。

`ctime` 使用静态存储存储。

## 示例 9.3 timeprint.c

以下程序打印日期。

```c
#include <stdio.h>
#include <time.h>
int main(void) {
    time_t tcurrent;
    tcurrent = time(NULL);
    printf("The current time is %s", ctime(&tcurrent));
    return 0;
}
```

## 习题 9.4 badtiming.c

以下打印时间的程序有什么问题？

```c
#include <stdio.h>
#include <time.h>
void function_to_time(void);
int main(void) {
    time_t tend, tstart;
    tstart = time(NULL);
    function_to_time();
    tend = time(NULL);
    printf("The time before was %s after was %s", ctime(&tstart), ctime(&tend));
}
```

答案：

`ctime` 使用静态存储存储字符串。每次调用 `ctime` 都会覆盖之前的值。很可能两次打印的是相同的值。

`gmtime` 和 `localtime` 函数将时间分解为单独字段以便程序输出。ISO C 定义 `struct tm` 如下：

```c
struct tm {
    int tm_sec;      /* 分内的秒 [0,60] */
    int tm_min;      /* 小时内的分 [0,59] */
    int tm_hour;     /* 午夜以来的小时 [0,23] */
    int tm_mday;     /* 月中的几 [1,31] */
    int tm_mon;      /* 自1月以来的月份 [0,11] */
    int tm_year;     /* 自1900年以来的年份 */
    int tm_wday;     /* 星期日几几 [0,6] */
    int tm_yday;     /* 自1月以来的天 [0,365] */
    int tm_isdst;    /* 夏令时标志 */
};
```

## 示例 9.5

以下代码段打印了自年初以来的天数。

```c
struct tm *tcurrent;
tcurrent = localtime(NULL);
printf("%d days have elapsed since Jan 1\n", tcurrent->tm_yday);
```

遗憾的是，`asctime`、`ctime` 和 `localtime` 不是线程安全的。POSIX:TSF 安全扩展提供了线程安全的替代方案，它们将调用者提供的缓冲区作为额外参数。

概要

```
#include <time.h>
char *asctime_r(const struct tm *restrict timeptr, char *restrict buf);
char *ctime_r(const time_t *clock, char *buf);
struct tm *gmtime_r(const time_t *restrict timer, struct tm *restrict result);
struct tm *localtime_r(const time_t *restrict timer, struct tm *restrict result);
```

POSIX:TSF

如果成功，这些函数返回指向结果参数的指针。对于 `asctime_r` 和 `ctime_r`，结果在 `buf` 中。对于 `gmtime_r` 和 `localtime_r`，结果在 `result` 中。

结果。如果失败，函数返回 NULL 指针。

## 示例 9.6

以下代码段使用线程安全的 `localtime_r` 函数打印自年初以来经过的天数。

```c
struct tm buffer;
if (localtime_r(NULL, &buffer) != NULL)
    printf("%d days have elapsed since Jan 1\n", buffer.tm_ymday);
```

## 9.1.3 使用 struct timeval 表示时间

秒级刻度对于计时程序或控制游戏事件来说太粗糙了。POSIX.1X1 使用 `struct timeval` 结构在更精细的尺度上表示时间。`struct timeval` 结构包含以下成员。

```c
time_t tv_sec;    /* 自 Epoch 以来的秒数 */
time_t tv_usec;    /* 秒和微秒 */
```

某些支持超时的函数（例如 `select`）使用 `timeval` 类型变量设置超时值。在这种情况下，结构存储了以秒和微秒计算的间隔长度。

`gettimeofday` 获取自 Epoch 以来的秒和微秒级系统时间。`tp` 指向的 `struct timeval` 结构接收获取的时间。`tzp` 指针必须为 NULL，出于历史原因将其包含内。

> 概要
> `#include <sys/time.h>`
> `int gettimeofday(struct timeval *restrict tp, void *restrict tzp);`
> POSIX.1X1

`gettimeofday` 返回 0。没有预留值来表示错误。然而，许多系统实现的 `gettimeofday` 使得其在失败时返回 -1 并设置 `errno`。我们的程序会进行检查以确保 `gettimeofday` 返回 0。

程序 9.1 显示了如何使用 `gettimeofday` 通过函数 `function_to_time` 来测量运行时间。`gettimeofdaytiming` 程序读取调用 `function_to_time` 前后的时间，并以微秒数的形式打印时间差。

## 练习 9.7

使用程序 9.1 的方法可以计时的最大持续时间是多少？该如何扩展它？

答案：

如果 `long` 是 32 位，则最大持续时间为 $2^{31} – 1$ 微秒，约 35 分钟。你可以通过对 `timedif` 使用 `long long`（通常为 64 位）来扩展它。必须对 `timedif` 的声明、`MILLION` (1000000LL) 的定义以及格式说明符 `lld` 进行修改。

## 程序 9.1 gettimeofdaytiming.c

一个使用 `gettimeofday` 测量函数时间的程序。

```c
#include <stdio.h>
#include <sys/time.h>
#define MILLION 1000000L
void function_to_time(void);
int main(void) {
    long timedif;
    struct timeval tpend;
    struct timeval tpstart;
    if (gettimeofday(&tpstart, NULL)) {
        fprintf(stderr, "Failed to get start time\n");
        return 1;
    }
    function_to_time();
    if (gettimeofday(&tpend, NULL)) {
        fprintf(stderr, "Failed to get end time\n");
        return 1;
    }
    timedif = MILLION*(tpend.tv_sec - tpstart.tv_sec) + tpend.tv_usec - tpstart.tv_usec;
    printf("The function took %ld microseconds\n", timedif);
    return 0;
}
```

程序 9.2 中的 `gettimeofdaytest` 程序在循环中测试 `gettimeofday` 直到产生 20 个差异。程序 9.2 显示了差异、平均差异值以及调用 `gettimeofday` 的次数。在大多数系统上，分辨率不大于几微秒。如果调用 `gettimeofday` 的次数不超过 21 次，那么限制分辨率的因素因素是执行 `gettimeofday` 所需的时间。在大多数系统中，连续调用 `gettimeofday` 将返回相同的值。显示的值中有一个将远大于其他值。如果是在执行计时循环期间发生了上下文切换，就会发生这种情况。

## 9.1.4 使用实时时钟

时钟是一个以固定间隔增加的计数器，该间隔称为时钟分辨率。POSIX TMR 定时器扩展计算由 `clockid_t` 类型变量表示的时钟。POSIX 时钟可以是系统范围内的，也可以仅在进程内可见。所有实现必须支持一个 `clockid_t` 值为 `CLOCK_REALTIME` 的对应系统实时时间的系统时钟。特权用户可以使用此时钟，但任何用户都可以读取它。

## 程序 9.2 gettimeofday.c

一个测试 `gettimeofday` 分辨率的程序。

```c
#include <stdio.h>
#include <sys/time.h>
#define MILLION 1000000L
#define NUMDIFF 20
int main(void) {
    int i;
    int numcalls = 1;
    int numdone = 0;
    long sum = 0;
    long timid[NUMDIFF];
    struct timeval tlast;
    struct timeval this;
    if (gettimeofday(&tlast, NULL)) {
        fprintf(stderr, "Failed to get gettimeofday.\n");
        return 1;
    }
    while (numdone < NUMDIFF) {
        numcalls++;
        // ... (剩余的逻辑)
    }
}
```

```c
printf("Found %d differences in CLOCK_REALTIME:\n", NUMDIF);
printf("%d calls to CLOCK_REALTIME were required\n", numcalls);
for (i = 0; i < NUMDIF; i++) {
    printf("%02d: %01d nanoseconds\n", i, timedif[i]);
    sum += timedif[i];
}
```

## 9.1.5 对比经过时间与处理器时间

`time` 函数测量的是真实时间，有时也称为经过时间或挂钟时间（wall-clock time）。在许多进程共享 CPU 的多程序环境中，真实时间不是执行时间的准确衡量标准。进程的虚拟时间是该进程在运行状态下花费的时间。执行时间通常用虚拟时间而非挂钟时间来表示。

`times` 函数向其缓冲区参数指向的 `struct tms` 结构体中填充时间计数信息。

### 概要

```c
#include <sys/times.h>
clock_t times(struct tms *buffer);
```

### POSIX

如果成功，`times` 返回自过去某个任意点（如进程或启动时间）以来经过的真实时间，单位为时钟刻。返回值可能会超出其可能范围。如果 `times` 失败，它返回 (`clock_t)-1` 并设置 `errno`。

`struct tms` 结构体至少设置以下成员：

```c
clock_t tms_utime;    /* 进程的用户 CPU 时间 */
clock_t tms_stime;    /* 代表进程的系统 CPU 时间 */
clock_t tms_cutime;   /* 进程及其已终止进程的用户 CPU 时间 */
clock_t tms_cstime;   /* 进程及其已终止进程的系统 CPU 时间 */
```

程序 9.4 估计了 `function_to_time` 使用的 CPU 总时间以及总 CPU 使用的比例。它以 `double` 类型表示的秒为单位显示时间。计算的分辨率是刻。每秒时钟刻数的典型值为 100。这个数字对于计数是足够的，但对于短事件的性能测量来说，分辨率不够。如果 `function_to_time` 执行仅需几个时钟刻，可以通过在循环中多次调用它，并将结果时间除以循环次数来获得更好的分辨率。

程序 9.4 调用了 `showtimes`（第 53 页的程序 2.10）中引入的 `sysconf` 来确定每秒刻数。计算不包括进程子进程使用的任何 CPU 时间，但它包含了代表进程使用的的用户时间和系统时间。如果在函数执行期间发生了上下文切换，CPU 时间的比例可能是不准确的。

程序 9.5 类似于 `time` shell 命令，它打印执行任意程序所需的时钟刻数和秒数。`timechild` 函数以与第 81 页程序 3.5 相同的方式将其自己的命令行参数传递给 `execv`，并通过从时间中减去进程时间来计算子进程的时间。由于进程只有一个子进程，这就是子进程的时间。

## 程序 9.4 cpufraction.c

一个计算 `function_to_time` 以秒为单位的 CPU 时间及其占总量比例的程序。

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/times.h>
void function_to_time(void);
int main(void) {
    double clockticks, cticks;
    clock_t tend, tstart;
    struct tms tmend, tmstart;
    if ((clockticks = (double)sysconf(_SC_CLK_TCK)) == -1) {
        perror("Failed to determine clock ticks per second");
        return 1;
    }
    printf("The number of ticks per second is %f\n", clockticks);
    if (clockticks == 0) {
        fprintf(stderr, "The number of ticks per second is invalid\n");
        return 1;
    }
    if ((tstart = times(&tmstart)) == -1) {
```
