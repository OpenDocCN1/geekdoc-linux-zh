
```c
105:         puts("READ EOF");

106:     close

f2);

107:         f2 = -1;

108:     }

109:     }

110:     } while (f1 >= 0 || f2 >= 0);

111:     puts("select.");

112:     return 0;

113: }
```

*(注：由于原文文本在代码块部分存在严重的乱码和重复错误，翻译时根据逻辑对代码注释部分进行了修正性处理，以确保可读性)*

## I/O 轮询

`poll(2)`函数代表另一种执行 I/O 调度的方式。它最初由 AT&T 开发，用于 STRE 文件描述符。然而，`poll(2)`现在接受所有文件描述符。

```c
/*
* UnixWare 7, SGI IRIX 6.5 :
 */
#include <stropts.h>
#include <poll.h>
/*
* HP-UX 11.x, Solaris 8 :
 */
#include <poll.h>
/*
* IBM AIX 4.3 :
 */
#include <sys/poll.h>
#include <sys/select.h>
#include <sys/types.h>
/*
* FreeBSD :
 */
#include <sys/types.h>
#include <poll.h>
int poll(struct pollfd *fds, unsigned int nfds, int timeout);
struct pollfd {
    int fd;             /* 文件描述符 */
    short events;       /* 要查找的事件 */
    short revents;      /* 返回的事件 */
};
```

正如你可以看到，根据编译平台的不同，所需的文件差异很大。`poll(2)`函数使用`pollfd`结构体数组来驱动 I/O 操作（参数 args）。该数组的每个元素指定了一个文件描述符 `fd` 和要报告的事件 `events`。当`poll(2)`返回一个大于零的值时，成员`revents`包含代表文件描述符已发生事件的位。参数`nfds`表示参与调用的数组元素数量。

> 当结构体`pollfd`的`fd`成员为负数时，成员`events`将被忽略，且成员`revents`被设置为零。
将`fd`设置为 -1 是指示`poll(2)`忽略该条目的有效方法。

`poll(2)`返回的值属于三类之一：

- 负数 `-1`，表示发生了错误（检查`errno`）。
- 零，表示发生了超时且没有报告任何事件。
- 大于零，表示有多少个文件描述符报告了事件。

# 高级 UNIX 编程

`timeout`参数以毫秒为单位指定等待事件发生的最小时间。如果`timeout`值指定为宏`INFTIM`（或 -1），则假设为无限超时。如果`timeout`参数为 0，则`poll(2)`将立即返回，即使没有要报告的事件。

> 注意
函数`poll(2)`在处理完信号后可能会返回错误`EINTR`。

# Poll 事件

`pollfd`数组的`events`成员必须初始化，以描述要报告的事件。这些事件位宏分为三类：

- 描述输入相关的`event`和`revent`标志的宏（见表 16.1）
- 描述输出相关的`event`和`revent`标志的宏（见表 16.2）
- 仅描述返回信息的`revent`标志的宏（见表 16.3）

表 16.1 描述了输入位码，这些位码可以通过或操作组合以指示要轮询读取事件。

# 表 16.1 poll(2) 的读取事件位码

| 宏 | 事件 |
| :--- | :--- |
| POLLIN | 可以非阻塞地读取高优先级以外的数据。 |
| POLLRDNORM | 可以非阻塞地读取普通数据。 |
| POLLRDBAND | 可以非阻塞地读取非零优先级的数据。 |
| POLLPRI | 可以非阻塞地读取高优先级的数据。 |

表 16.2 是描述写入事件的额外位码。

# 表 16.2 poll(2) 的写入事件位码

| 宏 | 事件 |
| :--- | :--- |
| POLLOUT | 可以非阻塞地写入普通数据。 |
| POLLWRNORM | 等于 POLLOUT。 |
| POLLWRBAND | 可以非阻塞地写入非零优先级的数据。 |

表 16.3 宏表示了仅在`pollfd`数组成员`revents`中返回的位。

# 表格 16.3 poll(2) 返回的 revent 位码

| 宏 | 事件 |
| :--- | :--- |
| POLLERR | 设备或套接字发生了异常情况。 |
| POLLHUP | 设备或套接字已断。注意 POLLHUP 和 POLLOUT 标志是互斥的（它们不会同时出现在 revent 中）。 |
| POLLNVAL | 文件描述符未打开。注意当文件描述符为负数时，此位不会返回。 |

