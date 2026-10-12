
## 第 4 章：Perl 编程

### 本章内容
- 编写你的第一个 Perl 程序
- Perl 概览
- 理解 Perl 包和模块
- 在 Perl 中使用对象

在编写脚本方面，Perl 语言在系统管理员中非常流行，尤其是在 UNIX 和 Linux 系统上。系统管理员使用 Perl 来自动执行常规的系统管理任务，例如查找可以归档并删除以释放磁盘空间的旧文件。

Perl 是一种脚本语言，这意味着你不需要编译和链接 Perl 脚本（包含 Perl 命令的文本文件）。相反，是由解释器执行 Perl 脚本。这一特性使得编写和测试 Perl 脚本变得容易，因为你不需要经历典型的编辑-编译-链接循环来编写 Perl 程序。

除了编程简便性之外，Perl 流行的另一个原因是 Perl 是免费分发的，并且可用于多种计算机系统，包括 Fedora Core 以及其他许多系统，如 UNIX、Windows 95/98/NT/2000/XP 和 Apple Macintosh。

在本章中，我将向你介绍 Perl 脚本编程。

### 理解 Perl

Perl 的官方全称是*实用提取报告语言*（Practical Extraction Report Language），但 Perl 的创建者 Larry Wall 说，人们通常将 Perl 称为*病态的 eclectic 垃圾列表器*（Pathologically Electic Rubbish Lister）。正如这些名称所暗示的，Perl 最初旨在从文本文件中提取信息并生成报告。

Perl 诞生于 1986 年，当时是由 Larry Wall 创建的一种系统管理工具。随着时间推移，Perl 通过积累许多新特性和功能而成长。最新版本——Perl 5.8——支持面向对象编程，并允许任何人通过以指定格式添加新模块来扩展 Perl。

与其作为系统管理工具的起源相符，Perl 多年来在 UNIX 系统管理员中一直很受欢迎。最近，随着万维网（或简称为 Web）变得流行，以及通用网关接口（CGI）程序的需求出现，Perl 成为那些已经熟悉该语言的人的自然选择。Perl 近年来的流行激增主要归因于 Perl 在编写 Web CGI 程序中的使用。当然，随着人们更加关注 Perl，他们发现 Perl 的用途远不止 CGI 编程。反过来，这也使 Perl 在用户中变得更加流行。

Perl 可在多种计算机系统上获得，因为与 Linux 操作系统一样，Perl 可以免费分发。

如果你熟悉 Shell 编程或 C 编程语言，你可以很快学会 Perl。如果你从未编写过程序，精通 Perl 可能需要一些时间。我建议你从 Perl 功能的一个小子集开始，忽略你立即无法理解的内容。然后，慢慢将 Perl 功能添加到你的技能库中。

### 确定你是否有 Perl

在继续 Perl 教程之前，请检查你的 Fedora Core 系统上是否安装了 perl 程序。输入以下命令：

```
which perl
```

which 命令告诉你是否在 PATH 环境变量列出的目录中找到了指定的程序。如果安装了 perl，你会看到以下输出：

```
/usr/bin/perl
```

如果 which 命令抱怨当前 PATH 中不存在该程序，这并不一定意味着你没有安装 perl；这可能仅仅意味着你的 PATH 中没有 /usr/bin 目录。确保 /usr/bin 在 PATH 中；通过输入以下命令进行检查：

```
echo $PATH
```

查看输出是否列出了 /usr/bin 目录。如果 PATH 中没有 /usr/bin，请使用以下命令重新定义 PATH：

```
export PATH=$PATH:/usr/bin
```

现在，再次尝试 which perl 命令。如果你仍然收到错误，你可能未安装 Perl。你可以通过执行以下步骤从配套 DVD-ROM 安装 Perl：

- 1. 以 root 身份登录。
- 2. 将配套 DVD-ROM 插入 DVD-ROM 驱动器。如果你正在 GNOME 或 KDE 图形环境中工作，DVD-ROM 会自动挂载。否则，输入以下命令挂载 DVD-ROM：
    ```
    mount /mnt/cdrom
    ```
- 3. 输入以下命令将目录更改为 Red Hat 包的位置：
    ```
    cd /mnt/cdrom/Fedora/RPMS
    ```
- 4. 输入以下 rpm（Red Hat 包管理器）命令安装 Perl：
    ```
    rpm -ivh perl*
    ```

在你的系统上安装 Perl 后，输入以下命令查看其版本号：
`perl -v`
以下是该命令的典型输出：

