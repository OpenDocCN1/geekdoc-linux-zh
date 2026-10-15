
这非常有用！使用这种技术，我们可以方便地检查任何产生标准输出的命令的输出。

# 过滤器

管道通常用于对数据执行复杂操作。可以将多个命令组合成一个管道。通常，以这种方式使用的命令被称为过滤器（filters）。过滤器接收输入，以某种方式对其进行更改，然后输出。我们将尝试的第一个是 `sort`。假设我们想对 `/bin` 和 `/usr/bin` 中的所有可执行程序创建一个合并列表，将它们按顺序排序，并查看该列表：

```
~linux$ ls /bin /usr/bin | sort | less
```

由于我们指定了两个目录（`/bin` 和 `/usr/bin`），`ls` 的输出将包含两个排序后的列表，每个目录一个。通过在管道中加入 `sort`，我们更改了数据，生成了一个单一的排序列表。

# 报告或省略重复行

`uniq` 命令经常与 `sort` 配合使用。`uniq` 接受来自标准输入或单个文件参数的排序列表（详情参见 `uniq` 的 `man`页），并默认删除列表中的任何重复项。因此，为了让我们的列表没有重复项（即同时出现在 `/bin` 和 `/usr/bin` 目录中的同名程序），我们在管道中添加了 `uniq`：

```
~linux$ ls /bin /usr/bin | sort | uniq | less
```

在这个示例中，我们使用 `uniq` 来移除 `sort` 命令产生的任何重复项。如果我们想查看重复项列表，则给 `uniq` 添加 `-d` 选项，如下所示：

```
~linux$ ls /bin /usr/bin | sort | uniq -d | less
```

# 打印行、字和字节数

`wc`（word count）命令用于显示在文件中统计的行数、字数和字节数。例如：

```
~linux$ wc ls-output.txt
7902 64566 503634 ls-output.txt
```

在这种情况下，它打印三个数字：`ls-output.txt` 中包含的行、字和字节。与我们之前的命令一样，如果不带命令行参数执行，它接受标准输入。`-l` 选项将其输出限制为仅报告行。将其添加到管道中是计数项目的一种方便方法。要查看我们排序列表中的项目数量，我们可以这样做：

```
@melinux~$ ls /bin /usr/bin | sort | uniq | wc -l
2728
```

# grep—打印匹配模式的行

`grep` 是一个强大的程序，用于在文件中查找文本模式，如下：`grep pattern [file]`。

当 `grep` 在文件中遇到“模式”时，它会打印包含该模式的行。`grep` 匹配的模式可以非常复杂，但目前我们将集中在简单的文本匹配上。我们将在第 19 章介绍被称为*正则表达式*（regular expressions）的高级模式。

假设我们想在程序列表中找到所有名称中包含 `zip` 的文件。这样的搜索可能会让我们了解系统中有哪些程序与压缩有关。我们将这样做：

```
@melinux~$ ls /bin /usr/bin | sort | uniq | grep zip
bunzip2
bzip2
gunzip
gzip
unzip
zip
zipcloak
zipgrep
zipinfo
zipnote
zipsplit
```

`grep` 有几个实用的选项：`-i` 导致 `grep` 在执行搜索时忽略大小写（通常搜索是区分大小写的），以及 `-v`，它告诉 `grep` 只打印不匹配模式的行。

# head/tail—打印文件的开头/末尾部分

有时你不需要命令的所有输出。你可能只需要前几行或最后几行。`head` 命令打印文件的前 10 行，而 `tail` 命令打印最后 10 行。默认情况下，两个命令都打印 10 行文本，但可以使用 `-n` 选项进行调整：

```
@melinux~$ head -n 5 ls-output.txt
total 343496
-rwxr-xr-x 1 root 31316 2011-12-05 08:58 [
-rwxr-xr-x 1 root root 8240 2011-11-26 13:39 a11toppm
-rwxr-xr-x 1 root root 111276 2011-11-26 14:27 a2
-rwxr-xr-x 1 root root 25368 2010-10-06 20:16 a52dec
```

