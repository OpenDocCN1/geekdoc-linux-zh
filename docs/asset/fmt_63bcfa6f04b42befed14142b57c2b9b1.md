
# Linux 命令参考

## 文件管理

### `mv`：移动或重命名文件

`mv existing-filename new-filename`

图 5–3 中的命令行将文件 `memo` 的名称更改为 `memo.0130`。初始的 `ls` 命令显示目录中只有一个文件 `memo`。在执行 `mv` 命令后，目录中唯一的文件是 `memo.0130`。将此结果与图 5–2 中 `cp` 示例的结果进行比较。

`mv` 工具不仅可用于更改文件名。请参阅第 212 页的“mv, cp：移动或复制文件”。更多信息请参阅 `mv` 的 info 页面。

#### `mv` 可能破坏文件

就像 `cp` 可能会破坏文件一样，`mv` 也可能如此。与 `cp` 类似，`mv` 也有一个 `-i`（交互）选项。请参阅标有“cp 可能破坏文件”的警告框。

```bash
$ ls
memo
$ mv memo memo.0130
$ ls
memo.0130
```

**图 5-3** `mv` 重命名文件

### `lpr`：打印文件

`lpr`（line printer，行式打印机）工具将一个或多个文件放入打印队列中以便打印。Linux 提供打印队列，以确保在给定打印机上每次只打印一个任务。队列允许多个用户或任务同时向单个打印机发送输出，并预期能获得正确的结果。在可以访问多台打印机的系统上，你可以使用 `lpstat -p` 来显示可用打印机的列表。使用 `-P` 选项指示 `lpr` 将文件放入特定打印机的队列中——甚至是连接到网络上另一台系统的打印机。以下命令打印名为 `report` 的文件：

```bash
$ lpr report
```

由于此命令未指定打印机，输出将发送到默认打印机，当你只有一台打印机时，它就是唯一的打印机。

下一条命令行在名为 `mailroom` 的打印机上打印同一文件：

```bash
$ lpr -P mailroom report
```

你可以通过执行 `lpstat -o` 命令或使用 `lpq` 工具来查看打印队列中的任务：

```bash
$ lpq
lp is ready and printing
Rank Owner Job Files Total Size
active max 86 (standard input) 954061 bytes
```

在此示例中，Max 有一个正在打印的任务；队列中没有其他任务。你可以使用任务编号（在此例中为 86）配合 `lprm` 工具，将任务从打印队列中移除并停止其打印：

```bash
$ lprm 86
```

你可以用一条命令向打印机发送多个文件。以下命令行在名为 `laser1` 的打印机上打印三个文件：

```bash
$ lpr -P laser1 05.txt 108.txt 12.txt
```

有关设置打印机和定义默认打印机的信息，请参阅第 14 章。

![图 5-4 grep 搜索字符串](img/2344fc4a798f29dca9e8b5ed7288171a_216_0.png)

### `grep`：搜索字符串

`grep` 实用程序会在一个或多个文件中搜索是否包含指定的字符序列。该实用程序不会修改被搜索的文件，而是简单地显示包含该字符串的每一行。

图 5-4 中的 `grep` 命令在文件 `memo` 中搜索包含字符串 `credit` 的行，并显示符合此条件的唯一一行。如果 `memo` 中包含诸如 `discredit`、`creditor` 或 `accreditation` 等单词，`grep` 也会显示这些行，因为它们包含正在搜索的字符串。`-w`（words，单词）选项使 `grep` 仅匹配完整的单词。虽然您不必用单引号括起要搜索的字符串，但这样做允许您在搜索字符串中加入空格（SPACES）和特殊字符。

`grep` 实用程序能做的远不止在单个文件中搜索简单字符串。有关更多信息，请参阅 `grep` 的信息页和附录 A“正则表达式”。

> 最初，grep 这个名字是对 `ed`——一个原始 UNIX 编辑器，在 Ubuntu Linux 上可用——的一个命令 `g/re/p` 的双关。在这个命令中，`g` 代表 global（全局），`re` 是由斜杠分隔的正则表达式，`p` 代表 print（打印）。

