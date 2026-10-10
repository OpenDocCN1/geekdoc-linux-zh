

下面是一个不区分大小写的 `strstr()` 版本的简单实现。该函数首先复制参数字符串，将这些副本转换为大写，然后对这些副本执行标准的 `strstr()` 操作。由于目标字符串在源字符串中的偏移量在副本中保持不变，因此可以相对于原始参数字符串返回该偏移量：

```c
char *stristr(char *s1, char *s2)
{
    char c1[1000];
    char c2[1000];
    char *p;

    strcpy(c1, s1);
    strcpy(c2, s2);

    strupr(c1);
    strupr(c2);

    p = stristr(c1, c2);
    if (p)
        return s1 + (p - c1);
    return NULL;
}
```

该函数扫描字符串 `s1`，寻找由 `s2` 持有的单词。为了函数返回 TRUE，该单词必须是一个完整的单词，而不仅仅是字符模式。它使用了前文描述的 `stristr()` 函数：

```c
int word_in(char *s1, char *s2)
{
    /* return non-zero if s2 occurs as a word in s1 */
    char *p;
    char *q;
    int ok;

    ok = 0;
    q = s1;

    do
    {
        /* Locate character occurrence s2 in s1 */
        p = stristr(q, s2);
        if (p)
        {
            /* Found */
            ok = 1;

            if (p > s1)
            {
                /* Check previous character */
                if (*(p - 1) >= 'A' && *(p - 1) <= 'z')
                    ok = 0;
            }

            /* Move p to end of character set */
            p += strlen(s2);

            if (*p)
            {
                /* Check character following */
                if (*p >= 'A' && *p <= 'z')
                    ok = 0;
            }
            q = p;
        }
    } while (p && !ok);
    return ok;
}
```

更多用于处理文本的实用函数如下：`truncstr()`，用于截断字符串：

```c
void truncstr(char *p, int num)
{
    /* Truncate string by losing last num characters */
    if (num < strlen(p))
        p[strlen(p) - num] = 0;
}
```

`trim()`，用于移除字符串末尾的空格：

```c
void trim(char *text)
{
    /* remove trailing spaces */
    char *p;

    p = &text[strlen(text) - 1];
    while (*p == 32 && p >= text)
        *p-- = 0;
}
```

`strlench()`，通过增加或删除字符来改变字符串的长度：

```c
void strlench(char *p, int num)
{
    /* Change length of string by adding or deleting characters */

    if (num > 0)
        memmove(p + num, p, strlen(p) + 1);
    else
    {
        num = 0 - num;
        memmove(p, p + num, strlen(p) + 1);
    }
}
```

`strins()`，将一个字符串插入到另一个字符串中：

```c
void strins(char *p, char *q)
{
    /* Insert string q into p */
    strlench(p, strlen(q));
    strncpy(p, q, strlen(q));
}
```

以及 `strchg()`，在目标字符串中用另一个子串替换所有出现的子串：

```c
void strchg(char *data, char *s1, char *s2)
{
    /* Replace all occurrences of s1 with s2 */
    char *p;
    char changed;

    do
    {
        changed = 0;
        p = strstr(data, s1);
        if (p)
        {
            /* Delete original string */
            strlench(p, 0 - strlen(s1));

            /* Insert replacement string */
            strins(p, s2);
            changed = 1;
        }
    } while (changed);
}
```

## 时间

C 语言提供了 `time()` 函数，用于读取计算机的系统时钟，并返回自 1970 年 1 月 1 日午夜以来经过的秒数。可以使用函数 `ctime()` 将此值转换为有用的字符串，示例如下：

```c
#include <stdio.h>
#include <time.h>

int main()
{
    /* Structure to hold time, as defined in time.h */
    time_t t;

    /* Get system date and time from computer */
    t = time(NULL);
    printf("Today's date and time: %s\n", ctime(&t));
}
```

由 `ctime()` 返回的字符串由七个字段组成：

- 星期几
- 月份
- 日期
- 小时
- 分钟
- 秒
- 世纪（注：原文如此，通常指年份）

这些字段以换行符和空终止字节结束。由于字段始终占据相同的宽度，因此可以轻松地对该字符串进行切片操作。以下程序定义了一个结构体 `time` 和一个函数 `gettime()`，该函数提取当前时间的小时、分钟和秒，并将它们放入结构体中：

