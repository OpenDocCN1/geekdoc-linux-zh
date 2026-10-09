
## 时间转换函数

UTC.[^20] 这是将时间存储在文件中以及在函数之间传递时间的好方法，因为它紧凑且不依赖时区。

- 一种结构体类型 `timeval`，它保存秒和微秒的时间。（同时用于日历时间和执行时间。）
- 一种结构体类型 `struct tm`，它将时间分解为年、月、日、小时、分钟、秒以及几件其他事情。
- 一个字符串，例如 `Tue Jul 23 09:44:17 2002`。

有一整套库函数，其中大部分来自标准 C，用于在三种形式之间进行转换。这些函数的名称是一个毫无意义的疯狂集合（没有像 `cvt_tm_to_time` 这样简单的名字）；图 1.1 提供了一个地图，展示了九个转换函数的功能。第十个函数 `time` 用于获取当前时间。

以下是 `tm` 和 `timeval` 结构体[^21]，随后是主要日历时间函数的概要：[^22]

[^20]: 协调世界时 (Universal Coordinated Time)。以前被称为 GMT，即格林尼治标准时间 (Greenwich Mean Time)。
[^21]: 有一个过时的结构体 `timeb`，它保存秒和毫秒的时间，以及一个过时的函数 `ftime`，用于填充它。请使用 `gettimeofday` 代替。
[^22]: 一些标准 C 函数也有可重入形式（例如 `ctime_r`），不使用静态缓冲区，但这些不在本书中涵盖。

### struct tm—分解时间的结构体

```c
struct tm {
	int tm_sec;	/* second [0,61] (up to 2 leap seconds) */
	int tm_min;	/* minute [0,59] */
	int tm_hour;	/* hour [0,23] */
	int tm_mday;	/* day of month [1,31] */
	int tm_mon;	/* month [0,11] */
	int tm_year;	/* years since 1900 */
	int tm_wday;	/* day of week [0,6] (0 = Sunday) */
	int tm_yday;	/* day of year [0,365] */
	int tm_isdst;	/* daylight-savings flag */
};
```

### struct timeval—用于 gettimeofday 的结构体

```c
struct timeval {
	time_t tv_sec;	/* seconds */
	useconds_t tv_usec;	/* microseconds */
};
```

### time—作为 time_t 获取当前日期和时间

```c
#include <time.h>

time_t time(
	time_t *t		/* NULL or returned time */
);
/* Returns time or -1 on error (errno not defined) */
```

### gettimeofday—作为 timeval 获取当前日期和时间

```c
#include <sys/time.h>

int gettimeofday(
	struct timeval *tvalbuf,	/* returned time */
	void *dummy		/* always NULL */
);
/* Returns 0 on success or -1 (maybe) on error (may set errno) */
```

### localtime—将 time_t 转换为本地分解时间

```c
#include <time.h>

struct tm *localtime(
	const time_t *t		/* time */
);
/* Returns broken-down time or NULL on error (sets errno) */
```

### gmtime—将 time_t 转换为 UTC 分解时间

```c
#include <time.h>

struct tm *gmtime(
	const time_t *t		/* time */
);
/* Returns broken-down time or NULL on error (sets errno) */
```

### mktime—将本地分解时间转换为 time_t

```c
#include <time.h>

time_t mktime(
    struct tm *tmbuf              /* broken-down time */
);
/* Returns time or -1 on error (errno not defined) */
```

### ctime—将 time_t 转换为本地时间字符串

```c
#include <time.h>

char *ctime(
    const time_t *t               /* time */
);
/* Returns string or NULL on error (errno not defined) */
```

### asctime—将分解时间转换为本地时间字符串 [^23]

```c
#include <time.h>

char *asctime(
    const struct tm *tmbuf        /* broken-down time */
);
/* Returns string or NULL on error (errno not defined) */
```

### strftime—将分解时间转换为带有格式的字符串

```c
#include <time.h>

size_t strftime(
    char *buf,                    /* output buffer */
    size_t bufsiz,               /* size of buffer */
    const char *format,          /* format */
    const struct tm *tmbuf       /* broken-down time */
);
/* Returns byte count or 0 on error (errno not defined) */
```

### wcsftime—将分解时间转换为带有格式的双字符字符串

