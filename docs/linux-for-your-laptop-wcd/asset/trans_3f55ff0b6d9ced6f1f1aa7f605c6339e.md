

- 选择对内存和磁盘空间使用较为保守的应用程序。如果需要执行电子表格操作，请尝试使用 `sc` 或 `teapop` 编辑器，而不是 `Applix`、`StarOffice` 或其他基于 GUI 的 X11 客户端。
- 删除不需要的文档。如果你安装了大多数发行版的全部文档，最终会得到法语、德语、意大利语、波兰语、希腊语、中文以及其他许多语言的文档。大多数完整的 /usr/doc 目录安装至少需要 200MB 的存储空间！
- 压缩所需的文档。如果你决定确实需要保留所有的 HOWTO，请使用 `gzip` 或 `bzip2` 命令来压缩所有文件。然后你可以使用 `zless` 等解压工具或分页器来阅读这些文件。
- 删除不需要的文档格式。大多数 Linux 发行版包含 HTML 和 SGML 格式的 HOWTO 和其他文件。你可以删除这些目录（通常位于 /usr/doc/HOWTO/otherformats 目录下），以节省至少 25MB 的驱动器空间。
- 删除示例文件。如果你熟悉已安装的软件，可以删除 /usr/doc 目录下几乎所有程序的辅助文档和示例文件。
- 清理临时文件或备份文件。定期使用脚本清理文件系统。
- 保持良好的备份。始终备份 /home 和 /etc 等重要目录。
- 如果需要更多存储空间，请考虑使用辅助外围设备，例如 Zip 驱动器。如果那太笨重，请使用 II 型闪存卡。IBM 现在市场销售的 MicroDrive 是一款 170 至 340MB 的驱动器，大小与紧凑闪存卡相当，可与 Linux 配合使用。
- 不要启动你不需要的服务。为了安全起见，编辑 /etc/inetd.conf 文件以关闭不需要的服务。Red Hat 和 Mandrake 用户应使用 `ntsysv` 命令来选择在启动过程中要启动的服务。SuSE Linux 用户应使用 `yast` 命令，Caldera OpenLinux 用户可以使用 `liisa` 命令或图形化 COAS 工具来控制系统服务。这将节省系统内存，并将运行的进程数保持在最低水平。

## 资源信息

