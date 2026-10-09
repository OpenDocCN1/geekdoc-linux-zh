

_SC_ATEXIT_MAX 未定义
这同样是可以接受的，因为该符号并不是 POSIX1990 的一部分，而 FreeBSD 所声称符合的正是 POSIX1990。这仅仅说明了检查符号是否已定义的重要性。（由于标准 C 规定 atexit 的最小值为 32，我们可以假设 FreeBSD 的数值也是 32，尽管这个数值来源于 C 标准，而非 sysconf。）

## 1.5.6 pathconf 和 fpathconf 系统调用

sysconf 仅用于检查系统级的选项和限制。其他依赖于你正在讨论的文件，为此有两个非常相似的函数，分别名为 fpathconf 和 pathconf：

**pathconf**—根据路径获取系统选项或限制
#include <unistd.h>

```c
long pathconf(
    const char *path, /* pathname */
    int name          /* option or limit name */
);
/* Returns option/limit value or -1 (sets errno on error) */
```

**fpathconf**—根据文件描述符获取系统选项或限制
#include <unistd.h>

```c
long fpathconf(
    int fd,   /* file descriptor */
    int name  /* option or limit name */
);
/* Returns option/limit value or -1 (sets errno on error) */
```

这两个函数接受相同的第二个参数并返回相同的结果；当你有一个打开的文件时，使用 fpathconf；当你有一个文件的路径名（该文件可能已打开也可能未打开）时，使用 pathconf。name 的有效值在 [SUS2002] 或你系统的手册页中。

返回值的解释与 sysconf（前一节）相同。特别是，只有当 errno 发生变化时，-1 才意味着错误，因此你在调用之前必须将其设置为零。我们在第 1.5.4 节中展示了使用 pathconf 的代码。

### 1.5.7 confstr 系统调用

*confstr* 调用类似于 *sysconf*，但它用于字符串值，而非数值：

![](img/41b4c8f6d6a5c349eee321a301703d97_67_0.png)

当你进行调用时，将 *len* 设置为你作为 *buf* 参数传入的缓冲区大小；在输出时，它会用 NUL 终止的字符串填充缓冲区，如果整个字符串放不下则进行截断。返回值为存放整个字符串所需的大小。如果返回 0，则 *errno* 指示了错误（如果它发生了变化）。如果 *errno* 没有变化，则意味着 name 无效。因此，与前几个函数一样，你必须在调用前将 *errno* 设置为零。

### 1.5.8 检查特定的操作系统

以 POSIX/SUS 的方式检查功能是最好的，但有时你确实需要知道是否正在 Solaris、HP/UX、AIX、FreeBSD、Darwin、Linux 或其他系统上。有时你甚至需要知道主版本号和次版本号。我们已经看到了一个这是合理的案例：我们不希望在 FreeBSD 或 Darwin 系统上定义 _POSIX_SOURCE。其他情况是操作系统存在 bug，或者具有超出其声称符合的标准的功能（例如 System V 消息，见下一节）。

没有可移植的方法来检查操作系统，并且在某些系统（例如 Solaris）上，甚至没有非可移植的方法。在大多数系统上，一旦包含特定的头文件，可能会设置一个符号，但我们希望非常早期就获得该指示，甚至在我们包含 unistd.h（通常应该是第一个包含的 POSIX 或标准 C 头文件）之前。因此，我们在编译时设置一个符号，确保每个系统都不同，如下所示：

```bash
gcc -DSOLARIS -c xyz.c
```

实际上，我们的命令行比这更复杂，并且它们位于 makefiles 中，但你明白了其意图。

### 1.5.9 附加功能

像 FreeBSD 和 Darwin 这样的系统在声称符合 POSIX 时相当保守，但它们比纯 POSIX 1988 或 POSIX1990 系统要完善得多，后者既不包含套接字式网络，也不包含 System V IPC。FreeBSD 具有这些功能，它们大多按预期工作，此外还有更多功能。[19]

操作系统无法同时设置一个 POSIX 级别和一个指示其具有附加功能的选项符号，因为 (1) 一些功能（如我列出的那些）在 SUS3（即 POSIX2001，如果你愿意的话）之前的任何 POSIX 标准中都不存在，以及 (2) 在 SUS3 中，它们不是可选的，所以没有为它们定义符号。FreeBSD 不能通过声称符合，比如说，SUS1 来解决这个问题，因为它并不符合。

