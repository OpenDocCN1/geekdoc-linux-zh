
```c
struct itimerval tm;
tm.it_value.tv_sec = 5;
tm.it_value.tv_usec = 250000;
tm.it_interval.tv_sec = 0;
tm.it_interval.tv_usec = 0;
```

下一个示例显示了如何在 3.75 秒后到期并每 4.25 秒重复一次的定时器：

```c
struct itimerval tm;
tm.it_value.tv_sec = 3;
tm.it_value.tv_usec = 750000;
tm.it_interval.tv_sec = 4;
tm.it_interval.tv_usec = 250000;
```

# 间隔定时器宏

`setimer(2)` 的手册页通常提到三个有用的宏：

- `timerclear(tv)` 清除定时器值。
- `timerisset(tv)` 表示定时器值非零。
- `timercmp(tv,uv,cmp)` 比较两个定时器。

以下示例显示了如何使用 `timerclear()` 清除定时器值：

```c
struct itimerval tm;

timerclear(&tm);      /* 清除 tm */
```

以下测试值 `tm` 是否为零：

```c
if ( timerisset(&tm) )
    /* 非零 */
```

最后一个示例测试 `tm1` 和 `tm2` 是否表示相同的定时器值：

```c
struct itimerval tm1;
struct itimerval tm2;

if ( timercmp(&tm1,&tm2) == 0 )
    /* 相等 */
```

以下测试变量 `tm1` 是否小于 `tm2`：

```c
struct itimerval tm1;
struct itimerval tm2;

if ( timercmp(&tm1,&tm2) < 0 )
    /* tm1 < tm2 */
```

# 间隔定时器限制

大多数 UNIX 平台的间隔时间规格微秒部分 (`tv_usec`) 不超过 1,000,000 微秒。否则将报告错误。

定时器的粒度取决于平台。虽然规范允许微秒单位，但你的平台可能会将时间设置舍入为不精确的值。如果你的应用程序对时间敏感，在依赖特定精度之前可能需要测试你的间隔定时器。

Linux 文说明定时器信号的产生和传递是分开的。这意味着在极端情况下，如果实时定时器信号发生太快无法处理，可能会丢失。它们不会堆叠或计数。

某些 UNIX 平台记录了额外的间隔定时器。例如，Solaris 8 文档记录了 `ITIMER_REALPROF` 定时器，它传递相同的 `SIGPROF` 但具有不同的语义。

注意，`ITIMER_PROF` 可能导致系统调用中断，因为信号可以在系统模式下执行时产生。这意味着你的应用程序必须正确处理系统调用的 `EINTR` 错误。

# 创建单次定时器

列表 17.5 展示了间隔定时器的用法。该程序建立了一个简单的单次实时定时器，产生信号 `SIGALRM` 并退出。

## 列表 17.5 rish.c——单次实时定时器演示

```c
1:  /* rish.c */
2:
3:   #include <stdio.h>
4:   #include <stdlib.h>
5:   #include <unistd.h>
6:   #include <signal.h>
7:   #include <errno.h>
8:   #include <sys/time.h>
9:
10:  static int count = 0;      /* 计数器 */
11:
12:  /*
13:   * 信号处理器 :
14:   */
15:  static void
16:  handler(int signo) {
17:      int e = errno;               /* 保存 errno */
18:      ++count;                   /* 计数计数 */
19:      write(1,"<<<SIGALRM>>>\n",14);
20:      errno = e;                 /* 恢复 errno */
21:  }
22:
```

```c
struct sigaction new_sigrm; /* 新信号动作 */
struct itimerval old_timer; /* * 旧定时器值 */
struct itimerval new_timer; /* * 新定时器值 */
/*
 * 建立 SIGALRM 需要的信号处理器：
 */
new_sigrm.sa_handler = handler;
sigemptyset(&new_sigrm.sa_mask);
new_sigrm.sa_flags = 0;
sigaction(SIGALRM,&new_sigrm,NULL);
/*
 * 建立一个单次实时定时器：
 */
new_timer.it_interval.tv_sec = 0;
new_timer.it_interval.tv_usec = 0;
new_timer.it_value.tv_sec = 5;
new_timer.it_value.tv_usec = 250000; /* * 5.25 秒 */
puts("Starting ITIMER_REAL...");

z = setitimer(ITIMER_REAL,&new_timer,&old_timer);
if ( z ) {
    perror("setitimer(ITIMER_REAL)");
    return 1;
}
/*
 * 一个循环：
 */
do {
    /* 执行工作... */
} while ( count < 1 );

printf("ITIMER count is %d\n",count);
return 0;
}
```

