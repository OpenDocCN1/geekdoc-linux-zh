

# 第 3 章 命令行

不存在于你的主目录，然后在同一行中紧接着执行 `date` 命令：

```
[master@server ~]$ ls does-not-exist.txt && date
ls: cannot access does-not-exist.txt: No such file or directory
```

此命令将运行 `ls` 命令，但该命令会失败，因为它尝试列出的文件并不存在，因此 `date` 命令不会被执行。但如果你交换命令的顺序，你会发现 `date` 命令执行成功，而 `ls` 命令将失败：

```
[master@server ~]$ date && ls does-not-exist.txt
Sun Jan 30 18:06:37 PDT 2092
ls: cannot access does-not-exist.txt: No such file or directory
```

# 反引号 (Backticks)

这听起来酷吗？你可以将一个程序的输出作为另一个程序的参数。听起来很不可思议吗？是时候了解它了——这是 UNIX Shell 中提供的许多实用且创新的特性之一。

任何在反引号 `` ` `` 内的文本都会被视为要执行的命令。它允许你在反引号中嵌入命令，并将结果作为参数传递给其他命令，例如。你将在本书和各种系统脚本中经常看到这种技术。例如，你可以传递一个数字（存储在文件中的进程 ID，然后将该数字作为参数传递给 `kill` 命令）。

这种用法的一个示例是杀死（停止）名为 `named` 的域名系统（DNS）服务器。当 `named` 启动时，它会将进程标识（PID）写入文件 `/var/run/named/named.pid`。因此，杀死 `named` 进程的一种通用且粗暴的方法是使用 `cat` 命令查看 `/var/run/named/named.pid` 中的数字，然后使用该值发出 `kill` 命令。这里有一个例子：

```
[root@server ~]$ cat /var/run/named/named.pid
253
```

```
[root@server ~]$ kill 253
```

通过这种方式处理 `named` 进程的一个问题是它无法被自动化——我们依赖于人类会读取 `/var/run/named/named.pid` 并传递给 `kill` 工具。另一个问题与其说是麻烦，不如说是令人不便：停止 DNS 服务器需要两个步骤。

然而，使用反引号，你可以将这些步骤合并为一个，并以可以自动化的方式进行。反引号版本看起来如下：

```
[root@server ~]$ kill 'cat /var/run/named/named.pid'
```

# Linux 系统管理：学者指南

当 Bash 看到此命令时，它会首先运行 `cat /var/run/named/named.pid` 并存储结果。然后它将运行 `kill` 并将存储的结果传递给它。从我们的角度来看，这是在一个优雅的步骤中完成的。

> 注意到本章为止，我们查看了 Bash 内部的特性（有时称为 Bash 内置命令，Bash built-ins）。该章节的剩余部分探索了 Bash 之外的几个常用命令。

# 文档工具

Linux 提供了两个优秀的工具来让文档易于获取：`man` 和 `info`。目前，这两个文档系统之间存在大量重叠，因为许多应用程序正在将文档迁移到 `info` 格式。它被认为优于 `man`，因为它允许以类似网页的方式进行超链接，而无需实际上使用超文本标记语言（HTML）格式。

另一方面，`man` 格式已经存在了几十年了。对于数千个工具/程序来说，它们的 man 页面是它们唯一的文档来源。此外，许多应用程序继续利用 `man` 格式，因为许多类 Unix 操作系统（如 Sun Solaris）都在使用它。

`man` 和 `info` 文档系统在未来一段时间内都会存在。强烈建议你熟悉两者。

> 提示 Linux 发行版在 `/usr/doc` 或 `/usr/share/doc` 目录下也包含大量文档。

# man 命令

man 页面是 Linux 系统上的一种内置和自文档化系统，涵盖了工具的使用及其相应的配置文件。`man` 命令的语法如下：

```
man program_name
```

在这里，`program_name` 指定你感兴趣的程序。例如，要查看你一直在使用的 `ls` 工具的 man 页面，请输入：

```
[master@server ~]$ ls
```

在阅读关于 Linux 和 Linux 相关信息源（新闻组等）时，你可能会遇到命令后面跟着括号数字的引用——例如 `ls (1)`。该数字代表手册页的章节（参见表 3-1）。每个章节涵盖不同的主题以适应...

# 表 3-1 man 页面章节

| 手册章节 | 主题 |
| --- | --- |
| 1 | 标准命令、可执行程序或 shell 命令 |
| 1p | 标准命令的 POSIX 版本；小写 p 代表 POSIX |
| 2 | Linux 内核系统调用（内核提供的函数） |
| 3 | C 语言库调用 |
| 4 | 设备驱动程序信息 |
| 5 | 配置文件 |
| 6 | 游戏 |
| 7 | 软件包 |
| 8 | 系统工具 |

