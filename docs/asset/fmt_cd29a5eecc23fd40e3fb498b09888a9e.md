
| 此函数 | 功能 |
| --- | --- |
| `trap [-l] [cmd] [sigspec]` | 当接收到信号 `sigspec` 时执行 `cmd`。 |
| `type [-a] [-type | _path] name [name ...]` | 说明 shell 如何解释每个名称。 |
| `ulimit [-SHacdfmstpnuv [limit]]` | 控制 shell 可用的资源。 |
| `umask [-S] [mode]` | 设置文件创建掩码——文件的默认权限。 |
| `unalias [-a] [name ...]` | 取消指定的别名。 |
| `unset [-fv] [name ...]` | 移除指定变量的定义。 |
| `wait [n]` | 等待指定的进程终止。 |

# 第 4 章：使用 Perl 编程

## 本章内容

- 编写你的第一个 Perl 程序
- 了解 Perl 概述
- 理解 Perl 包和模块
- 在 Perl 中使用对象

在编写脚本时，Perl 语言在系统管理员之间非常流行，特别是在 UNIX 和 Linux 系统上。系统管理员使用 Perl 来自动化常规管理任务，例如寻找可以归档和删除的老文件以释放磁盘空间。

Perl 是一种脚本语言，这意味着你不需要编译和链接脚本（一个包含 Perl 命令的文本文件）。相反，解释器会执行 Perl 脚本。这使得编写和测试 Perl 脚本变得简单，你不需要通过典型的“编辑-编译-链接”循环来编写 Perl 程序。

除了易用之外，Perl 流行的另一个原因是 Perl 是免费分发的，适用于各种计算机系统，包括 Red Hat Linux 以及其他许多如 UNIX、Windows 95/98/NT/2000/XP 和 Apple Macintosh。

在本章中，我将向你介绍 Perl 脚本。

# 理解 Perl

Perl 官方代表“实用提取报告语言”（Practical Extraction Report Language），但根据 Perl 创建者 Larry Wall 的，人们经常将 Perl 称为“病态杂乱的垃圾列表”（Pathologically Eclectic Rubish List）。正如这些名称所示，Perl 最初的设计是为了从文本文件中提取信息并生成报告。

Perl 起于 1986 年，是 Larry Wall 创建的一个系统管理工具。随着时间的推移，Perl 通过许多新功能和函数的积累而成长。最新版本——Perl 5.8 支持面向对象的编程，并允许任何人通过指定格式添加新模块来扩展 Perl。

# 782 确定你是否安装了 Perl

由于其作为系统管理工具的起源，Perl 多年来一直受到 UNIX 系统管理员的欢迎。最近，当万维网（或 Web）流行以及对通用网关接口（CGI）的需求出现时，Perl 成为那些熟悉该语言的人的自然选择。近期 Perl 流行气的飙升主要是由于在编写 Web 的 CGI 程序中使用 Perl。当然，随着人们对 Perl 的关注增加，他们发现 Perl 在 CGI 编程之外还有用得多。这反过来又让 Perl 在用户中变得更加流行。

Perl 可用于多种计算机系统，例如 Linux 操作系统，Perl 是免费分发的。如果你可以访问互联网，将你的浏览器指向 http://www.perl.com/，主页。你可以通过将你的万维浏览器指向全面 Perl 存档网络（CPAN）获取最新版本的 Perl。以下地址将你连接到离最近的 CPAN 站点：

```
http://www.perl.com/CPAN/
```

# 确定你是否安装了 Perl

如果你熟悉 shell 编程，你可以很快上手 Perl。如果你不熟悉，可以通过以下命令检查 perl 是否安装：

```
which perl
```

`which` 命令告诉你它在 PATH 列出的目录中找到了程序。如果 `perl` 已安装，你会看到以下输出：

```
/usr/bin/perl
```

如果 `/usr/bin` 不在 `PATH` 中，可以通过以下命令查看：

```
echo $PATH
```

`=$PATH:/usr/bin`

我建议你从较小的 Perl 子集开始。如果你从未编写过程序，精通 Perl 可能需要一段时间。然后，将 Perl 加入你的知识库。

# 783 确定你是否安装了 Perl

