
虽然 Usenet 可以作为一个作为一个强大的信息源，但你也会发现很多不准确的信息，因为几乎任何人都可以进入 Usenet。所以，对你读到的内容保持保留态度。通常，技术性越强的组，你获得的信息就越准确。`comp.compilers` 组（关于为计算机语言编写编译器的信息）显然比 `comp.sys.next.advocacy` 组（NeXT 工作站的拥者——如果存在这样一个中立组的话）包含更多无偏的信息。

然而，你会发现许多 Usenet 新闻组非常有用。我们自己也是技术人员，经常浏览与 UNIX、X Window 系统以及相关主题的新闻组（如 Elm 和 Pine 等电子邮件软件包，emacs 等软件）。附录 A 列出了 Linux 相关的新闻组。

这些分类划分为具体的新闻组名称的方法很简单：分类名称后加上一个描述性后缀。例如，致力于 UNIX 操作系统相关问题的新闻组名称为 `comp.unix.questions`。使用句点来分隔元素。表 9.5 列出了一些常用新闻组的列表。

## 表 9.5 频繁访问的新闻组示例

| 新闻组 | 主题 |
| :--- | :--- |
| `comp.databases` | 数据库管理 |
| `comp.lang.c` | C 语言问题 |
| `comp.text` | 文本处理问题 |
| `comp.unix.questions` | 关于操作系统的问题 |
| `misc.jobs` | 职位机会 |
| `sci.space` | 空间探索问题 |
| `space.shuttle` | 航天器 |

## 阅读与写入新闻

虽然所有的新闻项目都是文本文件，从理论上可以用 `vi` 或 `emacs` 读取，但由于文件数量巨大且分散在许多不同的文件中，实际上读取每个文件是不可行的。一个完整的 Usenet 新闻源，即来自所有新闻组的所有输入消息文件，每天向硬盘添加超过 50 MB 的文件。（记得我们之前说过 UNIX 文件似乎会传播吗？这就是你的例子。）这就是所谓的“阅读器”（readers）软件演变出来的。新闻器帮助你从每天出现的数百个新文件中筛选出你感兴趣的内容并跳过其他的。这根本无法做到。

我们不会深入介绍许多新闻器；Linux 提供了多种，鼓励你尝试所有一种。你将使用哪种部分取决于你如何获取新闻。如果你在公司网络上，你将从本地服务器访问新闻。如果你通过 ISP 连接互联网，你将使用 `NNTP` 协议从 ISP 的新闻服务器获取新闻。你在第 2 章运行 `setup` 时，系统询问过你这个问题；如果你安装了错误类型的新闻器，可以随时返回 `setup` 安装一个你喜欢的。Linux 新闻器包括：

- `tn`，一个具有扩展搜索阅读器（如图 9.7 所示）
- `inn`，一个基础阅读器
- `tin`，一种按主题排列消息的线程阅读器（如图 9.8 所示）

# 第 9 章：Linux 与互联网

组选择 (353)

| u | 逻辑 | 激活活动 |
|---|---|---|
| 1 | alt | |
| 2 | alt,activism | |
| 3 | alt,answers | 周期仓库 |
| 4 | alt,astrology | 闪烁的小星 |
| 5 | alt,atheism | 无神论讨论 |
| 6 | alt,atheism, moderated | 无神论与辩论 |
| 7 | alt,bbs | Computer BBS 系统 |
| 8 | alt,bbs.binews | BBS 系统建立 |
| 9 | alt,lists | 定期发布内容 |
| 10 | alt.bbs.un-bbs | BBS 讨论 |
| 11 | alt,binaries | |
| 12 | alt.binaries.pictures | |
| 13 | alt.binaries.pictures.d | 帖子讨论 |
| 14 | alt,binaries.pictures.erotica | 用于 AL 的发布 |
| 15 | alt,binaries.pictures.erotica | 色情讨论 |

```
=set current to n, TBR=unread, /search pattern, catch,
goto, j=line down, k=line up, h=help, m=move, q=quit, r=toggle all/unread,
subscribe, S pattern, usread pattern, yank in/out
```

图 9.8 Usenet 滚动条。

## 抓取新闻

随着互联网的普及，越来越多的 Usenet 新闻通过互联网传输，而不是旧的 `uucp` 电话线方法。

在互联网上，Usenet 新闻通过 `NNTP` 从一台机器跳转到另一台。如果你使用 `NNTP` 获取新闻，可以使用 Netscape Navigator 等 浏览器查看新闻。

