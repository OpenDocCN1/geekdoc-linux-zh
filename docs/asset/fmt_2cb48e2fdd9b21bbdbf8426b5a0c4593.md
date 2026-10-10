
``` 
27:                  break;

28: 

29:              case 'c':

30:                  printf("Command %s!\n", optarg);

31:                  break;

32: 

33:              case '?':

34:                  default:

35:                  printf("Unknown option\n");

36:                  break;

37:  }

38:    }

39:

40:    }

41:

42:    return 0;

43:    }

```
任何需要命令行配置的应用程序都可以从 `getopt` 或 `getopt_long` 中获益。

## 时间 API

GNU/Linux 提供了多种函数来处理时间（例如一天的时间）。时间通常由 `tm` 结构表示，其标识如下：

```
struct tm {
    int tm_sec;    /* 秒 (0..59) *
    int tm_min;    /* 分 (0..59) *
    int tm_hour;   /* 小时 (0..23) *
    int tm_mday;   /* 份中的一天 (1..31) *
    int tm_mon;    /* 月 (1..12) *
    int tm_year;   /* 年 (200x) *
    int tm_wday;   /* 星期 (0..6, 0 = 周一) *
    int tm_yday;   /* 一年中的一天 (1..366) *
    int tm_isdst;  /* 夏令时 (0, 1, -1) *
};
```

一种简化的表示方法定义为 `time_t` 结构，它仅表示以秒为单位的时间（自从纪时间 1970 年 1 月 1 日 00:00:00 UTC 起）。本节介绍的时间函数有：

```
#include <time.h>

time_t time(time_t *t);

struct tm *localtime(const time_t *time);

struct tm *gmtime(const time_t *time);

char *asctime(const struct tm *tm);

char *ctime(const time_t *timeDay);

time_t mktime(struct tm *tm);
```

可以使用 `time` 函数获取当前时间，如下所示：

```
time_t currentTime;

currentTime = time( NULL );
```

其中传递 `NULL` 是为了 `time` 函数返回本地时间。也可以通过向函数传递 `time_t` 引用将时间加载到变量中：

```
time_t currentTime;

(void)time (&currentTime);
```

存储该时间后，你现在可以使用 `localtime` 函数将其转换为 `tm` 结构。结合时间使用，你还可以得到：

```
time_t currentTime;

struct tm *tm_time;

currentTime = time(NULL);

tm_time = localtime(&currentTime);

printf("%02d:%02d:%02d\n",

tm_time->tm_hour, tm_time->tm_min, tm_time->tm_sec);
```

使用 `asctime` 或 `ctime` 函数可以轻松将时间转换为 ASCII 字符串。`ctime` 函数接收一个 `time_t` 引用，而 `asctime` 接收一个 `tm` 结构，如下：

```
time_t currentTime;

struct tm *tm_time;

currentTime = time(NULL);

printf("%s\n", ctime(&currentTime));

tm_time = localtime(&currentTime);

printf("%s\n", asctime(tm_time));
```

`gmtime` 函数将 `time_t` 变量分解为 `tm` 结构，但使用的是协调世界时 (UTC)。这与 GMT（格林威治标准时间）相同。`gmtime` 函数示例所示：

```
tm_time = gmtime(&currentTime);
```

最后，`mktime` 函数将 `tm` 结构转换为 `time_t` 格式。其示例所示：

```
tm_time = mktime(&currentTime);
```

整个函数集在列表 20.3 所示的简单应用程序中演示。

### 列表 20.3 时间转换函数的演示（位于 CD-ROM 的 `./source/ch20/time.c`）

```
1:   #include <time.h>
2:   #include <stdio.h>

3:   int main(

4:     {

5:       time_t currentTime;
6:       struct tm *tm_time;

7:       currentTime = time( NULL );
8:      tm_time = localtime(&currentTime);

9:      printf( "from localtime %02d:%02d:%02d\n",

10:               tm_time->tm_hour, tm_time->tm_min, tm_time->tm_sec );

11:      printf( "from ctime %s\n", ctime(currentTime) );

12:      printf( "from asctime/localtime %s\n", asctime(tm_time) );

13:      printf =time(&(&);

14::2222printfprintf "2time %02d:%02d\n",

15:               tm_time->tm_hour, tm_time->tm_min, tm_time->tm_sec);

16:      printf( "from asctime/localtime %s\n", asctime(tm_time) );

17:      currentTime = mktime(&currentTime);

18:      printf( "timetimetimetime);

19:      return 0;
20:  }
```

运行此应用程序将得到如下结果：

```
$ ./time

from localtime 14:30:00

from ctime Wed May 17 14:30:00 2023

from asctime/localtime Wed May 17 14:30:00 2023

from gmtime 14:30:00
```

`sysinfo` 函数允许应用程序获取系统信息，其用法如下：

```
int sysinfo(struct sysinfo *info);
```

它返回 0 并填充 `info` 结构，见表 20.1。注意所有大小单位均为字节。

| 元素 | 说明 |
| --- | --- |
| totalram | 总内存大小 |
| freeram | 可用内存大小 |
| totalswap | 总交换内存大小 |
| freeswap | 可用交换内存大小 |
| procs | 运行的进程数 |
| totalhigh | 总高内存大小 |
| freehigh | 可用高内存大小 |
| uptime | 运行时间（秒） |
| loads[0] | 1 分钟负载平均 |
| loads[1] | 5 分钟负载平均 |
| loads[2] | 15 分钟负载平均 |

`sysinfo` 进一步分解为关于系统的详细信息。

### 列表 20.4 `sysinfo` 的示例（位于 CD-ROM 的 `./source/ch20/sysinfo.c`）

```
1: #include <sysinfo.h>
2: #include <stdio.h>

3: int main()

4: {

5:     struct sysinfo info;
6:     int ret;
7:     int days, hours, minutes, seconds;

8:    ret = sysinfo(&info);

9:    if (ret == 0) {
```
