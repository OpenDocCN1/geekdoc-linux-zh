
某些程序不支持 `--help` 选项，但仍可以尝试一下。它通常会产生一条错误信息，从而显示相同的用法信息。

## man—显示程序的手册页

大多数为命令行设计的可执行程序都提供一份正式文档，被称为 *manual*（手册）或 *man page*。使用名为 `man` 的特殊编程语言来查看它们。其用法如下：

```
man program
```

其中 `program` 是要查看的命令名称。

手册页的格式略有不同，但通常包含以下内容：

- 标题（页名）
- 命令语法的摘要
- 命令用途的描述
- 命令每个选项的列表和描述

然而，手册页通常不包含作为参考的示例，而不是教程。作为一个例子，让我们尝试查看 `ls` 命令的手册页。

```
me@linuxbox ~$ man ls
```

在大多数 Linux 系统上，`man` 使用 `less` 来显示手册页，因此在显示页面时所有熟悉的命令都可以正常工作。

`man` 显示的“手册”分为若干章节，不仅涵盖了用户命令，还涵盖了系统管理命令、编程接口、文件格式等。表 5-1 描述了布局。

### 表 5-1: 手册页结构

| 章节 | 内容 |
|---|---|
| 1 | 用户命令 |
| 2 | 内核系统调用的编程接口 |
| 3 | C 库的编程接口 |
| 4 | 特殊文件，如设备节点和驱动程序 |
| 5 | 文件格式 |
| 6 | 作为屏幕保护的游戏和娱乐 |
| 7 | 杂项 |
| 8 | 系统管理命令 |

有时我们需要参考手册的特定章节来找到我们要寻找的内容。如果我们寻找的格式格式恰好也是某个命令名称，这一点尤为如此。如果不指定章节号，我们总是得到第一个匹配项，可能在第 1 节。要指定章节号，我们这样使用 `man`：

```
man section search_term
```

这里有一个示例：

```
me@linuxbox~$ man 5 passwd
```

这将显示描述 `/etc/passwd` 文件格式的手册页。

## apropos—显示相关的命令

也可以根据搜索词在手册页列表中搜索可能的匹配项。这听起来很奇怪，但有时很有帮助。这是一个使用搜索词 `partition` 搜索手册页的示例：

```
[me@linuxbox~$ apropos partition
part (8) - "add partition" ioctl 的简单封装
all-swaps (7) - 表示所有交换分区已完成的事件信号
cfdisk (8) - 显示或操作磁盘分区表
cgdisk (8) - Curses-GUID 分区表 (GPT) 操纵器
delpart (8) - "del partition" ioctl 的简单封装
fdisk (8) - 操作磁盘分区表
fixparts (8) - MTR 分区表修复工具
gdisk (8) - 交互式 GUID 分区表 (GPT) 操纵器
partition (1) - 分区和硬盘
partprobe (8) - 通知操作系统分区表更改
partx (8) - 告诉 Linux 内核分区的存在和编号...
resizepart (8) - "resize partition" ioctl 的简单封装
sfdisk (8) - Linux 分区表操纵器
sdisk (8) - 命令行分区表 (GPT) 操纵器。
```

输出每行的第一个字段是手册页的名称，第二个字段显示章节。注意带有 `-k` 选项的 `man` 命令与 `apropos` 功能相同。

## whatis—显示单行页面描述

`whatis` 程序显示匹配关键词的手册页名称和单行描述。

```
me@linuxbox~$ whatis ls
ls (1) - 列出目录内容
```

## 显示程序的信息

GNU 项目为其程序提供了手册页的替代方案，称为 `info`。`info` 手册使用阅读器显示。`info` 页面像网页一样带有超链接。以下是一个示例：

```
File: coreutils.info, Next: dir invocation, Up:
Directory listing
10.1 'ls': List directory contents
=====================
The `ls` 列出关于文件（任何类型，包括目录）的信息。选项和文件参数可以像往常一样任意交替出现。
对于目录的非选项命令行参数，默认情况下 `ls` 列出目录的内容，而不是递归的，并省略以 ' .' 开头的文件。对于其他非选项参数，默认情况下 `ls` 列出文件名。如果未指定非选项参数，`ls` 将在当前目录上操作，就像被带有一个单个参数 '.' 被调用用一样。
```

