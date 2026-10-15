
- `SVID 3`, `POSIX`, `BSD 4.3`, `ISO 9899`

## 相关参考

- `errno(3)`, `perror(3)`, `strsignal(3)`

`GNU`, 1993年4月13日

# `strfry`

`strfry`—随机化字符串

## 概要

```
#include <string.h>
char *strfry(char *s);
```

## 描述

`strfry()` 随机化字符串。

## 返回值

`strfry()` 返回随机化字符串的指针。

## 符合标准

`strfry()` 是 Linux 特有的。

## 相关参考

- `strftime(3)`

`GNU`, 1993年4月12日

随机化字符串

# `strftime`

`strftime`—格式化日期和时间

## 概要

```
#include <time.h>
size_t strftime(char *s, size_t max, const char *format, const struct tm *tm);
```

## 描述

`strftime()` 根据程序当前区域设置中类别 `LC_COLLATE` 适当解释的字符串格式化拆分时间 `tm`。生成的 `s` 中的格式说明符如下：

- `%a` 简区域的星期名称
- `%A` 完整的星期名称
- `%b` 简写的月份名称
- `%B` 完整的月份名称
- `%c` 区域设置的日期时间格式
- `%d` 日期（范围 1 到 31）
- `%H` 24 小制小时（范围 0 到 23）
- `%I` 12 小制小时（范围 1 到 12）
- `%j` 天（范围 1 到 31）
- `%m` 月份（范围 1 到 12）
- `%p` AM 或 PM
- `%S` 秒（范围 0 到 59）
- `%U` 周，从星期日为第一天的周
- `%W` 周，从周一为第一天的周
- `%w` 星期几，星期日为 0
- `%x` 区域设置的日期格式
- `%Y` 包含世纪的数字年份（范围 0 到 99）
- `%Z` 区域设置的时区名称
- `%*` 字面字符

拆分时间结构体 `tm` 在 `<time.h>` 中定义如下：

```
struct tm {
    int tm_sec; /* 秒 */
    int tm_min; /* 分钟 */
    int tm_hour; /* 小时 */
    int tm_mday; /* 日期 */
    int tm_mon; /* 月份 */
    int tm_year; /* 年 */
    int tm_wday; /* 星期 */
    int tm_yday; /* 年中的天 */
    int tm_isdst; /* 夏令时 */
};
```

## `tm` 结构的成员

- `tm_sec` 分钟后的秒数，通常范围 0 到 59，但可以达到 61 以允许闰秒。
- `tm_min` 小时后的分钟，范围 0 到 59。
- `tm_hour` 午夜后的小时数，范围 0 到 23。
- `tm_mday` 月中的几，范围 1 到 31。
- `tm_mon` 自 1 月起的月份数，范围 0 到 11。
- `tm_year` 自 1900 年起的年份，范围 0 到 99。
- `tm_wday` 星期几，范围 0 到 6。
- `tm_yday` 自 1 月 1 日起的天数，范围 0 到 365。
- `tm_isdst` 一个标志，指示描述处启用夏令时。如果夏令时生效则为正，不生效为零，信息不可用为负。

## 返回值

`strftime()` 函数返回放入数组的字符数，不包括终止的 `NULL` 字符。如果值等于 `max`，则意味着数组太小。

## 符合标准

- `SVID 3`, `POSIX`, `BSD 4.3`, `ISO 9899`

## 相关参考

- `date(1)`, `time(2)`, `ctime(3)`, `setlocale(3)`, `sprintf(3)`

## 注意事项

该函数仅支持 `locale(7)` 中指定的区域设置

> `GNU`. 1993年7月2日

```c
char free(char *string);
size_t strlen(const char *s);
char strcat(char *dest, char *src, size_t n);
int strncmp(const char *s1, const char *s2, size_t n);
char strncpy(char *dest, char *src, size_t n);
int strcsp(const char *s, char *s2);
char *strbrk(const char *s, char *accept);
char *strchr(const char *s, int c);
int strcspn(const char *s, char *delim);
size_t strspn(const char *s, char *accept);
char *strstr(const char *haystack, const char *needle);
char *strtok(char *s, char *delim);
size_t strnlen(const char *s, int c);
char *rindex(const char *s, int c);
```

## 描述

字符串函数对以 `NULL` 终止的字符串进行操作。每个函数的描述请参见相应的 man 页面。

# 另请

`index(3)`, `rindex(3)`, `strcasecmp(3)`, `strctr(3)`, `strncmp(3)`, `strcoll(3)`, `strncpy(3)`, `strcspn(3)`, `strdup(3)`, `strftime(3)`, `strlen(3)`, `strcat(3)`, `strncmp(3)`, `strcasecmp(3)`, `strbrk(3)`, `strrchr(3)`, `strsep(3)`, `strspn(3)`, `strstr(3)`, `strtok(3)`, `strxfm(3)`。

1993年4月9日

# `strlen`

`strlen`—计算字符串的长度

## 概要

```c
#include <string.h>
size_t strlen(const char *s);
```

## 描述

`strlen()` 计算字符串 `s` 的长度，不包括空字符。

## 返回值

`strlen()` 返回 `s` 中字符的个数。

## 符合标准

`SVID 3`, `POSIX`, `BSD 4.3`, `ISO 1989`

## 另请

`strlen(3)`

1993年4月12日

# `strpbrk`

`strpbrk`—在字符串中搜索一组字符中的任意字符

# 第三部分：库函数

## 概要

```c
#include <string.h>
char *strbrk(const char *s, char *accept);
```

## 描述

`strbrk()` 函数定位 `s` 中首次出现的字符串字符串中的任意一个字符。

## 返回值

`strbrk()` 返回指向 `s` 中匹配 `accept` 中任意一个字符的指针。

## 符合标准

`SVID 3`, `POSIX`, `BSD 4.3`, `ISO 9899`

## 另请

`index(3)`, `memchr(3)`, `rindex(3)`, `strchr(3)`, `strsep(3)`, `strspn(3)`, `strstrn(3)`, `strtok(3)`

1998年4月12日

# `strftime`

`strftime`—将时间表示形式的字符串转换为 `tm` 结构体

## 概要

```c
#include <time.h>
char *strftime(char *buf, size_t max, const char *format, const struct tm *tm);
```

## 描述

`strftime()` 是 `strftime()` 的互补函数（注：此处原文可能有误，应为 `localtime` 的互补函数），并返回 `buf` 指向的字符字符串，该字符串使用 `format` 指定的格式存储在 `tm` 指向的结构体中的时间值。`format` 是一个由字段描述符和文本组成的字符字符串，类似于 `strftime(3)`。

* `%A` 星期几，使用区域（`locale`）的星期名称；可以指定缩写或全称。
* `%b`, `%B`, `%h` 月份，使用区域的月份名称；可以指定缩写或全称。
* `%x`, `%X` 日期和时间。
* `%C` 使用区域的长格式日期时间表示的日期和时间。
* `%d`, `%e` 月份中的一天（1–31；允许前导零，但不是强制）。
* `%H`, `%k` 小时（0–23；允许前导零，但不是强制）。
* `%I`, `%l` 小时（1–12；允许前导零，但不是强制）。
* `%j` 一年中的某一天（001–366）。
* `%m` 月份数字（1–12；允许前导零，但不是强制）。
* `%M` 分钟（0–59；允许前导零，但不是强制）。
* `%p` 区域中 `%a` 或 `%A` 的等价。
* `%r` 格式为 `%I:%M:%S` 的时间。