> 这是 perl，v5.8.3 为 i386-linux-thread-multi 构建
> 版权 1987-2003，Larry Wall
> Perl 仅可在艺术许可证或 GNU 通用公共许可证的条款下复制，这些许可证可以在 Perl 5 源码套件中找到。
> Perl 的完整文档，包括 FAQ 列表，应使用 'man perl' 或 'perldoc perl' 在此系统上找到。如果你可以访问互联网，请将浏览器指向 http://www.perl.com/，Perl 主页。

此输出告诉你，你拥有 Perl 版本 5.8，补丁级别 3，并且 Perl 的创始人 Larry Wall 持有版权。（请记住，然而，Perl 是在 GNU 通用公共许可证下免费分发的。）

你可以通过将万维网浏览器指向综合 Perl 归档网络（CPAN）来获取最新版本的 Perl。以下地址将连接到你最近的 CPAN 站点：
www.perl.com/CPAN/

![](img/9f89727199836b0f871f1745838aa8b2_807_0.png)

### 编写你的第一个 Perl 脚本

Perl 具有 C 的许多特性，并且如你可能知道的那样，大多数关于 C 的书都以在终端上显示“你好，世界！”（Hello, World!）的示例程序开头。由于 Perl 是一种解释型语言，你可以直接从命令行完成此任务。如果你输入

```
perl -e 'print "Hello, World!\n";'
```

Perl 会响应以下内容：

```
Hello, World!
```

此命令使用 perl 程序的 -e 选项将 Perl 程序作为命令行参数传递给 Perl 解释器。在这种情况下，以下行构成了 Perl 程序：

```
print "Hello, World!\n";
```

要将此行转换为 Perl 脚本，只需将该行放入文件中，并在文件开头添加一个运行 perl 程序的指令（就像你在 shell 脚本中放置诸如 #!/bin/sh 这样的行来运行 shell 以处理脚本一样）。

要尝试此 Perl 脚本，请按照以下步骤操作：

- 1. **使用文本编辑器在名为 hello.pl 的文件中输入并保存以下行：**

    ```
    #!/usr/bin/perl
    # This is a comment.
    print "Hello, World!\n";
    ```

- 2. **使用以下命令使 hello.pl 文件可执行：**

    ```
    chmod +x hello.pl
    ```

- 3. **通过在 shell 提示符下输入以下内容来运行 Perl 脚本：**

    ```
    ./hello.pl
    ```

它显示以下输出：

```
Hello, World!
```

就这样！你已经编写并尝试了你的第一个 Perl 脚本。

请注意，Perl 脚本的第一行以 #! 开头，后面是 perl 程序的完整路径名。如果脚本的第一行以 #! 开头，shell 会简单地去掉 #!，将脚本文件的名称附加到末尾，并运行脚本。因此，如果脚本文件名为 hello.pl 且第一行是 #!/usr/bin/perl，shell 将执行以下命令：

```
/usr/bin/perl hello.pl
```

### Perl 概览

大多数编程语言，包括 Perl，都有一些共同特征：

- **变量**存储不同类型的数据。你可以将每个变量视为数据的占位符——有点像信箱，有名称和存储数据的空间。变量的内容是其值。
- **表达式**使用运算符组合变量。一个表达式可能添加几个变量；另一个可能提取字符串的一部分。
- **语句**执行某些操作，例如将值赋给变量或打印字符串。
- **流程控制语句**使语句能够根据某个表达式的值按不同顺序执行。通常，流程控制语句包括 `for`、`do-while`、`while` 和 `if-then-else` 语句。
- **函数**（也称为*子例程*或*例程*）允许你将几个语句分组并给它们命名。使用此功能，你可以通过调用代表这些语句的函数来执行相同的语句集。通常，编程语言提供一些预定义的函数。
- **包和模块**允许你组织一组相关的、旨在可重用的 Perl 子例程。（模块是在 Perl 5 中引入的。）

在接下来的几个部分中，我将概述 Perl 的这些主要特性，并通过简单的示例说明这些特性。

### 基本 Perl 语法

Perl 是自由格式的，就像 C 一样。对任何关键字的确切位置没有限制。通常，Perl 程序存储在以 `.pl` 结尾的文件名中，但对你使用的文件名没有限制。

与 C 一样，每个 Perl 语句以分号（`;`）结束。井号或井字符（`#`）标记注释的开始；`perl` 程序忽略从井号开始的行余下部分。

Perl 语句的组用大括号（`{ ... }`）包围。此特性在 C 中也是类似的。

