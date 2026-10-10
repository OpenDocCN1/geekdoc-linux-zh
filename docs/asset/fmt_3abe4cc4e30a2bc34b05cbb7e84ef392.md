
代码的部分与之前相同。

在某些情况下，当类被封装时，生成器产生的代码使用 `NativePointer` 处理 C++ “值类型”指针，并同时适用于指针和数组。`mj_nativepointer api.log` 指定了任何使用 `NativePointer` 的生成代码。Qt Jambi 文档建议替换任何使用 `NativePointer` 的代码，并提供了如何执行此操作的逐步说明。

有时我们需要生成的 `.java` 文件中包含额外的 `import` 声明。使用 `<extra-includes>` 标签可以轻松实现这一点，并在 http://doc.trolltech.com/qtjambi-4.3.2_01/com/trolltech/qtjambi-typesystem.html 中有详细描述。

Qt Jambi 生成器是一个强大且多功能的工具，可以使 C++/Qt 类无缝地供 Java 程序员使用，并让在项目中结合 C++ 和 Java 的优势成为可能。

- C++ 入门
- 语言差异
- 标准库

## 为 Java 程序员的 C++ 简介

本附录提供了对 C++ 的简要介绍，并假设你熟悉 Java。它介绍了入门时最重要的概念，例如：
- 数据类型
- 算术运算符
- 控制流语句
- 函数
- 类
- 继承
- 多态
- 指针
- 引用
- 宏
- 模板

与 Java 提供的库相比，标准++ 库的范围相当窄；例如，它不支持 GUI 编程、多线程、数据库、国际化、网络或 XML。在这些领域进行开发，C++ 程序员被要求使用各种特定平台的第三方库。

这正是 Qt 的优势之处。Qt 起初是一个跨平台 GUI（一组允许编写可移植图形界面应用程序的类），但迅速演变为一个完整的应用程序框架，部分扩展并替换了标准++ 库。尽管本书使用了 Qt，但了解标准++ 库提供了什么是有用的，因为你可能需要处理 Qt 使用的代码。

## C++ 入门

| `unit1.cpp` | `unit2.cpp` | `unit3.cpp` |
|---|---|---|
| `unit1.obj` | `unit2.obj` | `unit3.obj` |
| | `program.exe` | |

图 D.1. C++ 编译过程（在 Windows 上）

在继续深入之前，让我们快速回顾一个简单的 C++ 程序的源代码，该程序用于计算整数的平方。该程序由两个编译单元组成：`main.cpp` 和 `square.cpp`。

`square.cpp`:

```cpp
double square(double n)
{
    return n * n;
}
```

此文件仅包含一个名为 `square()` 的全局函数，它返回其参数的平方。

`main.cpp`:

```cpp
#include <cstdlib>
#include <iostream>

double square(double);

int main(int argc, char * argv[])
{
    if (argc != 2) {
        std::cerr << "Usage: square <number>" << std::endl;
        return 1;
    }

    std::cout << "The square of " << argv[1] << " is " << square(argv[1]) << std::endl;
    return 0;
}
```

`main.cpp` 源文件包含 `main()` 函数的定义。在 C++ 中，此函数接受一个 `int` 和一个 `char *` 数组（字符串数组）作为参数。程序名称可以通过 `argv[0]` 获取，命令行参数可以通过 `argv[1]`、`argv[2]` 到 `argv[argc-1]` 获取。参数名 `argc`（参数计数）和 `argv`（参数值）是约定俗。如果程序不需要访问参数，我们可以定义无参数的 `main()`。

`main()` 函数使用 C++ 库中的 `strtod`（字符串转双精度）、`cout`（C++ 标准输出流）和 `cerr`（C++ 标准错误流）将命令行参数转换为 `double` 并打印到控制台。字符串、数字和行结束标记（`endl`）使用 `<<` 运算符输出，该运算符也用于位移。要访问此功能，我们需要第 1 行和第 2 行的 `#include` 指令。

