
```c
1: // gettime.cc
2:
3: #Include "dtime.h"
4:
5: //////////////////////////////////////////////////////////////////
6: // 构造函数:
7: //////////////////////////////////////////////////////////////////
8:
9: DTime::DTime() {
10:     dt = (time_t) (-1);      // 无时间
11: }
12:
13: //////////////////////////////////////////////////////////////////
14: // 给 this->dt 的当前时间加秒
15: //////////////////////////////////////////////////////////////////
16: DTime &
17: DTime::operator+=(long secs) {
18:     dt += (time_t) secs;
19:     return *this;
20: }
21:
22: //////////////////////////////////////////////////////////////////
23: // 从 this->dt 的当前时间减去秒
24: //////////////////////////////////////////////////////////////////
25: DTime &
26: DTime::operator-=(long secs) {
27:     dt -= (time_t) secs;
28:     return *this;
29: }
30:
31: //////////////////////////////////////////////////////////////////
32: // 返回当前时间
33: //////////////////////////////////////////////////////////////////
34: time_t
35: DTime::getTime() {
36:     return ::time(&dt);
37: }
38:
39: //////////////////////////////////////////////////////////////////
40: // 允许调用者接入 time_t 值
41: //////////////////////////////////////////////////////////////////
42: time_t
43: DTime::putTime(time_t dt) {
44:     this->dt = dt;
45: }
50: // End getty.cc
```

构造函数初始化返回的值表示未设置时间。

运算符 `+=` 和 `-=` 为此类进行了重载，允许用户从对象增加或减少时间（第 17-31 行）。这将在后文中演示。

成员 `getTime()` 使用 `time(3)` 获取当前时间到成员 `dt`（第 37-40 行）。返回相同的值。

提供 `putTime()` 方法是为了让用户提供指定的 `time_t` 值（第 46-49）。

## 使用 ctime(3) 将时间转换为字符串

这可能是最简单的日期时间函数。该函数接收 `time_t` 作为输入并将其转换为可以显示的 ASCII 字符串。`ctime(3)` 的原型如下：

```c
#include <time.h>
char * ctime(const time_t *timep);
```

`ctime(3)` 需要指向要转换的日期变量。以下示例显示了如何获取当前系统日期并传递给 `ctime(3)`。然后显示返回的字符串：

```c
time_t td;               /* 时间和日期 */
time(&td);                /* 获取当前日期 */
printf("Today is %s", ctime(&td));
```

`ctime(3)` 返回的 26 字节字符串是格式如下的日期时间字符串：

```
Mon Jan 18 22:14:07 2038
```

该函数返回一个指向内部静态缓冲区的指针，该返回的日期字符串的一个问题是结尾有一个换行符。

## ctime_r (3) 函数

`ctime(3)` 函数返回其内部静态缓冲区。这使得它对于线程程序是不安全的。该程序的线程安全版本作为 `ctime_r(3)` 提供：

```c
#include <time.h>
char *ctime_r(const time_t *clock, char *buf);
```

为参数 `buf` 提供的缓冲区至少要有 26 个字符长度。返回的指针是存储在 `buf` 中的指针。

`DTime::ctime()` 方法如列表 11.3。

### 列表 11.3 ctime.cc—DTime::ctime() 方法的实现

```c
1:    // ctime.cc
2:
3:    #include "time.h"
4:    ////////////////////////////////////////////////////////////////
5:    //存储在 this->dt 中的当前 time_t
6:    // 值返回 ctime(3) 字符串。此程序假设
7:    // 已经调用过 this->getTime()：
8:    ///////////////////////////////////////////////////
9:
10:    char *
11:    DTime::ctime() {
12:        char *cp;
13:
14:        ctime_r(&dt,buf);      // 将 ctime(3) 字符串放入 buf[]
15:        if ((cp = strchr(buf,'\n')) != NULL) {
16:            *cp = 0;               // 消除讨厌的换行符
17:            return buf;           // 返回缓冲区的指针
18:        }
19:    }
20:
21:    // End ctime.cc
```

`DTime::ctime()` 调用函数 `ctime_r(3)`。函数 `ctime_r(3)` 获取成员 `dt` 中的时间并转换为私有缓冲区 `buf[]`（第 15 行）中的 ASCII 形式。讨厌的换行符在第 15 和 16 行消除。第 18 行返回私有缓冲区的指针。

