
如果它指定了一个未识别的错误号，`strerror()` 返回形如 `Unknown error nnn` 的字符串。对于其他实现，在这种情况下 `strerror()` 返回 `NULL`。

由于 `perror()` 和 `strerror()` 函数是区域设置敏感的（第 10.4 节），错误描述以本地语言显示。

### 通过库函数处理错误

各种库函数返回不同的数据类型和不同的值来指示失败。（查看每个函数的函数页。）库函数可以分为：

- 某些库函数在错误时返回 `-1`，但仍设置 `errno` 以指示错误。例如，`fopen()` 在错误时返回 `NULL`，此时可以使用 `perror()` 或 `strerror()` 来诊断错误。
- 其他库函数不使用 `errno`。这种函数是 `remove()`，它以与系统调用相同的方式删除文件（使用 `unlink()`）或目录（使用 `rmdir()`）。

## 3.5 示例程序

在本节中，我们描述了示例程序常用的约定和特性。

### 3.5.1 命令行选项和参数

许多示例程序依赖命令行选项和参数来确定行为。传统的 UNIX 命令行选项由连字符、标识选项的字母和一个可选参数组成。（GNU 工具提供了双连字符、标识字符串和参数。）为了解析这些，我们使用标准的 `getopt()` 函数（见附录 B）。

我们的具有复杂命令行语法的程序都提供了简单的帮助功能：如果使用 `--help` 选项调用，程序将显示语法。

### 3.5.2 通用函数和头文件

大多数示例程序包含一个常用定义的头文件，并且使用一组常用函数。我们在本节中讨论头文件和函数。

#### 通用头文件

列表 3-1 是书中每个程序使用的头文件。该头文件包含了许多程序所需的头文件，定义了 Boolean 类型，并定义了计算两个数值的最小值和最大值的宏。使用此头文件使我们的示例程序变得简洁一些。

列表 3-1: 大多数程序使用的头文件

```
#ifndef TLPI_HDR_H
#define TLPI_HDR_H      /* 防止重复包含 */

#include <sys/types.h>    /* 许多程序的类型定义 */
#include <stdio.h>         /* 标准 I/O 函数 */
#include <stdlib.h>        /* 常用库函数的原型，加上 EXIT_SUCCESS 和 EXIT FAILURE 常量 */
#include <unistd.h>        /* 许多系统用的原型 */
#include <errno.h>         /* 定义 errno 并定义错误常量 */
#include <string.h>        /* 常用的字符串处理函数 */

#include "get_num.h"       /* 声明我们的用于数值参数的函数 (getint(), getlong()) */

#include "error_functions.h" /* 声明我们的错误处理函数 */
typedef enum { FALSE, TRUE } : Boolean;

#define min(m,n) ((m) < (n) ? (m) : (n))
#define max(m,n) ((m) > (n) ? (m) : (n))

#endif
```

#### 错误诊断函数

为了简化程序中的错误处理，我们使用了列表 3-2 中声明的错误诊断函数。

##### 列表 3-2：常用错误处理函数的声明

```
lib/error_functions.h
#ifndef ERROR_FUNCTIONS_H
#define ERROR_FUNCTIONS_H

void errMsg(const char *format, ...);
#ifdef __GNUC__
#

/* 此宏防止当我们使用以下函数终止 main() 或其他非空函数时，
'gcc -Wall' 报出“控制流到达非空函数的末尾”的警告。 */

#define NORETURN __attribute__ (__noreturn))
#else
#define NORETURN
#endif
)

void errExit(const char *format, ...) NORETURN;

void err_exit(const char *format, ...) NORETURN;

void errExitEN(int errnum, const char *format, ...) NORETURN;

void fatal(const char *format, ...) NORETURN;

void usageErr(const char *format, ...) NORETURN;

void cmdLineErr(const char *format, ...) NORETURN;

#endif
```

为了诊断来自系统调用和库函数的错误，我们使用 `errMsg()`、`errExit()`、`err_exit()` 和 `errExitEN()`。

```
#include "tlpi_hdr.h"

void errMsg(const char *format, ...);
void errExit(const char *format, ...);
void err_exit(const char *format, ...);
void errExitEN(int errnum, const char *format, ...);
```

`errMsg` 函数在标准错误输出上打印消息。其参数列表与 `printf()` 相同，不同在于输出字符串末尾会自动附加一个换行符。`errMsg` 函数会打印当前 `errno` 值对应的错误文本——这包括错误名称（如 `EPERM`）以及由 `strerror` 返回的错误描述——紧跟在参数列表中指定的格式化输出之后。

`errExit()` 函数的操作与 `errMsg()` 相似，但它还会终止程序。它通过调用 `exit()`，或者如果环境变量 `EF_DUMPCORE` 被定义为非空字符串值，则调用 `abort()` 生成一个核心转储文件（core dump）供调试器使用。（我们在第 22.1 节中解释核心转储文件）。

`err_exit()` 函数与 `errExit()` 相似，但在两个方面有所不同：

- 它在打印错误消息之前不会刷新标准输出。
- 它通过调用 `_exit()` 而不是 `exit()` 来终止进程。这会导致进程在不刷新 `stdio` 缓冲区或不调用退出处理程序的情况下终止。

关于 `err_exit()` 操作中这些差异的细节将在第 25 节变得更加清晰，在该节中我们将描述 `_exit()` 和 `exit()` 之间的区别，并考虑 `fork()` 创建的子进程对 `stdio` 缓冲区和处理器的处理。目前，我们只需注意到，如果我们使用创建一个因错误而需要终止进程的库函数，`err_exit()` 是很有用的。这种终止应该在不刷新子进程拷贝的父进程（即调用进程）`stdio` 缓冲区且不调用父进程建立的退出处理程序发生。

`errExitEN()` 函数与 `errExit()` 不同在于它不是打印当前 `errno` 值对应的错误文本，而是打印与参数 `errno` 给出的 `errname`（即 `EN` 后缀）对应的文本。

主要，我们在使用 POSIX 线程（pthreads）API 的程序中使用 `errExitEN()`。与传统的 UNIX 系统调用（在错误时返回 `-1`）不同，POSIX 线程函数通过返回一个错误码（即通常定义在 `errno` 中的类型正数）作为其函数结果来诊断错误。（POSIX 线程在成功时返回 `0`。）

我们可以使用如下所示的代码来诊断来自 POSIX 线程函数的错误：

```
errno = pthread_create(&thread, NULL, func, &arg);
if (errno != 0)
    errExit("pthread_create");
```

然而，这种方法是低效的，因为在线程程序中，`errno` 被定义为一个宏，展开后为返回返回可修改数值的函数。因此，每次使用 `errno` 都会导致一次函数调用。`errExitEN()` 允许我们编写以下代码的高效等效实现：

```
int s;
s = pthread_create(&thread, NULL, func, &arg);
if (s != 0)
    errExitEN(s, "pthread_create");
```

在 C 语言术中，左值（lvalue）是指引用存储区域的表达式。左值最常见的例子是变量的标识符。某些运算符也会产生值。如果 `p` 是指向存储区域的指针，那么 `*p` 就是一个左值。在 POSIX 线程 API 下，`errno` 被重新定义为返回线程安全存储区域的函数（见第 31.3 节）。

为了诊断其他类型的错误，我们使用 `fatal()`、`usageErr()` 和 `cmdLineErr()`。