```
me[linuxbox ~]$ tail -n 5 ls-output.txt
-rwxr-xr-x 1 root root 5234 2011-06-27 10:56 znew
-rwxr-xr-x 1 root root 691 2009-09-10 04:21 zonetab2pot.py
-rw--r---- 1 root root 930 2011-01-11 12:23 zonetab2pot.py
-rw--r---- 1 root root 930 2011-01-11 12:23 zonetab2pot.py
-lrwxr-xr-x 1 root root 6 2012-01-31 05:22 z
```

这些命令也可以用于管道：

```
me[linuxbox ~]$ ls /usr/bin | tail -n 5
```

`tail` 有一个 `-f` 选项，允许你实时查看文件。这对于观察日志文件写入写入进度非常有用。在下面的示例中，我们查看 `/var/log/messages` 文件。在某些 Linux 发行版中执行此操作需要超级用户权限，因为 `/var/log/messages` 文件可能包含安全信息。

```
me[linuxbox ~]$ tail -f /var/log/messages
Feb 08 13:40:05 DHCPACK from 192.168.1.1 -- renewal in 1771 seconds.
Feb 08 13:40:05 DHCPACK bound to 192.168.1.4 -- renewal in 1652 seconds.
Feb 08 15:53:32 mount[dev/sda], SMART Prefetch Attribute 8: Seek Time changed from 237 to 236
Feb 08 14:10:37 mount[/var/nFS4/] exported to both 192.168.1.0 and 192.168.1.24
Feb 08 14:25:07 session(pam_unix): session opened for user (uid=0)
Feb 08 14:25:36 su(pam_unix): session opened for root by (uid=0)
```

使用 `-f` 选项会继续监控文件，当追加新行时，它们会立即显示在屏幕上。一直持续直到你输入 `CTRL-C`。

# Tee—从标准输入读取并输出到标准输出和文件

延续管道类比，Linux 提供了一个名为 `tee` 的命令，它创建一个“T”型结构。`tee` 程序读取标准输入并将其复制到标准输出（允许数据继续向下传递）以及一个或多个文件。这在处理中间阶段捕捉内容非常有用。我们重复之前的期的示例，这次通过 `tee` 将整个目录列表输出到文件，然后进行 `grep` 过滤：

```
[me@linuxbox]$ ls /usr/bin | tee ls.txt | grep zip
bunzip2
bzip2
gunzip
gzip
unzip
zip
zipcloak
zipgrep
zipinfo
zipnote
zsplit
```

# 注意

一如既往，请查看本章涵盖的每个命令的文档。我们只看到了它们最基本的用法，它们都有许多有趣的选项。

# Linux 关于想象力

当我被解释 Windows 和 Linux 的区别时，我经常使用玩具做类比。Windows 就像 Game Boy。你去商店买了一个全新的。你把它带回家，打开，开始玩。精美的画面，好听的声音。过了一段时间，你厌倦了随附的游戏，于是你又去商店买了另一个。最后，你想要一个实现某种功能的游戏！却被告诉没有这样的游戏，因为没有“市场需求”。这时你说：“但我只想修改这个东西！”柜台的人说你不能修改。所有的游戏都密封在卡带里。你发现你的玩具受限于别人认为你需要的游戏，仅此而已。

相反，Linux 就像是世界上最大的积木套装。你打开它，里面有一大堆零件——大量的钢架、螺丝、螺母、齿轮、滑轮和电机，以及关于如何构建的一些建议。你开始玩它。你发现自己对制作什么自己的主想法。你永远不需要回到商店，因为你已经拥有了的一切。积木套装呈现出你想象力的形状。它随你所愿。

你对玩具的选择是个人的事情，所以哪种玩具会让你感到更有满足？

# 第 6 章

## 7 从 Shell 的视角观察世界

在本章中，我们将观察在按下 ENTER 键时在命令行中发生的一些“魔法”。虽然我们将检查 shell 的一些有趣且复杂的特性，但我们只需要通过一个新命令来实现：

- `echo`—显示一行文本。

## 扩展 (Expansion)
