
一旦根目录被更改，就没有办法使用`chroot`返回原来的根目录。然而，某些系统提供了一个姊妹函数`fchroot`，它接受一个文件描述符。（这与第 3.6.2 节中解释的`fchdir`和`chdir`之间的关系类似。）你可以通过打开当前根目录的文件描述符来获取它，执行`chroot`，然后使用保存的文件描述符作为参数通过`fchroot`返回。

## 5.15 获取和设置优先级

如我在第 1.1.6 节中提到，每个进程都有一个*nice*值，这是进程影响内核调度优先级的一种方式。较高的值意味着进程希望更*nice*——即以较低的优先级运行。较低的值意味着不那么*nice*——优先级更高。为了使*nice*值保持为正，它们会从某个随系统变化的数字（奇怪的是，在 UNIX 文档中被称为`NZERO`）偏移；典型值为 20。进程以 20 开始，最*nice*可达 39，最不*nice*为 0。

要使进程*nice*或不*nice*，进程执行*nice*系统调用：

```
nice—change nice value

```c
#include <unistd.h>

int nice(int incr)          /* increment */

/* Returns old nice value - NZERO or -1 on error (sets errno) */
```
```

*nice*系统调用将*incr*加到*nice*值上。结果*nice*值必须在 0 到 39 之间（包含两端）；如果产生无效值，则使用最近的合法值。只有超级用户可以降低*nice*值，从而获得优于平均水平的服务。

*nice*实际上返回新的*nice*值减去 20，因此如果`NZERO`为 20，返回值的范围是从 -20 到 19。然而，返回的值很少很有用。这也挺好，因为新的*nice*值 19 与错误返回（$19 - 20 = -1$）无法区分。这个 bug 如果在如此多年间未被修复（甚至未被注意到），这表明大多数 UNIX 系统程序员对像*nice*这样的小系统调用的错误返回值并不怎么关心。

大多数 UNIX 用户熟悉*nice*命令，它以较低的优先级运行程序（如果是超级用户运行，则以较高的优先级运行）。以下是我们的版本：

```c
#define USAGE "usage: aupnice [-num] command\n"

int main(int argc, char *argv[])
{
  int incr, cmdarg;
  char *cmdname, *cmdpath;

  if (argc < 2) {
    fprintf(stderr, USAGE);
    exit(EXIT_FAILURE);
  }
  if (argv[1][0] == '-') {
    incr = atoi(&argv[1][1]);
    cmdarg = 2;
  }
  else {
    incr = 10;
    cmdarg = 1;
  }
  if (cmdarg >= argc) {
    fprintf(stderr, USAGE);
    exit(EXIT_FAILURE);
  }
  (void)nice(incr);
  cmdname = strchr(argv[cmdarg], '/');
  if (cmdname == NULL)
    cmdname = argv[cmdarg];
  else
    cmdname++;
  cmdpath = argv[cmdarg];
  argv[cmdarg] = cmdname;
  execvp(cmdpath, &argv[cmdarg]);
  EC_FAIL

  EC_CLEANUP_BGN
  exit(EXIT_FAILURE);
  EC_CLEANUP_END
}
```

注意我们在调用*execvp*时如何重用传入的*argv*。变量*cmdarg*持有命令路径的下标（1 或 2，取决于是否指定了增量）。*argv*中从*cmdarg*开始的部分是传递下去的部分。您可能想要将此与第 5.3 节中为`execvp2`所需的更广泛操作进行对比。在那里我们需要*插入*一个参数，这要求我们重新复制整个数组。

向量中的第一个字符串应该只是命令名称，而不是完整的路径，因此我们必须剥离路径中除最后一个组件以外的所有部分，以防命令是通过包含斜杠的路径名执行的。然而，`execvp`的第一个参数必须是在`aupnice`命令行上输入的内容。

还要注意我们使用了没有`fork`的`execvp`。在更改了优先级之后，没有必要保持一个父进程活着来等待。

下面是`aupnice`在 Solaris 上的运行情况。对于示例命令，它使用`ps`报告自身。请注意，内部优先级（无论那是什么）在 nice 值增加 10 时（`aupnice`的默认值）从 58 变为 28。

```
$ ps -ac
  PID CLS PRI TTY     TIME CMD
 10460 TS 58 pts/2    0:00 ps
$ aupnice ps -ac
  PID CLS PRI TTY     TIME CMD
 10461 TS 28 pts/2    0:00 ps
```

有一些更新的、更花哨的调用称为`getpriority`和`setpriority`，您可以使用它们来操纵 nice 值；有关详细信息，请参阅 [SUS2002] 或您系统的文档。

## 5.16 进程限制

