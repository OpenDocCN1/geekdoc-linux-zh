

# 176

# cpp

```cpp
#include <filename>
```

```cpp
# 在此位置读取 filename 的内容。这些数据将由 cpp 处理，就像它们是当前文件的一部分一样。当使用 <filename> 符号时，仅在标准包含目录中搜索 filename。更多详细信息请参见上文的 -I 和 -Y 选项。在指令行的最后一次 "or" 之后不允许出现任何额外的标记（tokens）。
```

```cpp
#line integer-constant "filename"
```

```cpp
为 C 编译器的下一次通过生成行控制信息。
integer-constant 被解释为下一行的行号，
filename 被解释为它所包含的文件。如果未给出 "filename"，则当前文件名保持不变。在可选的 filename 之后，指令行不允许出现任何额外的标记。
```

```cpp
#if constant-expression
```

```cpp
 仅当 constant-expression 产生非零值时，才在输出中包含直到匹配的 #else、#elif 或 #endif 指令后续行。所有二进制赋值运算符（包括 &&、||、=）在 constant-expression 中都是合法的。?: 运算符、一元运算符 ! 以及 - 运算符在 constant-expression 中也是合法的。
```

```cpp这些运算符的优先级与 C 语言相同。此外，定义的一元运算符可以通过以下两种形式用于 constant-expression 中：defined (name) 或 defined name。这允许在 #if 指令中实现 #ifdef 和 #endif 指令的效果。在 constant-expression 中仅使用 cpp  way已的运算符、整数常量和名称。特别是，运算符的大小（size of operator）并不
```

```cpp
#ifdef name
```

```cpp
 仅当 name 已经通过 #define 指令或 -D 选项被定义，且在没有中间插入的 #undef 指令的情况下，才在输出中包含直到匹配的 #else、#elif 或 #endif 指令后续行。指令行中 name 之后的额外标记将被静默忽略。
```

```cpp
#ifndef name
```

```cpp 仅当 name 未被定义，或者其定义已通过 #undef 指令移除时，才在输出中包含直到匹配的 #else、#elif 或 #endif 指令后续行。指令行中 name 之后不允许出现任何额外的标记。
```

```cpp
#elif constant-expression
```

```cpp
在 #if、#ifdef 或 #ifndef 指令与匹配的 #else 或 #endif 指令之间可以出现任意数量的 #if 指令。仅当所有条件成立时，才在输出中包含 #elif 指令后的行。
```

# cpp 177

- 前一个 #if 指令中的 constant-expression 值为零，前一个 #ifdef 中的 name 未定义，或者前一个 #ifndef 指令中的 name 已经定义。
- 所有中间 #elif 指令中的 constant-expression 的值均为零。
- 当前表达式的值为非零。如果 constant-expression 的值为非零，则忽略直到匹配的 #endif 的后续 #elif 和 #else 指令。在 #if 指令中允许的任何 constant-expression 在 #elif 指令中都是允许的。

- #else 反转当前生效的条件指令的含义。如果之前的条件指示这些行被包含，则忽略 #else 和匹配的 #endif 之间的行。如果之前的条件指示这些行被忽略，则在输出中包含后续行。你可以嵌套条件指令和相应的 #else 指令。

- #endif 结束由条件指令 #if、#ifdef 或 #ifndef 开始的行段。每个此类指令都必须有一个匹配的 #endif。

被包含文件的标准目录在不同环境中可能不同，使用以下形式的 #include：#include <file.h>

而不是使用带有绝对路径的格式，例如：#include "/usr/include/file.h"

cpp 会对使用绝对路径发出警告。

> 注意 — 虽然编译器允许 8 位字符串和注释，但在其他地方都不允许 8 位。

# 宏

宏的形式化参数在 #define 指令体中会被识别，即使它们出现在字符常量和引号字符串内部。例如，从以下代码的输出：#define abc(a) ||a| abc (xyz)

```
输出为：
# 1 ""
|'xyz|
```

第二行是一个换行符。最后七个字符是 |xyz|（竖线、反引号、竖线、x、y、z、竖线）。在常规扫描期间，字符常量或引号字符串内部不会被识别为宏名。因此：

