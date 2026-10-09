

- 如果时区不应应用夏令时，则 `daylight` 被设置为零（false）；如果应该应用，则设置为非零（true）。切换周期是以实现定义的方式内置于库函数中的。
- `timezone` 被设置为 UTC 与当地标准时间之间以秒为单位的差值。（将其除以 3,600 即可得到以小时为单位的差值。）
- `tzname` 是一个包含两个字符串的数组，`tzname[0]` 用于指定标准时间下的本地时区，而 `tzname[1]` 用于指定夏令时。

这三个全局变量在 POSIX 2002 之前并不包含在 POSIX 中，并且在 FreeBSD 或 Darwin 上未定义。但通常你不需要直接调用 `tzset` 或查询这些全局变量。标准函数会按需执行这些操作。

无论如何，这里有一个示例：

```c
tzset();
printf("daylight = %d; timezone = %ld hrs.; tzname = %s/%s\n",
       daylight, timezone / 3600, tzname[0], tzname[1]);
```

输出如下：

```
daylight = 1; timezone = 7 hrs.; tzname = MST/MCT
```

关于所有日历时间函数用法的细节，特别是涉及格式化字符串的函数，请参见 [SUS2002] 或一本优秀的标准 C 书籍，例如 [Har2002]。以下是一些需要牢记的杂项要点：

- 忽略错误返回的可能性，`ctime(t)` 定义为 `asctime(localtime(t))`。
- `tm` 结构体中的 `tm_sec` 字段可以达到 61（而不仅仅是 59），以容纳偶尔出现的闰秒。
- `tm` 结构体中的 `tm_year` 字段是从 1900 年开始的偏移量。它完全兼容 Y2K 世纪末问题，只是有些奇怪（2002 年表示为 102）。
- 同样奇怪的是，`ctime` 和 `asctime` 在输出字符串的末尾放置了一个换行符。
- 一些函数接受指向 `time_t` 的指针，尽管按值传递的 `time_t` 也能正常工作。这是早期 UNIX 时代的遗留问题，当时 C 语言没有 `long` 数据类型，必须传入一个包含两个 16 位整数的数组。
- `time` 函数的 `time_t` 指针参数完全是不必要的，应该只是 `NULL`。它看起来像是为 `time` 提供一个缓冲区，但并不需要缓冲区，因为返回的 `time_t` 是一个算术类型。
- 这里介绍的所有返回指向 `tm` 结构体指针的函数，在大多数实现中内部都使用静态缓冲区，因此在调用另一个此类函数之前，请使用该缓冲区或复制它。如果需要，可以使用带有 `_r` 后缀的重入形式在多线程程序中。
- 使用 `formats`、`strftime`、`wcsftime`、`getdate` 和 `strptime` 的函数非常复杂，但功能强大，非常值得学习。前两个在标准 C 中；后两个在 SUS 中。`getdate` 在 FreeBSD 或 Darwin 中不存在，虽然可以在 GNU C 库中找到它的版本，如果你需要可以安装。
- 使用 `getdate` 获取用户输入日期和时间，以及在读取包含日期的数据文件时使用 `strptime` 或 `getdate`。原因是 `strptime` 只接受单一格式，这使得用户难以正确格式化日期和时间。`getdate` 使用一个完整的格式列表，并逐一尝试寻找匹配。

### 1.7.2 执行时间

执行时间用于测量时间间隔和进程执行时间，以及用于记账记录。内核会自动记录每个进程的执行时间。时间间隔以各种亚秒级单位表示，范围从纳秒到百分之一秒。

执行时间类型和函数与日历时间函数一样令人困惑。首先，这是主要的类型：

- `clock_t`，在标准 C 中，一个算术类型（通常是 `long`，但不要假设如此），表示以 `CLOCKS_PER_SEC` 或时钟滴答为单位的时间间隔
- `struct timeval`，保存以秒和微秒为单位的间隔（也用于日历时间，并在上一节中详细解释）
- `struct timespec`，保存以秒和纳秒为单位的间隔

这是 `timespec` 的结构体（我们之前已经展示了 `timeval`），它定义在头文件 `<time.h>` 中：

```c
struct timespec {
    time_t tv_sec;      /* 秒 */
    long tv_nsec;       /* 纳秒 */
};
```

有三个主要函数用于测量时间间隔，*gettimeofday*（在上一节中详细讲解）、*clock* 和 *times*。后两个函数以及 *times* 使用的结构体如下：

```c
#include <time.h>
clock_t clock(void);
/* 返回 CLOCKS_PER_SEC 的时间，出错时返回 -1（未定义 errno） */
```

```c
#include <sys/times.h>
clock_t times(
    struct tms *buffer  /* 返回的时间 */
);
/* 返回时钟滴答的时间，出错时返回 -1（设置 errno） */
```

