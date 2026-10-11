
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <unistd.h>
#include <pwd.h>

int main(void)
{
    char *login;
    struct passwd *pentry;

    /* Get the login name */
    if((login = getlogin()) == NULL) { /* oops */
        perror("getlogin");
        exit(EXIT_FAILURE);
    }
    printf("getlogin returned %s\n", login);

    /* get the password entry for login */
    if((pentry = getpwnam(login)) == NULL) {
        perror("getpwnam");
        exit(EXIT_FAILURE);
    }
    /* display the full name */
    printf("gecos: %s\n", pentry->pw_gecos);

    exit(EXIT_SUCCESS);
}

## 输出

```
$ ./getname
getlogin returned kwall
gecos: Kurt Wall
```

`if` 语句用于防范 `getlogin` 或 `getpwnam` 返回 `NULL` 的可能性。如果任一函数返回 `NULL`，`perror` 将打印错误消息，并且程序将退出。首先，该程序使用 `getlogin` 来检索并显示运行程序的登录名。然后，它使用此名称检索密码条目并显示用户的全名（存储在 `/etc/passwd` 的 GECOS 字段中——更多信息请参见 man 5 passwd）。

## 附加进程信息

除了进程、用户和组 ID 之外，还可以获取有关进程的其他信息，例如它们的资源使用和运行时间。请注意，我写的是运行 *times*（复数），而不是 *time*（单数）。这是因为 Linux 内核为进程维护三个独立的时间值，如下所示：

- *墙上时钟时间* 是已经过去的时间。
- *用户 CPU 时间* 是处理器执行用户模式（非内核模式）代码所花费的时间。
- *系统 CPU 时间* 是执行内核代码所花费的时间。

> • 用户模式和内核模式之间的区别在第 120 页的“什么是系统调用？”中进行了讨论。

你可以通过调用 `times` 或 `getrusage` 来获取这些信息。然而，进程的资源使用只能从 `getrusage` 调用中获得。这些资源都与内存访问统计有关。本节首先讨论获取计时信息，然后介绍资源使用。

> **提示**
> 为了获取计时信息，你应该使用哪个调用，`times` 还是 `getrusage`？嗯，Linux 从 BSD 和 SVR4 UNIX 继承了功能，而它们都有这两个函数。POSIX（Linux 试图遵循的标准）只强制要求 *times*。然而，至少在理论上，`getrusage` 为程序员提供了关于进程资源使用情况的更完整的图片。它是理论性的，因为 Linux（截至 2.2.10 版本）只实现了 *rusage* 结构中定义的十六个资源中的五个。最后，*times* 返回的计时信息比 *getrusage* 返回的更精细。因此，如果你只需要计时信息或希望遵守 POSIX 标准，请使用 `times`。如果你不关心 POSIX 兼容性，或者如果你需要 `getrusage` 提供的额外信息，则使用它。

## 进程计时

`times` 函数在 `<sys/times.h>` 中的原型如下：

```
clock_t times(struct tms *buf);
```

*times* 返回自系统启动以来经过的时钟滴答数，也称为墙上时钟时间。*buf* 是指向 *tms* 结构的指针，该结构存储当前进程 *times*。

### 示例

![](img/be588b36b489136ce784030a08a1d3d4_101_0.png)

该程序使用 *system* 函数执行外部命令，然后使用 *times* 调用打印结果计时信息。

```c
/* resusg1.c - 获取进程时间和资源使用情况
 */
#include <stdio.h>
#include <stdlib.h>
#include <sys/times.h>
#include <time.h>
#include <unistd.h>

void doit(char * , clock_t);

int main(void)
{
    clock_t start, end;
    struct tms t_start, t_end;

    start = times(&t_start);
    /* 重定向输出以防止屏幕杂乱 */
    system("grep the /usr/doc/*/* > /dev/null 2> /dev/null");
    end = times(&t_end);

    doit("elapsed", end - start);

    fputs("Parent times\n", stdout);
    doit("  tuser CPU", t_end.tms_utime);
    doit("  tsys CPU", t_end.tms_stime);

    fputs("Child times\n", stdout);
    doit("  tuser CPU", t_end.tms_cutime);
    doit("  tsys CPU", t_end.tms_cstime);

    exit(EXIT_SUCCESS);
}

void doit(char *str, clock_t time)
{
    /* 获取每秒时钟滴答数 */
    long tps = sysconf(_SC_CLK_TCK);

    printf("%s: %6.2f secs\n", str, (float)time/tps);
}
```

