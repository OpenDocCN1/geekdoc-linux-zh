

```
scanf ("%f", &y);
printf ("x^y is: %6.3f\n", pow((double)x,(double)y));
return(0);
}
% gcc power.c
/tmp//ccnEwHNH.o: In function `main':
power_lib.c:(.text+0x73): undefined reference to `pow'
collect2: ld returned 1 exit status
% gcc power.c -lm -o power
% power
The program takes x and y from stdin and displays x^y.
Enter integer x: 9.82
Enter integer y: 2.3
x^y is: 191.362
%
```

## 17.5.3.3 编译 C++ 和 Java 程序

你也可以使用 gcc 编译器来编译 C++ 程序。包含 C++ 源代码的文件必须具有以下扩展名之一：.C、.CPP、.cpp、.c++ 或 .cc。

Java 源代码被编译（翻译）成 Java 字节码，并由 Java 虚拟机（JVM）解释，也称为 Java 解释器。我们 UNIX 系统上的 Java 编译器称为 javac，而 JVM 是 java。因此，为了运行一个文件中的 Java 程序，例如 Hello.java，我们使用 javac 编译器来编译它。它生成 Java 字节码并将其存储在 Hello.class 文件中，该文件使用 java 命令进行解释，如以下会话所示。

```
% javac Hello.java
$ java Hello
Hello, world!
%
```

在下面的章节练习中，你将使用 gcc 和 javac 编译器命令在你的 UNIX 系统上编译简单的 C、C++ 和 Java 程序并运行它们。

## EXERCISE 17.2

在你的 UNIX 系统上创建简单的 C、C++ 和 Java 程序。编译并运行它们，以了解两个编译器（gcc 和 javac）以及 Java 虚拟机 java 的基本工作原理。

## 17.5.4 处理基于模块的 C 软件

大多数有用的 C 软件分为多个源文件（.c 和 .h）。这种软件结构相比于存储在单个文件中的单体程序有几个优势。首先，它导致更模块化的软件，从而产生更小的程序文件，编辑、编译、测试和调试所需的时间更少。它还允许仅重新编译已修改的源文件，而不是整个软件系统。此外，多模块结构支持信息隐藏，这是面向对象（OO）设计和编程的关键特性。

然而，多模块实现也有其缺点。首先，你必须知道构成整个系统的文件、这些文件之间的相互依赖关系，以及自上次创建可执行系统以来已修改的文件。此外，当处理多模块 C 软件时，将多个文件编译成可执行文件有时会变得麻烦，因为必须输入两条很长的命令行：一行用于为所有 C 源文件创建目标文件，另一行用于将目标文件链接以创建单个可执行文件。解决这种不便的一种简单方法是创建一个执行此工作的简单 shell 脚本。这种技术的缺点是，即使只有一个源文件（或头文件）被修改，所有目标文件都会被重新创建，其中大部分是不必要的。

UNIX 有一个更强大的工具称为 make，它允许你管理多个模块的编译成可执行文件。make 实用程序读取一个名为 makefile 的规范文件，该文件描述了软件系统的模块如何相互依赖。make 实用程序使用 makefile 中的依赖关系规范以及各个组件被修改的时间，以最小化重新编译量。当你的软件系统由数十个文件和几个可执行程序组成时，此实用程序非常有用。在这样的系统中，记住并跟踪所有头文件、源文件、目标文件和可执行文件可能是一场噩梦。以下是 make 实用程序的简要描述。

### SYNTAX

```
make [-f makefile]
```

Purpose: Updates a file based on the dependency relationship stored in a makefile called makefile; the dependency relationship is specified in makefile in a particular format.

### Commonly used options/features:

- **-f** 此选项允许你指示 make 从任何文件中读取相互依赖规范；如果没有此选项，文件名将被视为 makefile 或 Makefile。
- **-h** 显示所有选项的简要说明。
- **-n** 不运行任何 makefile 命令；仅显示它们。
- **-s** 以静默模式运行，不显示任何消息。

make 实用程序基于文件的相互依赖关系、需要构建的目标文件（例如，可执行文件或目标文件）和用于构建目标文件而执行的命令。这些相互依赖关系、目标和命令在 makefile 中作为 make 规则指定。以下是 make 规则的语法。

### SYNTAX

```
target-list: dependency-list
Or
```
