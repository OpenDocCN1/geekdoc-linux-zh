
与线程示例一样，即使我们的主方法结束，JVM 仍然保持运行。这是因为 `java.awt.Frame` 实现启动了新线程来处理窗口事件。

![](img/f36419c0b225d12fa66de83fa271829b_850_0.png)

## 总结

我们在这一章中看到的只是冰山一角。

我们没有查看 Java 如何管理文件、它支持的标准数据结构（如 `vector` 和 `hashtable`）、使用 socket 的低级网络支持、使用 RMI（远程方法调用）的高级网络、使用 JDBC 访问数据库或文件压缩。所有这些功能都包含在标准的 JDK 1.1 运行时库中。

还有许多标准库、扩展和规范：Java 2D、Java 3D、Java Media Framework、Java Sound API、Java Advanced Imaging API、Servlets、Java Server Pages、Java Beans、Enterprise Java Beans 以及更多。

# tcl 与 tk 编程

作者 Steve Wells

## 本章内容

- tcl 基础 820
- tcl 语言 822
- tk 工具包 840
- tcl/tk 控件编程示例 842
- tcl/tk 与 xsetroot 的接口 844

## 开发环境
第四部分

`tcl`（读音为 "tickle"）是一种脚本语言，用于为 X Window 系统创建图形用户界面编程环境。`tcl` 和 `tk` 易于学习和使用，通过它们，你可以比传统的 X Window 编程方法快地构建出用户界面。

`tcl/tk` 由 John K. Ousterhout 在担任加利福尼亚大学伯克利分校电气工程与计算机科学教授期间编写的。它最初的设计目的是为交互式工具提供一种可重用的命令语言，但它的应用已远超这一范围，被广泛用于软件产品，例如客户端/服务器和数据库支持。

`tcl/tk` 的强大之处在于，完全可以使用 `tcl` 脚本语言编写复杂的图形化应用程序，从而隐藏了在使用 C 语言编写界面时所遇到的许多界面编程复杂性。这意味着你可以使用 `tcl/tk` 编写类似 Netscape 的图形化浏览器。

`tcl/tk` 官方网站位于 `http://www.scripts.com/`。

根据其网站，Scripts Corporation 是 `tcl` 平台公司。Scripts 由 John Ousterhout 创立，专注于将 `tcl` 脚本语言引入企业主流市场。Scripts 将为 `tcl` 提供开发工具、技术扩展和商业支持服务，同时继续开发开源 `tcl` 和 `tk` 包。

该网站还提供了下载和安装最新版本 `tcl/tk` 的链接。

`tcl` 二进制文件、`tclsh`、`wish` 和 `tclhelp` 通过 Debian 的 rpm 安装在 `/usr/bin` 中。运行 `tclhelp` 命令可以获得关于 `tcl` 和 `tk` 的详尽帮助信息。此外还有 `tcl` 和 `wish` 的帮助页（man pages）。

本章讨论的程序与大多数版本的 `tcl` 和 `tk` 兼容，并在当前版本上应该运行良好。

## tcl 基础

`tcl` 是一种类似于 Perl 或 UNIX shell 的解释型语言，这意味着 `tcl` 命令首先被读取，然后被求。`tk` 是一个窗口工具包，它使用 `tcl` 语法来创建图形用户界面（GUI）组件，如按钮、滚动条、对话框和窗口。

运行 `tcl` 需要 `tcl` shell（`tclsh`）或窗口 shell（`wish`）。`tcl` 和 `wish` 都类似于 `sh` 或 `tsh` 等 UNIX shell；它们允许以交互式方式执行命令，或从文件中读取命令。在实践中，由于这些 shell 很少以交互式方式使用，因为它们的交互能力相当有限。

`tclsh` 和 `wish` 之间的主要区别在于，`tclsh` 只理解 `tcl` 命令，而 `wish` 同时理解 `tcl` 和 `tk` 命令。

### tcl 的交互式使用

本节简要介绍 `tcl` shell 的交互式使用，以说明其风险之一。

要以交互方式启动 `tcl`，请在 UNIX shell 提示符处输入 `tclsh`（或 `wish`，后者仅在图形环境下有效）。应该出现以下提示符：

```
%
```

在本章中，交互式命令以百分号 (%) 开头。在提示符后输入：

