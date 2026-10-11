
第一个参数 `name` 仅用于别名处理（后文将讨论）。它应该是正在解析选项的应用程序的名称，或者在不需要选项别名时设为 `NULL`。接下来的两个参数指定了要解析的命令行参数。这些参数通常是按照它们传递给程序 `main()` 函数的方式原样传递给 `popGetContext()` 的。`options` 参数指向命令行选项表，该表在上一节中已描述。最后一个参数 `flags` 目前没有使用，但为了与 pop 库的未来版本兼容，应始终将其指定为 `0`。

`popContext` 跟踪哪些选项已经解析，哪些仍然剩余等信息。如果程序想要重启一组参数的选项处理，可以通过将上下文作为唯一传递传递 `popResetContext()` 来重置 `popContext`。

当参数处理完成后，应该释放 `popContext`，因为它包含了动态分配的组件。`popFreeContext()` 函数接收 `popContext` 作为其唯一参数，并释放上下文正在使用的资源。

以下是 `popResetContext()` 和 `popFreeContext()` 的原型。

```c
#include <pop.h>
```

```c
void popFreeContext(popContext con);
void popResetContext(popContext con);
```

## 24.1.3 解析命令行

应用程序创建 `popContext` 之后，它就可以开始解析参数。`popGetNextOpt()` 执行实际的参数解析。

```c
#include <popt.h>
```

```c
int popGetNextOpt(poptContext con);
```

该函数以上下文作为唯一参数，解析找到的下一个命令行参数。在选项表中找到下一个参数后，如果选项表的 `arg` 条目不为 `NULL`，则函数将填充该条目指向的对象。如果选项的 `val` 条目非 0，则函数随后返回该值。否则，`popGetNextOpt()` 继续执行到下一个参数。

`popGetNextOpt()` 在解析完最后一个参数时返回 `-1`，在发生错误时返回其他负值。因此，将选项表中的 `val` 元素保持大于 0 是一个好主意。

如果所有的命令行选项都通过 `arg` 指针处理，命令行解析将简化为以下行代码：

```c
rc = popGetNextOpt(poptcon);
```

然而，许多应用程序需要比这更复杂的命令行解析，并使用以下结构：

```c
while ((rc = popGetNextOpt(poptcon)) > 0) {
  switch (rc) {
    /* 在此处处理特定参数 */
  }
}
```

在处理返回的选项时，应用程序需要知道指定在选项之后的任何参数的值。这里有两种方法可以发现它们。一种是要求 pop 通过选项表的 `arg` 条目将选项的值填充到变量中。另一种是使用 `poptGetOptArg()`。

```c
#include <popt.h>
char * poptGetOptArg(poptContext con);
```

此函数返回 `poptGetNextOpt()` 返回的最后一个选项的给定的参数，如果没有指定参数则返回 `NULL`。

## 24.1 剩余参数 (Leftover Arguments)

许多应用程序接收任意数量的命令行参数，例如文件名列表。当 `popt` 遇到不以 `-` 开头的参数时，它假设该参数此类此类并将其添加到剩余参数列表中。三个函数允许应用程序访问此类参数：

```c
char * poptGetArg(poptContext con);
```
此函数返回下一个剩余参数并将其标记为已处理。

```c
char * poptPeekArg(poptContext con);
```
返回下一个剩余参数但不将其标记为已处理。这允许应用程序预读参数列表，而不修改该列表。

```c
char ** poptGetArgs(poptContext con);
```
所有剩余参数将以与 `argv` 相同的方式返回。返回数组的最后一个元素指向 `NULL`，表示参数的结束。

## 24.2 错误处理

所有可能返回错误的 `popt` 函数都返回整数。当发生错误时，会返回负错误代码。表 24.2 总结了发生的错误代码。这里是对每个错误的更详细的讨论。

### 表 24.2 popt 错误