在某个系统上，一次示例运行产生了以下输出：

![](img/be588b36b489136ce784030a08a1d3d4_103_0.png)

### 输出

```
$ ./resusql
elapsed time: 19.91 secs
Parent times
  user CPU time: 0.00 secs
  sys CPU time: 0.00 secs
Child times
  user CPU time: 2.34 secs
  sys CPU time: 1.10 secs
```

首先值得注意的是，父进程中似乎没有积累任何时间。虽然这在后面本章的“创建进程”部分有更详细的覆盖，但发生的情况是，当程序调用 *system* 函数时，它生成了一个子进程，而执行所有工作并积累 CPU 时间的是子进程，而不是父进程。

第二个值得注意的观察结果是，进程的经过时间，19.91 秒，并不等于用户和系统 CPU 时间之和，即 3.44 秒。造成这种表面差异的原因是，子进程执行的 *grep* 操作比 CPU 密集型更具 I/O 密集型。它必须扫描相关系统上的 2331 个头文件，超过 10 兆字节文本。缺失的 16 秒都用于读取硬盘。当然，在你的系统上，计时结果会不同。

*times'* 的返回值是相对时间，而不是绝对时间（自系统启动以来的时钟滴答数），因此要使其有用，你必须进行两次测量并使用它们的差值。这就得出了经过时间，或称为墙上时钟时间。*resusql* 通过将开始和结束的时钟滴答数分别存储在 *start* 和 *end* 中来实现这一点。其他进程计时值取自头文件 <sys/times.h> 中定义的 *tms* 结构。tms 结构存储进程及其子进程使用的当前 CPU 时间。它定义为

```
struct tms {
    clock_t tms_utime;     /* 用户 CPU 时间 */
    clock_t tms_stime;     /* 系统 CPU 时间 */
    clock_t tms_cutime;    /* 子进程的用户 CPU 时间 */
    clock_t tms_cstime;    /* 子进程的系统 CPU 时间 */
};
```

同样，这些值是时钟滴答数，而不是秒数。要将时钟滴答数转换为秒，使用 *sysconf* 函数，该函数将其参数转换为在运行时定义系统限制或选项的值。`_SC_CLK_TCK` 是一个宏，定义每秒有多少个时钟滴答数；`sysconf` 以 `long` 类型返回该值，程序使用它来计算进程运行所花费的秒数。该程序真正的核心是 `doit` 函数。它接受一个字符串指针和一个 `clock_t` 值，然后计算并打印进程每个部分的实际计时信息。

## 资源使用情况

进程的资源使用情况不仅仅涉及 CPU 时间。你还需要考虑进程的内存足迹，内存的结构，进程进行的内存访问类型，它执行的 I/O 数量和类型，以及它生成的网络活动数量和类型（如果有的话）。内核跟踪每个进程的所有这些以及更多这样的信息。至少，它具备执行此操作的能力。获取此信息的结构是一个 `rusage` 结构，定义在 <sys/resource.h> 头文件中。该结构定义如下：

```
struct rusage {
    struct timeval ru_utime;     /* 使用的用户时间 */
    struct timeval ru_stime;     /* 使用的系统时间 */
    long ru_maxrss;             /* 最大驻留集大小 */
    long ru_ixrss;              /* 共享内存大小 */
    long ru_idrss;              /* 非共享数据大小 */
    long ru_isrss;              /* 非共享栈大小 */
    long ru_minflt;             /* 页面回收 */
    long ru_majflt;             /* 页面错误 */
    long ru_nswap;              /* 交换 */
    long ru_inblock;            /* 块输入操作 */
    long ru_oublock;            /* 块输出操作 */
    long ru_msgsnd;             /* 发送的消息 */
    long ru_msgrcv;             /* 接收的消息 */
    long ru_nsignals;           /* 接收的信号 */
    long ru_nvcsw;              /* 自愿上下文切换 */
    long ru_nivcsw;            /* 非自愿上下文切换 */
};
```

不幸的是，Linux 只跟踪表 4.2 中列出的资源。

