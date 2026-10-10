
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

`gmtime()` 函数将本地时间值（由 `time()` 返回）转换为 GMT 时间，并将其存储在一个时间块中。此函数依赖于全局变量时区的设置。时间块是一个预定义的结构体（在 `time.h` 中声明），如下所示：

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

`if (p != NULL)`
`tstruct.tm_year = atoi(p);`
`else`
`continue;`
`okay = 1;`
`}`
`while(!okay);`
`tstruct.tm_hour = 0;`
`tstruct.tm_min = 0;`
`tstruct.tm_sec = 1;`
`tstruct.tm_isdst = -1;`
`/* 现在获取星期几 */`
`if (mktime(&tstruct) == -1)`
`tstruct.tm_wday = 7;`
`printf ("That was %s\n",wday[tstruct.tm_wday]);`
`}`

`mktime()` 函数还会对超出范围的数值进行必要的调整。这种能力可用于发现 $n$ 天后的日期，如下所示：

```c
#include <stdio.h>
#include <time.h>
#include <string.h>

void main()
{
    struct tm *tstruct;
    time_t today;
    
    today = time(NULL);
    tstruct = localtime(&today);
    
    tstruct->tm_mday += 10;
    mktime(tstruct);
    
    printf ("In ten days it will be %02d/%02d/%2d\n", tstruct->tm_mday,tstruct->tm_mon + 1,tstruct->tm_year);
}
```

## 头文件

C 编译器提供的库函数的函数原型以及标准宏，都在头文件中声明。C 语言编程的 ANSI 标准列出了以下头文件：

- `assert.h`：定义 `assert` 调试宏。
- `ctype.h`：包含字符分类和转换宏。
- `errno.h`：包含错误代码的常量助记符。
- `float.h`：定义用于处理浮点数运算的实现相关宏。
- `limits.h`：定义类型值的实现相关限制。
- `locale.h`：包含国家特定参数。
- `math.h`：列出数学函数的原型。
- `setjmp.h`：定义 `setjmp`/`longjmp` 的 typedef 和函数。
- `signal.h`：包含供 `signal()` 和 `raise()` 使用的常量和声明。
- `stdarg.h`：包含处理参数列表的宏。
- `stddef.h`：包含通用数据类型和宏。
