

# Linux 简介

目录，只需输入 **ls** 然后按 **Enter** 键即可获取。某些命令需要参数，有时参数是可选的。

你可以通过查看该命令的在线帮助来了解它是否接受选项和参数，以及哪些是有效的，参见第 2.3 节。

在 Linux 中，就像在 UNIX 中一样，目录使用正斜杠分隔，就像在网址（URL）中使用的那样。我们稍后会深入讨论目录结构。

符号 **.** 和 **..** 在涉及目录时有特殊含义。我们将在练习中尝试了解这些符号，并在下一章中更详细地探讨。

尽量避免登录或使用*系统管理员*账户，即 *root*。除了执行常规工作外，大多数任务，包括检查系统、收集信息等，都可以使用没有任何特殊权限的普通用户账户来执行。如果需要，例如在创建新用户或安装新软件时，获取 root 访问权限的首选方式是切换用户 ID，参见第 3.2.1 节的示例。

本书中几乎所有的命令都可以在没有系统管理员权限的情况下执行。在大多数情况下，当以非特权用户身份发出命令或启动程序时，如果需要 root 访问权限，系统会发出警告或提示你输入 root 密码。完成后，请立即退出给你 root 权限的应用程序或会话。

阅读文档应该成为你的第二天性。尤其是在开始时，阅读系统文档、基本命令手册、HOWTO 指南等非常重要。由于文档的数量如此巨大，不可能包含所有相关文档。本书将尝试引导你找到每个讨论主题的最适当文档，以刺激阅读手册页（man pages）的习惯。

### 2.2.3 使用 Bash 功能

几种特殊的键组合可以让你在使用 GNU shell，Bash（几乎在任何 Linux 系统上的默认 shell）时更轻松、更快地完成任务，参见第 3.2.3.2 节。以下是常用功能列表；强烈建议你养成使用它们的习惯，以便从一开始就最大化你的 Linux 体验。

| **按键或键组合** | **功能** |
|-------------------------|------------|
| Ctrl+A | 将光标移动到命令行的开头。 |
| Ctrl+C | 结束正在运行的程序并返回提示符，参见第 4 章。 |
| Ctrl+D | 注销当前 shell 会话，等同于输入 `exit` 或 `logout`。 |
| Ctrl+E | 将光标移动到命令行的末尾。 |
| Ctrl+H | 生成退格字符。 |
| Ctrl+L | 清除此终端。 |
| Ctrl+R | 搜索命令历史，参见第 3.3.3.4 节。 |
| Ctrl+Z | 暂停程序，参见第 4 章。 |
| ArrowLeft 和 ArrowRight | 将光标在命令行上向左或向右移动一个位置，以便你可以不仅限于开头和结尾的其他位置插入字符。 |
| ArrowUp 和 ArrowDown | 浏览历史。转到你想要重复的行，如有必要编辑详细信息，然后按 Enter 以节省时间。 |
| Shift+PageUp 和 Shift+PageDown | 浏览终端缓冲区（查看已“滚动出”屏幕的文本）。 |
| Tab | 命令或文件名补全；当有多个选项时，系统会通过听觉或视觉铃声发出信号，或者如果可能的选项太多，询问你是否想查看它们。 |
| TabTab | 显示文件或命令补全的可能性。 |

表 2.2. Bash 中的键组合

上述表格中的最后两项可能需要额外的解释。例如，如果你想切换到目录 `directory_with_a_very_long_name`，你不需要输入那个非常长的名称。不。你只需在命令行输入 `cd dir`，然后按 **Tab** 键，如果没有其他文件以相同的三个字符开头，shell 就会为你补全名称。当然，如果没有其他以"d"开头的项，那么你最好直接输入 `cd d` 然后按 **Tab**。如果有多个文件以相同的字符开头，shell 会向你发出信号，此时你可以快速按两次 **Tab**，shell 会展示你拥有的选项：

```
your_prompt> cd st
starthere     stuff           stuffit
```

在上面的示例中，如果你在前两个字符后输入 "a" 并再次按 Tab，没有其他可能性了，shell 会补全目录名称，而不需要你输入字符串 "rthere"：

```
your_prompt> cd starthere
```

当然，你仍然需要按 Enter 来接受这个选择。

在同一个示例中，如果你输入 "u"，然后按 Tab，shell 会为你添加 "ff"，但它再次提出抗议，因为存在多个可能的选项。如果你再次按 Tab Tab，你会看到选项；如果你输入一个或多个使系统选择变得明确的字符，然后再次按 Tab，或者当你到达想要选择的文件名末尾时按 Enter，shell 会补全文件名并将你切换到该目录 - 如果它确实是一个目录名的话。

这对于作为命令参数的所有文件名都适用。

命令名称补全也是如此。输入 l s 然后按两次 Tab 键，会列出你的 PATH（参见第 3.2.1 节）中所有以这两个字符开头的命令：

```
your_prompt> l s
ls                lsdev             lspci             lsraid            lsw
lsattr            lsmod             lspnp             ls1616toppm
```

## 2.3 获取帮助

### 2.3.1 预警

GNU/Linux 的核心在于变得更加自力更生。通常在这个系统中，实现目标有多种方式。一种常见的求助方式是找一个懂的人，尽管使用 Linux 的社区再怎么耐心和爱好和平，几乎所有人都会期望你在询问他们之前已经尝试过本节中的一种或多种方法，如果你被证明没有遵循这一基本规则，表达这种观点的方式可能会相当严厉。

### 2.3.2 man 手册页

许多初学者害怕 man（manual）手册页，因为它们是一个压倒性的文档来源。然而，正如你从下面关于 man man 的示例中看到的，它们结构非常清晰。

阅读 man 手册页通常在图形模式下的终端窗口中进行，或者如果你更喜欢的话，也可以在文本模式下进行。在提示符处像这样输入命令，然后按 Enter：

`yourname@yourcomp ~ -> man man`

按 Enter 后，man 的文档将显示在你的屏幕上：

```
man(1)

NAME
man - format and display the on-line manual pages
manpath - determine user's search path for man pages

SYNOPSIS
man [-abcdefhkww?W] [-path] [-m system] [-p string] [-C config_file]
[-M pathlist] [-P pager] [-S section_list] [section] name ...

DESCRIPTION
man formats and displays the on-line manual pages. If you specify
section, man only looks in that section of the manual.
name is normally the name of the manual page, which is typically the
name of a command, function, or file. However, if name contains a
slash (/) then man interprets it as a file specification, so that you
can do man ./foo.5 or even man /cd/foo/bar.1.gz.

See below for a description of where man looks for the manual
page files.

OPTIONS
-C config_file
lines 1-27
```

使用空格键浏览到下一页。你可以使用 b 键返回上一页。当你到达末尾时，**man** 通常会退出，你重新获得提示符。如果你想在到达末尾之前离开 man 手册页，或者如果查看器没有在手页末尾自动退出，请键入 **q**。

### 分页器

用于操作 man 手册页的可用键组合取决于你的发行版中使用的*分页器*。大多数发行版使用 **less** 来查看 man 手册页和滚动。有关分页器的更多信息，参见第 3.3.4.2 节。

每个 man 手册页通常包含几个标准部分，正如我们从 **man** man 示例中看到的：

- 第一行包含你正在阅读的命令行名称，以及该 man 手册页所在部分的标识符。man 手册页按章节排序。命令可能有多个 man 手册页，例如来自用户部分的手册页、来自系统管理员部分的手册页，以及来自程序员部分的手册页。

