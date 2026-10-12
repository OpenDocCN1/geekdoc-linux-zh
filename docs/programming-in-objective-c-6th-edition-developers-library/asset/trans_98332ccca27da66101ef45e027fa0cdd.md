

你只能在对指针变量进行赋值使其指向某处**之后**，才能对该指针变量使用间接引用运算符。在这个示例中，`c` 从未被设置为指向任何内容，因此该赋值没有意义。

### 11. **在 `switch` 语句的某个 `case` 末尾省略 `break` 语句。**

- 请记住，如果在某个 case 末尾没有包含 `break`，则执行将继续进入下一个 case。

### 12. **在预处理器定义的末尾插入分号。**

- 这种情况通常发生是因为以分号结束所有语句已成为一种习惯。请记住，出现在 `#` 语句中定义名称右侧的所有内容都会被直接替换到程序中。因此，如果在表达式中使用了该定义，例如 `#define MAX (500) ;`，会导致语法错误，因为预处理器之后编译器会看到如下语句：`#define MAX (500) ;`

### 13. **在宏定义中省略参数周围的括号。**

- 示例：`#define SQUARE(x) x * x`
- 上述赋值语句会被错误地计算为 `1 + 3 * 3`，而不是 `(1 + 3) * (1 + 3)`。

### 14. **在任何语句中省略右括号或右引号。**

- 示例：
  ```c
  printf( "%d\n", (a+b);
  ```
- 在第一行中，使用嵌入式括号来分隔方程的每一部分使得代码行更易读，但始终存在遗漏右括号（或在某些情况下多加了一个括号）的可能性。第二行也缺少发送给函数的字符串的右引号。这两者都会产生编译器错误，但有时错误会被标识为出现在另一行，具体取决于编译器是否使用后续行中的括号或引号来完成表达式，从而将缺失的字符移至程序中更靠后的位置。

### 15. **未包含定义程序中使用的 C 编程语言库函数的头文件。**

- 示例：
  ```c
  #include <stdio.h>
  int main() {
      printf("Hello");
      return 0;
  }
  ```
- 如果该程序没有 `#include` `<stdio.h>` 文件，这将产生一个 `printf` 未定义的错误。

### 16. **在 `#define` 语句中，宏名称与其参数列表之间留下一个空格。**

- 示例：
  `#define MAX(a, b) (a > b ? a : b)`
  此定义是不正确的，因为预处理器将定义名称后的第一个空格视为该名称定义的起始位置。在这种情况下，语句 `MAX` 会被预处理器扩展为 `(a > b ? a : b)`，这显然不是预期的结果。

### 17. **在宏调用中使用具有副作用的表达式。**

- 示例：
  `#define SQUARE(x) x * x`
  `SQUARE(v++)`
  调用 `SQUARE` 宏会导致 `v` 被递增*两次*，因为该语句被预处理器扩展为 `v++ * v++`。

## E. 资源

本附录包含了一份精选资源列表，你可以参考这些资源获取更多相关信息。其中一些信息可能在网站上线上提供，或者可以从书籍中获得。

### C 编程语言

C 语言已经存在了 40 多年，因此关于该主题的信息肯定不缺乏。以下内容只是冰山一角。

### 书籍

- Kernighan, Brian W., and Dennis M. Ritchie. *The C Programming Language, 2nd Ed.* Englewood-Cliffs, NJ: Prentice Hall, Inc., 1988.
  - 这本书一直被视为 C 语言参考资料的“圣经”。它是第一本关于 C 语言的书籍，由该语言的创造者 Dennis Ritchie 合著。尽管已有 25 年历史，第二版仍然是最新的版本，并且仍被视为必不可少的参考资料。

- Harbison, Samuel P. III, and Guy L. Steele Jr. *C: A Reference Manual, 5th Ed.* Englewood-Cliffs, NJ: Prentice Hall, Inc., 2002.
  - 另一本优秀的 C 程序员参考书。

- Plauger, P. J. *The Standard C Library.* Englewood-Cliffs, NJ: Prentice Hall, Inc., 1992.
  - 这本书涵盖了标准 C 库，但正如你所看到的出版日期所示，它并不涵盖任何 ANSI C99 的添加内容（例如复数数学库）。

### 网站