```c
#include <wchar.h>

size_t wcsftime(
    wchar_t *buf,                /* output buffer */
    size_t bufsiz,               /* size of buffer */
    const wchar_t *format,       /* format */
    const struct tm *tmbuf       /* broken-down time */
);
/* Returns wchar_t count or 0 on error (errno not defined) */
```

[^23]: SUS 并未说明 `asctime` 在出错时返回 NULL，但无论如何检查都是个好主意。

### getdate—根据规则将字符串转换为分解时间

```c
#include <time.h>
struct tm *getdate(
    const char *s        /* string to convert */
);
/* Returns broken-down time or NULL on error (sets getdate_err) */
```

### strptime—根据格式将字符串转换为分解时间

```c
#include <time.h>
char *strptime(
    const char *s,                /* string to convert */
    const char *format,           /* format */
    struct tm *tmbuf             /* broken-down time (output) */
);
/* Returns pointer to first unparsed char or NULL on error (errno not
   defined) */
```

根据标准，这些函数都不设置 **errno**，其中大多数甚至不返回错误指示，但无论如何将返回的指针与 **NULL** 进行测试都是一个好主意。**getdate** 真的很奇怪：在出错时，它将变量或宏 **getdate_err**（在其他地方没有使用）设置为 1 到 8 之间的一个数字，以指示问题的性质；详见 [SUS2002]。

大多数 UNIX 系统将 **time_t** 实现为 *long* 整数，通常只有 32 位（有符号）；这足以让我们计数到 19–Jan-2038[^24] 的秒数。在某个时候，需要更多的位，它将被更改为保证 64 位的东西[^25]。为了准备，始终使用 **time_t**（而不是，比如说，*long*），并且不要对它是做什么的做出任何假设。**time_t** 对于历史时间来说已经不够用了，因为在许多系统中，它（通过负数）只能回溯到 1901 年。

在不假设 **time_t** 是什么的情况下，减去两个 **time_t** 是困难的，这是一个常见需求，因此有一个专门的函数：

### difftime—减去两个 time_t 值

```c
#include <time.h>
double difftime(
    time_t time1,               /* time */
    time_t time0                /* time */
);
/* Returns time1 – time0 in seconds (no error return) */
```

[^24]: 如果我们坚持激进的 19 年修订周期，这应该是本书第四版出现的时候。
[^25]: 显然这是过度kill，但在计算机中，32 之后的数字通常是 64。

`gettimeofday` 是 `time` 的高分辨率替代方案，但其他函数都不接受 `struct timeval` 作为参数。然而，它们将单独接受 `tv_sec` 字段，因为它是 `time_t`，你可以单独处理微秒。关于类型 `tv_usec` 唯一可以安全假设的是它是一个某种大小的有符号整数。但是，没有理由它比 32 位更宽，因为一秒只有 1,000,000 微秒，所以将 `tv_usec` 字段强制转换为 `long` 可以正常工作。你可以通过用两次 `gettimeofday` 调用来括住执行间隔，然后对 `tv_sec` 字段使用 `difftime`，对 `tv_usec` 字段使用裸减法，来计时执行间隔。

一些实现（FreeBSD、Darwin 和 Linux，但不是 Solaris）使用 `gettimeofday` 的第二个参数返回时区信息，但这是非标准的。大多数实现通过返回 -1 来指示错误，甚至设置 `errno`。那些没有这样做的总是返回零，因此你可以在所有情况下安全地检查错误返回值。

`time_t` 始终以 UTC 为基准，但分解时间（`struct tm`）和字符串可以是 UTC 或本地时间。当时间被输入或打印时，使用本地时间很方便，这使事情变得复杂。必须有一种方式让计算机知道用户所在的时区，以及当前是标准时间还是夏令时。更糟糕的是，在打印过去的时间时，计算机必须知道*那时*是标准时间还是夏令时。涉及本地时间的各个函数相当好地解决了这个问题。

用户的时区记录在环境变量 `TZ` 中，或者如果未设置 `TZ`，则作为系统默认值。为了提供可移植性，有一个函数和三个全局变量来处理时区和夏令时设置：

![Figure showing timezone related functions](img/41b4c8f6d6a5c349eee321a301703d97_75_0.png)

应用程序可以调用 `tzset` 来以某种方式获取时区（来自 `TZ` 或其他地方）并设置这三个全局变量，如下所示：