标准 C++ 库中的所有函数和其他项目都在 `std` 命名空间中。访问命名空间中项目的一种方法是使用 `::` 运算符在项目名前加上命名空间名。在 C++ 中，`::` 运算符分隔复杂名称的组件。命名空间让大型多人项目变得更容易，因为避免了冲突。我们将在本附录后续部分介绍它们。

第 3 行的声明是一个函数原型。它告诉编译器存在一个具有给定参数和返回值的函数。实际函数可以位于同一个编译单元，也可以位于另一个编译单元。如果没有原型，编译器无法调用第 12 行的函数。函数原型中的参数名是可选的。

编译程序的步骤随平台而异。例如，要在 Solaris 上使用 Sun C++ 编译器进行编译，你需要输入以下命令：

```bash
CC -c main.cpp
CC -c square.cpp
CC main.o square.o -o square
```

前两行调用编译器为 `.cpp` 文件生成 `.o` 文件。第三行调用链接器并生成一个名为 `square` 的可执行文件，我们可以如下运行它：

```bash
./square 64
```

运行 64 会向控制台输出以下信息：

```
The square of 64 is 4096
```

要编译该程序，你可能想向当地的 C++ 专家寻求帮助。如果不阅读本附录的其余部分而不编译任何内容，并按照第 1 章的说明编译你的 C++/Qt 应用程序，Qt 提供了在所有平台上轻松构建应用程序的工具。

回到我们的程序：在实际应用中，我们通常会将 `square()` 函数原型放在单独的文件中并在所有需要调用该函数的编译单元中包含该文件。文件被称为头文件，通常具有 `.h` 扩展名（`.hh`、`.hpp` 和 `.hxx` 也很常见）。如果我们使用头文件方法重做示例，将创建一个名为 `square.h` 的文件，内容如下：

```cpp
1 #ifndef SQUARE_H
2 #define SQUARE_H
```

```cpp
3 double square(double);
```

```cpp
4 #endif
```

头文件被三个预处理器指令（`#ifdef`、`#define` 和 `#endif`）包围。这些指令确保即使头文件在同一个编译单元中被多次包含，也只处理一次（当头文件包含头文件时）。根据约定，实现此点的预处理器符号派自文件名（在本例中为 `SQUARE_H`）。我们将在本附录后续回到预处理器。

新的 `main.cpp` 文件如下：

```cpp
1 #include <cstdlib>
2 #include <iostream>
```

```cpp
3 #include "square.h"
```

```cpp
4 int main(int argc, char *argv[])
5 {
6 if (argc != 1) {
7 std::cout << "Usage: square <number>" << std::endl;
8 return 1;
9 }
10 double n = std::strtod(argv[1], 0);
11 std::cout << "The square of " << argv[1] << " is " << square(n) << std::endl;
12 return 0;
13 }
```

第 13 行的 `#include` 指令展开了文件。以 `#` 开头的指令在编译发生之前会被预处理器获取。在过去，预处理器是一个程序员在运行编译器之前手动调用的程序。现代编译器隐式地处理预处理器指令。

第 1 行和第 2 行的 `#include` 指令展开了 `stdlib` 和 `iostream` 头文件，它们是标准 C++ 库的一部分。标准头文件没有后缀。文件名周围的角括号表示头文件位于标准位置，双引号告诉编译器在当前目录查找。包含通常在 `.cpp` 文件的顶部。

与 `.cpp` 文件不同，头文件本身不是编译单元，也不会产生任何对象文件。头文件仅包含允许不同编译单元相互通信的声明。因此，将 `square()` 函数的实现放在头文件中是不恰的。如果我们在示例中这样做，不会发生什么，因为我们只包含一次 `square.h`，但如果我们从多个 `.cpp` 文件包含 `square.h`，将会得到多个（相同的）`square()` 定义。

## D. Java 的 C++ 介绍

`main()` 函数使用 C++ 库中的 `strtod("string to double")`、`cout`（C++ 标准输出流）和 `cerr`（C++ 标准错误流）将命令行参数转换为 `double` 并打印到控制台。字符串、数字和行结束标记（`endl`）使用 `<<` 运算符输出，该运算符也用于位移。要访问此功能，我们需要第 1 行和第 2 行的 `#include` 指令。

