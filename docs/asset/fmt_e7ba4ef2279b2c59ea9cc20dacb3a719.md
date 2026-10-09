
# 3-7 uniq 移除重复行

## `uniq` 从文件中移除重复行

`uniq`（unique）实用程序显示文件时会跳过相邻的重复行，但不会更改原始文件。如果文件包含姓名列表，并且同一个人有两个连续的条目，`uniq` 会跳过多余的行（图 3-7）。

如果文件在被 `uniq` 处理之前经过了排序，该实用程序可以确保文件中没有两行是完全相同的。（当然，`sort` 也可以通过 `-u` 选项本身完成这一工作）。

有关 `uniq` 的更多信息，请参阅第 812 页。

## `diff` 比较两个文件

`diff`（difference）实用程序比较两个文件并显示它们之间的差异列表。当你想要比较两个版本的信件、报告，或者程序的两个版本的源代码时，该实用程序非常有用。

带有 `-u`（统一输出格式）选项的 `diff` 实用程序会显示两行，指示你正在比较的文件哪些用加号 (`+`) 表示，哪些用减号 (`-`) 表示。在图 3-8 中，减号表示 `colors.1` 文件；加号表示 `colors.2` 文件。

`diff -u` 命令将单行或多行文本拆分为“块”（hunks）。每个块之前都有一个以两个 `@@` 开头和结尾的行。该行指示每个文件中该块的起始行号和包含的行数。在图 3-8 中，`-1,6` 表示该块涵盖了 `colors.1` 文件（由减号表示）从第一行开始并持续六行的部分（总共七行）。同样，`+1,5` 表示该块涵盖了 `colors.2` 从第一行到随后的五行。

```bash
$ diff -u colors.1 colors.2

--- colors.1  Fri Nov 25 15:45:32 2005

+++ colors.2  Fri Nov 25 15:24:46 2005

@@ -1,6 +1,5 @@

red

+blue

green

yellow

-pink

-purple

orange
```

**图 3-8** `diff` 显示统一输出格式

在这些标题行之后，`diff -u` 显示每行文本，其开头有减号、加号或什么都没有。开头的减号表示该行仅出现在由减号指示的文件中。开头的加号表示该行来自由加号指示的文件。既不加号也不以减号开头的行则出现在两个文件的相同位置。有关 `diff` 的更多信息，请参阅第 638 页。

## `file` 测试文件内容

你可以使用 `file` 来了解文件系统中任何文件的内容。以下示例展示了你如何选择格式并选择 `date` 输出的内容。有关后续示例的信息，请参阅第 650 页：

```bash
$ who am i

alex pts/4 Jan 8 22:15

$ apropos mtools

mtools (1) - utilities to access DOS disks in Unix

mtools.conf [mtools] (5) - mtools configuration files

mtools.testest (1) - tests and displays the configuration

$ exit

Script done, file is typescript

$
```

使用 `exit` 命令终止脚本会话。你可以使用 `cat`、`less`、`more` 或编辑器查看创建的文件。以下是由上一个脚本命令创建的文件：

```bash
$ cat typescript

Script started on Thu Jan 20 10:28:56 2005

$ date

Thu Jan 20 10:28:56 PST 2005

$ who am i

alex pts/4 Jan 8 22:15

$ apropos mtools

mtools (1) - utilities to access DOS disks in Unix

mtools.conf [mtools] (5) - mtools configuration files

mtools.testest (1) - tests and displays the configuration

$ exit

Script done on Thu Jan 20 10:29:58 2005
```

如果你将用 `vim`、`emacs` 或其他编辑器编辑该文件，可以使用 `dos2unix` 删除 `typescript` 文件末尾出现的 `^M` 字符。

## `unix2dos` 将 LINUX 文件转换为 WINDOWS 格式

如果你想将在 Linux 系统上创建的文本文件分享给 Windows 系统上的用户，你需要先转换该文件，Windows 系统上的用户才能轻松读取它。`unix2dos` 工具可以转换 Linux 文本文件，使其能够在 Windows 系统上读取。执行以下命令将名为 `memo.txt`（用文本编辑器创建）的文件转换为 DOS 格式文件：

```bash
$ unix2dos memo.txt
```

在不使用任何选项的情况下，`unix2dos` 会覆盖原始文件。你现在可以将该文件作为附件发送给 Windows 系统上的用户了。

`dos2unix` 你可以使用 `dos2unix` 工具转换 DOS 文件，使其能够在 Linux 系统上读取：

```bash
$ dos2unix memo.txt
```

## 第 56 页 第 3 章 命令行工具

更多信息请参阅 `unix2dos` 和 `dos2unix` 的 man 页。

你也可以使用 `tr`（第 804 页）将 DOS 文本文件转换为 Linux 文本文件。在下面的示例中，`-d` 选项会导致 `tr` 在创建文件副本时移除回车（由 `\r` 表示）：

```bash
$ cat memo | tr -d '\r' > memo.txt
```

不使用 `unix2dos` 反向转换文件并不简单。

## 压缩与归档

大文件占用大量的磁盘空间，并且从网络传输到另一个系统的时间比小文件更长。如果你不需要经常查看大文件的内容，可能希望将其保存在 CD、DVD 或其他介质上并从硬盘中删除。如果你对该文件有持续需求，从 CD 中检索副本可能会不方便。为了在不完全删除文件的情况下减少磁盘空间占用，可以在不丢失文件中包含任何信息的情况下压缩文件。你可能会经常从互联网下载压缩文件。本节使用的工具用于压缩和解压缩文件：

