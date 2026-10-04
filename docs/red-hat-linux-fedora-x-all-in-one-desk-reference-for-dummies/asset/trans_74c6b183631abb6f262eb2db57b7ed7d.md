

# 探索 Fedora Core 中的软件开发工具

-   变量用于存储不同类型的数据。你可以将每个变量看作数据的一个占位符——类似于一个邮箱，有一个名称和一个用于存储数据的房间。该邮箱的内容就是它的值。

-   表达式通过操作符将变量结合起来。一个表达式可以相加几个变量；另一个可以提取字符串的某部分。

-   语句执行某些操作，例如给变量赋值或打印字符串。

-   流控制语句允许根据根据某些表达式的值，以不同的顺序执行语句。通常情况下，流控制语句包括 `for`、`do-while`、`while` 和 `if-else` 语句。

-   函数（也称为子程序或例程）允许你将一组语句分组并给它们起一个名称。此功能允许你通过调用代表这些语句的函数来执行这组相同的语句。通常，编程语言会提供许多预定义函数来执行诸如打开（并从文件中读取）等任务。

# 探索 Fedora Core 中的软件开发工具

Fedora 包含了这些传统的 UNIX 软件开发工具：

- 文本编辑器，如 `vi` 和 `emacs`，用于编辑源代码。（要了解更多关于 `vi` 的信息，请参阅第二部分第 5.5 节。）

- C 编译器，用于编译和链接用 C 语言编写的程序——C 是编写 UNIX 应用的首选语言（尽管现在程序员正转向 C++ 和 Java）。Fedora Core 包含了 GNU C 和 C++ 编译器。GNU 编译器被称为 GCC —— 它现在代表 GNU 编译器集（GNU Compiler Collection，请参见 `gcc.gnu.org` 中的描述）。

- `make` 工具，用于自动化软件构建过程——即将对象模块组合成可执行文件或库的过程。

- 调试器，用于调试程序。Fedora Core 包含了调试器 `gdb`。

- 版本控制系统，用于跟踪源文件的各种版本。Linux 使用 RCS（修订控制系统）和 CVS（当前版本系统）。现在，大多数开源项目使用 CVS 作为它们版本控制系统。

如果你在从配套的 DVD-ROM 安装 Fedora Core 时选择了“开发工具（Development Tools）”，这些工具就会自动安装。在接下来的几个章节中，我将简要描述如何使用这些软件开发工具为 Fedora Core 编写应用程序。

# 探索 Fedora Core 中的软件开发工具

## GNU C 和 C++ 编译器

Fedora Core 中最重要的软件开发工具是 GCC —— GNU 和 C++ 编译器。事实上，GCC 可以编译三种语言：C、C++ 和 Objective-C（一种为 C 语言增加了面向对象编程能力的语言）。你可以使用 `gcc` 命令来编译和链接 C 和 C++ 源文件。GCC 编译器支持 ANSI 标准，使得将任何 ANSI C 程序移植到 Linux 变得非常容易。此外，如果你曾在 UNIX 系统上用过 C 编译器，那么你会觉得如如归家。

## 使用 GCC

使用 `gcc` 命令调用 GCC。默认情况下，当你对源文件使用 `gcc` 命令时，GCC 会进行预处理、编译和链接，以创建一个可执行文件。然而，你可以使用 GCC 选项在中间阶段停止此过程。例如，你可能需要调用 `gcc -c` 选项来生成对象文件，但不执行链接步骤。

编译和链接 C 源文件非常简单。假设你想编译并链接一个由两个文件组成的简单程序。使用以下源代码完成此任务；它存储在 `area.c` 文件中，它是计算圆面积的主程序，圆的半径通过以下命令指定：

```c
#include <stdio.h>
#include <stdlib.h>

/* 函数原型声明 */
double area_of_circle(double r);

int main(int argc, char **argv) {
    if (argc < 2) {
        printf("Usage: %s\n", argv[0]);
        exit(1);
    } else {
        double radius = atof(argv[1]);
        double area = area_of_circle(radius);
        printf("Area of circle with radius %f\n", radius, area);
    }
    return 0;
}
```

你需要另一个文件来实际计算圆的面积。这里是 `circle.c` 的列表，其中我定义了一个计算面积的函数：

```c
#include <math.h>

#define SQUARE(x) ((x)*(x))

double area_of_circle(double r) {
    return 4.0 * M_PI * SQUARE(r);
}
```

对于这样一个简单的程序，你可以将所有内容放在一个文件中，但这个示例向你展示了如何处理多个文件。要编译这两个文件并创建一个名为 `area` 的可执行文件，使用此命令：

```bash
gcc -o area area.c circle.c
```

这次调用 GCC 使用 `-o` 选项来指定可执行文件的名称。如果你不用 `-o` 选项指定输出文件名，GCC 将可执行文件保存在名为 `a.out` 的文件中。

如果你有很多源文件需要编译和链接，可以单独编译文件并生成对象文件（具有 `.o` 扩展）。当你更改源文件时，只需要将该文件编译为对象文件。以下命令显示了如何分离示例程序的编译和链接步骤：

```bash
gcc -c area.c
gcc -c circle.c
gcc -o area area.o circle.o
```

前两个命令运行带有 `-c` 选项的 gcc 来编译源文件。第三个命令将对象文件链接成可执行文件 `area`。如果你好奇的话，这里是运行 `area` 程序的方法（计算半径为 1 的圆的面积）：

```bash
./area
```

这次调用 GCC 使用 `-o` 选项来指定可执行文件的名称。如果你不用 `-o` 选项指定输出文件名，GCC 将可执行文件保存在名为 `a.out` 的文件中。