### `head`：显示文件开头

默认情况下，`head` 实用程序显示文件的前十行。您可以使用 `head` 来帮助您记住特定文件的内容。例如，如果您有一个名为 `months` 的文件，其中按日历顺序列出了一年中的 12 个月，每月占一行，那么 `head` 将显示从 `Jan` 到 `Oct` 的内容（图 5-5）。

此实用程序可以显示任意数量的行，因此您可以使用它来仅查看文件的第一行、一整个屏幕，甚至更多内容。要指定要显示的行数，请输入连字符后跟您希望 `head` 显示的行数。例如，以下命令仅显示 `months` 文件的第一行：

```bash
$ head months
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

$ tail -5 months
Aug
Sep
Oct
Nov
Dec
```

![图 5-5 head 和 tail 示例](img/2344fc4a798f29dca9e8b5ed7288171a_217_0.png)

```bash
$ head -1 months
Jan
```

`head` 实用程序还可以根据块或字符计数（而非行数）来显示文件的部分内容。有关更多信息，请参阅 `head` 的信息页。

### `tail`：显示文件末尾

`tail` 实用程序与 `head` 类似，但默认显示文件的最后十行。根据调用方式的不同，此实用程序可以显示少于或多于十行，使用块或字符计数而非行数来显示文件的部分内容，并显示正在添加到正在更改的文件中的行。图 5-5 中的 `tail` 命令显示了 `months` 文件的最后五行（从 `Aug` 到 `Dec`）。您可以使用以下命令监控随着文件增长而添加到名为 `logfile` 的文件末尾的行：

```bash
$ tail -f logfile
```

按中断键（通常是 `CONTROL-C`）以停止 `tail` 并显示 shell 提示符。有关更多信息，请参阅 `tail` 的信息页。

![图 5-6 sort 按顺序显示文件的行](img/2344fc4a798f29dca9e8b5ed7288171a_218_0.png)

### `sort`：按顺序显示文件

`sort` 实用程序按行顺序显示文件内容，但不更改原始文件。

图 5-6 显示 `cat` 正在显示名为 `days` 的文件，该文件按日历顺序将每周每一天的名称单独放在一行上。然后，`sort` 实用程序按字母顺序显示该文件。

`sort` 实用程序对于将列表排序很有用。`-u` 选项生成一个排序后的列表，其中每行都是唯一的（无重复项）。`-n` 选项将数字列表按数值顺序排列。有关更多信息，请参阅 `sort` 的信息页。

### `uniq`：从文件中删除重复行

`uniq`（unique，唯一）实用程序显示文件，跳过相邻的重复行，但不更改原始文件。如果文件包含一个名称列表，并且有同一人的两个连续条目，`uniq` 会跳过多余的那一行（图 5-7）。

如果在由 `uniq` 处理之前对文件进行排序，此实用程序可以确保文件中没有两行是相同的。（当然，`sort` 使用 `-u` 选项本身就可以做到这一点。）有关更多信息，请参阅 `uniq` 的信息页。

```bash
$ cat dups
Cathy
Fred
Joe
John
Mary
Mary
Paula
$ uniq dups
Cathy
Fred
Joe
John
Mary
Paula
```

![图 5-7 uniq 显示没有重复行的文件](img/2344fc4a798f29dca9e8b5ed7288171a_219_0.png)

### `diff`：比较两个文件

`diff`（difference，差异）实用程序比较两个文件并显示它们之间差异的列表。此实用程序不修改任何文件；当您想要比较信件或报告的两个版本，或程序源代码的两个版本时，它非常有用。

带有 `-u`（unified output format，统一输出格式）选项的 `diff` 实用程序首先显示两行，指示您要比较的文件中哪个将由加号（`+`）表示，哪个将由减号（`-`）表示。在图 5-8 中，减号表示 `colors.1` 文件；加号表示 `colors.2` 文件。

