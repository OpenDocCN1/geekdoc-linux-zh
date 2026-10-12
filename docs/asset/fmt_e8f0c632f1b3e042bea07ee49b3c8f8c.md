
Linux 文件系统还描述了存放构成 Linux 的所有文件的结构。它基于根树模型。该树由目录和文件组成。每个目录可以包含一个或多个子目录。目录用于组织文件，每个目录或子目录可以包含零或多个文件。文件包含信息（数据）、可执行程序或脚本、设备信息，或者空无一。

`![](img/29df11d9c5c608cff7b4fa65d0c78e37_144_1.png)`

## 第二部分：背景

你了解得越多，就越好。在操作一段时间后，你会直能地知道最重要文件的位置，以及通常在哪里可以找到大多数其他文件。

根目录是所有目录的母目录。`列表 3-5` 显示了红帽（Red Hat）配置下的根目录（其他发行版如 Slack 有不同的设置，但基本上是相同的）。它的结构非常重要，因为根目录是你访问其余 Linux 文件系统的起点。

### 列表 3-5：根目录列表

```
total 48

drwxr-xr-x  2 root root   2048 Dec  8 13:59 bin
drwxr-xr-x  2 root root   1024 Dec  8 14:01 boot
drwxr-xr-x  2 root root   2048 Dec  8 22:03 dev
drwxr-xr-x 19 root root   2048 Dec  8 22:03 etc
drwxr-xr-x 16 root root   1024 Dec  8 21:17 home
drwxr-xr-x  4 root root   2048 Dec  8 13:58 lib
drwxr-xr-x  2 root root  12288 Dec  8 13:51 lost+found
drwxr-xr-x  4 root root   1024 Dec  8 14:01 mnt
dr-xr-xr-x  5 root root      0 Dec  8 15:05 proc
drwxr-xr-x  3 root root   1024 Dec  8 22:11 root
drwxr-xr-x  3 root root   2048 Dec  8 13:59 sbin
drwxrwxr-t  2 root root   1024 Dec  8 13:56 tmp
drwxr-xr-x 18 root root   1024 Dec  8 13:55 usr
drwxr-xr-x 12 root root   1024 Dec  8 13:54 var
```

多年来，某些文件在某些目录中找到了家。例如，你可以预期在 `/etc` 目录下找到密码文件 `passwd`。运行以下命令并查看：

```
ls -l /
```

它应该在那里（如果不在那里，你可能无法登录）。不同 UNIX 版本使用的文件系统演化方式不同。你可以很容易地识别 `System V` 或 `BSD` 文件系统。它们通常看起来相似，但仔细观察会发现显著差异，例如启动脚本的位置（`System V` 将它们放在 `/etc/rc`，而 `BSD` 将它们留在 `/etc/`）。然而，Linux 社区正努力避免这种情况。

### 观察 Linux 文件系统标准

Linux 社区正在将 Linux 文件系统标准化。几个 Linux 发行版——特别是红帽和 `Candida`——在遵循 Linux 文件系统标准（`FHS`）方面做得很好。由于制造商标准的演变和市场的喜变化，你总是能发现例外，但 `FHS` 实际上考虑到了这一点，并且本身也是一个正在进行中的工作。

## 第 3 章：内部结构是什么？

- `/usr/X11R6/doc` 包含不属于标准 `XFree86` man 系统（man 页）的文档。（注意：`XFree86` man 页的格式与标准 Linux man 页格式相同。）

- `/usr/X11R6/include` 存放头文件。这些文件包含了在编译期间包含到源代码文件中的常量和其他内容。

- `/usr/X11R6/lib` 包含 `XFree86` 特有的库。

- `/usr/X11R6/man` 存放 `XFree86` 的手册页。

- `/usr/bin` 以及 `/sbin` 包含了大多数被认为是标准的 Linux 程序——从 `clear` 到 `gcc` 再到 `zip` 的一切。

- `/usr/dict` 拥有 Linux 字典。

- `/usr/doc` 包含许多实用的文档、`FAQ`、`HOWTO` 等。更多信息请参见第 5 章。

- `/usr/etc` 目前是空的。（注意：`Slack` 有指向 `printconfig` 文件的链接，该文件配置打印机。）

- `/usr/games` 是存储游戏的地方。

- `/usr/i486-linux-lib5` 包含旧版本的库。

- `/usr/include` 拥有更多的头文件。

- `/usr/info` 包含各种主题的 `GNU` 超文本文件。有关这些文件的信息，请参见 `info` 的 man 页。

- `/usr/lib` 包含 Linux 库。

- `/usr/man` 存放大多数 Linux man 页。它分为九部分，反映了 `Linux/UNIX` 惯例。`表 3-1` 详细说明了 Linux man 页的组织。

- `/usr/sbin` 拥有系统命令和守护进程。

- `/usr/share` 用于存储通用应用程序——`awk`、`ghostscript` 等——所有用户通用的程序。

- `/usr/src` 是你存储 Linux 或其他源代码的地方。

- `/usr/local` 包含一个与 `/usr` 类似的层次结构，用于存储本地程序和库。它用于保持 `/usr` 尽可能稳定。通过遵循这一惯例，可以更容易跟踪你在系统上安装的所有内容。

## 第二部分：背景

`表 3-1 LINUX MAN 页组织`

| 编号 | 内容 |
| :--- | :--- |
| 1 | 用户命令和应用程序 |
| 2 | 系统调用和内核错误代码 |
| 3 | 库调用 |
| 4 | 设备驱动程序 |
| 5 | 文件格式 |
| 6 | 导读 man 页 |
| 7 | 系统和软件包描述 |
| 8 | 网络和系统命令及工具 |
| 9 | 当前为空 |

尽管 `System V` 和 `BSD` 通常具有相似的结构，但它们在许多细节上有所不同。

当你将这一切整合在一起时，你就拥有了一个高效实用的文件系统。随着时间的推移，它将变成一个熟悉、有些枯燥的朋友。我怀疑随着时间的推移，它将成为整个 Linux 世界的标准，你将在世界上任何地方熟练操作 Linux 系统。

### 理解 Linux 启动过程

Linux 启动过程相当复杂。当 `PC` 开启或重启时，位于磁盘引导区的一个小型自型引导程序会被自动执行。内核存储在磁盘上的已知位置，引导程序将内核加载到内存并启动它（你会看到几行点，表示内核正在加载）。

> 如果你想阅读有关此启动过程的详细信息，《系统管理员指南》在 `http://www.redhat.com/linux-info/ldp/LDP/sag` 讨论了该主题

## 第 3 章：内部结构是什么？

内核启动后，它会对计算机的硬件配置进行扫描。当你观察内核启动时，你会看到类似于 `列表 3-6` 所示的信息。注意内核如何检查内存、软磁盘、硬盘、`CD-ROM` 和以太网适配器。它需要这些设备的参数以便管理它们与你的交互。

`列表 3-6：内核在启动过程中确定硬件配置`