```c
struct tms {
    clock_t tms_utime;      /* 用户时间 */
    clock_t tms_cutime;     /* 已终止子进程的用户时间 */
    clock_t tms_stime;      /* 系统时间 */
    clock_t tms_cstime;     /* 已终止子进程的系统时间 */
};
```

*times* 返回自过去某一点以来经过的时间（通常是自系统启动以来），有时被称为 *wall-clock* 或 *real* 时间。这与上一节中函数返回的时间不同，后者返回的是自纪元时间（通常是 1970 年 1 月 1 日）以来的时间。

*times* 使用时钟滴答作为单位；你可以通过 *sysconf*（第 1.5.5 节）获取每秒的时钟滴答数，如下所示：

```c
clock_ticks = sysconf(_SC_CLK_TCK);
```

此外，*times* 将更具体的信息加载到 *tms* 结构中：

- `tms_utime`（用户时间）是执行进程用户代码指令所花费的时间。这只是 CPU 时间，不包括等待运行的时间。
- `tms_stime`（系统时间）是为进程执行系统调用所花费的 CPU 时间。
- `tms_cutime`（子进程用户时间）是所有已终止子进程的用户 CPU 时间总和，且父进程已针对它们发出 wait 系统调用（在第 5 章中详细解释）。
- `tms_cstime`（子进程系统时间）是已终止并已 wait 的子进程的系统 CPU 时间总和。

尽管 `clock` 返回的类型与 `times` 相同，但它的值是进程启动以来使用的 CPU 时间，而不是实际时间，并且单位由宏 `CLOCKS_PER_SEC` 给定，而不是时钟滴答。除了单位不同外，它等同于 `tms_utime + tms_stime`。

`CLOCKS_PER_SEC` 在 SUS 中定义为 1,000,000（即微秒），但非 SUS 系统可能使用不同的值，因此始终使用宏。（FreeBSD 将 `CLOCKS_PER_SEC` 定义为 128；Darwin 定义为 100。）

如果 `clock_t` 是 32 位有符号整数（通常如此），并使用微秒作为单位，它在大约 36 分钟后会溢出，但至少 `clock` 是在进程启动时开始计时的。`times` 以时钟滴答为单位运行，可以运行更长时间，但它开始得更早——如果 UNIX 系统已运行数周或数月，开始得会早得多，这种情况非常常见。不过，以滴答为单位的 32 位有符号 `clock_t` 在大约 250 天内不会溢出，因此，如果可以安排，每年半重启一次可以解决此问题。

然而，你不能假设 `clock_t` 是 32 位有符号整数，或者它是有符号的，甚至不能假设它是整数。它可能是无符号 long，甚至是 double。

我们将在这本书中广泛使用 `times` 来对各个程序进行计时，因为它能一次性提供实际时间、用户 CPU 时间和系统 CPU 时间。下面是我们将使用的两个实用函数——一个用于开始计时，一个用于停止并打印结果：

```c
#include <sys/times.h>

static struct tms tbuf1;
static clock_t real1;
static long clock_ticks;

void timestart(void)
{
    ec_negl( real1 = times(&tbuf1) )
    /* 将所有 -1 返回值视为错误 */
    ec_negl( clock_ticks = sysconf(_SC_CLK_TCK) )
    return;

EC_CLEANUP_BGN
    EC_FLUSH("timestart");
EC_CLEANUP_END
}

void timestep(char *msg)
{
    struct tms tbuf2;
    clock_t real2;

    ec_negl( real2 = times(&tbuf2) )
    fprintf (stderr,"%s:\n\tTotal (user/sys/real)=%2.2f, %2.2f, %2.2f\n"
             "\t  Child (user/sys)=%2.2f, %2.2f\n", msg,
             ((double)(tbuf2.tms_utime + tbuf2.tms_cutime) -
               (tbuf1.tms_utime + tbuf1.tms_cutime)) / clock_ticks,
             ((double)(tbuf2.tms_stime + tbuf2.tms_cstime) -
               (tbuf1.tms_stime + tbuf1.tms_cstime)) / clock_ticks,
             (double)(real2 - real1) / clock_ticks,
             (double)(tbuf2.tms_cutime - tbuf1.tms_cutime) / clock_ticks,
             (double)(tbuf2.tms_cstime - tbuf1.tms_cstime) / clock_ticks);
    return;

EC_CLEANUP_BGN
    EC_FLUSH("timestep");
EC_CLEANUP_END
}
```

当我们想要对某事物进行计时时，只需在间隔开始时调用 `timestart`，在结束时调用 `timestep`，如下例所示，该示例还包含对 `gettimeofday` 和 `clock` 的调用以供比较：

```c
#define REPS 1000000
#define TV_SUBTRACT(t2, t1) \
    ((double)(t2).tv_sec + (t2).tv_usec / 1000000.0 - \
     ((double)(t1).tv_sec + (t1).tv_usec / 1000000.0)

int main(void)
{
    int i;
    char msg[100];
    clock_t c1, c2;
    struct timeval tv1, tv2;
```

