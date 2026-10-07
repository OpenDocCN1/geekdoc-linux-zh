
```c
#include <popt.h>

void popFreeContext(poptContext context);
void popResetContext(poptContext context);
```

## 24.1.3 解析命令行

在创建 `popContext` 后，它可以开始解析参数。`popGetNextOpt()` 执行实际的参数解析。

```c
#include <popt.h>

int popGetNextOpt(poptContext con);
```

该函数接收上下文作为唯一参数，解析下一个命令行。在选项表中找到下一个参数后，它会填充选项项的指针所指向的对象（如果它不为 NULL）。如果选项的 `val` 项非 0，函数将返回该值。否则，`popGetNextOpt()` 继续处理下一个参数。

`popGetNextOpt()` 在解析完参数时返回 -1，在发生错误时返回其他负值。这使得将 `val` 元素大于 0 是一个好主意。

如果所有的命令行选项都通过参数指针处理，命令行解析将简化为以下代码：

```c
rc = popGetNextOpt(popoptcon);
```

然而，许多应用程序比这更复杂的命令行解析，并使用以下结构。

```c
while ((rc = popGetNextOpt(popoptcon)) > 0) {
    switch (rc) {
        /* 在此处处理特定的参数 */
    }
}
```

当处理返回的选项时，应用程序需要知道指定选项之后的任何参数的值。有两种方法可以发现它们。一种是让 `popt` 通过选项表的 `arg` 元素向变量填充值；另一种是使用 `popGetNextOptArg()`。

# 第 24 章 解析命令行选项

```c
#include <popt.h>
```

```c
char * popgetOptArg(poptContext con);
```

此函数返回 `popgetNextOpt()` 返回的最后一个选项的参数，如果没有指定任何参数，则返回 NULL。

## 24.1.4 剩余参数

许多应用程序会接受任意数量的命令行参数，例如文件名列表。当 `popt` 遇到不以 `-` 开头的参数时，它认为该参数是一个值并将其添加到剩余参数列表中。三个函数允许应用程序访问此类参数：

- `char * popgetArg(poptContext con);`

此函数返回下一个剩余参数并将其标记为已处理。

- `char * poptPeekArg(poptContext con);`

返回下一个剩余参数但不将其标记为已处理。这允许应用程序在不修改列表的情况下，向前查看参数列表的内容。

- `char ** popgetArgs(poptContext con);`

以与 `argv` 相同的方式返回所有剩余参数。返回数组的最后一个元素指向 NULL，表示参数的结束。

## 24.2 错误处理

所有可能返回错误的 `popt` 函数都返回整数。当发生错误时，会返回一个负数错误代码。表 24.2 总结了可能发生的错误代码。以下是对每个错误更详细的讨论。

| 表 24.2 popt 错误 |

| 错误 | 描述 |

| :--- | :--- |

| `POPT_ERROR_NOARG` | 选项缺少参数。 |

| `POPT_ERROR_BADOPT` | 无法解析选项的参数。 |

| `POPT_ERROR_OPTSTOODDEEP` | 选项别名嵌套太深。 |

| `POPT_ERROR_BADQUOTE` | 引号不匹配。 |

| `POPT_ERROR_BADNUMBER` | 选项无法转换为数字。 |

| `POPT_ERROR_OVERFLOW` | 给定的数字太大或太小。 |

`POPT_ERROR_NOARG`

命令行上指定了一个需要参数的选项，但没有提供任何参数。此错误只能由 `poptGetNextOpt()` 返回。

`POPT_ERROR_BADOPT`

在 `arg` 中指定了一个选项表中不存在的选项。此错误只能由 `poptGetNextOpt()` 返回。

`POPT_ERROR_OPTSTOODDEEP`

一组选项别名嵌套太深。目前，`popt` 限制选项深度为 10 层以防止无限递归。只有 `poptGetNextOpt()` 可以返回此错误。

`POPT_ERROR_BADQUOTE`

