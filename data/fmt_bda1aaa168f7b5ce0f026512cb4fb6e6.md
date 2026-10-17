
```bash
$ ls
memo
$mv memo memo.0130
$ls
memo.0130
```

图 3-3 中的命令行将文件名 `memo` 更改为 `memo.0130`。初始 `ls` 命令显示 `memo` 是目录中的唯一文件。执行 `mv` 命令后，`memo.0130` 是目录中的唯一文件。将此结果与之前的 `cp` 示例比较。

`mv` 工具更多用于更改文件名。请参阅第 90 页的“mv, cp: 移动或复制文件”。

## 注意：`mv` 可能会破坏文件

正如 `cp` 可以破坏文件一样，某些 `mv` 操作也会。同样像 `cp`，`mv` 有一个 `-i`（交互式）选项。参见第 46 页标记为“cp 可以破坏文件”的警告框。

## `lpr`：打印文件

`lpr`（行打印机）将一个或多个文件放入打印队列中。Linux 提供了队列，一次只有一个作业在打印机上打印。队列允许几个人或多个作业同时向单个打印机发送输出，并获得预期的结果。在可以访问多个打印机的机器上，你可以使用 `-P` 选项指示 `lpr` 将文件放入特定打印机的队列中，包括连接到网络上另一台机器的打印机。以下命令打印名为 `report` 文件：

```bash
$lpr report
```

此命令没有指定打印机，输出将发送默认打印机，即当你只有一个打印机时使用的打印机。

下一条命令行在名为 `playroom` 的打印机上打印同一个文件：

```bash
$lpr -P mailroom report
```

你可以使用 `lpq` 工具查看打印队列中有哪些作业。

```bash
$lpq
lp is ready and printing
Rank Owner Job Files Total Size
active alex 86 (standard input) 954061 bytes
```

在例中，Alex 有一个正在打印的作业；队列中没有其他作业。你可以使用 `lpmrm` 工具配合作业号（在此例中为 86）从打印队列中删除该作业并停止打印：

```bash
$lpmrm 86
```

你可以用一个命令向打印机发送多个文件。以下命令行在名为 `laser1` 的打印机上打印文件：

```bash
$lpr -Plaser1 05.txt 108.txt 12.txt
```

## `grep`：查找字符串

`grep`（全局正则表达式打印 [1]）工具搜索一个或多个文件，以检查其中是否包含指定的字符字符串。它不会更改所搜索的文件，只是显示包含该字符串的每一行。

> [1] 该工具的名称最初是对 `ed`（一种 Linux 上可用的 UNIX 编辑器）命令 `grep/p` 的双关游戏。在这条命令中，`g` 代表全局（global），`re` 是被斜杠删除的正则表达式，`p` 代表打印（print）。

图 3-4 中的 `grep` 在文件 `memo` 中搜索包含 `credit` 字符串的行，并显示符合此标准的行。如果 `memo` 包含 `discredit`、`creditor` 或 `accreditation` 等单词，`grep` 将显示这些行，因为它们包含了正在搜索的字符串。`-w` 选项使 `grep` 只匹配单词。你不需要将搜索的字符串包含在单引号中，但这样做允许你在搜索字符串中放入空格和特殊字符。

`grep` 工具可以在单个文件中对简单字符串进行更多搜索。更多关于 `grep` 的信息请参阅第 683 页。

## 图 3-4. `grep` 搜索字符串

```bash
$cat memo
Helen:
In our meeting on June 6 we discussed the issue of credit.
Have you had any further thoughts about it?
Alex
```

```bash
$grep 'credit' memo
discussed the issue of credit.
```

## `head`：显示文件开头

默认情况下，`head` 工具显示文件的前十行。你可以使用 `head` 来帮助记忆文件内容。例如，如果你有一个列出 12 个月的 `months` 文件，`head` 显示月份（图 3-5）。该工具可以显示任意行数，要指定 `head` 显示的行数，请包含连字符和数字。

```bash
$head -n 5 months
```

`head` 工具显示文件的开头。你可以使用它查看文件的开头。更多信息请参阅第 684 页。