## localtime(3) 和 gmtime(3) 函数

程序员需要直接访问日期和时间组件。`time_t` 数据类型对于数学运算可能方便，但对于所有形式的日期运算并不方便。要从 `time_t` 值中提取日期组件，可以使用 `localtime()` 或 `gmtime()` 函数：

```c
#include <time.h>

struct tm *localtime(const time_t *timep);

struct tm *gmtime(const time_t *timep);

struct tm *localtime_r(const time_t *clock, struct tm *result);

struct tm *gmtime_r(const time_t *clock, struct tm *result);
```

`localtime(3)` 函数根据本地时间返回时间和日期分量。要根据 UTC 时区获取时间组件，请使用 `gmtime(3)` 函数。这些函数都接受一个指向要转换的 `time_t` 值的指针。这些函数的返回值仅在下一次调用之前有效。

函数 `localtime_r(3)` 和 `gmtime_r(3)` 分别是旧版 `localtime(3)` 和 `gmtime(3)` 函数的线程安全版本。它们多了一个额外的指针参数 `result`，结果将写入其中。这与旧版 `localtime(3)` 和 `gmtime(3)` 函数将结果返回在内部静态缓冲区的方式不同。

返回的结果是一个指向 `struct tm` 的指针，它可以访问日期和时间分量，例如几号和年份。下面的示例使用 `time(3)` 获取当前日期并调用 `localtime(3)`。在此示例中，返回的结果被复制到结构体变量 `dc` 中：

```c
time_t dt;                   /* Current date */
struct tm dc;             /* Date components */
time(&dt);                /* Get current date */
dc = *localtime(&dt);     /* convert dt -> dc */
```

将结果放入 `dc` 结构体的更好方法是使用 `localtime(3)` 的可重入对应版本：

```c
time_t dt;                   /* Current date */
struct tm dc;             /* Date components */
time(&dt);                /* Get current date */
localtime_r(&dt, &dc);   /* convert dt -> dc */
```

通过这种方式，结果直接存放在 `dc` 中，而不是从一个结构体复制到另一个。

列表 11.4 显示了使用 `localtime_r(3)` 和 `gmtime_r(3)` 实现的 `DTime::localtime()` 和 `DTime::gmtime()` 方法。

### 列表 11.4 localtime.cc--DTime::localtime() 和 DTime::gmtime() 的实现

```c
1: // localtime.cc
2:
3: #include "time.h"
4:
5: // Return the local time components, based upon the
6: // current value of this->dt; assumes that a prior
7: // call to getTime() has been made:
8: ////////////////////////////////////////////////////////
9: ////////////////////////////////////////////////////////
10:
11: struct tm *
12: DTime::localtime() {
13: ::localtime_r(&dt,this);
14:     return this;
15: }
16: 
17: /////////////////////////////////////////////////////////////////////
18: // Return the UTC (GMT) time components, based upon the
19: // current value of this->dt; assumes that a prior
20: // call to gettime() has been made:
21: /////////////////////////////////////////////////////////////////////
22: 
23:     struct tm *
24: DTime::gmtime() {
25:     ::gmtime_r(&dt,this);
26:     return this;
27: }
28: 
29: // End method localtime.cc
```

在这两个方法中，`DTime` 类被用第二个参数，因为它继承自 `struct tm`。返回的是该类的指针。

## struct tm 的成员

这是多个日期/时间函数使用的结构体，包括 `localtime(3)`、`gmtime(3)` 和 `mktime(3)`。该结构体的定义如下：

```c
struct tm {
    int tm_sec;      /* seconds */
    int tm_min;      /* minutes */
    int tm_hour;     /* hours (0-23) */
    int tm_mday;     /* day of the month (1-31) */
    int tm_mon;      /* month (0-11) */
    int tm_year;     /* year 2000=100 * */
    int tm_wday;     /* day of the week (0-6) */
    int tm_yday;     /* day in the year (0-365) */
    int tm_isdst;   /* daylight saving time */
};
```

此 C 定义在 `<time.h>` 文件中。该结构的各个成员记录见表 11.1。

## 警告

