
## gcc 使用

实际上，选项及其参数的顺序并不重要。在某些情况下，同类型的多个选项之间的顺序是重要的。例如，`-I`选项指定包含文件的目录或多个目录。因此，如果你多次指定`-I`，`gcc`将按照指定的顺序搜索列出的目录。

使用`gcc`创建单个源文件`hello.c`非常简单——只需调用`gcc`，并将文件名作为参数传递，如下例所示：

`cc hello.c`

结果是在当前目录下生成一个名为`a.out`的可执行文件，你通过`./a.out`执行它。要定义`gcc`生成的输出文件的名称，请使用`-o`选项，如下：

`cc hello.c -o runme`

使用`gcc`编译多个源文件时，你可以在`gcc`命令行上指定所有文件，如下例所示，编译并链接后的可执行文件将放在名为`showdate`的文件中：

`cc showdate.c helper.c –o showdate`

要增量编译这些文件并最终将其链接成二进制文件，你可以在编译期间使用`-c`选项生成对象文件。然后你可以使用单个`gcc`命令将它们链接在一起并指定输出文件的名称，如下例所示：

```
cc -c showdate.c
cc -c helper.c
cc showdate.o helper.o –o showdate
```

很容易看出，如果一个项目包含多个源文件，从命令行进行编译将很快变得繁琐，特别是当你开始链接外部库、使用优化命令以及提供其他杂`gcc`选项之后。解决命令行繁琐问题的方案是`make`工具，将在下一节中讨论。

## 简单的 Makefile

自 Unix 时代以来，大多数 Unix 应用都是使用一种名为`make`的规则驱动程序进行构建的，它会调用编译器和其他工具，从所有程序源代码生成可执行文件。`make`程序也是在 Linux 以及所有其他 Unix 类系统上构建 C 和 C++ 的基石。`make`程序执行以下操作：

- 允许开发者识别成功编译所需的源模块、包含文件和库之间的关系和依赖关系
- 指定成功构建应用程序时必须编译的顺序
- 通过将编译限制在应用程序中受源代码或静态链接库任何更改影响的部分，来避免重复编译

`make`程序最初由 Stu Feldman 在 AT&T 为早期版本的 Unix 编写。作为历史的一部分，`make`程序的源代码曾未自由免费提供，因此在很大程度上被 GNU `make`程序所取代。GNU `make`提供了原始`make`程序的所有功能以及其他功能。因此，本章后续对`make`程序的引用均指 GNU `make`。

任何`make`程序使用的规则都存储在名为`Makefile`的文本文件中，其中包含依赖信息和满足这些依赖所需的命令。正如你所预期的，复杂应用的`Makefile`本身也会极其复杂且具有平台特定性，因为它们需要调用特定平台的编译器和工具，这些工具可能位于不同的目录，或在不同的系统上具有不同的名称。最简单的`Makefile`是用于从单个 C 语言文件编译的简单应用的，例如“Hello, World!”。该应用的`Makefile`如下：

```
hello: hello.c
	gcc hello.c -o hello
```

所有构建规则的行必须以制表符（tab）开头，这是手工`Makefile`最常见的问题之一。要调用此`Makefile`，只需在包含`Makefile`的目录下执行`make`。`make`程序会自动查找`Makefile`并遵循其包含的任何规则生成目标文件。

在上一节中，我使用的示例从两个模块编译，使用了以下命令行：

```
cc -c showdate.c
cc -c helper.c
cc showdate.o helper.o –o showdate
```

该应用的`Makefile`看起来如下：

```
showdate: showdate.o helper.o
	gcc showdate.o helper.o -o showdate

showdate.o: showdate.c
	gcc -c showdate.c

helper.o: helper.c
	gcc -c helper.c
```

这突出了`Makefile`在拥有多个文件时如何减少必要的重新编译。例如，此`Makefile`说明`showdate`依赖于对象模块`showdate.o`和`helper.o`，并提供了使用`gcc`链接两个对象文件生成二进制文件的规则。它继续强调每个对象模块都依赖于对应的 C 文件，并提供了生成每个模块的规则。如果修改了一个 C 文件，`Makefile`可以简化重新编译。`make`只重新生成修改的文件对应的对象模块，然后使用新的对象文件重新链接二进制文件。