## `tail`：显示文件结尾

`tail` 工具与 `head` 类似，但显示文件的最后部分。默认情况下显示文件的最后十行。你可以使用 `tail` 查看大文件的结尾。

```bash
$tail -n 5 months
```

可以使用 `-f`（跟踪）选项使用 `tail` 监控文件的增长。更多关于 `tail` 的信息请参阅第 685 页。

## `diff`：比较两个文件

`diff`（差异）工具比较两个文件并显示它们之间的差异。该工具不会更改任何文件，因此当你想要比较程序版本时非常有用。

带有 `-u`（统一输出）选项的 `diff` 工具首先会指示正在比较的两个文件。

## `sort`：排序

`sort` 工具对文本文件进行排序。默认情况下，它按升序对排序。

```bash
$sort months
```

`sort` 工具还可以使用 `-k` 选项按特定列排序。更多关于 `sort` 的信息请参阅第 686 页。

## `uniq`：删除重复行

`uniq` 工具识别文件中重复的。为了使其工作，必须先进行排序。

```bash
$sort months | uniq
```

## `file`：测试文件内容

你可以使用 `file` 工具了解 Linux 系统上任何文件的内容，而无需亲自打开并检查文件。在此例中，`file` 报告 `letter_e.bz2` 包含由 `bzip2` 工具压缩的数据（第 56 页）：

```bash
$file letter_e.bz2
letter_e.bz2: bzip2 compressed data, block size = 900k
```

Nextfile 报告了另外两个文件：

```
$file memo zach.jpg
nmemo:    ASCII text
zach.jpg: JPEG image data, ... resolution (DPI), 72 x 72
```

关于文件的更多信息请参考第 653 页。

![](img/bf98da8888128a6a4235ca4c80ee1f24_83_0.png)

# |（管道）：进程间的通信

管道是 Linux 系统运行不可或缺的一部分，在这里引入它们是为了用于示例。管道在第 122 页有详细介绍。

进程是 Linux 对命令的执行。进程间的通信是 UNIX/Linux 的标志之一。管道（在命令行中写为竖线 `|`，在键盘上显示为实线或虚线垂直线）提供了这种通信的最简单形式。使用管道，管道可以获取一个进程的标准输出并将其重定向为另一个进程的标准输入。使用 UNIX/Linux 术语，管道获取一个进程的标准输出并将其重定向为另一个进程的标准输入。进程在屏幕上显示的大部分内容都发送到标准输出。（有关标准输入和输出的更多信息请参见第 113 页）。如果你不重定向，这些输出就会显示在屏幕上。使用管道，你可以重定向输出使其成为另一个进程的标准输入。像 `head` 这样的工具可以从你在命令行中跟在单词 `head` 之后指定的文件中获取输入，或者如第 49 页所示，从标准输入获取输入。例如，你可以如下所示执行该页图 3-5 所示的命令：

```
$cat months | head
Jan
Feb
Mar
Apr
May
Jun
Jul
Aug
Sep
Oct
```

下一个命令显示 `months` 文件的第一行：

```
$cat months | head -1
Jan
```

你可以使用管道将程序的输出发送到打印机：

```
$tail months | lpr
```

# 另外四个实用工具

`echo` 和 `date` 工具是 Linux 庞大工具集中最常用的两个。`script` 工具有助于将会话的部分内容记录到文件中，而 `unix2dos` 则为文本文件创建一个副本，使其可以在 Windows 机器上读取。

# `echo`：显示文本

`echo` 将你放在 `echo` 之后命令行上的任何内容复制到屏幕上。图 3-9 显示了一些示例。最后一个示例显示了 shell 对命令行上未加引号的星号（`*`）的操作：它将星号扩展为目录中的文件名列表。

图 3-9. `echo` 将命令行（但不包括 `echo` 单词）复制到屏幕上

```
$ls
memo memo.0714 practice
$echo Hi
Hi
$echo This is a sentence.
This is a sentence.
$echo star: *
star: memo memo.0714 practice
$
```