解析后的字符串存在引号不匹配（例如单引号）。`poptParseArgString()`、`poptConfigFile()` 或 `poptReadDefaultConfig()` 可能会返回此错误。

`POPT_ERROR_BADNUMBER`

由于字符串包含非数字字符，从字符串到数字（int 或 long）的转换失败。发生在 `poptGetNextOpt()` 处理类型为 `POPT_ARG_INT` 或 `POPT_ARG_LONG` 的参数时。

`POPT_ERROR_OVERFLOW`

由于数字太大或太小，字符串到数字的转换失败。与 `POPT_ERROR_BADNUMBER` 类似，此错误发生在 `poptGetNextOpt()` 处理类型为 `POPT_ARG_INT` 或 `POPT_ARG_LONG` 的参数时。

`POPT_ERROR_ERRNO`

系统调用返回错误，且 `errno` 仍包含系统调用的错误。`poptReadConfigFile()` 和 `poptReadDefaultConfig()` 都可以返回此错误。

提供了两个函数，方便应用程序提供良好的错误信息。

```c
const char * poptStstrerror(const int error);
```

此函数接收一个 `popt` 错误代码并返回描述该错误的字符串，类似于标准的 `strerror()` 函数。

```c
char * poptBadOption(poptContext, int flags);
```

如果在 `poptNextOpt()` 期间发生错误，此函数将返回导致错误的错误的选项。如果 `flags` 参数设置为 `POPT_BADOPTION_NOALIAS`，则返回最外层的选项。否则，`flags` 应为 0，并返回可能可能通过别名指定的选项。

这两个函数使得大多数应用程序的 `popt` 错误处理变得非常简单。当从大多数函数中检测到错误时，会打印错误消息以及来自 `poptStstrerror()` 的错误字符串。在解析参数期间发生错误时，类似下面的代码将显示有错误信息。

```c
fprintf(stderr, "%s: %s\n",
        poptBadOption(optCon, POPT_BADOPTION_NOALIAS),
        poptStstrerror(rc));
```

## 24.3 选项别名

使用 `popt` 替代 `getopt()` 的主要优势之一是可以使用选项别名。这允许用户指定选项，当这些选项被指定时，`popt` 会将其展开为选项。如果 `grep` 程序使用 `popt`，用户可以在 `-i -n -E -2` 中添加 `--text` 选项，以便他们更容易在文本文件中查找信息。

### 24.3.1 指定别名

别名通常在两个地方指定：`/etc/popt` 和用户目录下的 `.pop` 文件（通过环境变量 `HOME` 找到）。这两个文件具有相同的格式，即任意数量的格式如下的行：

```
char * popgetArg(poptContext con);
```

此函数返回下一个剩余参数并将其标记为已处理。

```
char * poptPeekArg(poptContext con);
```

返回下一个剩余参数但不将其标记为已处理。这允许应用程序在不修改列表的情况下，向前查看参数列表。

```
char ** popgetArgs(poptContext con);
```

以与 `argv` 相同的方式返回所有剩余参数。返回数组的最后一个元素指向 NULL，表示参数的结束。

### 24.3.2 启用别名

一组选项别名嵌套太深。目前，`popt` 限制深度为 10 层以防止无限递归。只有 `poptGetNextOpt()` 可以返回此错误。

```c
struct poptAlias {
    char * longName;      /* 可以为 NULL */
    char * shortName;      /* 可以为 '\0' */
    int argc;
    char ** argv;         /* 必须可释放 */
};
```

前两个元素 `longName` 和 `shortName` 指定了别名选项。最后两个 `argc` 和 `argv` 定义了展开。

## 24.4 解析字符串

虽然 `popt` 通常用于解析已经分为 `argv` 风格数组的参数，但某些程序需要解析类似于命令行的字符串。为了方便，`popt` 提供了一个使用类似 shell 规则解析字符串的函数。

```c
#include <popt.h>
```

```c
int poptArgvString(char * s, int * argcPtr, char *** argvPtr);
```

