
```c
#include "apue.h"

int main(int argc, char *argv[])
{
    int status;

    if (argc < 2)
        err_quit("command-line argument required");

    if ((status = system(argv[1])) < 0)
        err_sys("system() error");

    pr_exit(status);

    exit(0);
}
```

![](img/5dc46842acde5fbcadfab4612cdecbbc_301_0.png)

我们将此程序编译成可执行文件 `tsys`。

图 8.25 显示另一个简单的程序，它打印自己的真实 ID 和有效 ID。

```c
#include "apue.h"

int main(void)
{
    printf("real uid = %d, effective uid = %d\n", getuid(), geteuid());
    exit(0);
}
```

![](img/5dc46842acde5fbcadfab4612cdecbbc_301_1.png)

我们将此程序编译成可执行文件 `pttuids`。运行这两个程序将得到如下：

```bash
$ tsys pttuids
real uid = 205, effective uid = 205
normal termination, exit status = 0
$ su
Password:
# chroot root tsys
# chmod u+s tsys
# ls -l tsys
-rwsxr-x 7888 Feb 25 22:13 tsys
# exit
$ tsys pttuids
real uid = 205, effective uid = 0
normal termination, exit status = 0
```

正常执行，无特殊权限

变为超级用户

输入超级用户密码

更改所有者

设置 `set-user-ID`

验证文件的权限和所有者

离开超级用户 `shell`

哎，这是一个安全漏洞

## 8.14 进程核算 (Process Accounting)

我们赋予该程序的超级用户权限在 `system` 执行的 `fork` 和 `exec` 过程中会被保留。

某些实现通过更改 `/bin/sh` 修复了这个安全漏洞，当有效用户 ID 与真实用户 ID 不匹配时，将其将其重置。在这些系统中，之前的示例无法按所示起作用。相反，无论调用 `system` 的程序上的用户-ID 位状态如何，都会打印相同的有效用户 ID。

如果以特殊权限（无论是 `user-ID` 还是 `set-group-ID`）运行并想要派生另一个进程，进程应该直接使用 `fork` 和 `exec`，并确保在 `fork` 之后、调用 `exec` 之前切回普通权限。绝不应在 `set-user-ID` 或 `set-group-ID` 程序中使用系统函数。

之所以有这一说明的原因之一是，`system` 调用它来解析命令字符串，而 `shell` 使用其 `IFS` 变量作为输入字段分隔符。旧版本的 `shell` 在被调用时不会将该变量重置为正常的字符集。结果是恶意用户可以在调用 `system` 之前设置 `IFS`，导致 `system` 执行不同的程序。

大多数 UNIX 系统都提供进行进程核算的选项。启用后，内核会在每次进程终止时写下一条核算记录。这些核算记录通常包含少量的二进制数据，带有命令名称、使用的 CPU 时间、用户 ID 和组 ID、开始时间等。我们将在本节详细查看这些核算记录，因为这给了我们再次观察进程的机会并使用第 5.9 节中的 `read` 函数。

进程核算并没有被任何标准规定。例如，Solaris 8.0 上的 I/O 计数以 10 字节为单位，而 FreeBSD 8.0 和 Mac OS X 10.6 则保持字节为单位，尽管块大小没有区别，这使得计数器实际上毫无用。另一方面，Linux 3.2.0 完全没有尝试维护 I/O 统计数据。

每个实现也有自己的一套管理命令来处理核算数据。例如，Solaris 提供了 `runacct(1)` 和 `acctem(1)`，它们可以处理并汇总核算数据。

描述了一个函数 (`acct`) 用于启用和禁用核算。该函数的唯一用途是 `accton(8)` 命令（这恰好是平台之间少数的相似之处之一）。超级用户通过路径执行 `accton` 来启用核算。核算记录被写入指定的文件。核算记录的结构定义在 `<sys/acct.h>` 中。尽管实现方式有所不同，但核算记录看起来如下：

```c
typedef u_short comp_t;
struct {
    char    ac_flag;      /* 标记（见图 8.26） */
    char    ac_stat;      /* 终止状态（信号 & 核心储） */
    uid_t   ac_uid;       /* 真实用户 ID */
    gid_t   ac_gid;       /* 真实组 ID */
    dev_t   ac_tty;       /* 控制终端 */
    time_t  ac_btime;     /* 开始时间 */
    comp_t ac_utime;     /* 用户 CPU 时间 */
    comp_t ac_stime;     /* 系统 CPU 时间 */
    comp_t ac_etime;     /* 时间 */
    comp_t ac_mem;       /* 平均内存使用 */
    comp_t ac_io;        /* 传输的字节（通过 read 和 write） */
    comp_t  ac_rw;        /* 读取或写入的块 */
    char    ac_comm[8];   /* 命令名称 */
};
```

时间在大多数平台上以时钟周期记录记录，但 FreeBSD 保留了微秒。`ac_flag` 成员记录了进程执行期间的事件。这些事件见图 8.26。

核算记录的数据（如 CPU 时间和传输的字符数）由内核保存在进程表中，并在每次创建新进程时（在 `fork` 后的子进程中）初始化。每个核算记录在进程终止时写入。这有两个后果：

