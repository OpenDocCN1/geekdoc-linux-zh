

顺便一提，只有当当前目录不在 PATH 环境变量中时，才需要在程序名称（区域）前添加 `./` 前缀。即使你的 PATH 包含当前目录，添加该前缀也无害。

## 编译 C++ 程序

GNU CC 是一个集成的 C 和 C++ 编译器，因此 gcc 命令也可以编译 C++ 源文件。GCC 使用文件扩展名来判断文件是 C 还是 C++。C 文件的扩展名为小写的 .c，而 C++ 文件则以 .C 或 .cpp 结尾。

虽然 gcc 命令可以编译 C++ 文件，但该命令不会自动链接 C++ 程序通常所需的各类类库。这就是为什么使用 g++ 命令编译和链接 C++ 程序很轻松，因为它实际上是以适当的选项运行 gcc。

假设你要编译一个存储在名为 hello.C 的文件中的简单 C++ 程序。（使用大写 C 扩展名作为 C++ 源文件的扩展名是惯例。）

```
#include <iostream>
int main()
{
using namespace std;
cout << "Hello from Linux!" << endl;
}
```

要将此程序编译和链接为名为 hello 的可执行程序，请使用以下命令：

g++ -o hello hello.C

该命令会创建 hello 可执行文件，你可以按以下方式运行它：

./hello

程序将显示以下输出：

Hello from Linux!

众多 GCC 选项控制着编译 C 和 C++ 程序的各个方面。

## 探索 GCC 选项

以下是 gcc 命令的基本语法：

```
gcc options filenames
```

每个选项都以连字符 (-) 开头，通常具有较长的名称，例如 `-funsigned-char` 或 `-ffinite-functions`。然而，许多常用选项较短，例如用于仅编译的 `-c`，以及用于生成调试信息的 `-g`（使用 GNU 调试器 gdb 调试程序时需要这些信息）。

你可以在终端窗口中键入以下命令查看所有 GCC 选项的摘要：

```
man gcc
```

然后你可以浏览常用的 GCC 选项。通常，你不需要显式提供 GCC 选项，因为默认设置对于大多数应用程序都是合适的。表 1-1 列出了你可能使用的一些 GCC 选项。

**表 1-1 常用 GCC 选项**

| 选项 | 含义 |
| :--- | :--- |
| -ansi | 仅支持 ANSI 标准 C 语法。（此选项禁用某些 GNU C 特有的功能，如 `__asm__` 和 `__typeof__` 关键字。）当与 g++ 一起使用时，仅支持 ISO 标准 C++。 |
| -c | 仅编译并生成目标文件 |
| -DMACRO | 定义宏，其值为字符串 "1" |
| -DMACRO=DEFN | 将宏定义为 DEFN，其中 DEFN 是某个文本字符串。 |
| -E | 仅运行 C 预处理器 |
| -fallow-single-precision | 以单精度执行所有数学运算 |
| -fpic-struct-return | 在内存中返回所有结构体和联合体值，而不是在寄存器中返回。（以这种方式返回值效率较低，但至少与其他编译器兼容。） |
| -fPIC | 生成适用于共享库的位置无关代码 (PIC) |
| -freg-struct-return | 在可能时，在寄存器中返回结构体和联合体值 |
| -g | 生成调试信息。（GNU 调试器可以使用这些信息。） |
| -I DIRECTORY | 搜索指定目录中通过使用 #include 预处理器指令包含的文件 |
| -L DIRECTORY | 搜索指定目录中的库 |
| -l LIBRARY | 在链接时搜索指定的库 |
| -mcputype | 针对特定处理器优化代码。（*cpptype* 可以取许多不同的值 - 一些常见的值包括 *i386, i486, i586, i686, pentium, pentiumpro, pentium2, pentium3, pentium4*。） |
| -O FILE | 生成指定的输出文件（用于指定可执行文件的名称） |
| -00 (两个零) | 不进行优化 |
| -O 或 -O1 (字母 O) | 优化生成的代码 |
| -O2 (字母 O) | 进行更多优化 |
| -O3 (字母 O) | 执行超出 `-O2` 范围的优化 |
| -Os (字母 O) | 针对大小进行优化（以减少代码总量） |
| -pedantic | 如果使用了任何非 ANSI 标准扩展，则生成错误 |
| -pg | 向程序添加额外代码，使其在运行时生成 *gprof* 程序可用来显示程序各部分计时详情的信息 |
| -shared | 生成共享对象文件（通常用于创建共享库） |
| -UNMACRO | 取消定义指定的宏 |
| -v | 显示 GCC 的版本号 |
| -w | 不生成任何警告消息 |
| -W1, OPTION | 将 *OPTION* 字符串（包含多个以逗号分隔的选项）传递给链接器。例如，要创建名为 *libXXX.so.1* 的共享库，请使用以下标志：`-W1,-soname,libXXX.so.1`。 |