列表 17.5 中的程序在第 34–40 行为信号 `SIGALRM` 建立了信号处理器。

函数 `handler()` 在信号触发时被调用，它简单地在第 19 行中变量 `Count` 并在第 20 行报告消息。

单次定时器在第 45–52 行配置。注意 `it_interval` 成员为 0，`setitimer` 会导致定时器在初始值过期后不会重启。

> 警告

列表 17.5 中的程序在第 61–63 行使用了 CPU 密集型循环。出于顾他人考虑，请勿在多用户环境中频繁调用此程序。

## 高级 UNIX 编程

编译并运行该程序应产生以下结果：

```
$ make rishot
cc -c -Wall rishot.c
cc -o rishot rishot.o
$ ./rishot
Starting ITIMER_REAL...
<<<SIGALRM>>>
ITIMER_REAL count is 1.
$
```

你将在程序启动 5.25 秒后看到触发的 `<<<SIGALRM>>>` 消息。程序返回 `count` 的最终值并正常退出。

# 建立重复定时器

列表 17.6 显示的程序最有趣。它同时启动了实时、虚拟和分析定时器。

## 列表 17.6 一个使用实时、虚拟和分析定时器的程序

```c
1:   /* timers.c */
2:
3:   #include <stdio.h>
4:   #include <stdlib.h>
5:   #include <unistd.h>
6:   #include <signal.h>
7:   #include <errno.h>
8:   #include <sys/time.h>
9:
10:  static int count = 0;      /* 计数器 */
11:
12:  /*
13:  * 信号处理器：
14:  */
15:  static void
16:  handler(int signos) {
17:      int e = errno;           /* 保存 errno */
18:      char *signame = "?";    /* 信号名称 */
19:
20:      switch(signo) {
21:          case SIGALRM:          /* 实时定时器过期 */
22:              ++count;             /* 计数器计数 */
23:              signame = "<<<SIGALRM>>>\n";
24:              break;
25:
26:          case SIGVTALRM:
27:              signame = "<<<SIGVTALRM>>>\n"; /* 虚拟定时器过期 */
28:              break;
29:
30:          case SIGPROF:         /* 系统虚拟定时器过期 */
31:              signame = "<<<SIGPROF>>>\n";
32:              break;
33:  }}
33: write(1,signame,strlen(signame));
34: errno = e;                               /* 恢复 errno */
35: } /*
36:
37: /*
38: * 主程序：
39: */
40: int main(int argc, char **argv) {      /* 状态返回码 */
41: int z;                                  /* 新信号动作 */
42: struct sigaction sigaction_alrm;      /* 实时定时器值 */
43: struct itimerval real_timer;             /* 用户模式定时器 */
44: struct itimerval virt_timer;         /* 系统+用户模式定时器 */
45: struct itimerval virt_timer_values;   /* 定时器值 */
46:
47:
48: /*
49:
50: * 建立针对 SIGALRM 的信号动作：
51: */
52: new_sigrm.sa_handler = handler;
53: sigemptyset(&new_sigrm.sa_mask);
54: new_sigrm.sa_flags = 0;
55:
56:
57: sigaction(SIGALRM, &new_sigrm,NULL);
58:
59: /*
60: * 建立单次实时定时器：
61: */
62: new_timer.it_interval.tv_sec = 0;
63: new_timer.it_interval.tv_usec = 0;
64: new_timer.it_value.tv_sec = 5;
65: new_timer.it_value.tv_usec = 250000; /* * 5.25 秒 */
66: puts("Starting ITIMER_REAL...");

67:
68: z = setitimer(ITIMER_REAL,&new_timer,&old_timer);
69: if ( z ) {
70:     perror("setitimer(ITIMER_REAL)");
71:     return 1;
72: }
73: /*
74: * 一个循环：
75: */
76: do {
77:     /* 执行工作... */
78: } while ( count < 1 );

79:
80: printf("ITIMER count is %d\n",count);
81: return 0;
82: }
```