- [www.ansi.org](http://www.ansi.org)
  - 这是 ANSI 的网站。你可以在此处购买官方的 ANSI C 规范。在搜索窗口中输入 9899:2011 以查找 ANSI C11 规范。

- [www.opengroup.org/onlinepubs/007904975/idx/index.html](http://www.opengroup.org/onlinepubs/007904975/idx/index.html)
  - 这是一个优秀的在线库函数参考资源（这里也有非 ANSI C 函数）。

### 新闻组

- comp.lang.c
  - 这是一个专门讨论 C 编程语言的新兴小组。你可以在这里提问并帮助他人——在你获得更多经验之后。仅仅观察讨论也很有用。通过 http://groups.google.com 访问此新闻组是一个很好的方式。

### C 编译器和集成开发环境

以下是一个网站列表，你可以在其中下载和/或购买 C 编译器和集成开发环境（IDE），以及获取在线文档。

- **gcc**
  - [http://gcc.gnu.org/](http://gcc.gnu.org/)
  - 由自由软件基金会 (FSF) 开发的 C 编译器称为 gcc。你可以从本网站免费下载 C 编译器。

- **MinGW**
  - [www.mingw.org](http://www.mingw.org)
  - 如果你想在 Windows 环境中开始编写 C 程序，你可以从此网站获取 GNU gcc 编译器。也建议下载 MSYS 作为一个易于使用的 shell 环境来进行工作。

- **CygWin**
  - [www.cygwin.com](http://www.cygwin.com)
  - CygWin 提供一个在 Windows 下运行的类似 Linux 的环境。此开发环境免费提供。

- **Visual Studio**
  - [http://msdn.microsoft.com/vstudio](http://msdn.microsoft.com/vstudio)
  - Visual Studio 是微软的 IDE，允许你使用多种不同的编程语言开发应用程序。

- **CodeWarrior**
  - [www.freescale.com/webapp/sps/site/homepage.jsp?code=CW_HOME](http://www.freescale.com/webapp/sps/site/homepage.jsp?code=CW_HOME)
  - 最初由 Metrowerks 提供，但现在来自一家名为 Freescale 的公司，CodeWarrior 提供运行在多种操作系统上的专业 IDE 工具，包括 Linux、Mac OS X、Solaris 和 Windows。

- **Code::Blocks**
  - [www.codeblocks.org](http://www.codeblocks.org)
  - Code::Blocks 是一个免费的 IDE，你可以在多种平台上开发 C、C++ 和 Fortran 应用程序，包括 Windows、Linux 和 Mac。

### 其他

以下部分包含有关深入学习面向对象编程语言和开发工具的资源。

### 面向对象编程

- Budd, Timothy. *The Introduction to Object-Oriented Programming* (3rd Edition). Boston: Addison-Wesley Publishing Company, 2001.
  - 这本书被认为是一本介绍面向对象编程的经典教材。

### C++ 语言

- Prata, Stephen. *C++ Primer Plus (6th Edition)*. Indianapolis: Addison-Wesley, 2011.
  - Stephen 的教程广受好评。这本教程涵盖了 C++ 语言。

- Stroustrup, Bjarne. *The C++ Programming Language (4th Edition)*. Boston: Addison-Wesley Professional, 2013.
  - 这是对该语言经典教材的最新更新，该教材由该语言的发明者撰写。

### C# 语言

- Petzold, Charles. *Programming in the Key of C#*. Redmond, WA: Microsoft Press, 2003.
  - 这本书被认为是一本适合 C# 初学者的优秀书籍。

- Liberty, Jesse. *Programming C# 3.0.* Cambridge, MA: O’Reilly & Associates, 2008.
  - 适合更有经验的程序员的 C# 优秀入门书。

- Albahari, Joseph and Ben Albahari. *C# 5.0 in a Nutshell: The Definitive Reference*. Sebastopol, CA: 2012.
  - 一本优秀的参考书，特别是在你了解语言基础知识之后。

### Objective-C 语言

- Kochan, Stephen. *Programming in Objective-C (Sixth Edition)*. Indianapolis: Sams Publishing, 2013.
  - 由笔者撰写，它在假设读者没有 C 或面向对象编程经验的情况下，提供了 Objective-C 语言的入门介绍。该版本涵盖了 OS X Mavericks 和 iOS 7。预计将于 2014 年末或 2015 年初发布的该书的新一版将涵盖 Apple 新的 Swift 编程语言。

- [https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/ProgrammingWithObjC](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/ProgrammingWithObjC)
  - 虽然这本身不是一本书，但这份在线文档是 Apple 官方关于如何使用 Objective-C 语言编程的入门指南。它展示了该语言的许多功能，并提供了使用示例。

### 开发工具

- [www.gnu.org/manual/manual.html](http://www.gnu.org/manual/manual.html)
  - 在这里，你会发现大量有用的手册，包括关于 `cc`、`gcc`、`make` 以及其他 Unix 命令行工具的手册。