```
% echo "hello world"
```

应该出现 `hello world` 单词，随后是新的提示符。现在尝试：

```
% puts "hello world"
```

应该出现相同的输出，但两者之间存在巨大差异。第一个命令运行了 `echo` 二进制文件处理字符串 "hello world"，而第二个命令使用了 `puts`（put string）`tcl` 命令。"hello world" 的 `echo` 版本仅在 `tcl` 以交互方式运行时有效，这是在交互式下使用 `tclsh` 和 `wish` 的风险之一。例如，如果你将命令

```
echo "hello world"
```

写入 `hello.tcl` 并在 `tclsh` 中 `source` 该文件，如如下所示：

```
% source hello.tcl
```

你将得到以下错误：

```
invalid command name "echo"
```

这会在 UNIX shell 中执行带参数的命令。这仅仅是 `tcl` shell 交互模式下行为不同的内容的示例之一。

### tcl 的非交互式使用

交互模式有严重的局限性，因为你需要逐个输入并执行每个命令。`tcl` 的真正威力源于非交互脚本的使用。通常，`tcl` 和 `wish` 以非交互方式使用，这意味着它们是从 UNIX 提示符 ($) 通过脚本调用的，例如：

```
$ tcl myprog.tcl
$ wish myprog.tcl
```

或者在脚本内部调用，该脚本的第一行类似于如下所示：

![](img/f36419c0b225d12fa66de83fa271829b_854_0.png)

```
#!/usr/bin/tcl
```

通常，必须为每个脚本的安装修改此第一行，因为 `wish` 或 `tcl` 会位于不同的位置。为了避免每次安装都要编辑脚本，`tcl` 的帮助页建议将以下三行作为所有 `tcl/tk` 脚本的前三行：

```
#!/bin/sh
# the next line restarts with tcl \
exec wish "$0" "$"
```

这意味着用户路径中仅需 `tcl` 即可使用该脚本。这种方法的具体结果可能有所不同，取决于 `sh` 的版本。`tcl` 的真正优势能够将命令组合在一起。

## tcl 语言

本节包含 `tcl` 语法及其用法的介绍。

### 命令结构

`tcl` 命令的基本结构是给出命令名（`commandname`）和参数（`arguments`）。命令由换行符或分号 `;` 结束。如果每行只给出一个命令，不需要分号。作为示例，两个命令可以每行写一个：

```
set foo 0
set bar 1
```

或者在同一行上：

```
set foo 0; set bar 1
```

有时需要在另一个表达式中使用一个表达式的值。为了做到这一点，使用括号。

### 注释

除了命令外，`tcl` 脚本中其他唯一的行是注释。与 UNIX shell 和 Perl 一样，注释行是以井号符号 (`#`) 开头的行：

```
# this is a comment
```

但与 shell 不同的是，以下内容不是注释：

```
set foo 0 # initialize foo
```

这将导致错误，因为 `tcl` 解析器认为命令在换行符处结束。要在与命令相同的行上包含注释，需要用分号结束命令：

```
set foo 0; initialize foo
```

将所有命令都用分号结束可能是一个好主意，尽管这不是要求的。

### 数据类型

`tcl` 不支持变量类型，如 `int`、`float`、`double` 或 `char`。这意味着变量可以在同一个程序中的不同时间被设置为数字、字符或字符串。`tcl` 内生地理解你何时将变量作为数字或字符串使用，并相应执行所需的操作；因此，程序员不需要显式设置它们。

然而，在内部，`tk` 将所有变量视为字符串。当需要操作变量时，`tcl` 允许以 ANSI C 理解的所有形式给出数字（实数整数）。以下是变量有效数值的示例：

| Value | Data Type |
| :--- | :--- |
| 74 | Integer |
| 0112 | Octal,以 0 开头 |
| 0x4a | Hexadecimal,以 0x 开头 |
| 74. | Real |
| 74.0 | Real |
| 7.4e1 | Real |
| 7.4e+1 | Real |

![](img/f36419c0b225d12fa66de83fa271829b_856_0.png)

其他值被处理为字符串，如果在数学表达式中使用它们将产生错误。

### 变量

`tcl` 定义了两种类型的变量：*标量*和*数组*。要创建一个标量变量并给其赋值，请使用 `set` 命令。例如：

```
set banana 1;
```
