
`pr` 和 `enscript` 都可以将输出发送到打印机，并且默认情况下它们就是这样做的。抛开这一点，这些基本调用几乎不会产生你期望的输出。页边距是什么？行在哪里折叠？你明白了。你需要在 `pr` 或 `enscript` 上设置所有这些选项，否则你的文档将使用打印机的默认设置。你的默认值将类似于从纸张边缘起左侧和顶部页边距为 1/2"，行长度约为 72 个字符宽，以及 Courier（打字机）字体——很可能不是你想要的。那你该怎么办？

你需要做的第一件事是阅读 `man` 手册并弄清楚你想要的 `pr` 或 `enscript` 的默认设置。除此之外，你可能还必须使用另一个格式化命令，例如 `fmt`。当你弄清楚各种设置后，你只需反复使用它们。

我的典型 `enscript` 会话大致如下：

```
[alberto@digital alberto]$ fmt -w 65 intro.txt | enscript --margins=100:100:100:100 -h -B
[ 1 pages * 1 copy ] sent to printer
```

我使用 `fmt` 创建约 65 个字符宽的行，然后将输出通过管道传递给 `enscript`。我将页边距选项设置为 100 像素（72 像素 = 1"），并且使用 `-h` 选项，抑制横幅页的打印（该页说明谁打印了文件并浪费纸张）。`-B` 选项抑制通常显示文档标题、上次保存时间和页码的页眉行的打印。

我也可以使用 `pr` 产生类似的输出，如下所示：

```
fmt -w 65 intro.txt | pr -o 15
```

`-o` 选项指定左侧页边距的字符数；15 个字符约为 1.5"。

要访问内容，请点击章节和节标题。

# 完全傻瓜的 Linux 使用指南

（出版社：Macmillan Computer Publishing）

作者：Manuel Ricart

ISBN：078971826x

出版日期：12/22/98

搜索本书：

## UNIX 文本处理

要生成更精美的输出，例如粗体文本、不同字体等，你需要使用 UNIX 的格式化程序之一，例如 `groff`（传统 `troff` 格式化程序的 GNU 版本）。如果你查看 `man` 页的源代码，你会看到你在使用 `groff` 时使用的格式化代码。（要查看源代码，请对 `/usr/man/man1/` 中的任何文档使用 `zless`。）这是一个你会看到的例子：

```
.TH man 1 "September 2, 1995"
.LO 1
.SH NAME
man \- format and display the on-line manual pages
.br
manpath \- determine user's search path for man pages
.SH SYNOPSIS
man [\-acd fhkKtwW] [\-m system] [\-p string] [\-C config_file] [\-M path] [\-P pager] [\-S section_list] [section] name ...
.SH DESCRIPTION
.B man
formats and displays the on-line manual pages. This version knows about the
.B MANPATH
and
.B (MAN) PAGER
environment variables, so you can have
your own set(s) of personal man pages and choose whatever program you like to display the formatted pages. If
.I section
is specified,
.B man
only looks in that section of the manual.
You may also specify the order to search the sections for entries
```

正如你从此源文本中看到的，`groff`（`troff`！）格式化的文件没有任何空行。格式化命令（宏）必须从左边缘开始。宏的名称通常以点（`.`）或撇号（`'`）开头。格式化一直持续到另一个宏覆盖它为止。

你使用的宏将取决于你设计的文档类型。前面列表中的宏是为格式化 UNIX 手册页而设计的。例如，`Man` 定义了诸如 `.B` 用于粗体和 `.I` 用于斜体以及更复杂的用于定义标题、描述等的宏。如果你曾经使用文本编辑器编写过 HTML 页面，从 UNIX 命令行格式化文本在概念上并没有那么不同，只是标记标签不同。标记标签会根据你使用的宏包而改变。例如，另一个名为 `ms` 的包提供了论文的格式化。