## GNU make 实用工具

当应用程序由多个源文件组成时，手动键入 *gcc* 命令来编译和链接这些文件可能会非常繁琐。此外，你也不希望在更改单个源文件时重新编译每个文件。正是在这种情况下，*GNU make* 实用工具可以助你一臂之力。

*make* 实用工具通过读取和解释 *makefile* 来工作——*makefile* 是一个文本文件，描述了构建特定程序所需哪些文件，以及如何编译和链接这些文件来构建程序。每当更改一个或多个文件时，*make* 会确定需要重新编译哪些文件——并发出编译这些文件和重建程序的适当命令。

## Makefile 名称

默认情况下，GNU make 查找名为以下之一（按所示顺序）的 makefile：

- GNUmakefile
- makefile
- Makefile

在 UNIX 系统中，习惯使用 Makefile 作为 makefile 的名称，因为它出现在目录列表的开头附近，其中大写名称出现在小写名称之前。

当你从互联网下载软件时，你通常会找到 Makefile，以及源文件一起。要构建软件，你只需在 shell 提示符下键入 make，make 就会处理构建软件所需的所有步骤。

如果你的 makefile 没有标准名称（例如 Makefile），你必须使用 make 的 -f 选项来指定 makefile 名称。例如，如果你的 makefile 名为 myprogram.mk，你必须使用以下命令行运行 make：

```
make -f myprogram.mk
```

## The makefile

对于一个由多个源文件和头文件组成的程序，makefile 指定以下内容：

- make 创建的项目——通常是目标文件和可执行文件。常用术语 target 来指代 make 需要创建的任何项目。
- 创建 target 所需的文件或其他操作。
- 创建每个 target 时要执行哪些命令。

假设你有一个名为 form.C 的 C++ 源文件，其中包含以下预处理器指令：

```
#include "form.h"  // 包含头文件
```

目标文件 form.o 显然依赖于源文件 form.C 和头文件 form.h。除了这些依赖项之外，你还必须指定 make 如何将 form.C 文件转换为目标文件 form.o。假设你希望 make 调用 g++（因为源文件是 C++），并使用以下选项：

- -c (仅编译)
- -g (生成调试信息)
- -O2 (进行一些优化)

在 makefile 中，你可以用以下规则来表示这些选项：

```
# 这是 makefile 中的一行注释
# 以下行说明 form.o 如何依赖
# 于 form.C 和 form.h 以及如何创建 form.o。
form.o: form.C form.h
    g++ -c -g -O2 form.C
```

在此示例中，第一个非注释行显示 form.o 为 target，form.C 和 form.h 为依赖文件。

依赖项之后的行说明了如何从依赖项构建 target。此行必须以制表符（Tab）开头。否则，make 命令将退出并显示错误消息，你会抓耳挠腮，因为在文本编辑器中查看 makefile 时，你无法区分制表符和空格。既然你已经知道了这个秘密，解决方法就是用单个制表符替换有问题的行开头的空格。

使用 make 的好处是它可以防止不必要的编译。毕竟，你可以从 shell 脚本运行 g++（或 gcc）来编译和链接组成你应用程序的所有文件，但 shell 脚本会编译所有内容，即使编译是不必要的。另一方面，GNU make 仅在 target 的一个或多个依赖项自上次构建 target 以来发生了变化时才构建 target。make 通过检查 target 和依赖项的最后修改时间验证此更改。

make 将 target 视为要达成的目标名称；target 不必是文件。你可以有这样的规则：

```
clean:
    rm -f *.o
```

此规则指定了一个名为 clean 的抽象 target，它不依赖任何内容。这个依赖声明表示，为了创建 target clean，GNU make 调用命令 rm -f *.o，该命令删除所有具有 .o 扩展名的文件（即目标文件）。因此，创建名为 clean 的 target 的净效果是删除目标文件。

## 变量（或宏）

除了从依赖项构建 target 的基本功能外，GNU make 还包括许多实用功能，使您能够轻松表达从依赖项构建 target 的依赖项和规则。如果需要