`s` 被解析为 `argv` 风格的数组。指向第二个参数 `argcPtr` 的整数包含解析出的元素数量，指向最后一个参数的指针指向创建的数组。该数组是动态分配的，在应用程序在使用后应被释放。

## 24.5 处理额外参数

某些应用程序实现了选项别名的功能，但需要通过特殊逻辑来实现。`poptStuffArgs()` 函数允许应用程序向当前的 `poptContext` 插入新参数。

```c
#include <popt.h>

int poptStuffArgs(poptContext con, char ** argv);
```

传递的 `argv` 最后一个元素必须为 NULL 指针。下次调用 `poptGetOpt()` 时，“填充”参数将被首先解析。在耗尽所有填充参数后，`popt` 将返回普通参数。

## 24.6 示例应用程序

第 15 章第 274–281 页的示例应用程序 `Robin` 使用 `popt` 进行参数解析。它提供了如何使用 `popt` 库的良好示例。

`RPM` 是一个流行的 Linux 软件包管理程序，它大量使用了 `popt` 的特性。它的许多命令行参数通过 `popt` 别名实现，这使得 `RPM` 成为利用 `popt` 库的绝示例。有关 `RPM` 的更多信息，请参阅 `http://www.rpm.org`

## 运行时动态加载

在运行时加载共享对象（shared objects）是组织应用程序的一种实用方法。如果得当，它可以使应用程序具有可扩展性，并且强制你将代码划分为逻辑上独立的模块，这是一种非常有用的编码规范。

许多 Unix 应用（特别是大型应用）大部分由独立的代码块实现，这些块通常被称为插件或模块。在某些情况下，它们被实现为完全不同的程序，通过管道或其他形式的进程间通信（IPC）与应用程序内核进行通信。在其他情况下，它们被实现为共享对象。

这些共享对象可能是标准的对象文件，也可以像标准共享库一样构建（见第 7 章），但它们的使用方式完全不同。链接器从不会被告知这些共享对象的存在，它们在应用程序链接时并不需要存在。它们不需要像大多数共享库那样安装在系统上。它们使用的符号名称不需要是唯一的；事实上，这些符号名称通常是不唯一的。为同一接口编写的不同共享对象会使用相同名称的入口。对于普通共享库来说，这将是一个灾难；但对于运行时动态加载的共享对象来说，这是理所当然的。

运行时加载共享对象最常见的用途是为某些可能有许多不同实现的通用类型功能创建接口。例如，考虑保存图形文件。应用程序可能有一个内部格式来格式化其图形，但有许多它可能想要保存图形的文件格式，并且会不规则地创建更多格式 [Murray, 1996]。一个用于保存图形文件并导出到运行时加载的共享对象的通用接口，允许程序员在不重新编译应用程序的情况下为应用程序添加新的图形格式。如果接口有良好的文档支持，没有应用程序源代码的第三方也可以添加新的图形格式。

类似的用途是框架代码，它只提供接口而不提供实现。例如，`PAM`（可插验证模块）框架为挑战-响应验证方法（如用户名和密码）提供了一个通用接口。所有的验证都由模块完成，而选择在哪个应用程序中使用哪些验证模块是在运行时通过查询配置文件完成的，而不是在编译时。该接口定义良好且稳定，新模块可以随时丢入对应位置并使用，而无需重新编译框架或应用程序。框架作为共享库被加载，而该共享库中的代码负责加载和卸载提供验证方法的模块。

## 25.1 dl 接口

动态加载包括打开库、查找任意数量的符号、处理发生的任何错误以及关闭库。所有的动态加载函数都声明在一个头文件 `<dlfcn.h>` 中。

`dlerror()` 返回一个字符串，描述在其他动态加载函数中发生的最新错误。

```c
const char * dlerror(void);
```

每当它返回一个值时，它都会清除错误状态。在另一个错误状态产生之前，它将继续返回 `NULL` 而不是字符串。这种异常行为的原因在 `dlsym()` 函数的描述中详细说明。

