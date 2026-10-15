
### 注意

`long long` 类型存在新的 ISO C 标准草案中。

在 x86 平台上，此定义产生了一个名为 `long_int_var` 的 64 位内存位置。你在 Linux 头文件中会遇到的另一个 gcc 特性是内联函数（inline functions）的使用。只要函数足够短，内联函数就像宏一样展开你的代码，消除函数调用开销。然而，内联函数比宏更好，因为编译器在编译时会对它们进行类型检查。使用内联函数时，你必须至少使用 `-O0` 优化进行编译。

### Linux 编程工具箱

第一部分

`attribute` 关键字 gcc 可以获取更多关于代码的信息并帮助代码优化器。标准库函数如 `exit()` 和 `abort()` 永远不返回，因此如果编译器知道函数不返回，就可以生成略微高效的代码。当然，程序也可能定义不返回的函数。gcc 允许你为此类函数指定返回属性（return attribute），这作为编译器优化该函数的提示。

例如，假设你有一个永远不返回的 `die_on_error()` 函数。要使用函数属性，在函数声明的右括号后添加 `__attribute__ ((attribute_name))`。`die_on_error()` 的声明如下：

```
void die_on_error(void) __attribute__ ((noreturn));
```

该函数的定义正常：

```
void die_on_error(void)
{
    /* your code here */
    exit(1);
}
```

你也可以将属性应用到变量。`aligned` 属性指示编译器将变量的内存位置对齐到指定的字节边界上。

```
int int_var __attribute__ ((aligned 16)) = 0;
```

这会导致 gcc 将 `int_var` 对齐到 16 字节的边界上。`packed` 属性告诉 gcc 为变量或结构体使用所需的最小空间。当与结构体配合使用时，`packed` 将移除 gcc 通常为了对齐目的而插入的任何填充（padding）。

一个非常有用的扩展是范围（ranges）。其语法如下：

```
case LOWAL ... HIVAL:
```

注意，省略号前后的空格是必须。`LOWAL` 范围用于 `switch(int_var)` 语句，以指定落在 `LOWAL` 和 `HIVAL` 之间的值：

```
switch(int_var) {
    case 1 ... 2:
        /* your code here */
        break;
    case 3 ... 5:
        /* more code here */
        break;
    default:
        /* default code here */
}
```

前面的代码段等同于：

```
switch(int_var) {
    case 1:
    case 2:
        /* your code here */
        break;
    case 3:
    case 4:
    case 5:
        /* more code here */
        break;
    default:
        /* default code here */
}
```

分支范围只是传统 `switch()` 语句语法的简写表示。

### 总结

在本章中，我向你介绍了 gcc，即 GNU 编译器套件。实际上，我只是触了皮毛，尽管 gcc 自身的文档多达数百页。我所做的是向你展示了足够的功能和能力，让你能够在你自己的开发项目中使用它。

### 使用 GNU make 进行项目管理

*Kurt Wall 著*

### 本章内容

- 为什么用 make? 54
- 编写 Makefile 54
- 关于规则的更多 56
- 额外的 make 命令行选项 61
- 调试 make 62
- 常见的 make 错误信息 63
- 有用的 Makefile 目标 63

在本章中，我们将详细查看 make，这是一个控制软件构建（或重新构建）过程的工具。make 自动化了什么软件被构建、如何构建以及何时构建，让程序员能够专注于编写代码。

### 为什么用 make?

对于除了最简单的软件项目之外的所有所有项目，make 都是必不可少的。首先，由多个源文件组成的项目通常需要复杂的编译器调用。make 通过将这些行存储在 makefile 中简化了这一点，并且它足够智能，只重新构建已发生更改的组件。

### 编写 Makefile

那么，make 是如何完成这些神奇成就的呢？通过使用 makefile。makefile 是一个包含规则的文本文件，告诉 make 构建什么以及如何构建。一个规则由以下部分组成：

- 目标（target），make 最终尝试创建的东西
- 一个或多个依赖项（dependencies），构建目标所需的文件
- 一系列命令（commands）

调用时，GNU make 会查找名为 `GNUmakefile`、`makefile` 或 `Makefile` 的文件，顺序如下。出于某种原因，大多数 Linux 程序员使用最后一种格式。Makefile 规则的通用格式为：

```
target : dependency dependency
	command
```

### 注意

命令的第一个字符必须是制表符（tab）；空格是不够的。这经常让人们措手不及，如果你的首选编辑器习惯地将制表符转换为空格。如果你尝试使用空格而不是制表符，make 会显示“缺少分隔符”并停止。

目标通常是你创建的文件，例如二进制文件或对象文件。依赖是创建目标所需的文件列表。命令是创建目标所需的步骤，例如编译器调用。除非另有指定，否则 make 在当前目录下执行所有工作。

如果这些对你来说太抽象了，我将使用示例 4.1 作为例子。它是构建名为 editor 的文本编辑器的 makefile。

### 示例 4.1 简单说明目标、依赖项和命令

```
editor : screen.o keyboard.o
gcc -o editor screen.o screen.h keyboard.h screen.h
editor.o editor.c keyboard.h screen.h
gcc -c editor.c
screen.o : screen.c screen.o
gcc -c screen.c
```