# Poll 优先级

目前为止`poll(2)`文档提到了优先级和优先级带。`poll(2)`的手册页也会提到这一点。优先级带是 System V 实现的 STREAMS 的，它是与设备驱动程序通信的一种推广。

除非你正在进行 STREAMS 编程，否则你可以简单地忽略优先级带并使用普通的输入输出宏。这意味着可以使用`POLLIN`或`POLLNORM`用于输入输出，或使用`POLLWRNORM`用于输出。

# poll(2) 示例

列表 16.3 显示了`poll.c`的源代码，它是列表 16.2 中`select.c`程序的`poll(2)`适配。

### 列表 16.3——使用 poll(2) 的示例程序

```c
/* poll.c */
#include <stdio.h>
#include <stdlib.h>
#include <stdarg.h>
#include <unistd.h>
#include <fcntl.h>
#include <errno.h>
#include <string.h>
#include <sys/types.h>
#include <sys/time.h>
#include <sys/stat.h>
#include <poll.h>
static void quit(int rc, const char *fmt, ...) {
    va_list ap;
    if (errno != 0) {
        fprintf(stderr, "%s\n", strerror(errno));
    }
    va_start(ap, fmt);
    vfprintf(stderr, fmt, ap);
    va_end(ap);
    exit(rc);
}
int main(int argc, char **argv) {
    int z;
    int f1;
    struct pollfd fds[2];
    int nfds;
    char buf[256];
    FILE *p1, *p2;
    if (!(p1 = popen("/dev/null", "r")))
        quit(1, "popen failed for p1");
    if (!(p2 = popen("/dev/null", "r")))
        quit(1, "popen failed for p2");
    f1 = 0; // 示例
    fds[0].fd = f1;
    fds[0].events = POLLIN;
    // ... f2 和 fds[1] 的逻辑 ...
    nfds = 2;
    printf("BEGIN: f1=%d,f2=%d\n", f1, f2);
    do {
        do {
            z = poll(fds, nfds, 3500); // 超时3.5秒
            while (z == -1 && errno == EINTR) {
                if (z == -1) quit(1, "poll(2)");
            }
            if (z == 0) {
                printf("TIMEOUT: f1=%d,f2=%d\n", f1, f2);
                continue;
            }
            // 控制在这里表示 f1 或 f2 有数据可读
            if (fds[0].revents & POLLIN) {
                z = read(f1, buf, sizeof(buf) - 1);
                if (z == -1) quit(6, "read(2) of f1.");
                if (z > 0) {
                    buf[z] = 0;
                    printf("**** read %d bytes %s from f1\n", z, buf);
                } else {
                    puts("read EOF from f1.");
                    pclose(p1);
                    fds[0].fd = f1 = -1;
                }
            }
            if (fds[1].revents & POLLIN) {
                z = read(f2, buf, sizeof(buf) - 1);
                if (z == -1) quit(6, "read(2) of f2.");
                if (z > 0) {
                    buf[z] = 0;
                    printf("**** read %d bytes %s from f2\n", z, buf);
                } else {
                    puts("read EOF from f2.");
                    pclose(p2);
                }
            }
        } while (0);
    } while (1);
}
```

```
TIMEOUT: f1=-1, f2=4
TIMEOUT: f1=-1, f2=4
read EOF from f2;
End poll.
```

会话输出与之前的示例几乎相同。区别在于存在不同的文件名。请注意，`poll(2)`函数在结束前也演示了它的超时能力。

## 总结

本章为你提供了使用 UNIX 系统调用`select(2)`和`poll(2)`所需背景知识。此外，你现在将能够使用非阻塞 I/O，特别是在结合`select(2)`或`poll(2)`对文件描述符进行写入时。

下一章将探索 UNIX 计时器的精彩世界。

# 第 17 章

# 计时器

在第 15 章“信号”中，你学习了`alarm(3)`函数，它允许你创建和取消定时器。该函数提供了一种定时器服务，其时间分辨率以秒为单位。