内核对进程资源执行各种限制，例如最大文件大小和最大堆栈大小。通常，当达到限制时，导致限制的功能（例如`write`、`malloc`）会返回错误，或者会产生一个信号，例如在堆栈溢出的情况下产生`SIGSEGV`（第 9 章）。

> 14. 如果捕获了`SIGSEGV`，当没有堆栈时，信号处理器如何执行？您可以设置一个备用堆栈，如第 9.3 节所述。如果没有这样做，信号将恢复其默认行为，即终止进程。

下面列出了七种标准资源，它们的限制值可以设置或获取，实现中可能定义其他资源。

对于每种资源，都有一个*最大*（*或硬*）限制和一个*当前*（*或软*）限制。当前限制是生效的限制，普通进程允许将其设置为不超过最大值的任何合理数值。普通进程还可以不可逆地降低（但不能提高）最大值，使其等于当前限制。超级用户进程可以将任一限制设置为内核支持的任何值。

以下是获取和设置限制的系统调用：

`getrlimit`——获取资源限制

```c
#include <sys/resource.h>
int getrlimit(
    int resource,        /* resource */
    struct rlimit *rlp   /* returned limits */
);
/* Returns 0 on success or -1 on error (sets errno) */
```

`setrlimit`——设置资源限制

```c
#include <sys/resource.h>
int setrlimit(
    int resource,        /* resource */
    const struct rlimit *rlp  /* limits to set */
);
/* Returns 0 on success or -1 on error (sets errno) */
```

`struct rlimit`——*getrlimit* 和 *setrlimit* 的结构体

```c
struct rlimit {
    rlim_t rlim_cur;     /* current (soft) limit */
    rlim_t rlim_max;     /* maximum (hard) limit */
};
```

每个调用针对单一资源；您通过*getrlimit*获取其限制，并根据之前给出的规则通过*setrlimit*设置它们。标准资源包括：

- **RLIMIT_CORE** 核心转储（内存转储）文件的最大大小（以字节为单位）；零表示根本不写入文件。如果超过该大小，不会报告错误——写入仅在该大小时停止，可能会留下一个无用的文件。
- **RLIMIT_CPU** 最大 CPU 时间（以秒为单位）。超过它会生成 *SIGXCPU*，默认情况下会终止进程。标准没有定义如果捕获、忽略或阻止此信号会发生什么——进程可能会被终止，因为没有办法在不积累更多 CPU 时间的情况下继续执行。

## 进程限制

| 常量 | 描述 |
| :--- | :--- |
| `RLIMIT_DATA` | 数据段的最大大小（以字节为单位）。超出此值会导致内存分配函数（例如 `malloc`）失败。 |
| `RLIMIT_FSIZE` | 最大文件大小（以字节为单位）。超出此值会生成 `SIGXFSZ` 信号；如果捕获、忽略或阻塞该信号，则导致违规函数失败。 |
| `RLIMIT_NOFILE` | 进程可能使用的文件描述符的最大数量。[^15] 超出此值会导致违规函数失败。 |
| `RLIMIT_STACK` | 最大堆栈大小（以字节为单位）。如果超出此值，将生成 `SIGSEGV` 信号。 |
| `RLIMIT_AS` | 最大总内存大小，包括数据段、堆栈以及通过 `mmap`（第 7.14 节）映射的任何内容。超出此值会导致违规函数失败，或者如果是堆栈，则产生与 `RLIMIT_STACK` 描述相同的效果。 |

[^15]: 脚注 15

进程限制在 `exec` 过程中保持不变，并在 `fork` 之后被子进程继承，因此如果在登录时设置一次，它们将影响从登录 shell 派生的所有进程。但是，与 `cd` 一样，设置它们的命令必须内置于 shell 中——在 shell 的子进程中执行该命令是无效的。大多数 shell 都有一个设置文件大小限制的 `ulimit` 命令，而其他 shell 则有一个更通用的命令，可能称为 `limit`、`limits` 或 `plimit`。[^16]

[^16]: 脚注 16

除了实际数字外，对于 `rlimit` 结构中的 `rlim_cur` 和 `rlim_max` 成员，还有一些特殊的宏：`RLIM_SAVED_CUR`、`RLIM_SAVED_MAX` 和 `RLIM_INFINITY`。

当你调用 `getrlimit` 时，如果数值适合 `rlim_t`（这是一种宽度未由标准指定的无符号类型），则返回实际数字。如果数值不适合，则如果该成员等于最大值，该成员将被设置为 `RLIM_SAVED_MAX`。否则，它被设置为 `RLIM_SAVED_CUR`，这意味着“限制被设置为限制本身所在的值”。如果某个成员被设置为 `RLIM_INFINITY`，则意味着没有限制。