```c
#include <stdio.h>
#include <time.h>

struct time
{
    int ti_min;      /* Minutes */
    int ti_hour;     /* Hours */
    int ti_sec;      /* Seconds */
};

void gettime(struct time *now)
{
    time_t t;
    char temp[26];
    char *ts;

    /* Get system date and time from computer */
    t = time(NULL);

    /* Translate date and time into a string */
    strcpy(temp, ctime(&t));

    /* Copy out just time part of string */
    temp[19] = 0;

    ts = &temp[11];

    /* Scan time string and copy into time structure */
    sscanf(ts, "%2d:%2d:%2d", &now->ti_hour, &now->ti_min, &now->ti_sec);
}

int main()
{
    struct time now;

    gettime(&now);

    printf("\nThe time is %02d:%02d:%02d",
           now.ti_hour, now.ti_min, now.ti_sec);
}
```

ANSI C 标准确实提供了一个函数，可将 `time()` 返回的值转换为结构体，如下面代码片段所示。请注意，结构体 `tm` 定义在 `time.h` 中：

```c
#include <stdio.h>
#include <time.h>

int main()
{
    time_t t;
    struct tm *tb;

    /* Get time into t */
    t = time(NULL);

    /* Convert time value t into structure pointed to by tb */
    tb = localtime(&t);

    printf("\nTime is %02d:%02d:%02d", tb->tm_hour, tb->tm_min, tb->tm_sec);
}

struct tm
{
    int tm_sec;
    int tm_min;
    int tm_hour;
    int tm_mday;
    int tm_mon;
    int tm_year;
    int tm_wday;
    int tm_yday;
    int tm_isdst;
};
```

## 定时器

通常，程序必须从宿主计算机的非易失性 RAM 中确定日期和时间。ANSI C 标准提供了多个时间函数，使程序能够检索当前的日期和时间。首先，`time()` 返回自 1970 年 1 月 1 日午夜以来经过的秒数。其原型为：

```c
time_t time(time_t *timer);
```

在这里，`time()` 填充作为参数发送的 `time_t` 变量，并返回相同的值。你可以调用 `time()` 并传入 NULL 参数，然后收集返回值，如下所示：

```c
#include <time.h>

void main()
{
    time_t now;

    now = time(NULL);
}
```

在这里，`asctime()` 将时间块转换为格式为 26 个字符的字符串。`asctime()` 函数的原型为：

```c
char *asctime(const struct tm *tblock);
```

接下来，`ctime()` 将时间值（由 `time()` 返回）转换为与 `asctime()` 格式相同的 26 个字符的字符串。例如：

```c
#include <stdio.h>
#include <time.h>

void main()
{
    time_t now;
    char date[30];

    now = time(NULL);
    strcpy(date, ctime(&now));
}
```

另一个时间函数 `difftime()` 返回两个值（由 `time()` 返回）之间以秒为单位的差值。这在测试两个事件之间经过的时间、计算函数执行所需的时间，以及创建与宿主计算机无关的一致延迟时很有用。一个延迟程序的示例如下：

```c
#include <stdio.h>
#include <time.h>

void DELAY(int period)
{
    time_t start;

    start = time(NULL);
    while (time(NULL) < start + period)
        ;
}

void main()
{
    printf("\nStarting delay now... (please wait 5 seconds)");

    DELAY(5);

    puts("\nOkay, I've finished!");
}
```

`gmtime()` 函数将本地时间值（由 `time()` 返回）转换为 GMT 时间，并将其存储在一个时间块中。此函数依赖于全局变量时区的设置。时间块是一个预定义的结构体（在 *time.h* 中声明），如下所示：

```c
struct tm
{
    int tm_sec;
    int tm_min;
    int tm_hour;
    int tm_mday;
    int tm_mon;
    int tm_year;
    int tm_wday;
    int tm_yday;
    int tm_isdst;
};
```

在这里，`tm_mday` 记录的是月份中的日期，范围从 1 到 31；`tm_wday` 是星期几，其中周日表示为 0；年份从 1900 年开始记录；`tm_isdst` 是一个标志，用于指示是否实行夏令时。结构体及其元素的具体名称可能因编译器而异，但结构体本身应该是相同的。

`mktime()` 函数将时间块转换为日历格式。它遵循以下原型：

```c
time_t mktime(struct tm *t);
```

以下示例允许输入日期，并使用 `mktime()` 计算与该日期相对应的星期几。时间函数只能识别 1970 年 1 月 1 日到现在的日期：

```c
#include <stdio.h>
#include <time.h>
#include <string.h>

void main()
{
    struct tm tstruct;
    int okay;
    char data[100];
    char *p;
    char *wday[] = { "Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday",
    "prior to 1970, thus not known" };

    do
    {
        okay = 0;
        printf("\nEnter a date as dd/mm/yy ");
        p = fgets(data, 8, stdin);
        p = strtok(data, "/");

        if (p != NULL)
            tstruct.tm_mday = atoi(p);
        else
            continue;

        p = strtok(NULL, "/");
        if (p != NULL)
            tstruct.tm_mon = atoi(p);
        else
            continue;

        p = strtok(NULL, "/");
    } while (1);
}
```