正如你可能已经猜到的，你实际上能做什么取决于你拥有的宏。除了前面提到的 `man` 宏之外，其他库如 `ms`、`mm` 和 `me` 用于格式化其他类型的文档（请参阅 UNIX 手册第 7 节中的 `groff_ms`、`groff_mm`、`man` 和 `me`；要进入那里，输入 `man 7 keyword`）。代码以及它们如何格式化文档因包而异。

当你的文本以这种（有些别扭）的方式格式化时，你可以使用 `groff` 命令生成文本、PostScript、HTML、LaserJet 打印机和其他格式的输出。然后你将生成的此文件发送给 `lpr` 命令以打印它。`lpr` 命令接受你提供的内容并将其排队到打印机。语法如下所示：

```
nroff -Tps -macropackage filename | lpr
```

将 `macropackage` 替换为宏的名称（`man` 用于手册页，`ms`、`me`、`mm` 等）和 `filename` 替换为你的文件名。

正如你所知，要生成一个简单格式化的文档，你需要知道很多东西。UNIX 文本处理并不止于 `groff`。其他更复杂的排版系统如 `TeX` 和 `LaTeX` 可以生成专业格式的文档。许多印刷的技术出版物都是使用 `TeX` 和 `LaTeX` 开发和印刷的。

那么为什么这么复杂？UNIX 命令行打印系统的意图是使用任何可以显示和正确打印到各种设备的文本编辑器生成文件。因此，你可以生成手册页，在纸上打印它们，生成 HTML 页面，并生成 pdf（Adobe Acrobat）文件，所有这些都来自同一个格式化的文件。如果你只是想使用文字处理或桌面出版，请坚持使用 GUI 文字处理器，例如 StarOffice 中包含的文字处理器。当你只需要一份漂亮的纸质文档时，它会为你节省时间。

To access the contents, click the chapter and section titles.

# 完全傻瓜Linux指南

(Publisher: Macmillan Computer Publishing)

Author(s): Manuel Ricart

ISBN: 078971826x

Publication Date: 12/22/98

Search this book:

## Part 3

### Linux下的基本系统任务

你已经体验过 `KDE`，并且已经深入使用命令行。接下来还要做什么？与生活中的其他事情一样，在 Linux 中也有那些必须做的事情。别担心，情况并没有听起来那么糟糕——第 3 部分的信息会帮助你。 这些章节会指导你备份你的机器、安装软件、监控系统，你甚至会认识 LISA。还有一章专门为真正喜欢冒险的人介绍如何定制你的 Linux 系统。先给你提个醒，现在就开始吧！

## Chapter 18

### 用户、组和密码

#### In This Chapter

- Adding Users
- Modifying Users: `usermod`
- Deleting Users: `userdel`
- Adding, Modifying, and Removing Groups
- Users and Passwords
- Linux and Shadow Passwords

如果你有一台独立系统，你可能不必太担心管理多个用户和账户。你很可能还会继续使用安装系统时创建的同一个账户。

然而，如果你处于网络环境中，你可能想要授予其他用户访问你系统的权限。因此，本章的主题对你来说具有中等重要性。如果你管理的是具有多个账户的系统，你应该确保阅读本章并理解其中的内容。如需进一步帮助，请务必参考第 15 章“Help Please”中讨论的 Linux System Administrator’s Guide。

登录和密码存在的全部原因是为了安全。在 UNIX 中，我们希望保护自己的工作不被他人侵犯。与基于 Windows 95/98/NT 的 PC 不同，UNIX 系统可以支持大量并发用户。换句话说，多位用户可以通过网络或其他连接的终端同时使用你的计算机及其服务，而你也在使用它。如果你还没有阅读第 16 章“Permissions: Protecting and Sharing your Work”，现在可能是个好时机。

添加、删除和管理用户是一项管理任务。幸运的是，如今这项任务已相当自动化，因为工具更灵活，能够处理许多步骤。在早期，你必须手工添加、删除和管理用户，或许借助自己开发的自定义脚本。
