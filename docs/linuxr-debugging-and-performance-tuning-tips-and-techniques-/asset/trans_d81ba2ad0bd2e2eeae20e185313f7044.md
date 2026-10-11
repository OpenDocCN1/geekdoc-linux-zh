
## 15.4.2.2 优化调试缓冲区大小（推断的上下文）
*注意：提供的文本始于讨论中途。根据关于 `optimal_bufsize` 的内容，该章节标题很可能是“调试缓冲区大小问题”或类似内容，但由于输入中缺失，我将以逻辑方式格式化可用内容。*

长期以来，我们无法直接访问故障系统来运行 GDB。然而，我们最终设法复现了这个问题；事实证明，它与 gawk 用于读取数据文件的缓冲区大小有关：在故障系统上，缓冲区大小比我们在开发系统上的大。

我们需要一种方式在开发机上复现这个问题：故障系统与我们相隔九个时区，而跨大西洋交互运行 GDB 是非常痛苦的。我们通过让 `optimal_bufsize()` 查看一个特殊的环境变量 `AWKBUFSIZE` 来复现这个问题。当值为 "exact" 时，`optimal_bufsize()` 始终返回文件大小，无论其大小如何。如果 `AWKBUFSIZE` 的值是某个整数，该函数则返回该数字。否则，该函数回退到之前的算法。这使我们能够在不持续重新编译 gawk 的情况下运行测试。例如：

```
$ AWKBUFSIZE=42 make check
```

这使用 42 字节的缓冲区大小运行 gawk 测试套件。（测试套件通过。）

以下是 `optimal_bufsize()` 的修改版本：

```c
/* optimal_bufsize --- determine optimal buffer size */
/*
 *
 * Enhance this for debugging purposes, as follows:
 *
 * Always stat the file, stat buffer is used by higher-level code.
 *
 * if (AWKBUFSIZE == "exact")
 * return the file size
 * else if (AWKBUFSIZE == a number)
 * always return that number
 * else
 * if the size is < default_blocksize
 * return the size
 * else
 * return default_blocksize
 * end if
 * endif
 *
 * Hair comes in an effort to only deal with AWKBUFSIZE
 * once, the first time this routine is called, instead of
 * every time. Performance, dontyaknow.
 */

size_t
optimal_bufsize(fd, stb)
int fd;
struct stat *stb;
{
    char *val;
    static size_t env_val = 0;
    static short first = TRUE;
    static short exact = FALSE;

    /* force all members to zero in case OS doesn't use all of them. */
    memset(stb, '\0', sizeof(struct stat));

    /* always stat, in case stb is used by higher level code. */
    if (fstat(fd, stb) == -1)
        fatal("can't stat fd %d (%s)", fd, strerror(errno));

    if (first) {
        first = FALSE;

        if ((val = getenv("AWKBUFSIZE")) != NULL) {
            if (strcmp(val, "exact") == 0)
                exact = TRUE;
            else if (ISDIGIT(*val)) {
                for (; *val && ISDIGIT(*val); val++)
                    env_val = (env_val * 10) + *val - '0';

                return env_val;
            }
        }
    } else if (! exact && env_val > 0)
        return env_val;
    /* else
        fall through */

    /*
     * System V, n. n < 4, doesn't have the file system block size in the
     * stat structure.  So we have to make some sort of reasonable
     * guess.  We use stdio's BUFSIZ, since that is what it was
     * meant for in the first place.
     */
#ifdef HAVE_ST_BLKSIZE
#define DEFBFLKSZ     (stb->st_blksize > 0 ? stb->st_blksize : BUFSIZ)
#else
#define DEFBFLKSZ     BUFSIZ
#endif

    if (S_ISREG(stb->st_mode)            /* regular file */
        && 0 < stb->st_size              /* non-zero size */
        && stb->st_size < DEFBFLKSZ      /* small file */
            ||  exact) {                 /* or debugging */
        return stb->st_size;             /* use file size */
    }
    return DEFBFLKSZ;
}
```

第 3-23 行的注释解释了该算法。由于搜索环境变量可能很昂贵，且只需执行一次，该函数使用几个静态变量在第一次调用时收集适当的信息。

第 42-54 行在函数第一次被调用时执行，且仅执行第一次。第 43 行通过将 `first` 设置为 `false` 来强制满足此条件。第 45-54 行处理环境变量，查找 "exact" 或数字。在后一种情况下，它将字符串值转换为十进制数，并将其保存在 `env_val` 中。（我们当时可能应该在这里使用 `strtoul()`；当时我们没想到这一点。）

第 55 行在除第一次以外的每次执行时都会运行。如果给出了数值，条件将为真，并返回该值（第 56 行）。否则，它会落入函数的其余部分。

第 60-70 行定义了 `DEFBFLKSZ`；这部分没有改变。最后，第 72-76 行在适当时返回文件大小。如果不合适（第 78 行），则返回 `DEFBFLKSZ`。