`diff -u` 命令将长的多行文本拆分为块（hunks）。每个块前面都有一行以两个 at 符号（`@@`）开始和结束。这个块标识符指示每个文件在此块中的起始行号和行数。在图 5-8 中，该块覆盖了 `colors.1` 文件（由减号指示）从第一行到第六行的部分。然后 `+1,5` 指示该块覆盖了 `colors.2` 从第一行到第五行的部分。

在这些标题行之后，`diff -u` 显示每行文本，前面带有减号、加号或空格。前面的减号表示该行仅出现在由减号表示的文件中。前面的加号表示该行仅出现在由加号表示的文件中。以空格开头（既不是加号也不是减号）的行在两个文件中的同一位置出现。有关更多信息，请参阅 `diff` 的信息页。

```bash
$ diff -u colors.1 colors.2
--- colors.1 2010-07-29 16:41:11.000000000 -0700
+++ colors.2 2010-07-29 16:41:17.000000000 -0700
@@ -1,6 +1,5 @@
red
+blue
green
yellow
-pink
-purple
orange
```

![图 5-8 diff 显示两个文件之间的差异](img/2344fc4a798f29dca9e8b5ed7288171a_219_1.png)

### `file`：识别文件内容

您可以使用 `file` 实用程序来了解 Linux 系统上任何文件的内容，而无需自己打开并检查该文件。在以下示例中，`file` 报告 `letter_e.bz2` 包含由 `bzip2` 实用程序（第 174 页）压缩的数据：

```bash
$ file letter_e.bz2
letter_e.bz2: bzip2 compressed data, block size = 900k
```

接下来 `file` 报告另外两个文件：

```bash
$ file memo zach.jpg
memo: ASCII text
zach.jpg: JPEG image data, ... resolution (DPI), 72 x 72
```

有关更多信息，请参阅 `file` 的手册页。

## 管道与进程

### `(PIPE)`：进程间通信

由于管道是 Linux 系统功能的核心部分，本章将其引入示例中使用。从第 251 页开始将详细介绍管道。

进程是 Linux 执行命令的过程（第 328 页）。进程之间的通信是 UNIX 和 Linux 的显著特征之一。**管道**（在命令行上写作垂直线 `|`，在键盘上表现为实心或虚线垂直线）提供了这种通信的最简单形式。简而言之，管道获取一个实用程序的输出，并将该输出作为输入发送到另一个实用程序。使用 UNIX/Linux 术语，管道获取一个进程的标准输出并将其重定向为另一个进程的标准输入。（有关更多信息，请参阅第 243 页的“标准输入和标准输出”。）进程在屏幕上显示的大部分内容都发送到标准输出。如果您不重定向它，此输出将出现在屏幕上。使用管道，您可以重定向标准输出，使其成为另一个实用程序的标准输入。例如，像 `head` 这样的实用程序可以从您在命令中 `head` 之后指定的文件名获取输入，也可以从标准输入获取输入。以下命令行对 `months` 文件的行进行排序（图 5-5，第 167 页），并使用 `head` 显示排序列表的前四行：

```bash
$ sort months | head -4
Apr
Aug
Dec
Feb
```

下一条命令行显示目录中的文件数量。带有 `-w`（words，单词）选项的 `wc`（word count，单词计数）实用程序显示其标准输入或您在命令行上指定的文件中的单词数：

```bash
$ ls | wc -w
14
```

## 其他实用工具

### 另外四个实用工具

`echo` 和 `date` 实用工具是庞大的 Linux 实用工具集合中最常用的成员之一。`script` 实用工具将会话的一部分记录到文件中，而 `todos` 则创建文本文件的副本，该副本可以在 Windows 或 Macintosh 机器上读取。

#### `echo`：显示文本

`echo` 实用工具将你在 `echo` 之后在命令行上输入的字符复制到屏幕上。图 5-9 展示了一些示例。最后一个示例展示了 shell 如何处理命令行中未加引号的星号 (`*`)：它将星号扩展为目录中的文件名列表。

