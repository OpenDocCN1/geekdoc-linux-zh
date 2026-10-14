
```c
#include "tlpi_hdr.h"

int

main(int argc, char *argv[])

{

    int j;

    for (j = 0; j < argc; j++)

        printf("argv[%d] = %s\n", j, argv[j]);

    exit(EXIT_SUCCESS);

}
```

由于 `argv` 列表由 `NULL` 值终止，也可以以如下方式编写列表 6-2 中的程序体，以便每行输出一个命令行参数：

```c
char **argv;

for (p = argv; *p != NULL; p++)

    puts(*p);
```

`argc/ argv` 机制的一个局限性是，这些变量只能作为 `main()` 的参数可用。为了在其他函数可以使用命令行参数，我们必须将 `argv` 作为参数传递给这些函数，或者设置一个指向 `argv` 的全局变量。

有几种可以在程序的任何地方访问这些部分或全部信息的不可移植方法：

- 任何进程的命令行参数都可以通过 Linux 特有的 `/proc/PID/cmdline` 文件读取，每个参数都以空字节终止。程序可以通过 `/proc/self/cmdline` 访问自己的命令行参数。
- C 库提供了两个全局变量，可以在程序的任何地方使用，以获取调用程序时使用的名称（即第一个命令行参数）。其中第一个 `program_invocation_name`（`short_name`）提供了该名称的去除了任何目录前缀的版本（即路径的基准部分）。通过定义宏 `GNU_SOURCE`，可以从 `errno.h` 获取这两个变量的声明。

如图 6-1 所示，`argv` 和 `environ` 数组以及它们指向的字符串位于进程栈上方的单个连续内存区域中。我们将在下一节中描述 `environ`，它持有程序的环境列表。该区域可以存储的总字节数有一个上限。SuVS3 通过 `ARG_MAX`（定义在 `<limits.h>` 中）规定了该限制（或者通过调用 `sysconf(_ARG_MAX)`）。SuVS3 要求 `ARG_MAX` 至少为 `POSIX_ARG_MAX`（4096 字节）。大多数 Unix 实现的限制比这大得多。SuVS3 未规定实现是否将（终止空字节、对齐字节以及 `argv` 数组的指针）计算在 `ARG_MAX` 中。

在 Linux 上，`ARG_MAX` 在历史上固定为 32 页（即 x86 上为 131072 字节），并包含了开销空间。从内核 2.6.23 开始，用于 `argv` 和 `environ` 的总空间可以通过 `RLIMIT_STACK` 资源限制进行控制，并允许 `argv/environ` 具有更大的限制。该限制是 `exec()` 调用时软 `RLIMIT_STACK` 限制的四分之一。

许多程序（包括本文中的几个示例）使用 `getopt()` 库解析命令行选项（即以破折号开头的参数）。我们在附录 B 中描述 `getopt()`。

## 6.7 环境列表

每个进程都有一个名为环境列表的关联字符串数组，即环境。这些每一个字符串都是 `name=value` 格式的定义。因此，环境表示一组可以用于存储任意信息的键值对。列表中的名称是

并没有一个变量（对应 `argc`）来指定环境列表的大小。（出于类似的原因，我们没有对图 6-5 中环境数组的元素进行编号）。

### 列表 6-3：显示进程环境

```c
#include <tlpi_hdr.h>

extern char **environ;

int

main(int argc, char *argv[]) {

    char **ep;

    for (ep = environ; *ep != NULL; ep++)

        puts(*ep);

    exit(EXIT_SUCCESS);

}
```

访问环境列表的另一种方法是在 `main()` 函数中声明第三个参数：

```c
int main(int argc, char *argv[], char *envp[])
```

该参数可以像 `environ` 一样被处理，区别在于它的作用域限于 `main()`。尽管这一特性在 UNIX 系统上广泛实现，但由于它在作用域限制外 SUS3 中并未规定，因此应该避免使用。

`getenv()` 从进程环境中检索单个值。

```c
#include <stdlib.h>

char *getenv(const char *name);
```