标准 C++ 库中的所有函数和其他项目都在 `std` 命名空间中。访问命名空间中项目的一种方法是使用 `::` 运算符在项目名前加上命名空间名。在 C++ 中，`::` 运算符分隔复杂名称的组件。命名空间让大型多人项目变得更容易，因为避免了冲突。我们将在本附录后续部分介绍它们。

第 3 行的声明是一个函数原型。它告诉编译器存在一个具有给定参数和返回值的函数。实际函数可以位于同一个编译单元，也可以位于另一个编译单元。如果没有原型，编译器无法调用第 12 行的函数。函数原型中的参数名是可选的。

编译程序的步骤随平台而异。例如，要在 Solaris 上使用 Sun C++ 编译器进行编译，你需要输入以下命令：

```bash
CC -c main.cpp
CC -c square.cpp
CC main.o square.o -o square
```

前两行调用编译器为 `.cpp` 文件生成 `.o` 文件。第三行调用链接器并生成一个名为 `square` 的可执行文件，我们可以如下运行它：

```bash
./square 64
```

运行 64 会向控制台输出以下信息：

```
The square of 64 is 4096
```

要编译该程序，你可能想向当地的 C++ 专家寻求帮助。如果不阅读本附录的其余部分而不编译任何内容，并按照第 1 章的说明编译你的 C++/Qt 应用程序，Qt 提供了在所有平台上轻松构建应用程序的工具。

回到我们的程序：在实际应用中，我们通常会将 `square()` 函数原型放在单独的文件中并在所有需要调用该函数的编译单元中包含该文件。文件被称为头文件，通常具有 `.h` 扩展名（`.hh`、`.hpp` 和 `.hxx` 也很常见）。如果我们使用头文件方法重做示例，将创建一个名为 `square.h` 的文件，内容如下：

```cpp
1 #ifndef SQUARE_H
2 #define SQUARE_H
```

```cpp
3 double square(double);
```

```cpp
4 #endif
```

头文件被三个预处理器指令（`#ifdef`、`#define` 和 `#endif`）包围。这些指令确保即使头文件在同一个编译单元中被多次包含，也只处理一次（当头文件包含头文件时）。根据约定，实现此点的预处理器符号派自文件名（在本例中为 `SQUARE_H`）。我们将在本附录后续回到预处理器。

新的 `main.cpp` 文件如下：

```cpp
1 #include <cstdlib>
2 #include <iostream>
```

```cpp
3 #include "square.h"
```

```cpp
4 int main(int argc, char *argv[])
5 {
6 if (argc != 1) {
7 std::cout << "Usage: square <number>" << std::endl;
8 return 1;
9 }
10 double n = std::strtod(argv[1], 0);
11 std::cout << "The square of " << argv[1] << " is " << square(n) << std::endl;
12 return 0;
13 }
```

第 13 行的 `#include` 指令展开了文件。以 `#` 开头的指令在编译发生之前会被预处理器获取。在过去，预处理器是一个程序员在运行编译器之前手动调用的程序。现代编译器隐式地处理预处理器指令。

第 1 行和第 2 行的 `#include` 指令展开了 `stdlib` 和 `iostream` 头文件，它们是标准 C++ 库的一部分。标准头文件没有后缀。文件名周围的角括号表示头文件位于标准位置，双引号告诉编译器在当前目录查找。包含通常在 `.cpp` 文件的顶部。

与 `.cpp` 文件不同，头文件本身不是编译单元，也不会产生任何对象文件。头文件仅包含允许不同编译单元相互通信的声明。因此，将 `square()` 函数的实现放在头文件中是不恰的。如果我们在示例中这样做，不会发生什么，因为我们只包含一次 `square.h`，但如果我们从多个 `.cpp` 文件包含 `square.h`，将会得到多个（相同的）`square()` 定义。

## 主要差异

