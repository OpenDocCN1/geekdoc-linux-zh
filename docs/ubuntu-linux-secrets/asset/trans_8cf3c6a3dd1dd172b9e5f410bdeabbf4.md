

第一次检查使用 `-e` 比较来确定用户是否拥有 HOME 目录。如果有，下一次 `-e` 比较则检查测试文件是否存在于 HOME 目录中。如果文件不存在，shell 脚本使用单个大于号重定向符号，使用 `date` 命令的输出创建一个新文件。第二次运行 shell 脚本时，它使用双大于号符号，因此它只是将 `date` 输出追加到现有文件中。

## Summary

在本章中，我们讨论了如何使用 bash shell 脚本环境来创建和运行 shell 脚本程序。Shell 脚本允许我们将多个 shell 命令串联起来并同时运行。它还允许我们将值存储在变量中并操作命令的输出，以帮助我们完成正常的系统任务，例如列出文件、查看已登录用户以及处理正在运行的进程。

下一章将介绍 Ubuntu 中可用的一些更高级的脚本环境。Perl 和 Python 脚本语言与 shell 脚本类似，但提供了更多功能，允许我们自定义数据处理。

## Perl and Python

![](img/39e65e65eeb4f54001ede08c6114ae3cc6c_666_0.png)

## Secrets in This Chapter

- *What is Perl?*
- *Using Perl*
- *What is Python?*
- *Using Python*

## What Is Perl?

第 25 章“Shell Scripts”展示了使用包含命令行命令的脚本在 Ubuntu 中使用自动化程序的基本方法。不幸的是，使用 shell 命令编写 shell 脚本程序来操作大量数据可能有些繁琐。Ubuntu 环境提供了另外两种更适合处理数据的流行脚本语言。本章介绍 Ubuntu 中可用的 Perl 和 Python 语言，并演示如何使用它们来帮助管理数据。

Larry Wall 编写的 Practical Extraction and Report Language（Perl）是一种解释型脚本语言，用于增强标准 shell 语言。解释型脚本语言是一组由程序解释而不是直接由操作系统执行的命令。正如你从其名称可以猜到的那样，Perl 的基本目的是帮助以比 shell 脚本中更简单、更优雅的方式操作数据以生成报告。

Perl 借鉴了多种不同的编程语言，结合了 shell 脚本、C 编程语言甚至 Basic 编程语言的特性，创建了一种多功能的编程语言，对 UNIX 系统管理员非常有用。在 Perl 圈子中常见的一句座右铭是“做一件事的方法不止一种”（缩写为 TIMTOWTDI，常被称为 tim toady）。Perl 具有如此多的功能，以至于通常可以用几种不同的方法解决数据操作问题。当然，每当有不止一种方法做某事时，这就会在编程世界中引发有趣的争论，而 Perl 当然也有其份额的争论！

由于 Perl 的流行，许多操作数据的系统脚本都是用 Perl 编写的。正因如此，大多数 Linux 发行版（包括 Ubuntu）默认安装 Perl。对于少数未默认安装 Perl 的发行版，很容易下载并安装 Perl 解释器包来运行程序。这提供了一个很好的编程平台来编写自己的脚本代码。

## Working with Perl

由于 Perl 是一种解释型语言，Ubuntu 本身无法运行 Perl 程序。相反，必须有一个外部程序来解释 Perl 命令并执行它们。用于解释和执行 Perl 命令的程序称为 perl，通常位于 Linux 系统（包括 Ubuntu）上的 /usr/bin 文件夹中。

有两种方法可以调用 Perl 解释器来运行你的程序：

- 在命令行中，将 Perl 文件指定为 perl 程序的参数
- 在 Perl 脚本本身内部定义 perl 程序

以下各节演示如何使用这两种方法运行 Perl 程序。