`echo` 实用工具是学习 shell 和其他 Linux 实用工具的好工具。第 257 页上的一些示例使用 `echo` 来说明像星号这样的特殊字符是如何工作的。在第 7、9 和 27 章中，`echo` 有助于解释 shell 变量的工作原理以及如何将消息从 shell 脚本发送到屏幕。有关更多信息，请参考 coreutils info 页面的 `echo` 部分。

> **可选** 你可以通过将其输出重定向到文件来使用 `echo` 创建一个简单文件：
>
> ```bash
> $ echo 'My new file.' > myfile
> $ cat myfile
> My new file.
> ```
>
> 大于号 (`>`) 符号告诉 shell 将 `echo` 的输出发送到名为 `myfile` 的文件，而不是发送到屏幕。有关更多信息，请参考第 246 页的“重定向标准输出”。

```bash
$ ls
memo  memo.0714  practice
$ echo Hi
Hi
$ echo This is a sentence.
This is a sentence.
$ echo star: *
star: memo  memo.0714  practice
$
```

图 5-9：`echo` 将命令行（但不包括 `echo` 这个词本身）复制到屏幕上。

#### `date`：显示时间和日期

`date` 实用工具显示当前的日期和时间：

```bash
$ date
Thu Jan 21 10:24:00 PST 2010
```

以下示例展示了如何选择合适的格式并选择 `date` 输出的内容：

```bash
$ date "+%A %B %d"
Thursday January 21
```

有关更多信息，请参考 `date` 的 info 页面。

#### `script`：记录 shell 会话

`script` 实用工具记录登录会话的全部或部分，包括你的输入和系统的响应。此实用工具仅适用于基于字符的设备，例如终端或终端模拟器。它确实能捕获与 `vim` 的会话；然而，由于 `vim` 使用控制字符来定位光标并显示不同的字体（如粗体），因此输出将难以阅读且可能没有用处。当你 `cat` 一个捕获了 `vim` 会话的文件时，该会话会迅速从你眼前闪过。

默认情况下，`script` 将会话记录在名为 `typescript` 的文件中。若要指定不同的文件名，请在 `script` 命令后跟随一个空格和文件名。若要追加到文件，请在 `script` 之后、文件名之前使用 `-a` 选项；否则 `script` 会覆盖现有文件。以下是一个由 `script` 记录的会话：

```bash
$ script
Script started, file is typescript
$ whoami
sam
$ ls -l /bin | head -5
total 6632
-rwxr-xr-x 1 root root 818232 2010-04-10 05:10 bash
-rwxr-xr-x 1 root root 30200 2010-02-08 02:54 bunzip2
-rwxr-xr-x 1 root root 1269432 2010-01-22 08:23 busybox
-rwxr-xr-x 1 root root 30200 2010-02-08 02:54 bzcat
$ exit
exit
Script done, file is typescript
```

使用 `exit` 命令终止 `script` 会话。然后你可以使用 `cat`、`less`、`more` 或编辑器查看创建的文件。以下是由前面的 `script` 命令创建的文件：

```bash
$ cat typescript
Script started on Mon Sep 27 20:54:59 2010
$ whoami
sam
$ ls -l /bin | head -5
total 6632
-rwxr-xr-x 1 root root 818232 2010-04-10 05:10 bash
-rwxr-xr-x 1 root root 30200 2010-02-08 02:54 bunzip2
-rwxr-xr-x 1 root root 1269432 2010-01-22 08:23 busybox
-rwxr-xr-x 1 root root 30200 2010-02-08 02:54 bzcat
$ exit

Script done on Mon Sep 27 20:55:29 2010
```

如果你打算使用 `vim`、`emacs` 或其他编辑器编辑该文件，你可以使用 `fromdos`（下文提及）来消除 `typescript` 文件行末尾出现的 `^M` 字符。有关更多信息，请参考 `script man` 页面。

#### `todos`：将 Linux 和 Macintosh 文件转换为 Windows 格式
