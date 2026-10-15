
并用减号（`-`）标记。在图 5-8 中，减号表示颜色文件；加号表示颜色。

```
--- colors
+++ colors
@@ -1,6 +1,5 @@
-red
+blue
green
+yellow
orange
```

**图 5-8** `diff` 显示统一输出格式

## 识别文件内容

你可以使用 `file` 工具在无需打开和检查文件的情况下了解任何文件的内容。在下面的示例中，`file` 报告 `letter_e.bz2` 被 `bzip2` 压缩了：

```
$ letter_e.bz2
letter_e.bz2: bzip2 compressed data, block size = 900k
```

接下来 `file` 报告两个文件：

```
$ memo zach.jpg
memo: ASCII text
zach.jpg: JPEG image data, resolution: 72 x 72
```

更多信息请参阅 `file` 页面。

## (管道)：进程间的通信

由于管道是 `Linux` 系统运行不可不可或的一部分，本章将在示例中介绍它们。管道从第 237 页开始详细介绍。

进程是 `Linux` 执行命令的过程（第 312 页）。进程之间的通信是 `UNIX` 和 `Linux` 的特征之一。管道（在命令行中写为垂直线 `|`，在键盘上显示为实线或断开的垂直线）提供了这种通信最简单的形式。简单来说，管道接收一个工具的输出并将其作为输出发送给另一个工具。使用 `UNIX/Linux` 术语，管道接收一个进程的标准输出并将其重定向为另一个进程的标准输入。（更多信息请参阅第 229 页的“标准输入和输出”）。进程显示在屏幕上的大部分内容发送到标准输出。如果你不重定向它，此输出将显示在屏幕上。通过管道，你可以重定向输出使其成为另一个工具的标准输入。例如，像 `head` 这样的工具可以从命令行跟随 `head` 指定的文件获取输入，也可以从标准输入获取输入。以下命令对 `months` 文件（图 5-5，第 153 页）的行进行排序，并使用 `head` 显示排序列表的前四个月份：

```
$ sort months | head -4
Apr
Aug
Dec
Feb
```

下一条命令行显示目录中的文件数量。`wc`（单词计数）工具配合 `-w`（words）选项显示其标准输入或你在命令行指定的文件的字数：

```
$ ls | wc -w
14
```

## 其他四个实用工具

你可以使用管道（`pipe`）将程序的输出发送到打印机：

```
$ tail months | lpr
```

`echo` 和 `date` 工具是 `Linux` 大量实用工具集中常用的两个成员。`script` 工具可以记录文件的部分内容，而 `todos` 则可以创建一个可以在 `Windows` 或 `Macintosh` 系统上读取的文本文件副本。

### `echo`：显示文本

`echo` 工具将你在命令行中 `echo` 之后输入的字符复制到屏幕。图 5-9 显示了一些示例。最后一个示例显示了 `shell` 如何处理命令行上未加引号的星号（`*`）：它会将星号展开为该目录下的文件名列表。

`echo` 工具是学习 `shell` 和其他 `Linux` 实用工具的好工具。第 243 页的一些示例使用 `echo` 来阐明特殊字符（如星号）是如何工作的。在整个第 7、9 和第 27 章中，`echo` 解释了 `shell` 变量的工作原理，以及你如何从 `shell` 脚本发送消息到屏幕。更多信息请参阅 `echo` `info` 页面。

可选：你可以通过将输出重定向到文件来使用 `echo` 创建一个简单的文件：

```
$ echo 'My new file.' > myfile
$ cat myfile
```

大于号（`>`）符号告诉 `shell` 将 `echo` 的输出发送到文件 `myfile` 而不是屏幕。更多信息请参阅第 232 页的“重定向标准输出”。

```
$ ls
memo.0714 practice
$ echo Hi
Hi
$ echo This is a sentence.
This is a sentence.
$ echo star: *
star: memo.0714 practice
$
```

图 5-9 `echo` 将命令行（但不包含 `echo` 单词本身）复制到屏幕

### `date`：显示日期和日期

该工具显示当前的日期和时间：

```
$ date
Thu Jan 24 10:24:00 PST 2008
```

接下来的示例显示了你如何选择格式并选择 `date` 输出的内容：

```
$ date +"%A %B %d"
Thursday January 24
```

更多信息请参阅 `date` `info` 页面。

### `script`：记录 `shell` 会话

`script` 工具记录登录会话全部或部分，包括你的输入和系统的响应。该工具仅从基于字符的设备（如终端或终端模拟器）有效。它确实可以捕获 `vim` 会话；但由于 `vim` 使用控制字符来定位光标并显示不同的字体（如加粗），输出将难以阅读且可能没有用。当你剪切捕获了 `vim` 会话的文件时，会话会迅速掠过屏幕。

默认情况下，`script` 将会话记录在名为 `typescript` 的文件中。要指定文件名，请使用 `script` 命令并加上空格和文件名。要追加到文件，请在 `script` 之后文件名之前使用 `-a` 选项；否则 `script` 将覆盖现有文件。以下是 `script` 记录的会话：

```
$ script
Script started, file is typescript
$ whoami
sam ls -1 /bin | head -5
total 5024
-rw-r-xr-x 1 root root 2928 Sep 21 21:42 archdetect
-rw-r-xr-x 1 root root 1054 Apr 26 15:37 autopartition
-rw-r-xr-x 1 root root 7168 Sep 21 19:18 autopartition-loop
-rw-r-xr-x 1 root root 701008 Aug 27 02:41 bash
$ exit
exit
Script done, file is typescript
```

使用 `exit` 命令终止脚本会话。你可以使用 `cat`、`less`、`more` 或编辑器查看你创建的文件。以下是由之前的 `script` 命令创建的文件：

```
$ cat typescript
Script started on Mon Sep 24 20:54:59 2007
$ whoami
sam
```

```
$ ls -l /bin | head -5
total 5024
-rwxr-xr-x 1 root root     2928 Sep 21 21:42 archdetect
-rwxr-xr-x 1 root root     1054 Apr 26 16:53 autopartition
-rwxr-xr-x 1 root root     7168 Sep 21 19:18 autopartition-loop
$ exit
exit
```

Script done on Mon Sep 24 20:55:29 2007

如果你正在用 `vim`、`emacs` 或编辑器编辑该文件，可以使用 `fromdos`（下文）消除 `typescript` 文件行尾出现的 `^M` 字符。更多信息请参阅 `script` `man` 页面。

### `todos`：将 `Linux` 和 `Macintosh` 文件转换为 `Windows` 格式

如果你想将 `Linux` 系统上创建的文本文件分享给 `Windows` 或 `Macintosh` 系统上的人，你需要在对方系统的人轻松读取它之前对该文件进行转换。`todos` (to DOS) 工具可以转换 `Linux` 文本文件，使其可以在 `Windows` 或 `Macintosh` 系统上读取。该工具是 `tofords` 软件包的一部分；执行命令 `sudo aptitude install todos` 来安装此包。执行以下命令：

```
$ todos
```

压缩和归档文件

## `bunzip2` 和 `zcat`：解压文件