与此同时，我们当然不希望将针对 FREEBSD 符号的测试遍布我们的代码中，因为这不是我们的本意：我们的意思是“套接字”或“System V IPC”。随意的操作系统依赖性使得移植代码（特别是对于不同的程序员）变得困难，因为移植者完全不知道你在基于操作系统的测试中想要表达什么观点。将代码移植到 Linux 的人可能是 Linux 专家，但对于 FreeBSD 的特性可能一无所知。

因此，我们需要为我们所谓的附加功能发明更多的符号：那些在某处是标准的，但不属于操作系统声称符合的标准中的功能。我们将在进展中引入这些符号，你有时会在示例程序中看到它们，代码可能如下所示：

```c
#if (defined(_XOPEN_SOURCE) && _XOPEN_SOURCE >= 4) || defined(BSD_DERIVED)
#define HAVE_SYSVMSG
#endif
```

我们的公共头文件（见下一节）如果在定义了 `FREEBSD` 或 `DARWIN` 时定义 `BSD_DERIVED`，正如第 1.5.8 节中解释的那样。

> [19] Darwin 6.6，即 Mac OS X 10.2.6 中的版本，缺少 System V 消息，尽管它具有其他 System V IPC 功能。

你可以把我们正在做的事情理解为“部分符合”这一概念的形式化，这个概念会让标准制定者感到不适，但操作系统实现者和应用程序编写者认为它是必不可少的。

## 1.6 公共头文件

本书中的所有示例都包含公共头文件 defs.h，其中包含我们对 SUS_SUS2 的请求以及对 suvreq.h 的包含，我在第 1.5.3 节中谈到了这一点。它还包含我们通常需要的许多标准头文件；我们不担心如果程序不需要所有这些而包含多余的内容。其他不太常见的头文件我们在需要时包含。这里我不展示它，但 defs.h 还包含像 syserrmsg（第 1.4.1 节）这样的实用函数的原型。下面是 defs.h 的大部分内容，至少是编写本书时的样子；最新版本在网站上 [AUP2003]：

```c
#if defined(FREEBSD) || defined(DARWIN)
#define BSD_DERIVED
#endif

#if !defined(BSD_DERIVED) /* POSIX_SOURCE too restrictive */
#define SUV_SUS2
#include "suvreq.h"
#endif

#ifdef _GNU_
#define _GNU_SOURCE /* bring GNU as close to C99 as possible */
#endif

#include <unistd.h>

#ifdef __cplusplus
#include <stdbool.h> /* C99 only */
#endif
#include <sys/types.h>
#include <time.h>
#include <limits.h>
#ifdef SOLARIS
#define _VA_LIST /* can't define it in stdio.h */
#endif
#include <stdio.h>
#ifdef SOLARIS
#undef _VA_LIST
#endif
#include <stdarg.h> /* this is the place to define _VA_LIST */

#include <stdlib.h>
#include <stddef.h>
#include <string.h>
#include <ctype.h>
#include <errno.h>
#include <fcntl.h>
#include <assert.h>
#include <ec.h>
```

位于下方约三分之二的 `#ifdef SOLARIS` 部分是关于为什么有时需要操作系统相关代码的完美示例。对于“va”宏（用于 C 中的可变参数列表）是放在 stdio.h 还是 stdarg.h 中存在分歧，并且 Solaris 上的 gcc 与其他系统处理方式不同。因此，我使用了一个小技巧来有效地禁用 stdio.h 中的定义。这并不美观，且值得努力避免，但有时别无他法，你需要继续你的工作。

包含顺序有点奇怪，可能可以部分按字母顺序排列，但在几种情况下，我发现了顺序依赖关系，不得不稍微调整一下，以便在我尝试的所有系统上获得干净的编译。你看到的内容是最终结果。通常不应有顺序依赖关系，因为头文件应该包含它所依赖的其他头文件，但确实存在。

## 1.7 日期和时间

UNIX 中常用两种时间：*日历时间* 和 *执行时间*。本节包括用于获取时间和操纵时间的系统调用和函数。还可以设置间隔定时器；它们在 9.7 节中讨论。

### 1.7.1 日历时间

日历时间用于文件的访问、修改和状态变更时间，用于记录用户登录时间，用于显示当前日期和时间等。

日历时间通常有四种形式之一：

- 算术类型 `time_t`，它是自 *epoch* 以来的秒数，传统上设定为 1970 年 1 月 1 日午夜