## `bzip2` 压缩文件

`bzip2` 工具 (`sources.redhat.com/bzip2`) 通过更高效地分析和解码来压缩文件。压缩后的新文件看起来完全不同。事实上，由于新文件包含许多非打印字符，你无法直接查看它。`bzip2` 工具处理包含大量重复信息的文件（如文本和图像数据）时效果非常好，尽管大多数图像数据已经是压缩格式。

下面的示例显示了一个无聊的文件。这个名为 `letter_e` 的文件的 8,000 行中的每一行都包含 72 个 `e` 和一个标记行末尾的换行符。该文件占据了超过 1MB 的磁盘存储。

```bash
$ ls -l
-rw-rw-- 1 sam sam 584000 Mar 1 22:31 letter_e
```

`-l`（long）选项会导致显示更多关于文件的信息。这里显示 `letter_e` 长度为 584,000 字节。`--verbose`（或 `-v`）选项会让 `bzip2` 报告它减小了多少大小。在这种情况下，它缩小了 99.99%：

```bash
$ bzip2 -v letter_e
letter_e:168:00.1:0.001 bits/byte, 99.99% saved, 584000 in, 50 out.
$ ls -l
-rw-rw-r-- 1 sam sam 50 Mar 1 22:31 letter_e
```

## `bunzip2` 解压缩文件

你可以使用 `bunzip2` 工具恢复一个被压缩的文件：

```bash
$ bunzip2 letter_e.bz
$ ls -l
-rw-rw-- 1 sam sam 584000 Mar 1 22:31 letter_e

$ bunzip2 zip.jpg.bz2
$ ls -l
-rw-rw-r-- 1 sam sam 33287 Mar 22:40 zip.jpg
```

## `gzip` 压缩文件

`gzip` (GNU zip) 工具比 `bzip2` 更旧且效率较低。它的标志和操作与 `bzip2` 非常相似。被 `gzip` 压缩的文件以 `.gz` 扩展名标记。Linux 以 gzip 格式存储手册页以节省磁盘空间；同样，从互联网下载的文件经常是 gzip 格式。

`compress` 工具也可以压缩文件，尽管不如 `gzip`。该工具通过为文件名添加 `.Z` 来标记文件。

## `gzip` 与 `zip`

不要将 `gzip`/`gunzip` 与 `zip` 和 `unzip` 工具混淆。后者用于将包含多个文件的归档打包并解包到单个文件中。`zip` 工具构建归档，而 `unzip` 则解包归档。`zip` 和 `unzip` 工具与 Windows 压缩程序 PKZIP 兼容。

## `tar` 打与解包

`tar` 工具执行许多功能。它的名字是 tape archive（磁带归档），因为它最初的功能是创建和读取磁带。现在它用于从多个文件或目录层次创建一个单个文件（称为 tar 文件），并从 tar 文件中提取文件。

在下面的示例中，第一个 `ls` 显示了文件 `g`、`b` 和 `d` 的存在和大小。接下来使用 `-c`（创建）、`-v`（详细）和 `-f`（写入或读取文件）选项从这些文件创建一个名为 `all.tar` 的归档。输出的每行都以字母 `a` 开头，表示正在追加归档。该行后面是文件名。

`tar` 工具在创建归档时产生开销。下一个命令显示归档文件 `all.tar` 大约为 9,700 字节，而三个文件的大小总和约为 6,000 字节。这种开销对于较小文件（如本示例中的文件）更为明显。

```bash
$ tar -cvf all.tar a b d
a
b d
d
$ ls -l -- all.tar
-rw-r--r-- 1 jenny 9728 Aug 20 14:17 all.tar
$ tar -tvf all.tar
-rw-r--r-- jenny/jenny 1302 2003-08-20 14:16 5
-rw-r--r-- jenny/other 1178 2003-08-20 14:16 5
-rw-r--r-- jenny/jenny 3783 2003-08-20 14:17 5
```

上一个示例中的最后一个命令使用 `-t` 来显示归档的目录内容。使用 `-x` 代替 `-t` 可以从 tar 归档中提取文件。如果你希望它静默运行，可以省略 `-v` 选项。

你可以使用 `bzip2` 或 `gzip` 来压缩 tar 文件，使其更容易存储和处理。你从互联网下载的许多文件就是这些格式之一。经过 tar 和 gzipped bzip2 处理的文件通常具有 `.tar.bz2` 扩展名。经过 tar 和 gzip 处理的文件扩展名为 `.tar.gz`，而经过 tar 和 compress 处理的文件使用 `.tar.Z` 作为扩展名。

你可以通过两个步骤解压一个压缩并经过 gzipped 处理的文件。（如果文件是由 `bzip2` 压缩的，请遵循相同的步骤，并用 `bunzip2` 代替 `gunzip`。）下一个示例显示了如何在下载 GNU make 工具（`ftp.gnu.org/pub/gnu/make/make-3.80.tar.gz`）后解包：

```bash
$ ls -1 mak*
-rw-r--r-- 1 sam 1211924 Jan 20 11:49 make-3.80.tar.gz
```

```bash
$ gunzip mak*
$ ls -1 mak*
-rw-r--r-- 1 sam 4823040 Jan 20 11:49 make-3.80.tar
```

```bash
$ tar -xvf mak*
make-3.80/
make-3.80/po/
make-3.80/po/Makefile.in

...
make-3.80/tests/run_make_tests.pl
make-3.80/tests/test_driver.pl
```