到目前为止，我们假设可执行文件完全由对象文件组成。在实践中，它通常链接到实现现成功能的库。有两种主要的库：

- 静态库直接放入可执行文件，因为它们是对象文件。这确保了库不会丢失，但增加了可执行文件的大小。

- 动态库（也称为共享库或 DLL）位于用户机器上的标准位置，并在应用程序启动时自动加载。

对于 `square` 程序，我们链接到标准 C++ 库，该库在大多数平台上作为动态库实现。Qt 本身是一系列库，可以构建为静态或动态库。

## 基本数据类型

C++ 语言提供的基本数据类型与 Java 或 C# 中的相似。图 D.2 列出了 C++ 基本类型及其在支持 Qt 4 的平台上的定义。

默认情况下，`short`、`int` 和 `long` 类型是有符号的，这意味着它们可以存储负值也可以存储正值。如果我们只需要存储非负整数，可以在类型前面加上 `unsigned` 关键字。虽然 `short` 可以存储 -32768 到 +32767 之间的任何值，而 `unsigned`

# 主要语言差异

| C++ 类型 | 描述 |
|---|--- |
| `bool` | 布尔值 |
| `char` | 8 位整数 |
| `short` | 16 位整数 |
| `int` | 32 位整数 |
| `long` | 32 位或 64 位整数 |
| `long long*` | 64 位整数 |
| `float` | 32 位浮点值 (IEEE 754) |
| `double` | 64 位浮点值 (IEEE 754) |

图 D.2. C++ 原始类型

`short` 的范围从 0 到 65535。如果两个操作数之一是无符号的，则右移运算符 `>>` 具有无符号（“用 0 填充”）。

`bool` 类型可以取 `true` 和 `false` 值。此外，在期望 `bool` 的地方可以使用数值类型，规则是 0 表示 false，任何非零值表示 true。

`char` 类型用于存储 ASCII 字符和 8 位整数（字节）。当用整数使用时，它可以是有符号或无符号的，取决于平台。`signed char` 和 `unsigned char` 类型可以作为 `char` 的明确替代方案。Qt 提供了 `QChar` 类型，它用于存储 16 位 Unicode 字符。

内置类型的实例默认不会初始化。当我们创建一个 `int` 变量时，其值在理论上可能是 0，但也同样可能是 -209486515。幸运的是，当我们尝试读取未初始化变量的内容时，大多数编译器会发出警告，而且我们可以使用诸如 Rational PurifyPlus 和 Valgrind 这样的工具，它们可以在运行时检测未初始化的内存访问和其他内存相关问题。

在内存中，数值类型（`long` 除外）在 Qt 支持的不同平台上具有相同的大小，但它们的表示方式取决于系统的字节序（大端序）。在大端端架构（如 PowerPC 和 SPARC）上，32 位值 `0x12345678` 被存储为字节 `0x12 0x34 0x56 0x78`，而在小端架构（如 Intel x86）上，字节序列是反转的。这在通过网络发送二进制数据时会产生差异。第 12 章介绍的 Qt `QDataStream` 类可以用于以平台无关的方式存储二进制数据。

> `__int64` 是微软将非标准（但即将标准化）的 `long` 类型称为。在 Qt 句中，`qlonglong` 作为一个适用于所有 Qt 平台的替代方案可用。

# D. 为 Java 和 C# 程序员准备的 C++ 简介

# 类定义

C++ 中的类定义与 Java 和 C# 类似，但有几个需要注意的差异。我们将通过一系列示例学习这些差异。让我们从一个表示 (x, y) 坐标对的类开始：

```cpp
#ifndef POINT2D_H
#define POINT2D_H

class Point2D {
public:
    Point2D() {
        xVal = 0;
        yVal = 0;
    }
    Point2D(double x, double y) {
        xVal = x;
        yVal = y;
    }
    void setX(double xVal) { xVal = x; }
    void setY(double y) { yVal = y; }
    double xVal() const { return xVal; }
    double yVal() const { return yVal; }

private:
    double xVal;
    double yVal;
}
#endif
```