`dlopen()` 打开一个库。这涉及找到库文件、打开文件并进行一些处理。环境变量和传递给 `dlopen()` 的选项决定了具体细节。

```c
void * dlopen (const char *filename, int flag);
```

如果 `filename` 是绝对路径（即以 `/` 字符开头），`dlopen()` 不需要搜索该库。这是在应用程序代码内部使用 `dlopen()` 的通常方法。如果 `filename` 是一个简单的文件名，`dlopen()` 在以下位置搜索该文件名库：

- 环境变量 `LD_ELF_LIBRARY_PATH` 中指定的冒号分隔的目录集；或者如果 `LD_ELF_LIBRARY_PATH` 不存在，则使用 `LD_LIBRARY_PATH`。

- 文件 `/etc/dl.so` 中指定的库。该文件由 `ldconfig` 程序生成，该程序列出了它在 [运行] 时在 `/etc/ld.so.conf` 中找到的所有库。

- `/usr/lib`

- `/lib`

如果 `filename` 为 `NULL`，`dlopen()` 打开当前可执行文件的实例。这只在极少数情况下有用。`dlopen()` 在失败时返回 `NULL`。

找到文件是 `dlopen()` 工作中最简单的部分；解析符号更为复杂。符号解析有两种根本上不同的类型：立即解析（immediate）和惰性解析（lazy）。立即解析会导致 `dlopen()` 在返回之前解析所有未解析的符号；惰性解析意味着符号解析是按需进行的。

如果大多数符号最终会被解析，那么执行立即解析会更高效。然而，对于具有许多未解析符号的库，解析符号花费的时间可能会被察觉；如果这显著影响了你的用户界面，你可能更倾向于惰性解析。整体效率的差异并不显著。

在开发和调试期间，你总是希望使用立即解析。如果你的共享对象有未解析的符号，你希望立即知道它们，而不是在程序在看似无关的代码中间崩溃时才发现。如果你不先用立即解析测试你的共享对象，惰性解析将成为难以复现的 bug 的来源。

如果你有依赖其他共享对象来提供某些符号的共享对象，情况尤为如此。`dlopen()` 函数返回一个共享对象的句柄（handle）。这是一个不透明句柄，你应该将其作为 `dlsym()` 和 `dlclose()` 的参数。如果一个共享对象被打开多次，`dlopen()` 每次都会返回同一个句柄，每次调用都会增加引用计数。

`dlsym()` 函数在库中查找符号。

```c
void * dlsym(void *handle, char *symbol);
```

`handle` 必须是 `dlopen()` 返回的句柄，`symbol` 是要查找符号的 NULL 结尾字符串。`dlsym()` 返回符号地址，如果发生致命错误则返回 `NULL`。在已知 `NULL` 不是正确地址的情况下（例如查找函数），可以通过检查它是否返回 `NULL` 来测试错误。但在更通用的情况下，某些符号可能为零并等于 `NULL`。在这种情况下，你需要查看 `dlerror()` 是否返回了错误。由于 `dlerror()` 在返回一次错误后就会恢复为 `NULL`，你应该使用如下代码：

```c
/* 清除尚未读取的错误状态 */
dlerror();
p = dlsym(handle, this_symbol);
if ((error = dlerror()) != NULL) {
  /* 错误处理 */
}
```

`dlclose()` 关闭一个库。

```c
void * dlclose(void *handle);
```

`dlclose()` 检查每次重复 `dlopen()` 调用增加的引用计数，如果为零，则关闭库。这种引用计数允许库对任意对象使用 `dlopen()` 和 `dlclose()`，而无需担心调用它的代码是否已经打开了这些对象。

### 25.1.1 示例

在第 7 章中，我们展示了一个普通共享库的示例。我们构建的共享库 `libhello.so` 也可以动态加载。`loadhello` 程序动态加载 `libhello.so` 并调用从该库加载的 `print_hello` 函数。

## 第 25 章 运行时的动态加载

以下是 `loadhello.c`：