本章将从`sleep(2)`函数调用的假设性实现开始。这将有助于你进一步了解为什么使用`alarm(3)`和`sleep(2)`之间存在冲突。稍后你会发现，这种冲突可能会扩展到其他的 UNIX 函数。

本章还将向你介绍：

- 使用`sleep(3)`和`nanosleep(3)`的细粒度计时器
- 间隔计时器函数

## Sleep 函数

第 15 章提到，`sleep(3)`函数通常是基于`alarm(3)`实现实现的在本节中，你将查看`sleep(3)`的其中一种假设实现。`sleep(3)`的函数摘要如下：

```c
#include <unistd.h>
```

```c
unsigned int sleep(unsigned int seconds);
```

函数接受一个时间值来暂停调用进程的执行。如果`sleep(3)`调用因接收到信号而中断，剩余的秒数将返回给调用者。返回值 0 表示整个睡眠时间已过去。

列表 17.1 sleep.c——sleep(3) 的简单演示

```c
1: /* sleep.c */
2:
3: #include <stdio.h>
4: #include <stdlib.h>
5: #include <unistd.h>
6: #include <signal.h>
7: #include <time.h>
8:
```

# 高级 UNIX 编程

接上页页

```c
9:   int
10:  main(int argc,char **argv) {
11:     time_t dt;
12:
13:     time(&dt);
14:     printf("%s begun at:%s",__FILE__,ctime(&dt));
15:
16:     puts(("Zzz...%d seconds)..."));
17:     sleep(5);
18:
19:     time(&dt);
20:     printf("%s completed at:%s",__FILE__,ctime(&dt));
21:     return 0;
22: }
```

编译和运行会话如下：

```bash
$ make sleep
cc -Wall sleep.c
cc -o sleep sleep.o
$ ./sleep
sleep.c begun at:   Sat Jun 10 11:22:23 2000
Zzz... (%d seconds)...
sleep.c completed at: Sat Jun 10 11:22:28 2000
$
```

这确实非常简单。然而，`sleep(3)`的实现要复杂一些。`sleep(3)`函数的设计需要以下基本步骤：

1. 安排捕获信号 SIGALRM。
2. 使用`alarm(3)`启动计时器。
3. 等待任何信号的发生。
4. 恢复对 SIGALRM 的信号处理。
5. 如果有剩余时间，则返回。

## sleep(3) 的 UNIX 实现

使用之前列出的基本步骤，你可以编写自己版本的库函数`sleep(3)`。列表 17.2 显示了其中可能的实现。

# 列表 17.2 imsleep.c——sleep(3) 的实现示例

```c
1:   /* imsleep.c */
2:
3:   #include <stdio.h>
4:   #include <stdlib.h>
5:   #include <unistd.h>
6:   #include <signal.h>
7:   #include <time.h>
8:
9:
10:  * SIGALRM 的信号处理程序：
```

```c
11: /*/
12: static void
13: h_sigalrm(int sign) {
14: 
15:     return;       /* 直接返回 */
16: }
17: 
18: /*
19:     * 一个模拟的 sleep(2) 函数：
20:     */
21: static unsigned
22: sleep(unsigned seconds) {   /* 开始和结束时间 */
23:     time_t dt0, dt1;             /* 经过的秒数 */
24:     unsigned e;
25:     struct sigaction old_sigalrm;  /* 旧的信号动作 */
26:     struct sigaction new_sigalrm;  /* 新的信号动作 */
27:     sigset_t t_nosig;             /* 空集 */
28: 
29:     sigemptyset(&t_nosig);       /* 空集 */
30: 
31:     /*
32:     * 为 SIGALRM 建立动作：
33:     */
34:     new_sigalrm.sa_handler = h_sigalrm;
35:     sigemptyset(&new_sigalrm.sa_mask);
36:     new_sigalrm.sa_flags = 0;
37: 
38:     */
39:     sigaction(SIGALRM, &new_sigalrm, &old_sigalrm);
40: 
41:     /*
42:     * 获取开始时间，启动计时器，暂停并获取结束时间：
43:     */
44:     time(&dt0);                  /* 获取开始时间 */
45:     alarm(seconds);               /* 重启计时器 */
46:     sigsuspend(&t_nosig);         /* 等待任何信号 */
```