列表 17.5 中的程序在第 34–40 行为信号 `SIGALRM` 建立了信号处理器。

函数 `handler()` 在信号触发时被调用，它简单地在第 19 行中增加变量 `Count` 的值并在第 20 行报告消息。

单次定时器在第 45–52 行配置。注意 `it_interval` 成员为 0，`setitimer` 会导致定时器在初始值过期后不会重启。

> 警告

列表 17.5 中的程序在第 61–63 行使用了 CPU 密集型循环。出于顾他人考虑，请勿在多用户环境中频繁调用此程序。

## 高级 UNIX 编程

编译并运行该程序应产生以下结果：

```
$ make rishot
cc -c -Wall rishot.c
cc -o rishot rishot.o
$ ./rishot
Starting ITIMER_REAL...
<<<SIGALRM>>>
ITIMER_REAL count is 1.
$
```

你将在程序启动 5.25 秒后看到触发的 `<<<SIGALRM>>>` 消息。程序返回 `count` 的最终值并正常退出。

# 建立重复定时器

列表 17.6 显示的程序最有趣。它同时启动了实时、虚拟和分析定时器。

## 列表 17.6 一个使用实时、虚拟和分析定时器的程序

```c
1:   /* timers.c */
2:
3:   #include <stdio.h>
4:   #include <stdlib.h>
5:   #include <unistd.h>
6:   #include <signal.h>
7:   #include <errno.h>
8:   #include <sys/time.h>
9:
10:  static int count = 0;      /* 计数器 */
11:
12:  /*
13:  * 信号处理器：
14:  */
15:  static void
16:  handler(int signos) {
17:      int e = errno;           /* 保存 errno */
18:      char *signame = "?";    /* 信号名称 */
19:
20:      switch(signo) {
21:          case SIGALRM:          /* 实时定时器过期 */
22:              ++count;             /* 计数器计数 */
23:              signame = "<<<SIGALRM>>>\n";
24:              break;
25:
26:          case SIGVTALRM:
27:              signame = "<<<SIGVTALRM>>>\n"; /* 虚拟定时器过期 */
28:              break;
29:
30:          case SIGPROF:         /* 系统虚拟定时器过期 */
31:              signame = "<<<SIGPROF>>>\n";
32:              break;
33:  }}
33: write(1,signame,strlen(signame));
34: errno = e;                               /* 恢复 errno */
35: } /*
36:
37: /*
38: * 主程序：
39: */
40: int main(int argc, char **argv) {      /* 状态返回码 */
41: int z;                                  /* 新信号动作 */
42: struct sigaction sigaction_alrm;      /* 实时定时器值 */
43: struct itimerval real_timer;             /* 用户模式定时器 */
44: struct itimerval virt_timer;         /* 系统+用户模式定时器 */
45: struct itimerval virt_timer_values;   /* 定时器值 */
46:
47:
48: /*
49:
50: * 建立针对 SIGALRM 的信号动作：
51: */
52: new_sigrm.sa_handler = handler;
53: sigemptyset(&new_sigrm.sa_mask);
54: new_sigrm.sa_flags = 0;
55:
56:
57: sigaction(SIGALRM, &new_sigrm,NULL);
58:
59: /*
60: * 建立单次实时定时器：
61: */
62: new_timer.it_interval.tv_sec = 0;
63: new_timer.it_interval.tv_usec = 0;
64: new_timer.it_value.tv_sec = 5;
65: new_timer.it_value.tv_usec = 250000; /* * 5.25 秒 */
66: puts("Starting ITIMER_REAL...");

67:
68: z = setitimer(ITIMER_REAL,&new_timer,&old_timer);
69: if ( z ) {
70:     perror("setitimer(ITIMER_REAL)");
71:     return 1;
72: }
73: /*
74: * 一个循环：
75: */
76: do {
77:     /* 执行工作... */
78: } while ( count < 1 );

79:
80: printf("ITIMER count is %d\n",count);
81: return 0;
82: }
```

# 管道与进程