此外，一个名为 `Slurp` 的免费程序可以通过 `NNTP` 为你获取新闻。这对于将特定的 Usenet 新闻组下载到你的 Linux 系统非常有用。然后你可以使用 `xrn`、`nn` 或 `trn` 等新闻阅读程序离线阅读消息。我们在第二张附带光盘中包含了 `Slurp`。

## 如何找到要下载的文件？

如果你身处 Usenet，你会被大量关于免费软件以及如何获取它的信息包围。秘诀在于知道去哪里寻找它。

一些大学和公司维护支持匿名 FTP 的归档站点。这些位置在 `comp.answers` 新闻组中经常被提到。

此外，许多与计算机相关的新闻组将包含标记为 `FAQ`（常见问题）的新闻项目。这些常见问题之一（无疑）会涉及到归档站点的存在。

最后，你可以在新闻组中发布一个哀求的请求，询问有关特定程序的信息。你可能会收到一些厌倦了回答纯学者提问的粗鲁评论，但无疑会有一些心肠的人用有用信息回答你的请求。

## 总结

本章介绍了 Linux 许多使用 `TCP/IP` 功能连接到其他计算机系统和互联网的工具。这些包括到现有网络的 `TCP/IP` 连接，以及使用 Linux 的 `SLIP` 和 `PPP` 工具进行拨号访问。

一旦连接，Linux 提供了许多用于互联网访问和使用的命令，包括 `ftp`（允许你从远程站点传输软件）、`login` 和 `telnet`。得益于几个新闻浏览器，你还可以浏览 Usenet 新闻组。此外，Linux 还提供了几种邮件选项，包括 `mail` 命令以及 `xmh`、`pine` 和 `elm` 新闻阅读器。我们在第二张附带光盘中包含了几个免费的 Web 浏览器。

Usenet 是系列的新闻组。Linux 具有几个新闻阅读程序。

在下一章（也是最后一章）中，我们将介绍编程与 Linux。

## 第四部分

## Linux 编程

本书以第 10 章结束，即 Linux 编程概述。在书中你将找到对 Linux 编程工具（包括 `GNU C 编译器`）及其 X Window 编程工具的解释。

## 在 Linux 中编程

本章涵盖了：

- `GNU C 编译器`
- C 编程
- `cc` 命令
- 使用 `make`
- 在 X Window 系统下编程
- 使用 `LessTif` 模拟 `Motif`
- 使用共享库
- 使用 `imake`
- 使用 `Tcl/Tk`
- 使用 `Perl` 的简要介绍
- 使用 `gawk`（GNU 项目版本的 `awk`）

# 第 10 章：在 Linux 中编程

## 在 Linux 下编程

本章不会让你瞬间成为 Linux 和 X Window 程序员。然而，我们将向你展示如何在 Linux 环境中进行编程。我们将涵盖许多许多在 Linux 上编程时应该知道的奇怪事情，包括 X 库所在的位置，以及关于 Linux 如何使用共享库的一些有趣小知识。

对于程序员来说，Linux 提供了你所期望的、依赖自由软件基金会提供的软件免费工具和编译器。从 `GNU C 编译器`开始，你可以在你的 Linux 系统上开发 C、`C++`、`Fortran`（通过 `g77`）和 `Objective-C` 程序。除了这些主流语言外，Linux 还支持 `Tcl`、`Perl` 以及许多其他编程语言和辅助工具。此外，我们在第二张附带光盘上加入了名为 `LessTif` 的工具，提供给那些……

```
/*
* 第10章的示例C程序，
* Linux配置与安装。
 */
```

# 第 10 章：在 Linux 中编程

```c
#include <stdio.h>

int main(int argc, char** argv)
{
    /* 这是一个注释。 */
    printf("Linux is my favorite O.S.\n");

    return 0;
}
```

使用你最喜欢的 Linux 文本编辑器，将上述代码输入到名为 `chap10.c` 的文本文件中。

始终为 C 程序文件使用 `.c` 扩展名命名是一个好主意。虽然这不是强制的，但遵循这样的约定会让 Linux 更加易用。

在你输入这个简短程序后，可以执行以下简单步骤，从该 C 文件创建一个可运行的执行执行程序。

你输入的程序只是一个文本文件。它没有任何可以让其变成可执行命令的内容。要做到这一点，我们需要编译并链接该程序。这两个步骤都通过以下 `cc` 命令完成：