如果你有很多源文件需要编译和链接，可以单独编译文件并生成对象文件（具有 `.o` 扩展）。当你更改源文件时，只需要将该文件编译为对象文件。以下命令显示了如何分离示例程序的编译和链接步骤：（此处原文重复，已跳过）

# 探索 Fedora Core 中的软件开发工具

## GNU C 和 C++ 编译器

Fedora Core 中最重要的软件开发工具是 GCC —— GNU 和 C++ 编译器。事实上，GCC 可以编译三种语言：C、C++ 和 Objective-C（一种为 C 语言增加了面向对象编程能力的语言）。你可以使用 `gcc` 命令来编译和链接 C 和 C++ 源文件。GCC 编译器支持 ANSI 标准，使得将任何 ANSI C 程序移植到 Linux 变得非常容易。此外，如果你曾在 UNIX 系统上用过 C 编译器，那么你会觉得如如归家。

## 使用 GCC

使用 `gcc` 命令调用 GCC。默认情况下，当你对源文件使用 `gcc` 命令时，GCC 会进行预处理、编译和链接，以创建一个可执行文件。然而，你可以使用 GCC 选项在中间阶段停止此过程。例如，你可能需要调用 `gcc -c` 选项来生成对象文件，但不执行链接步骤。

编译和链接 C 源文件非常简单。假设你想编译并链接一个由两个文件组成的简单程序。使用以下源代码完成此任务；它存储在 `area.c` 文件中，它是计算圆面积的主程序，圆的半径通过以下命令指定：

```c
#include <stdio.h>
#include <stdlib.h>

/* 函数原型声明 */
double area_of_circle(double r);

int main(int argc, char **argv) {
    if (argc < 2) {
        printf("Usage: %s\n", argv[0]);
        exit(1);
    } else {
        double radius = atof(argv[1]);
        double area = area_of_circle(radius);
        printf("Area of circle with radius %f\n", radius, area);
    }
    return 0;
}
```

你需要另一个文件来实际计算圆的面积。这里是 `circle.c` 的列表，其中我定义了一个计算面积的函数：

```c
#include <math.h>

#define SQUARE(x) ((x)*(x))

double area_of_circle(double r) {
    return 4.0 * M_PI * SQUARE(r);
}
```

对于这样一个简单的程序，你可以将所有内容放在一个文件中，但这个示例向你展示了如何处理多个文件。要编译这两个文件并创建一个名为 `area` 的可执行文件，使用此命令：

```bash
gcc -o area area.c circle.c
```

这次调用 GCC 使用 `-o` 选项来指定可执行文件的名称。如果你不用 `-o` 选项指定输出文件名，GCC 将可执行文件保存在名为 `a.out` 的文件中。

如果你有很多源文件需要编译和链接，可以单独编译文件并生成对象文件（具有 `.o` 扩展）。当你更改源文件时，只需要将该文件编译为对象文件。以下命令显示了如何分离示例程序的编译和链接步骤：

```bash
gcc -c area.c
gcc -c circle.c
gcc -o area area.o circle.o
```

前两个命令运行带有 `-c` 选项的 gcc 来编译源文件。第三个命令将对象文件链接成可执行文件 `area`。如果你好奇的话，这里是运行 `area` 程序的方法（计算半径为 1 的圆的面积）：

```bash
./area
```

输出结果：
Area of circle with radius 1.000000 3.141593

## 编译 C++ 程序

GCC 是一个 C 和 C++ 编译器，使用 g++ 来编译 C++。C 文件以 `.c` 结尾，而 C++ 文件以 `.cpp` 结尾。

假设你想编译以下存储在 `hello.cpp` 中的 C++ 程序：

```cpp
#include <iostream>
int main() {
    using namespace std;
    cout << "Hello from Fedora!" << endl;
}
```

要编译并链接此程序为名为 `hello` 的可执行文件，使用此命令：

```bash
g++ -o hello hello.cpp
```

命令创建了 `hello` 可执行文件，你可以这样运行：

```bash
./hello
```

输出结果：
Hello from Fedora!

## 探索 GCC 选项

许多 GCC 选项控制着 C 和 C++ 程序的各个方面。

这里是 gcc 命令的基本语法：

```
gcc options filenames
```

每个选项以连字符（-）开头，并且通常有一个长名称，例如 `-funsigned-char` 或 `-finline-functions`。许多常用的选项是短的，例如 `-c` 编译，`-g` 生成调试信息（使用 GNU 调试器 gdb 调试所需）。

你可以通过终端输入以下命令查看所有 GCC 选项的摘要：

```
man gcc
```

然后你可以浏览常用的 GCC 选项。通常，你不需要显式提供 GCC 选项，因为默认设置对于大多数应用程序都是足够的。表 1-1 列出了你可能使用的一些 GCC 选项。

| 表 1-1 常用选项 |
| :--- | :--- |
| **选项** | **含义** |
| -ansi | 支持 ANSI 标准（ISO C89）语法。（此选项禁用了某些 GNU C 特性，例如 `asm` 和 `typeof` 关键字。） |
| -c | 编译并生成对象文件。 |
| -DMACRO | 将宏定义为字符串 "1"。 |
| -DMACRO=DEFN | 将宏定义为 DEFN，其中 DEFN 是某些文本字符串。 |
| -E | 仅运行 C 预处理器。 |
| -fallow-single-precision | 以单精度执行所有操作。 |
| -fpcc-struct-return | 在内存中返回所有结构体和联合体值，而不是寄存器。（这种返回效率较低，但至少与其他编译器兼容。） |
| -fPIC | 生成适用于共享库的位置无关代码 (PIC)。 |
| -freg-struct-return | 可能时在寄存器中返回结构体和联合体值。 |
| -g | 生成调试信息。（GNU 调试器可以使用这些信息。） |

