

要编辑你自己的 crontab 文件，输入 `crontab -e`。这会打开一个文本编辑器（默认是 vim，但你可以通过设置 EDITOR 环境变量来更改），在其中你可以输入条目。此文件的格式与主 crontab 的格式略有不同，因为这次无需指定作业的所有者——它始终是你。

因此，这次每一行由六个字段组成：分钟（0–59）、小时（0–23）、月份中的日期（1–31）、年份中的月份（1–12）、星期几（0–7），然后是要运行的命令。如果你使用 vim 并且是新手，按 i 进入插入模式以编辑文本；然后按 Esc 退出插入模式。要保存并退出，输入冒号后跟 wq 并按 Enter。

在编程时，我们倾向于在主目录中使用一个沙箱子目录，在那里我们存放各种临时文件，我们只是随便玩玩。我们可以使用个人作业在每天早上 6 点清空该目录，以便每天早上都能重新开始。以下是它在我们的 crontab 文件中的样子：

```
0 6 * * * rm -rf /home/paul/sandbox/*
```

如果你不被允许安排作业，你将无法编辑你的 crontab 文件。

一旦你的作业被放置，你可以使用命令 `crontab -l` 来列出你的作业。这只是打印你的 crontab 文件的内容，因此其输出将与你刚刚输入的行相同。

如果你只想删除一个作业，最简单的方法是输入 `crontab -e` 以在 vim 中编辑你的 crontab 文件；然后，在将光标移动到你想要删除的作业之后，输入 dd（两个 d）来删除该行。如果你想删除所有作业，你可以使用 `crontab -r` 来删除你的 crontab 文件。

## Basic Shell Control

Ubuntu 包含丰富的、功能强大、灵活且功能强大的 shell 集合。每个 shell 都不同，但都有许多内置命令和可配置的命令行提示，并且可能包括诸如命令行历史、召回和重用之前的命令行以及命令行编辑等功能。作为一个例子，bash shell 如此强大，以至于完全可以用 bash 的语言编写一个最小的 web 服务器，使用 114 行脚本（参见本章末尾的链接）。

尽管有许多 shell 可供选择，但大多数人坚持使用默认的 bash。这是因为 bash 可以完成大多数人需要做的一切，而且更多。只有在你真的需要时才更改你的 shell。

表 11.1 列出了每个 shell，以及在你的 Ubuntu 文件系统中的描述和位置。

### TABLE 11.1 Shells with Ubuntu

| Name | Description | Location |
|---|---|---|
| bash | The Bourne Again SHell | /bin/bash |
| ksh | The Korn shell | /bin/ksh, /usr/bin/ksh |
| pdksh | A symbolic link to ksh | /usr/bin/pdksh |
| rsh | The restricted shell (for network operation) | /usr/bin/rsh |
| sh | A symbolic link to bash | /bin/sh |
| tcsh | A csh-compatible shell | /bin/tcsh |
| zsh | A compatible csh, ksh, and sh shell | /bin/zsh |

## Learning More About Your Shell

表 11.1 中列出的所有 shell 都有相应的 man 手册，以及 /usr/share/doc 目录下的其他文档。有些文档可能相当冗长，但通常拥有太多文档总比太少要好！bash shell 的手册包含超过 100 页，而 zsh shell 的文档如此详尽，以至于它包含 zsh11 元 man 手册（使用 man zsh11 阅读此概述）！

## The Shell Command Line

对 shell 命令行功能的基本了解可以帮助你编写更好的 shell 脚本。如果在读完这篇简短介绍后，你想了解更多关于命令行的信息，请查看第 33 章，“Command Line Masterclass”。你可以使用 shell 命令行执行多种不同的任务，包括

- 使用模式匹配或表达式的程序搜索文件或目录；这些命令包括 GNU gawk（链接为 awk）和 grep 系列命令，包括 egrep 和 fgrep。
- 从文件或命令获取数据并向文件或命令发送数据，被称为输入和输出重定向。
- 将程序的输出馈送或过滤到另一个命令（称为使用管道）。

shell 还可以具有内置的作业控制命令，用于将命令行作为后台进程启动、挂起正在运行的程序、有选择地检索或终止正在运行或挂起的程序，并执行其他类型的进程控制。