返回指向（值）字符串的指针，若无变量则返回 NULL

给定环境变量的名称，`getenv()` 返回指向对应值字符串的指针。因此，在我们之前展示的示例中，如果将 `SHELL` 指定为名称参数，将返回 `/bin/bash`。如果不存在指定名称的环境变量，`getenv()` 返回 NULL。

使用 `getenv()` 时请注意以下可移植性考虑：

-   SUSv3 规定应用程序不应修改 `getenv()` 返回的字符串。这是因为（在大多数实现中）该字符串实际上是环境的一部分（即 `name=value` 字符串的 own部分）。如果我们需要更改环境变量的值，可以使用 `setenv()` 或 `putenv()` 函数（下文描述）。

-   SUSv3 允许 `getenv()` 的实现使用静态分配的缓冲区返回其结果，该缓冲区可能会被后续对 `getenv()`、`setenv()` 或 `unsetenv()` 的调用所覆盖。尽管 glibc 的 `getenv()` 实现没有以这种方式使用静态缓冲区，但需要处理由 `getenv()` 调用返回字符串的可移植程序，在随后调用这些函数之一之前，都应该将其复制到另一个位置。

### 修改环境

有时，进程修改其环境是有用的。一个原因是使更改在随后由该进程创建的所有子进程中可见。另一种可能性是，我们想要为加载到此进程内存中的（“execed”）新程序设置一个变量。从这个意义上说，环境不仅是进程间通信的一种形式，也是一种程序间通信的方法。（这一点在第 27 章将变得更加清晰，那里我们将解释 `exec()` 函数如何允许程序在同一进程中通过新程序替换自己。）

`putenv()` 函数向调用进程的环境中添加新变量，或修改现有变量的值。

```c
#include <stdlib.h>

int putenv(char *string);
```

成功时返回 0，或出错时返回非零

`string` 参数是一个指向 `name=value` 格式字符串的指针。在调用 `putenv()` 之后，该字符串将成为环境的一部分。换句话说，并不是复制 `string` 指向的字符串，`environ` 的元素之一将设置为指向与 `string` 相同的位置，因此，如果我们随后修改了 `string` 指向的字节，更改将影响进程环境。出于此原因，`string` 不应该是自动变量（即分配在栈上的字符），因为一旦定义该变量的函数返回，内存区域可能会被覆盖。

注意 `putenv()` 在出错时返回非零值，而不是 -1。glibc 的 `putenv()` 实现了一个非标准扩展。如果 `string` 不包含等号，则由 `string` 识别的环境变量将从环境列表中移除。

`setenv()` 函数是 `putenv()` 向环境中添加变量的替代方案。

```c
#include <stdlib.h>

int setenv(const char *name, const char *value, int overwrite);
```

成功时返回 0，或出错时返回 -1

`setenv()` 函数通过为 `name=value` 格式的字符串分配内存缓冲区来创建一个新的环境变量。（注：此处原文存在大量重复句子，翻译已按逻辑含义处理）

`unsetenv()` 函数从环境中移除由名称识别的变量。

```c
#include <stdlib.h>

unsetenv(const char *name);
```

成功时返回 0，或出错时返回 -1

## 示例程序

列表 6-4 展示了本节讨论的所有函数。在在清除环境后，该程序添加作为命令行参数提供的任何环境定义。然后它：如果环境中不存在名为 `GREET` 的变量，则添加该变量定义；移除任何名为 `BYE` 的变量定义；最后，打印当前的环境列表。这里是运行程序时产生的输出示例：

```
$ ./modify_env "GREET=Guten Tag" SHELL=/bin/bash BYE=Ciao

GREET=Guten Tag

SHELL=/bin/bash

./modify_env SHELL=/bin/sh BYE=byebye

SHELL=/bin/sh

GREET=Hello world
```

如果我们为 `environ` 分配 NULL（如列表 6-4 中 `clearenv()` 调用所示），那么我们预计如下形式的循环（在程序中使用）将会失败，因为 `*environ` 是无效的：

```c
```