- [http://www.tux.org/pub/knaff/mtools/](http://www.tux.org/pub/knaff/mtools/)

用于 UNIX 和 Linux 的 DOS 实用工具包 mtools 的主页。

- [http://www.mars.org/home/rob/proj/hfs/](http://www.mars.org/home/rob/proj/hfs/)

Robert Leslie 关于用于 UNIX 的 Macintosh 实用工具包 hfsutils 的主页。

- 多磁盘系统调优 HOWTO，作者 Stein Gjoen

包含关于 Linux 压缩文件系统方法的一些讨论。

- [http://www.netspace.net.au/~reiter/e2compr/](http://www.netspace.net.au/~reiter/e2compr/)

用于压缩 ext2 文件系统的 Linux 文件系统补丁的主页。

- crontab.5

详细列出 /etc/crontab 确切语法和结构的 man 手册页。

## 第 9 章：显示问题

- 使用控制台
- 使用虚拟控制台
- 使用 Xft
- 使用外部显示器
- 资源信息

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_236_0.png)

本章介绍你可以使用的技术和软件，以便在 Linux 会话期间充分利用你的笔记本显示屏。你将看到如何运行多个登录会话、运行和挂起程序、为控制台和 X11 设置颜色和字体、启动多个 X11 会话，以及如何最大化屏幕的实际使用空间。学习这里列出的一些技巧后，作为一名移动 Linux 用户，你将能够开发出属于自己的技术！

让我们从讨论 Linux 命令行界面开始，这就是控制台或纯文本模式。了解如何使用 Linux 命令行或 shell 是一项重要技能，也是学习 Linux 其他所有内容的基础。对于从其他操作系统迁移而来且不熟悉 DOS 的用户来说，命令行起初可能会让人望而生畏——但别担心！通过理解几个简单的概念并学习少量的命令，你可以快速掌握命令行。

### 使用控制台

与 Linux 内核（即核心操作系统）的主要接口是 shell。Linux 附带了十几个不同的 shell，但大多数用户会选择默认 shell，名为 `bash`（Bourne-Again Shell），它是自由软件基金会提供的成千上万个程序之一，对于操作 Linux 至关重要。Shell 解释你的命令并将信息发送给 Linux 内核，内核进而启动你的命令或提供其他服务，例如打开、读取、写入和关闭文件。

`bash` shell 具有许多不同的功能，例如提供内存变量（称为环境变量）；可自定义的提示符（即 shell 提示符）；内置帮助；以及将输入或输出发送到显示器、其他程序或其他文件的能力，这被称为输入/输出重定向。表 9.1 列出了你在 `bash` shell 中将使用的一些常见环境变量。

输入和输出重定向用于指定键盘输入、文本或程序从哪里获取输入，以及结果应发送到哪里，例如文件或设备。例如，你可以像这样构建 /usr/doc 目录下所有文件的即时目录：

```
$ ls -lR /usr/doc >helpfiles.txt
```

| 表 9.1 常见的 Bash Shell 变量 |
| :--- | :--- |
| BASH_ENV= | 你的 shell 资源文件 |
| EDITOR= | 默认的系统文本编辑器 |
| HISTSIZE= | 可用于历史记录的行数 |
| HOME= | 你的主目录 |
| HOSTNAME= | 你笔记本的主机名 |
| HOSTTYPE= | 正在使用的计算机类型 |
| LOGNAME= | 你的登录名 |
| MACHINE= | 你正在使用的系统类型 |
| MAIL= | 你的系统邮件目录 |
| NNTPSERVER= | 你的 ISP 的 Usenet 新闻服务器的主机名 |
| OSTYPE= | 正在使用的操作系统 |
| PATH= | 包含可执行程序的可识别目录 |
| PS1= | 你的 shell 提示符的定义 |
| PWD= | 当前工作目录 |
| SHELL= | 当前使用的 shell |
| TERM= | 如果你正在使用 X11，则是运行 shell 的终端类型 |
| USER= | 当前用户的用户名 |

在这个示例中，`ls` 命令的输出被重定向到一个文件。你还可以同时使用输入和输出重定向，使用 `cat` 命令创建一个简单的文本编辑器：

```
$ cat >myfile.txt <<.
> This is the most easy to use editor
> available for Linux, and will quickly
> create a short text file.
> .
```

在这个示例中，`cat` 命令被指示将其输出发送到文件 myfile.txt，而这里的重定向运算符（`<<.`）用于指定文件结束标记。在按下回车键后，你可以输入内容并按回车键来创建一个文本文件。

只有当 here 运算符检测到单独一行中有一个点 (.) 时，文件才会被关闭。这也表明 shell 是按行工作的。

你还可以将信息追加到现有文件中。例如，如果你有一个日志显示 Linux 已经运行了多长时间，你可以像这样将 `uptime` 命令的输出发送到日志：

```
$ uptime >>myuptime.log.txt
```

在这个示例中，使用追加 `>>` 运算符将 `uptime` 命令的输出附加到名为 myuptime.log.txt 的文件末尾。如果你只是使用输出 `>` 重定向运算符，`uptime` 命令的输出将抹掉日志文件中的任何现有文本。这表明你应该小心使用输出重定向。你可以快速且无情地覆盖文件。

### 使用 Shell

`bash` shell 还具有基本的命令行编辑功能，识别和使用命令同义词（称为别名）的能力，以及回忆之前命令行（称为历史编辑）的能力。表 9.2 列出了你可以在 `bash` shell 的命令行中使用的几种常见编辑命令。

你还可以使用称为扩展表达式或通配符（globbing）的功能来创建简单或极其复杂的模式或表达式。这些表达式可以从简单的（如 `*` 以匹配所有字符）到更复杂的（如 `{a-z}{0-9}*` 以匹配嵌入的字母和数字）范围不等。

经验丰富的移动 Linux 用户熟悉各种 Linux shell，并利用 shell 快速高效地完成任务。能够模拟其他 shell 的 `bash` shell 还可用于创建从简单到复杂的程序，称为 shell 脚本。Shell 编程是一门值得学习的精妙艺术和技艺，但你只需使用几个命令就可以构建自己的简单 shell 脚本。

### Bash 很大

如果你的笔记本硬盘空间紧张，并且你真的想使用精简系统，请考虑为 Linux 控制台会话使用替代 shell。你会发现至少还有另外两个 shell，即 `ash` 和 `csh`，它们能很好地满足大多数在线需求。其他 shell，如 `ksh`，也比 `bash` shell 小得多（`bash` 重近 0.5MB，而 `ash` shell 仅重 61,000 字符）。`csh` shell 在重启 Linux 进行紧急维修时被使用，因为它是独立的，不像其他 shell 那样需要共享软件库。