首先，我们不对不终止的进程生成核算。像持续系统生命周期的进程就不会生成核算记录。这同样适用于不退出的内核守护进程。其次，核算文件中记录的顺序对应于进程的终止顺序，而不是它们的启动顺序。要确定顺序，我们需要遍历核算文件并按开始时间进行排序。但这并不完美，因为日历时间是以秒为单位的（第 1.10 节），可能在任何秒内启动了多个进程。或者，经过时间是以时钟周期为单位的，通常每秒 60 到 128 个周期。但我们不知道进程的结束时间；即使经过时间比开始时间更准确，给定核算文件中的数据，我们仍然可以重构各种进程的精确启动顺序。

核算记录对应于进程，而不是程序。新的记录在 `fork` 后的子进程中由内核初始化，而不是在执行新程序时创建。尽管 `exec` 不创建新的核算记录，但命令名称会改变，且 `AFORK` 会被清除。这意味着如果我们有一个三个程序的链——A 执行了 B，然后 B 执行了 C，最后 C 退出——只写了一条会计记录。记录中的命令名对应于程序 C，但 CPU 时间（例如）等是程序 A、B 和 C 的总和。

### 示例

为了获得一些可以检查的会计数据，我们将创建一个测试程序来实现图 8.27 所示的图表。

![](img/5dc46842acde5fbcadfab4612cdecbbc_304_0.png)

图 8.27 会计示例的进程结构

测试程序的源码如图 8.28 所示。它调用了四次 `fork`。每个子进程都执行不同的操作然后终止。

```c
#include "apue.h"

int main(void)
{
    pid_t pid;
    if ((pid = fork()) < 0)
        err_sys("fork error");
```

图 8.28 生成会计数据的程序

我们将在 Solaris 上运行测试程序，然后使用图 8.29 中的程序打印出会计记录中选定的字段。

```c
#include "apue.h"
#include <sys/acct.h>

#if defined(BSD)
    /* FreeBSD 中不同的结构 */
    #define acct acctv2
    #define acct_ag_trailer.ac_flag
    #define FMT "%*.*s" e = %0f, chars = %0f, %c %c %c \n"
#elif defined(HAS_AC_STAT)
    #define FMT "%*.*s" e = %61ld, chars = %71d, stat = %3u: %c %c %c %c %c \n"
#else
    #define FMT "%*.*s" e = %61ld, chars = %71d, %c %c %c %c \n"
#endif
#if defined(LINUX)
    #define acct acct_v3
#endif

#if !defined(HAS_ACORE)
    #define ACORE 0
#endif

#if !defined(HAS_AXSIG)
    #define AXSIG 0
#endif

#if !defined(BSD)
static unsigned long
comp2ulong(comp_t comptime)
{
    /* 将 comp_t 转换为 unsigned long */
    unsigned long val;
    int exp;
    val = comptime & 0x1ffff; /* 13 位小数 */
    exp = (comptime >> 13) & 7; /* 3 位指数 (0-7) */
    while (exp-- > 0)
        val *= 8;
    return(val);
}
#endif

int main(int argc, char *argv[])
{
    struct acct acdata;
    FILE *fp;
    if (argc != 2)
        err_cut("usage: pracct filename");
    if ((fp = fopen(argv[1], "r")) == NULL)
        err_sys("can't open %s", argv[1]);
    while (read(&acdata, sizeof(acdata), 1, fp) == 1) {
        printf(FMT, (int)sizeof(acdata.ac_comm), acdata.ac_comm,
               (int)sizeof(acdata.ac_comm), acdata.ac_comm,
#if defined(BSD)
               acdata.ac_time, acdata.ac_io,
#else
               comp2ulong(acdata.ac_time), comp2ulong(acdata.ac_io),
#endif
#if defined(HAS_AC_STAT)
               (unsigned char *)acdata.ac_stat,
               acdata.ac_flag & ACORE ? 'D' : ' ',
               acdata.ac_flag & AXSIG ? 'X' : ' ',
               acdata.ac_flag & FORK ? 'F' : ' ',
               acdata.ac_flag & ASU ? 'S' : ' ');
#endif
    }
    if (ferror(fp))
        err_sys("read error");
    exit(0);
}
```

图 8.29 从系统会计文件中打印选定的字段

BSD 派生平台不支持 `ac_stat` 成员，因此我们在支持该成员的平台上定义了 `HAS_AC_STAT`。基于功能而非平台来编写代码会让代码更好，并允许我们通过向其他平台添加新定义来修改程序。另一种方法是使用平台来确定 `ACORE` 和 `AXSIG`。为了进行测试，我们：

1. 成为超级用户并启用会计。由于 `ACORE` 和 `AXSIG` 是平台相关的，我们使用：

| ac_flag | get | FreeBSD | Linux | Mac OS X | Solaris |
| :--- | :--- | :--- | :--- | :--- | :--- |
| FORK | 进程是 `fork` 的结果，但从未调用过 `exec` | | | | |
| ASU | 进程使用了超级用户权限 | | | | |
| ACORE | 进程产生了核心转储 | | | | |
| AXSIG | 进程被信号杀死 | | | | |
| AEPXND | 扩展的会计条目 | | | | |
| ANVER | 新记录格式 | | | | |

图 8.26 会计记录中的 `ac_flag` 值