| 错误 | 描述 |
|--- | --- |
| POPT_ERROR_NOARG | 选项缺少参数。 |
| POPT_ERROR_BADOPT | 无法解析选项的参数。 |
| POPT_ERROR_OPTOODEEP | 选项别名嵌套太深。 |
| POPT_ERROR_BADQUOTE | 引号不匹配。 |
| POPT_ERROR_BADNUMBER | 无法解析选项。 |
| POPT_ERROR_OVERFLOW | 数字太大或太小。 |
| POPT_ERROR_NOARG | 命令行上指定了一个需要参数的选项，但没有提供任何参数。 |
| POPT_ERROR_BADOPT | argv 中指定了一个选项表中不存在的选项。 |
| POPT_ERROR_OPTOODEEP | 选项别名嵌套太深。目前 popt 仅遵循 10 层以防止递归。 |
| POPT_ERROR_BADQUOTE | 解析的字符串有引号不匹配（如引号）。 |
| POPT_ERROR_BADNUMBER | 从字符串到数字的转换失败，因为字符串包含非数字字符。 |
| POPT_ERROR_OVERFLOW | 字符串到数字转换失败，因为数字太大或太小。 |
| POPT_ERROR_ERRNO | 系统调用返回错误，errno 包含系统错误。 |

提供了两个函数便于应用程序提供良好的错误消息。

```c
const char * popStrrerror(const int error);
```

此函数接收一个 popt 错误代码并返回字符串，就像标准的 `strerror()` 函数一样。

```c
char * poptBadOption(poptContext con, int flags);
```

如果在 `poptGetOpt()` 期间发生错误，此函数返回导致错误的选项。如果标志 `POPT_BADOPTION_NOALIAS`，则返回最外层的选项。否则，标志应为 `0`，返回的选项可能是通过别名指定的。

这两个函数使得大多数应用程序的 popt 错误处理变得简单。当从大多数函数检测到错误时，会带有来自 `poptStrrerror()` 的错误字符串打印错误消息。在参数解析期间发生错误时，类似下面的代码将显示用的错误消息。

```c
fprintf(stderr, "%s: %s\n",
poptBadOption(poptcon, POPT_BADOPTION_NOALIAS),
poptStrrerror(rc));
```

## 24.3 选项别名 (Option Aliasing)

使用 `popt` 相比 `getopt()` 的主要优势之一是可以使用选项别名。这允许用户指定选项，这些选项在指定时会被 `popt` 展开为其他选项。如果标准的 `grep` 程序使用 `popt`，用户可以添加一个文本选项，将其扩展为 `-i E -2`，以便更方便地在文本文件中查找信息。

## 24.3.1 指定别名

别名通常在两个地方指定：`/etc/popt` 和用户主目录下的 `.pop` 文件（通过 `HOME` 环境变量找到）。这两个文件具有相同的格式，由任意数量的如下格式行组成：

```
classname alias newoption expansion
```

`appname` 是应用程序的名称，必须与传递给 `popGetContext()` 的 `name` 参数相同。这允许每个文件为多个程序指定别名。`alias` 关键字表示正在定义一个别名；目前 `popt` 配置文件仅支持别名，但未来可能会添加其他功能。下一个选项是要设置别名的选项，它可以是短选项也可以是长选项。该行的其余部分指定别名的扩展内容。它的解析方式类似于 shell 命令，允许使用 `,`、`"` 和 `'` 进行引号引用。如果反斜杠 `\` 是行的最后一个字符，则文件的下一行被认为是包含反斜杠行的逻辑延续，如下所示：

下面的条目将为 `grep` 命令添加 `--text` 选项，正如本节开头建议的那样。

```
grep alias -i -n -E -2
```

## 24.3.2 启用别名

应用程序在第一次调用 `popGetNextArg()` 之前，必须为 `poptContext` 启用别名扩展。有三个函数为上下文定义别名。

```c
int poptReadDefaultConfig(poptContext con, int flags);
```