`info` 程序读取文件，这些文件以树形结构组成各个节点，每个节点包含一个主题。`info` 文件包含超链接，可以让你从一个节点跳转到另一个节点。超链接可以通过开头的星号 `*` 识别，并通过将光标置于其按下 ENTER 来激活。

调用 `info` 时，输入 `info` 后跟可选的程序名称。表 5-2 描述了在显示 `info` 页面时控制阅读器的命令。

### 表 5-2: info 命令

| 命令 | 操作 |
|---|---|
| ? | 显示帮助 |
| UP 或 BACKSPACE | 显示上一页 |
| PAGE DOWN 或 空格 | 显示下一页 |
| n | 显示下一个节点 |
| p | 显示上一个节点 |
| U | 显示当前显示节点的父节点，通常是菜单 |
| ENTER | 跟随光标处的超链接 |
| Q | 退出 |

我们为止讨论的大多数命令行程序都是 GNU 项目 `coreutils` 软件包的，因此输入以下：

```
$ me@linuxbox ~ info coreutils
```

将显示一个带有 `coreutils` 软件包中包含的程序超链接的菜单页面。

# README 和其他程序文档文件

安装在你的系统上的许多软件包都有位于 `/usr/share/doc` 目录的文档文件。其中大多数文件以普通文本格式存储，并可以使用 `less` 命令查看。某些文件是 HTML 格式，可以使用网络浏览器查看。我们可能会遇到一些以 `.gz` 扩展结尾的文件。这表示它们已用 `gzip` 压缩程序进行了压缩。`gzip` 软件包包含一个特殊版本的 `less`（即 `zled`），它可以显示 `gzip` 文件的内容。

# 使用 alias 创建我们自己的命令

现在开始我们的第一次编程之旅了！我们将使用 `alias` 命令创建一个我们自己的命令。但在开始之前，我们需要揭示一个小小的命令技巧。通过用分号 `;` 隔开每个命令，可以在同一行内放置多个命令。它的工作方式如下：

```
command1; command2; command3...
```

这里是我们使用的示例：

```
[me@linuxbox ~]$ cd /usr; ls; cd -
bin games include local sbin share src
home/me~
[me@linuxbox ~]$
```

正如我们所看到的，我们在一行中组合了三个命令。首先，我们将工作目录更改到 `/usr`，然后列出目录，最后返回原始目录（通过 `cd -`），这样我们就回到了起点。现在，让我们用 `alias` 将这个序列转换为新命令。我们必须做的第一件事是为新命令想一个名字。让我们尝试一下 `test`。在此之前，最好检查一下 `test` 这个名字是否已经在使用中。要查明这一点，我们可以再次使用 `type` 命令。

```
[me@linuxbox ~]$ type test
test is a shell builtin
```

哎呀！`test` 名字已经被占用了。让我们试试 `foo`。

```
[me@linuxbox ~]$ type foo
bash: type: foo: not found
```

太太棒了！`foo` 没有被占用。那么，让我们创建自己的别名。

```
@me@linux~$ alias foo='cd /usr; ls; cd -'
```

注意这个命令的结构，如下所示：

```
alias name='string'
```

在 `alias` 命令之后，我们给别名起一个名字，紧接着（一个等号（不允许有空格），等接着紧跟一个包含分配给该名称含义的引号字符串。定义好别名后，我们可以在 shell 预期命令的地方使用它。试试看。

```
@me@linux~$ foo
bins games include lib sbin share src
home/me
@me@linux~$
```

我们也可以使用 `type` 命令来查看我们的别名。

```
@me@linux~$ type foo
foo is aliased to cd /usr; ls; cd -
```

要删除别名，使用 `unalias` 命令，所以：

```
@me@linux~$ unalias foo
@me@linux~$ type foo
bash: type: foo: not found
```