`echo` 工具是学习 shell 和其他 Linux 程序的良好工具。第 129 页的某些示例使用 `echo` 来阐明特殊字符（如星号）是如何工作的。在解释 shell 的整个章节中，`echo` 解释了 shell 变量如何工作，以及你如何从脚本向 shell 发送消息。有关 `echo` 的更多信息请参考第 647 页。

# `date`：显示时间和日期

`date` 工具显示当前的日期和时间：

```
$date
```

Thu Jan 20 10:24:00 PST 2005

下面的示例显示了你如何选择格式并选择 `date` 输出的内容。有关 `date` 的更多信息请参考第 630 页。

```
$date +"A %B d"
```

Thursday January 20

# `script`：记录 Linux 会话

`script` 工具记录登录会话的所有部分，包括你的输入和系统的响应。`script` 仅在字符设备（如终端或终端模拟器）上有用。使用 `vim` 会话时，由于 `vim` 控制光标位置并显示不同的字体，输出将难以阅读。当你使用 `cat` 打开文件时，会话会快速通过你的眼睛。默认情况下，`script` 记录在一个名为 `typescript` 的文件中。要使用不同的文件名，请在 `script` 命令后加上文件名。要追加到文件，请在文件名后使用 `-a` 选项；否则，它将覆盖现有文件。以下是 `script` 记录的会话：

```
$script
Script started, file is typescript
$date
Thu Jan 20 10:28:56 PST 2005
$who i
alex pts/4 8:15
$exit
```

使用 `exit` 命令终止 `script` 会话。你可以使用 `cat`、`more` 或编辑器查看你创建的文件。以下是由上一个 `script` 命令创建的文件：

```
$cat
Script started, file is typescript
$date
Thu Jan 20 10:28:56 PST 2005
$who i
alex pts/4 8:15
$exit
```

# `unix2dos`：将 Linux 文件转换为 Windows 格式

如果你想将 Linux 系统上创建的文本文件分享给 Windows 系统上的某人，你需要转换文件以便 Windows 系统上的用户轻松读取。`unix2dos` 工具转换 Linux 文本文件使其可以在 Windows 系统上读取。使用以下命令将名为 `memo.txt`（用文本编辑器创建）的文件转换为 DOS：

```
$unix2dos memo.txt
```

现在文件只有 50 字节长。`bzip2` 工具也重命名了文件，在文件名末尾添加了 `.bz`。这种命名约定提醒你该文件是经过压缩的；例如，你可能不想在不解压的情况下显示或打印它。`bzip2` 工具没有更改与文件关联的修改日期，尽管它完全改变了文件的内容。

在下面这个更真实的示例中，文件 `zach.jpg` 包含一张计算机图形图像：

```
$ls -l
-rw-r--r-- 1 sam sam 33287 Mar 1 22:40 zach.jpg
```

`gzip` 工具只能减少 28% 的文件大小，因为该图像已经是压缩格式了：

```
$bzip2 -v zach.jpg
zach.jpg: 1.391:1, 5.749 bits/byte, 28.13% saved, 33287 in, 23922 out.
```

```
$ls -l
-rw-r--r-- 1 sam sam 23922 Mar 1 22:40 zach.jpg.bz
```

请参阅第 596 页和 Bzip2 mini-HOWTO（查找方法请参阅第 34 页）获取更多信息。

# `bunzip2` 和 `bzcat`: 解压文件

你可以使用 `bunzip2` 工具恢复用 `bzip2` 压缩的文件：

```
$bunzip2 letter_e.bz2
$ ls -l
-rw-rw-r-- 1 sam sam 584000 Mar 1 22:31 letter_e
$bunzip2 zach.jpg.bz2
$ ls -l
-rw-r--r-- 1 sam sam 33287 Mar 1 22:40 zach.jpg
```

`bzcat` 工具显示用 `bzip2` 压缩的文件。`bzcat` 相当于于对 `.bz2` 文件使用 `cat`，它会解压缩压缩数据并显示解压后的文件内容。像 `cat` 一样，`bzcat` 不更改源文件。以下示例中的管道符 `|` 重定向了 `zcat` 的输出，使其不再显示在屏幕上，而是成为 `head` 的输入，而 `head` 会显示前两行：