当你调用 `setrlimit` 时，如果成员是 `RLIM_SAVED_CUR`，则将其设置为当前限制；如果是 `RLIM_SAVED_MAX`，则将其设置为最大限制；如果是 `RLIM_INFINITY`，则不强制执行限制。否则，限制被设置为你使用的任何数字。但是，只有当对 `getrlimit` 的调用返回这些值时，你才能使用 `RLIM_SAVED_CUR` 或 `RLIM_SAVED_MAX`；否则，你必须使用实际数字。换句话说：只有当 `rlim_t` 无法容纳该数值时，你才被迫使用这些宏。

`RLIM_SAVED_CUR` 和 `RLIM_SAVED_MAX` 的繁琐过程实际上就是这样：即使你无法获取它们的实际值，你仍然可以在某种程度上操作这些限制。

如果一个实现永远不会拥有一个无法放入 `rlim_t` 的限制，那么 `RLIM_SAVED_CUR` 或 `RLIM_SAVED_MAX` 宏永远不会被使用，因此允许它们具有与 `RLIM_INFINITY` 相同的值。我们将在下面的示例中看到这一点的影响，该示例显示限制，将文件限制设置为一个低得离谱的数字，然后超出它，导致程序被 `SIGXFSZ` 终止：

```c
int main(void)
{
    struct rlimit r;
    int fd;
    char buf[500] = { 0 };

    if (sizeof(rlim_t) > sizeof(long long))
        printf("Warning: rlim_t > long long; results may be wrong\n");
    ec_false( showlimit(RLIMIT_CORE, "RLIMIT_CORE") )
    ec_false( showlimit(RLIMIT_CPU, "RLIMIT_CPU") )
    ec_false( showlimit(RLIMIT_DATA, "RLIMIT_DATA") )
    ec_false( showlimit(RLIMIT_FSIZE, "RLIMIT_FSIZE") )
    ec_false( showlimit(RLIMIT_NOFILE, "RLIMIT_NOFILE") )
    ec_false( showlimit(RLIMIT_STACK, "RLIMIT_STACK") )
#ifdef FREEBSD
    ec_false( showlimit(RLIMIT_AS, "RLIMIT_AS") )
#endif
    ec_negl( getrlimit(RLIMIT_FSIZE, &r) )
    r.rlim_cur = 500;
    ec_negl( setrlimit(RLIMIT_FSIZE, &r) )
    ec_negl( fd = open("tmp", O_WRONLY | O_CREAT | O_TRUNC, PERM_FILE) )
    ec_negl( write(fd, buf, sizeof(buf)) )
    ec_negl( write(fd, buf, sizeof(buf)) )
    printf("Wrote two buffers! (?)\n");
    exit(EXIT_SUCCESS);
}

EC_CLEANUP_BGN
    exit(EXIT_FAILURE);
EC_CLEANUP_END
```

```c
static bool showlimit(int resource, const char *name)
{
    struct rlimit r;

    ec_negl( getrlimit(resource, &r) );
    printf("%s: ", name);
    printf("rlim_cur = ");
    showvalue(r.rlim_cur);
    printf("; rlim_max = ");
    showvalue(r.rlim_max);
    printf("\n");
    return true;

    EC_CLEANUP_BGN
    return false;
    EC_CLEANUP_END
}

static void showvalue(rlim_t lim)
{
    /*
     * All macros may equal RLIM_INFINITY; that test
     * must be first; can't use switch statement.
     */
    if (lim == RLIM_INFINITY)
        printf("RLIM_INFINITY");
#ifdef BSD_DERIVED
    else if (lim == RLIM_SAVED_CUR)
        printf("RLIM_SAVED_CUR");
    else if (lim == RLIM_SAVED_MAX)
        printf("RLIM_SAVED_MAX");
#endif
    else
        printf("%llu", (unsigned long long)lim);
}
```

正如你从代码中可以看到的那样，FreeBSD 和 Darwin 没有实现整个过程。[^17]

[^17]: 脚注 17

这是我们在四个测试系统上得到的结果，从 Solaris 开始：

```
RLIMIT_CORE: rlim_cur = RLIM_INFINITY; rlim_max = RLIM_INFINITY
RLIMIT_CPU: rlim_cur = RLIM_INFINITY; rlim_max = RLIM_INFINITY
RLIMIT_DATA: rlim_cur = RLIM_INFINITY; rlim_max = RLIM_INFINITY
RLIMIT_FSIZE: rlim_cur = RLIM_INFINITY; rlim_max = RLIM_INFINITY
RLIMIT_NOFILE: rlim_cur = 256; rlim_max = 1024
RLIMIT_STACK: rlim_cur = 8683520; rlim_max = 133464064
RLIMIT_AS: rlim_cur = RLIM_INFINITY; rlim_max = RLIM_INFINITY
File Size Limit Exceeded - core dumped
```

### Linux
