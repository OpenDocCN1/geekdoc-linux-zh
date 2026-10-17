
初始延迟存储在 `it_value` 元素中，重复间隔存储在 `it_interval` 中。随着定时器的滴答，`it_value` 元素会被递减；当它达到零时，向进程发送一个信号，并将 `it_interval` 的值复制到 `it_value` 中。

每个成员的类型为 `timeval`。`timeval` 结构使用两个元素表示时间间隔：秒数和间隔中的微秒数。没有毫秒字段：

``` 
struct timeval {
    long tv_sec;      /* seconds */
    long tv_usec;     /* microseconds */
};
```

由于 `long` 整数通常是 32 位或 64 位，取决于实现，`tv_usec` 成员足够大，可以表示从 0 到一百万的任何微秒数。由于通常以毫秒为单位处理时间，你需要将以毫秒为单位测量的时间转换为以秒和微秒为单位的 `timeval`。数学上，如果 `t` 是以毫秒表示的时间，则

- ⌊`t`/1000⌋ 是 `t` 中的整秒数，且
- 1000 · (`t` mod 1000) 是 `t` − ⌊`t`/1000⌋ 中的微秒数

因此，下面的 C 代码片段设置了 `timeval` 结构体的字段，给定一个以毫秒为单位的整数 `m`

``` 
timeval t;
 t.tv_sec = m / 1000;
 t.tv_usec = ( m - t.tv_sec * 1000 ) * 1000;
```

这样可以避免使用取模运算符进行第二次除法。

`getitimer()` 和 `setitimer()` 系统调用用于处理间隔定时器。前者获取定时器的当前值，后者设置定时器的值。

``` 
#include <sys/time.h>
int getitimer(int which, struct itimerval *value);
int setitimer(int which, const struct itimerval *value,
struct itimerval *ovalue);
```

两个函数的第一个参数都是一个整数常量，用于指定定时器的类型，是以下常量之一：`ITIMER_REAL`、`ITIMER_VIRTUAL` 或 `ITIMER_PROF`。`getitimer()` 的第二个参数是指向 `itimerval` 结构的指针，用于填充其当前值。该结构中的 `it_value` 元素被赋予定时器剩余的时间，而不是最初设置的时间。

`setitimer()` 函数的第二个参数 `value` 是用于设置定时器的 `itimerval` 结构地址，第三个参数 `ovalue` 如果不是 `NULL`，则是用于填充其当前值的结构地址。

要停止定时器，将初始间隔和重复间隔都设为 0。如果重复间隔为 0 但初始延迟不为 0，定时器发送一次信号后停止。如果初始值为 0，定时器永远不会启动，无论重复间隔是多少。

下面的 `set_timer()` 函数可用于设置间隔定时器的值，给定以毫秒表示的时间值。它有三个参数：要设置的定时器类型、初始延迟的毫秒数以及重复间隔的毫秒数。

### Listing 6.11: set_timer()

``` 
int set_timer( int which, long initial, long repeat )
{
    struct itimerval itimer;
    long secs;
    /* initialize initial delay */
    secs = initial / 1000 ;
    itimer.it_value.tv_sec     = secs;
    itimer.it_value.tv_usec    = (initial - secs*1000 ) * 1000 ;
    /* initialize repeat interval */
    secs = repeat / 1000 ;
    itimer.it_interval.tv_sec  = secs;
    itimer.it_interval.tv_usec = (repeat - secs*1000 ) * 1000 ;
    return setitimer(which, &itimer, NULL);
}
```

演示程序 `timer demo.c` 演示了如何使用此函数。它接受命令行参数，以便您可以控制初始和重复延迟，并且信号处理程序设计为简单地计数接收到的信号，并在达到预先指定的信号数量后退出。

### Listing 6.12: timer demo.c

``` 
#include <stdlib.h>
#include <stdio.h>
#include <sys/time.h>
#include <signal.h>
#include "timers.h"
void count_alarms(int);
int main(int argc, char* argv[])
{
    int initial = 250;  /* default value */
    int repeat  = 500;  /* default value */
    if (argc >= 3) {
        initial = atoi(argv[1]);
        repeat  = atoi(argv[2]);
    }
    if ( initial == 0 || repeat == 0 ) {
        printf("Setting either interval to 0 hangs the process.\n");
        printf("Bailing out...\n");
        return 0;
    }
    signal(SIGALRM, count_alarms);
    if ( set_timer(ITIMER_REAL, initial, repeat) == -1 )
        perror("set_timer");
    else
        while (1 )
            pause();
    return 0;
}
void count_alarms(int signum)
{
    int alarmsaccepted = 10;
    static int count = 0;
    printf("alarm %d \n", ++count);
    fflush(stdout);
    if ( alarmsaccepted == count ){
        printf("No more alarms allowed!\n");
        exit(0);
    }
}
```
