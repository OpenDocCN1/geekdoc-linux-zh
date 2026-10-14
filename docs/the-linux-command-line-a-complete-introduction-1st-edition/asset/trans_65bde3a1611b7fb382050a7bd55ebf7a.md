

## 表 5-1：手册页组织

| 章节 | 内容 |
|---|---|
| 1 | 用户命令 |
| 2 | 内核系统调用的编程接口 |
| 3 | C 库的编程接口 |
| 4 | 特殊文件，如设备节点和驱动程序 |
| 5 | 文件格式 |
| 6 | 游戏和娱乐，如屏幕保护程序 |
| 7 | 杂项 |
| 8 | 系统管理命令 |

有时我们需要在手册的特定章节中查找所需内容。当我们查找的文件格式也与命令同名时尤其如此。如果我们不指定章节号，我们总是会得到匹配项的第一个实例，很可能在第 1 节。要指定章节号，我们这样使用 man：

```
man section search_term
```

例如：

```
[me@linuxbox ~]$ man 5 passwd
```

将显示描述 /etc/passwd 文件的文件格式的手册页。

## apropos—显示适当命令

也可以根据搜索词在手册页列表中搜索可能的匹配项。虽然粗糙，但这种方法有时很有帮助。以下是使用搜索词 floppy 搜索手册页的示例：

```
[me@linuxbox ~]$ apropos floppy
create_floppy_devices (8)  - udev callout to create all possible
floppy devices based on the CMOS type
fdformat              (8)  - Low-level formats a floppy disk
floppy                (8)  - format floppy disks
gfloppy               (1)  - a simple floppy formatter for the GNOME
mbadblocks            (1)  - tests a floppy disk, and marks the bad
blocks in the FAT
mformat               (1)  - add an MSDOS filesystem to a low-level
formatted floppy disk
```

每行输出中的第一个字段是手册页的名称，第二个字段显示章节。请注意，带有 -k 选项的 man 命令与 apropos 执行完全相同的功能。

## whatis—显示命令的非常简短的描述

whatis 程序显示与指定关键字匹配的手册页的名称和一行描述：

```
[me@linuxbox ~]$ whatis ls
ls (1) - list directory contents
```

## 有史以来最残酷的手册页

正如我们所见，随 Linux 及其他类 Unix 系统提供的手册页旨在作为参考文档，而不是教程。许多手册页难以阅读，但我认为难度大奖非 bash 的手册页莫属。在为本书做研究时，我仔细审阅了它，以确保涵盖了其大部分主题。打印出来超过 80 页，极其密集，其结构对新用户来说完全没有意义。

另一方面，它非常准确、简洁，而且极其完整。所以如果你敢，就去看看吧，并期待有一天你能读懂它，一切都变得有意义。

## info—显示程序的 Info 条目

GNU 项目提供了一种名为 info 页面的手册页替代方案。Info 页面由一个名为 info 的阅读器程序显示。Info 页面像网页一样具有超链接。以下是一个示例：

```
File: coreutils.info, Node: ls invocation, Next: dir invocation, Up: Directory listing
```

### 10.1 'ls'：列出目录内容

'ls' 程序列出有关文件的信息（任何类型，包括目录）。选项和文件参数可以任意混合，就像通常一样。

对于非选项命令行参数，如果是目录，默认情况下 'ls' 会列出目录的内容，而不是递归列出，并省略以 '.' 开头的文件名。对于其他非选项参数，默认情况下 'ls' 只列出文件名。如果未指定非选项参数，'ls' 将在当前目录上操作，就好像它是用单个参数 '.' 调用的那样。

info 程序读取 info 文件，info 文件以树状结构分为各个节点，每个节点包含一个主题。Info 文件包含可将您从一个节点移动到另一个节点的超链接。超链接可以通过其前导星号来识别，并通过将光标置于其上并按 ENTER 键来激活。

要调用 info，输入 info，后跟可选的程序名称。表 5-2 列出了在显示 info 页面时用于控制阅读器的命令。

### 表 5-2：info 命令

| 命令 | 操作 |
|---|---|
| ? | 显示命令帮助。 |
| PAGE UP 或 BACKSPACE | 显示上一页。 |
| PAGE DOWN 或 Spacebar | 显示下一页。 |
| n | 下一个—显示下一个节点。 |
| p | 上一个—显示上一个节点。 |
| u | 上级—显示当前显示节点的父节点，通常是菜单。 |
| ENTER | 跟随光标位置处的超链接。 |
| q | 退出。 |

我们迄今为止讨论的大多数命令行程序都是 GNU 项目 coreutils 包的一部分，因此您可以通过输入以下命令找到有关它们的更多信息

```
[me@linuxbox ~]$ info coreutils
```

这将显示一个菜单页面，其中包含指向 coreutils 包提供的每个程序文档的超链接。

## README 和其他程序文档文件

安装在系统上的许多软件包在 /usr/share/doc 目录中都有文档文件。其中大多数以纯文本格式存储，可以使用 less 查看。其中一些文件为 HTML 格式，可以使用网页浏览器查看。我们可能会遇到一些以 .gz 扩展名结尾的文件。这表示它们已使用 gzip 压缩程序进行压缩。gzip 包包含一个名为 zless 的特殊版本的 less，它将显示 gzip 压缩文本文件的内容。