```
$bzcat letter_e.bz2 | head -2
eeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee
```

运行 `bzcat` 后，`letter_e.bz` 的内容保持不变；该文件仍然以压缩形式存储在磁盘上。

### `bzip2recover`

`bzip2recover` 工具支持从媒体错误中进行有限的数据恢复。输入 `bzip2recover` 命令，后跟你想要尝试恢复数据的文件名。

# `gzip`: 压缩文件

### `gunzip` 和 `zcat`

`gzip` (GNU zip) 工具比 `bzip2` 更旧且效率更低。它的标志和操作与 `bzip2` 非常相似。由 `gzip` 压缩的文件以 `.gz` 文件名扩展名标记。Linux 以 `gzip` 格式存储帮助页以节省磁盘空间；同样，从互联网下载的文件也频繁采用 `gzip` 格式。像你使用 `bzip2`、`bunzip` 和 `bcat` 那样使用 `gzip`、`gunzip` 和 `zcat` 即可关于 `gzip` 的更多信息，请参阅第 688 页。

### `compress`

`compress` 工具也可以压缩文件，尽管效果没有 `gzip` 好。该工具通过在文件名后添加 `.Z` 来标记它已压缩的文件。

#### 提示：`gzip` 对比 `zip`

不要将 `gzip` 和 `gunzip` 与 `zip` 和 `unzip` 工具混淆。后两个用于将包含密封文件的归档打包并解包成单个文件，该文件可以导入或导出到 Windows。`zip` 工具构建 `zip` 归档，而 `unzip` 则解包归档。`zip` 和 `unzip` 工具与 PKZIP（一个 Windows 压缩和存档程序）兼容。

# `tar`: 打包和解包文件

`tar` 工具执行许多功能。它的名字是 tape archive（磁带存档）的缩写，因为它最初的功能是创建和存档备份带。今天，它被用于从多个文件或目录层次结构创建一个单个文件（称为 `tar` 文件），并从 `tar` 文件中提取文件。

在下面的示例中，`ls` 显示了文件 `g`、`b` 和 `d` 的存在及其大小。接下来 `tar` 使用 `--c`（创建）、`-v`（详细）和 `-f`（写入文件或从文件读取）选项[2] 从这些文件创建一个名为 `all.tar` 的归档。`tar` 输出的每行都以字母 `a` 开头，表示它正在附加归档。随后是 `tar` 正在追加的文件名。

- [2] 虽然原始的 UNIX `tar` 不在命令行中使用前导连字符来指示，但它现在接受连字符。这里描述的 GNU `tar` 接受带或不带前导连字符的命令。为了与其他方法保持一致，本书使用了连字符。

`tar` 工具在创建归档时会增加开销。接的命令显示归档 `all.tar` 约为 9,700 字节，而三个文件的大小之和约为 6,000 字节。对于较小的文件（例如示例中的文件），开销更为明显。

```
$ls -l g b d
--rw-r--r-- 1 jenny 1302 Aug 20 14:16 g
--rw-r--r-- 1 jenny other 1178 Aug 20 14:16 b
--rw-r--r-- 1 jenny 3783 Aug 20 14:16 d

$tar -cvf all.tar g b d
g
b
d
$ls -l all.tar
-rw-r--r-- 1 jenny 9700 Aug 20 14:16 all.tar
```

# 可选项

你可以通过管道 (`|`) 在一条命令行中将 `gzip` 和 `tar` 命令结合起来，这会重定向 `gzip` 的输出使其成为 `tar` 的输入：

```
$gzip -c make-3.80.tar.gz | tar -xvf -
```

`-c` 选项导致 `gzip` 将输出通过管道发送，而不是创建一个文件。有关此命令行如何工作的更多信息，请参阅“管道”（第 122 页）、`gzip`（第 688 页）和 `tar`（第 786 页）。

更简单的解决方案是使用 `tar` 的 `-z` 选项。此选项导致 `tar` 直接调用 `gzip`（或者在你创建归压缩包时调用 `gzip`），并将前面的命令行简化为：