如果你仍然遇到错误，你可能没有安装 Perl。你可以按照以下步骤从 DVD-ROM 安装 Perl：

1. 以 root 身份登录。
2. 将配套的 DVD-ROM 插入 DVD-ROM 驱动器。如果你在 GNOME 或 KDE 环境下，DVD-ROM 将自动挂载。否则，通过输入命令挂载 DVD-ROM：

```
mount /mnt/cdrom
```

3. 输入以下命令切换到 Red Hat 补丁的位置：

```
cd /mnt/cdrom/RedHat/RPMS
```

4. 输入以下 `rpm`（Red Hat 包管理器）命令进行：

```
rpm -ivh perl*
```

在系统中安装 Perl 后，输入以下命令查看版本号：

```
perl -v
```

这是 perl，v5.8.1，适用于 i386-linux-thread-multi（带有 1 个注册补丁，详情见 perl -V）

Copyright 1987-2003, Larry Wall

Perl 可以根据艺术许可（Artistic License）或 GNU 公许可证复制，许可证可以在 Perl 5 源码包中找到。

Perl 的完整文档（包括 FAQ 列表）可以在此系统使用 `man perl` 或 `perldoc` 找到。如果你可以访问互联网，将你的浏览器指向 http://www.perl.com/，

此输出告诉你你拥有 Perl 5.8，补丁级别 1，并且 Larry Wall（Perl 的创始人）拥有版权。（但请记住，Perl 是根据 GNU 公许可证免费分发的）。

![](img/509edf67e1a0798154916aafeb3f0878_810_0.png)

## 784 编写你的第一个 Perl 脚本

Perl 具有许多 C 语言的特性，正如你所知的，大多数关于 C 的书籍都从一个在终端显示 Hello, World! 的示例程序开始。因为 Perl 是一种解释型语言，你可以直接从命令行完成此任务。如果你输入：

```perl
perl -e 'print "Hello. World!\n";'
```

Perl 会响应如下：

Hello, World!

该命令使用 `perl` 程序的 `-e` 选项将命令行参数传递给 Perl 解释器。在这种情况下，以下行构成了 Perl 程序：

```perl
print "Hello. World!\n";
```

要将此行转换为 Perl 脚本，只需将该行放在带有指向 perl 程序指令的文件中（就像你在编写 shell 脚本时，通过放置诸如 `#!/bin/sh` 的行来运行 shell 来处理脚本一样）。

要运行此脚本，请遵循以下步骤：

- 1. 使用文本编辑器在名为 `hello.pl` 的文件中输入并保存以下行：

```perl
#!/usr/bin/perl
# This is a comment.
print "Hello. World!\n";
```

- 2. 通过以下命令使 `hello.pl` 文件可执行：

```bash
chmod +x hello.pl
```

- 3. 在 shell 提示符处输入以下内容运行 Perl 脚本：

```bash
./hello.pl
```

它应该显示以下输出：

Hello, World!

就是这样！你已经编写并尝试了你的第一个脚本。

注意 Perl 脚本的第一行以 `#!` 开头，后面是 perl 程序的完整路径。如果脚本的第一行以 `#!` 开头，shell 会剥离 `#!`，将脚本名称添加到末尾并运行脚本。因此，如果脚本文件名为 `hello.pl` 且第一行具有 `#!/usr/bin/perl`，shell 将执行以下命令：

```bash
/usr/bin/perl hello.pl
```

## Perl 概览

大多数编程语言（包括 Perl 在内）都有一些共同特性：

- **`变量`**存储不同类型的数据。你可以将每个变量视为数据的占位符——类似于邮箱，有一个名称和存储数据的空间。变量的内容是它的值。
- **`表达式`**通过操作符将变量结合起来。一个表达式可能会相加几个变量；另一个表达式可能会提取字符串的一部分。
- **`语句`**执行某些操作，例如为变量赋值或打印字符串。
- **`流程控制语句`**允许语句根据某些表达式的值以不同的顺序执行。通常，流程控制语句包括 `for`、`do-while` 和 `if-then-else` 语句。
- **`函数`**（也称为子程序或例）允许你将多个语句分组并给它们一个名称。使用此特性，你可以通过调用代表这些语句的函数来执行相同的语句set。通常，编程语言会提供一些预定义函数。