```cpp
#define abc xyz
printf("abc");
```

不会在第二行中展开 abc，因为它位于一个引号字符串内部，而该字符串不是 #define 宏定义的一部分。
在处理 #define 或 #undef 时，宏不会展开。因此：

```cpp
#define abc zingo
#define xyz abc
#undef abc
```

xyz
产生 abc。紧接在 #ifdef 或 #ifndef 之后的标记不会被展开。
在确定另一个宏调用的实际参数的扫描期间，宏不会展开。因此：

```cpp
#define reverse(first,second)second hello
#define greeting hello
reverse(greeting,
#define greeting goodbye
)
```

产生
#define hello goodbye hello

在 cpp 之前的某些版本中，当为待展开宏的参数列表中发现换行符时，换行符会按照发现它们的方式被输出并展开。当前 cpp 版本将它们替换为空格字符。

# 输出

指示后续输出行的原始源行号和文件名，以及这是否为进入包含文件后的第一行（level=1）。

# 目录搜索

被包含文件的标准目录在不同环境中可能不同，使用以下形式的 #include：#include <file.h>

而不是带有绝对路径的，例如：#include "/usr/include/file.h"

cpp 会对使用绝对路径发出警告。

# 特殊名称

在使用命令时，可以使用这些特殊名称：
- __LINE__ 被定义为行号。
- __FILE__ 被定义为文件名。
- __ARCH__ 被定义为架构。
- __STD__ 被定义为标准。
- __STDE__ 被定义为扩展。
- __LINE__ 被定义为行号。
- __FILE__ 被定义为文件名。
- __func__ 被定义为函数名。
- __LINE__ 被定义为转换单元。
- __LINE__ 被定义为行号。

# 换行符

在 cpp 之前的某些版本中，当为展开宏的参数列表中发现换行符时，换行符会按照发现它们的方式被输出并展开。当前 cpp 版本将它们替换为空格字符。

# 注释

虽然编译器允许 8 位字符串和注释，但在其他地方都不允许 8 位。

# 退出状态

- 0成功完成。
- 非零 发生错误。

# 属性

参见 attributes(5) 获取以下描述：

| 属性类型 | 属性值 | 可性 |
| :--- | :--- | :--- |
| 用户周期 | | 所有处理器 |
| 内核周期 | | 内核模式 |
| 系统周期 | | Solaris |

# 诊断

cpp 产生的错误信息旨在自明其。

# 概要

```
/bin/ctputrack -c eventspec [-c eventspec]... [-efvd] [-N count]
-o outfile] [-T interval] command [args]
```

# 180 描述

使用 ctputrack 命令可以使用 CPU 性能计数器监控进程或进程族的行为。当你使用 -t 选项指定间隔时，ctputrack 每秒采样。当你使用 -c 选项指定计数时，会对每个进程报告统计信息。当你未指定间隔或计数时，默认为秒。当你指定命令和可选参数时，ctputrack 执行该命令。或者，你可以使用 -p 选项指定现有进程的 ID。

由于 ctputrack 是非特权程序，它受到 truss(1) 的限制。例如，你无法跟踪 setuid(2) 执行文件。

# 选项

- -c eventspec：指定用于 CPU 性能计数器的事件集。你可以通过 -h 选项确定系统的可用事件列表和事件规范的语法。阅读 CPU 制造商的文档以确定这些事件规范的语义。语法参见 cpc_strtoevent(3PPC)。你可以指定多个 -c 选项在每次采样之间切换不同的事件设置。
- -D：启用调试模式。
- -e：跟踪所有的 exec(2)、execve(2)、fork(2)、fork1(2)、vfork(2) 系统调用。
- -h：打印关于如何使用命令以及如何对处理器相关的计数器的扩展帮助信息。
- -n：省略所有头部输出（如果 ctputrack 是管道的开头）。
- -N count：指定在退出前采集的最大 CPU 性能计数器采样数。
- -o outfile：指定用于 ctputrack 输出的文件。
- -p pid：将参数解释为附加并监控进程计数上下文的现有进程 ID。
- -T interval：指定 CPU 性能计数器采样之间的间隔，单位为秒。
- -v：启用更详细的输出。