注意成员 `tm_mon` 从零开始。要产生 1–12 的月份数字，你必须在该值上加 1。

同样注意，你必须在成员 `tm_year` 上加上 1900 才能世纪。

## 备注

成员 `tm_isdst` 有三种可能的状态：

- 当它为正数时，夏令时生效。
- 当它为零时，夏令时未生效。
- 当它为负数时，夏令时信息未知或不可。

| 成员 | 描述 |
| --- | --- |
| `tm_sec` | 分钟后的秒数。通常范围是 0 到 59，但此值可以高到 61 以允许闰秒。 |
| `tm_min` | 每小时后的分钟数；范围从 0 到 59。 |
| `tm_hour` | 午夜后的小时，从 0 到 23。 |
| `tm_mday` | 月份中的几号，从 1 到 31。 |
| `tm_mon` | 年中的月份，从 0 到 11。 |
| `tm_year` | 年份 2000=100 * |
| `tm_wday` | 星期 (0-6) |
| `tm_yday` | 一年中的天数 (0-365) |
| `tm_isdst` | 夏令时 |

不要依赖 `daylight` 变量精确等于 1 或 0。文档仅说明，当启用夏令时时，该值将为非零。

## 在 BSD 下确定时区

如果你发现没有对外部变量 `timezone` 和 `daylight` 的支持，可以通过更繁琐的过程确定时区：

```c
struct tm tmvals;
/* 日期/时间组件 */
time_t td;
/* 当前时间/日期 */
int x;
/* tmvals.is_dst */

time(&td);
localtime_r(&td, &tmvals);
/* 获取当前时间 */
x = tmvals.is_dst < 0 ? 0 : tmvals.is_dst; /* 如果未知则假设为 DST */
printf("Zone is %s\n", tzname[x ? 1 : 0]); /* 打印时区 */
```

必须注意的是，示例中对 `x` 的赋值是因为 `tmvals.tm_dst` 中的值是一个三状态标志位。它可以为负数，表示时区未知。在示例中，代码假设没有启用夏令时。

## 使用 mtime(3) 函数创建 Epoch 时间值

如果你想在特定日期构造一个 `time_t` 值，你需要 `mtime(3)` 函数。其原型如下：

```c
#include <time.h>
time_t mtime(struct tm *tm_ptr);
```

`mtime(3)` 函数返回一个指向 `struct tm` 的指针。该输入/输出结构包含日期和时间组件，用于计算并返回一个 `time_t` 值。该结构中还会返回一些值。

## 测试 mtime(3) 错误

如果 `struct tm` 中的值导致无法计算日期，则返回该值（`time_t (-1)`）。这通常发生在 `tm_year` 被设为 1970 年之前的年份，或者提供了不存在的日期（例如 2 月 30 日或 6 月 35 日）。

## 为 mtime(3) 设置 struct tm 的输入成员

当传递给 `mtime(3)` 函数时，并非所有的 `tm` 成员都用于输入。以下成员是输入强制性的，且不会被 `mtime(3)` 修改：

- `tm_sec` (秒：0 到 61)
- `tm_min` (分钟：0 到 59)
- `tm_hour` (小时：0 到 23)
- `tm_mday` (每月第几号：1 到 31)
- `tm_mon` (月份：0 到 11)
- `tm_year` (年份：2000 年对应值为 100)
- `tm_isdst`（夏令时为正数，若未启用夏令时为 0）

请确保将 `tm_mon` 为从 0 开始的月份值（0 到 11）。

## 被 mtime(3) 修改的 struct tm 成员

以下成员作为输入会被忽略，但在 `mtime(3)` 函数调用之前会被重新计算并修改：

- `tm_wday` 不作为输入，而会为输出重新计算。
- `tm_yday` 不作为输入，而会为输出重新计算。

这两个值会被重新计算的特性允许你输入一个日期和时间并调用 `mtime(3)`。结构中返回的值将告诉你是星期几以及一年中的第几天。

## 提示

不要忘记在调用 `mtime(3)` 之前设置 `tm_isdst`。此输入值决定了其他成员指定的本地日期和时间是否启用了夏令时。

未能正确设置此值可能会导致计算出的 UTC `time_t` 值因夏令时差而产生错误。

## 警告
