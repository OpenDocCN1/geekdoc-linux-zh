
保存`.bash_aliases`，使用`.bash_aliases`命令重新加载它，别名将不再生效。但如果你以后再次需要它，打开`.bash_aliases`，删除井号，保存并重新加载文件，它就可以再次使用了。

### 总结

作为Linux用户，你的目标之一是减少完成目标时需要输入的字符数量。Unix的原始开发者们深信这样一种理念：你应该输入`ls`而不是`makedirectory`。

你在本章中学习的命令在这一过程中都包含了别名（`alias`）的功能。厌倦了输入长而复杂的命令吗？通过`history`引用它，或者为它创建一个别名。无论哪种方式，你都能节省击键次数，你的键盘（更重要的是你的手和手腕）会为此感谢你的。

## 第 12 章 监控系统资源

一个良好的计算机用户应该兼任系统管理员，随时检查机器的健康状况，以确保一切运行顺利。为了帮助实现这一目标，Linux有几条命令可以监控资源。在本章中，你将查看其中的几个命令。它们中的许多都有多种用途，但Unix用小工具完美解决单一任务的传统在系统监控的一个特定方面尤为出色。它们的任务从跟踪计算机上运行的进程（`ps`和`top`）到结束错误进程（`kill`）、列出所有打开的文件（`lsof`），以及报告RAM使用情况（`free`）和磁盘空间（`df`和`du`）。学好这些工具，你会在各种情况下用到它们。

### 查看所有当前运行的进程

`ps aux`

偶尔你运行的某个程序会卡死并停止，需要你将其关闭。或者你可能想知道某个用户正在运行哪些程序。或者你只是想知道你机器上当前运行的进程。在这些任何一种以及许多其他情况下，你都会使用`ps`命令来列出计算机上的进程。

遗憾的是，`ps`有很多版本，它们具有不同类型的选项。取决于这些选项前是否带有连字符，它们的含义甚至可能不同，因此`u`和`-u`的含义是完全不同的。到目前为止，本书在描述`ps`的带连字符选项时一直非常严格，其实不必，这会让事情变得更简单、更统一。

要查看用户在系统上运行的所有进程，请在`ps`后面加上这些选项：`a`（表示所有用户）、`u`（面向用户，或显示谁在使用aux）以及`x`（没有控制终端的进程，即“显示每个进程”的另一种说法）。请准备好一大长列表将划过你的屏幕：这台电脑上有132行。

```bash
User      $ ps aux %CPU %MEM VSZ RSS TTY START STAT TIME COMMAND

scott 24224 4.1 4.2 115040 44036 7 R 11:02 12:03 /home/scott/.coxoffice/bin/wine-preloader

scott 5594 0.0 0.1 3432 1820 pts/6 S+ 12:14 0:00 scott@humbug,machine.com

scott 14957 0.3 7.5 171144 78628 7 S1 13:01 0:35 /usr/lib/openoffice2/program/soffice.bin -writer

scott 12369 0.0 0 0 7 Z 15:43 0:00 [wine-preloader]<defunct>

scott 14680 0.0 0.1 3860 1044 pts/5+ R 15:55 0:00 ps aux
```

`ps`命令为你提供了大量信息，包括哪个用户拥有该进程、标识进程的唯一ID数字（`PID`）、进程使用的CPU百分比（`%CPU`）和内存百分比（`%MEM`）、进程的当前状态（`STAT`）以及进程本身的名字。

`STAT`列可能有不同的字母，以下是最重要的：

| STAT字母 | 含义 |
| :--- | :--- |
| R | Running (运行中) |
| S | Sleeping (睡眠中) |
| T | Stopped (停止) |
| Z | Zombie (僵尸进程) |

`Z`是不好的，因为它意味着进程已经挂起。如果你对`.bash_aliases`中找到的别名使用`unalias`命令，它是没问题的，但仅限于你登录期间有效。当你注销并重新登录，或者重新加载`.bash_aliases`时，别名就会回来。

要从`.bash_aliases`中删除别名，你需要编辑该文件并手动删除包含该别名的行。如果你以后可能还会再次使用该别名，只需在文件行前加一个井号（这将其注释掉），如下：

```bash
# alias lsd='ls -d *'
```

保存`.bash_aliases`，使用`.bash_aliases`命令重新加载它，别名将不再生效。但如果你以后再次需要它，打开`.bash_aliases`，删除井号，保存并重新加载文件，它就可以再次使用了。

### 查看进程树 (Process Tree)

`ps axjf`

在Linux世界中，进程通常以父子关系组织。

```bash
$ ps axjf

UID  PPID PID TTY S TIME COMMAND

root    1 1 ? S 0:00 /systemd

root    1 2 ? S 0:00 /systemd-journal-write

scott 1 24224 ? R 12:03 /home/scott/.coxoffice/bin/wine-preloader

scott 1 5594 pts/6 S+ 0:00 scott@humbug,machine.com

scott 1 14957 pts/7 S1 0:35 /usr/lib/openoffice2/program/soffice.bin -writer

scott 1 12369 ? Z 0:00 [wine-preloader]<defunct>

scott 1 14680 pts/5+ R 0:00 ps aux
```

`ps`命令为你提供了大量信息，包括哪个用户拥有该进程、标识进程的唯一ID数字（`PID`）、进程使用的CPU百分比（`%CPU`）和内存百分比（`%MEM`）、进程的当前状态（`STAT`）以及进程本身的名字。

`STAT`列可能有不同的字母，以下是最重要的：

| STAT字母 | 含义 |
| :--- | :--- |
| R | Running (运行中) |
| S | Sleeping (睡眠中) |
| T | Stopped (停止) |
| Z | Zombie (僵尸进程) |

`Z`是不好的，因为它意味着进程已经挂起。如果你对`.bash_aliases`中找到的别名使用`unalias`命令，它是没问题的，但仅限于你登录期间有效。当你注销并重新登录，或者重新加载`.bash_aliases`时，别名就会回来。

要从`.bash_aliases`中删除别名，你需要编辑该文件并手动删除包含该别名的行。如果你以后可能还会再次使用该别名，只需在文件行前加一个井号（这将其注释掉），如下：

```bash
# alias lsd='ls -d *'
```