随着项目的扩大，你希望利用其他的`Makefile`功能，例如定义变量、使用某些晦涩的符号来简化`make`规则等。关于`make`程序和`Makefile`的高级信息的良好来源如下：

- `www.linuxdevcenter.com/pub/a/linux/2002/01/31/make_intro.html`: O’Reilly & Associates Linux Development Center 的关于使用 `make` 的优秀文章。
- `www.tldp.org/HOWTO/Software-Building-HOWTO-3.html`: Linux Documentation 项目 Linux 软件开发指南中关于 `make` 的章节。
- `www.gnu.org/software/make`: GNU `make` 的主页，包含指向官方 `make` 文档的链接。
- `www.gnu.org/software/make/manual`: GNU `make` 文档的官方在线首页，提供多种格式。

## 集成开发环境

集成开发环境（`IDE`）是一套统一的工具集，通常提供一个编辑环境、构建环境和调试器，这些工具在单一框架内协同工作。`IDE`通常为用于创建和管理由多个源文件和库组成的软件项目提供基础设施。大多数现代`IDE`都是图形化工具，运行在 Linux 系统、GNOME、KDE、Microsoft Windows 或 Mac OS X 等桌面环境中。由于这个原因，许多现代`IDE`还包含了用于创建用户界面以及图形应用程序其他图形元素的工具。

`IDE`的主要优势在于构成开发环境的各种工具之间的集成。无论提供多少种功能，大多数`IDE`都给人一种是一个单一工具的印象。

正如下一节所讨论的，`IDE`传统上面向特定语言或一组相关语言的开发者的需求。最近，像 Eclipse 这样的通用 `IDE` 变得越来越流行，因为它们提供了一个单一框架，无论开发者正在使用哪种语言，都能标准化开发体验，并支持插件模型，使其能够被轻松扩展。

## Linux 下的 IDE

对于一个用于开发庞大语言应用程序、且每个人对开发应该如何进行都有自己想法的操作系统，你能够从中期待什么？Ubuntu 在其仓库中为不同语言提供了大量的 `IDE`。Ubuntu 仓库中提供的一些广为人知的 `IDE` 包括：

- **Eclipse:** `Eclipse` 是一款用 Java 编写的多功能 `IDE`。`Eclipse` 最初是作为开发 Java 应用程序的 `IDE` 框架开发的，但已扩展到支持其他语言的开发。`Eclipse` 使用 Java 编写这一事实使其在各种图形环境和操作系统上具有非常好的移植性和可用性。关于 `Eclipse` 的更多信息，请参阅本章关于 `IDE` 的后续讨论，或访问 Eclipse 主页 `www.eclipse.org`。

- **KDevelop:** 这是一个基于 KDE 桌面环境的 C 和 C++ 应用程序图形 `IDE`。`KDevelop` 是一个非常流行且易用的 `IDE`，它提供了向导，帮助简化创建标准的命令行 Linux 应用程序，以及使用 Qt、GNOME 和 KDE 图形环境的图形应用程序。关于 `KDevelop` 的更多信息，请访问其主页 `www.kdevelop.org`。图 18.2 显示了 `KDevelop` 中一个传统的 C 语言“Hello, World!”应用程序。

- **Geany:** `geany` `IDE` 是一个用于 C、C++ 和 Java 应用程序的文本界面集成开发环境，可以在任何终端应用程序（如 `xterm` 或 GNOME 终端）中良好运行。`geany` `IDE` 为各种 GCC 编译器和 GNU 调试器 `gdb` 提供了集成支持。关于 Geany 的更详细信息，请访问其主页 `http://geany.org.ua/`。

- **Pida:** `pida` `IDE`（Python Integrated Development Application）是一个基于 GTK 的 `IDE`，用于用 Python 脚本语言编写文本模式或图形应用程序。`pida` `IDE` 非常流行，并支持在其统一的开发框架内轻松集成熟悉的开发工具。关于 `pida` 的更多信息，请访问其主页 `http://pida.berlios.de`。