我们确实修复了这个问题<sup>13</sup>，但在此期间，我们保留了新版本的 `optimal_bufsize()`，以便我们确信问题没有再次发生。

代码大小和复杂度的边际增加被我们目前拥有的用于测试的更大灵活性所抵消。此外，由于这是生产代码，让现场用户使用该功能进行测试以确定是否发生了类似问题是很方便的。（到目前为止，我们还没有要求进行测试，但知道如果我们必须处理这种情况时能够应对，这是很不错的。）

### 15.4.2.3 添加日志代码

经常会有这样的情况：你的应用程序正在一个无法使用调试器的系统上运行（例如在客户现场）。在这种情况下，你的目标是能够检查程序的内部状态，但必须从外部进行。做到这一点的唯一方法是让程序本身为你生成这些信息。

有多种方法可以做到这一点：

-   始终将信息记录到特定文件。这是最简单的：程序始终写入日志信息。然后你可以随时查看该文件。

缺点是，在某个时刻，日志文件将消耗所有可用的磁盘空间。因此，你应该拥有多个日志文件，让程序定期切换到新文件。

Brian Kernighan 建议按星期几命名日志文件：`myapp.log.sun`、`myapp.log.mon` 等。这里的优点是你不必手动将旧文件移开；你可以免费获得一周的日志文件。

-   仅当日志文件已存在时才写入日志文件。当程序启动时，如果日志文件存在，它会将信息写入日志。否则，它不会写入。若要启用日志记录，首先创建一个空的日志文件。
-   使用固定格式的消息，这种格式可以轻易被 awk 或 Perl 等脚本语言解析，用于生成摘要和报告。
-   或者，生成某种形式的 XML，它是自描述的，并且可能可以转换为其他格式。（我们并不是 XML 的大粉丝，但这不应阻碍你。）
-   使用 `syslog()` 进行日志记录；日志消息的最终去向可以由系统管理员控制。（`syslog()` 是一个相当高级的接口；参见 `syslog(3)` manpage。）

当然，选择如何记录信息是容易的部分。困难的部分是选择记录什么。与程序开发的各个部分一样，在编码之前深思熟虑是值得的。记录关于关键变量的信息。检查它们的值，确保它们在范围内或符合你的预期。记录异常情况；如果发生了不该发生的事情，记录它，并在可能的情况下继续运行。

关键在于只记录你需要用于追踪问题的信息，不多也不少。

### 15.4.2.4 运行时调试文件

在以前的职业生涯中，我们曾为一家初创公司工作，该公司的产品二进制可执行文件安装在客户现场。无法将调试器附加到正在运行的程序副本上，也无法在客户的系统上从调试器运行该程序。产品的主要组件不是直接从命令行启动的，而是通过 shell 脚本间接启动的，这些脚本进行了大量的初始设置。

## 15.4 为调试编程

为了使程序开始生成日志信息，我们提出了特殊调试文件的想法。当特定名称的文件存在于特定目录中时，程序会向日志文件生成信息消息，然后我们可以下载并分析该日志文件。这样的代码看起来像这样：

```c
struct stat sbuf;
extern int do_logging;     /* initialized to zero */

if (stat("/path/to/magic/.file*", &sbuf) == 0)
    do_logging = 1;
...
if (do_logging) {
    logging code here: open file, write info, close file, etc.
}
```

*注意：原文中的 `do_logging = "TRUE";` 很可能是 C 上下文中布尔值赋值的 OCR 错误，通常表示为 1 或 TRUE 常量。我将保留原始意图，但根据注释 "initialized to zero" 将语法更正为有效的类 C 伪代码。*

对 `stat()` 的调用发生在程序处理的每个作业中。因此，我们可以动态地启用和禁用日志记录，而无需停止并重启应用程序！

与调试选项和变量一样，这一主题有无数种变体：启用记录不同子系统信息的不同文件，添加到调试文件本身的调试指令，等等。与所有功能一样，你应该规划所需的设计，然后干净利落地实现它，而不是在凌晨 3 点匆忙编写一些快捷但不完美的代码（不幸的是，这在初创公司中并不罕见）。

> **注意** 闪光的东西并不都是金子。特殊调试文件只是所谓“后门”技术的一个例子——开发者以未记录的方式操作程序的一种或多种途径，通常出于不良目的。在我们的案例中，后门完全无害。但一个不道德的开发者同样可以轻松安排生成并下载客户列表、人事档案或其他敏感数据的隐藏副本。仅凭这一原因，你就应该仔细思考这种技术是否适用于你的应用程序。

### 15.4.2.5 为断点添加特殊挂钩

通常，问题可能是可复现的，但只有在你程序首先处理许多兆字节输入数据之后才会发生。或者，虽然你可能知道程序在哪个函数中失败，但该故障仅在函数被调用数百次甚至数千次之后才会发生。

[^13]: 通过重写缓冲区管理代码！

