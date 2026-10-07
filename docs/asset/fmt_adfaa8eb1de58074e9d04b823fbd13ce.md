
```
$ ls
2341chilla.doc          dead.letter
scmp-jpc.bak
DISKCOPY.COM           foo
svgalib-1.2.11-4.i386.rpm
DRWEBDEM.IMG           foo.html
test.txt
Xfigurator-3.26-1.i386.rpm  mail
wabi
Xrootenv.0            nsmail
xxserver-wrapper-1.1-1.i386.rpm
armand                  scmp-jpc
```

注意文件或目录名是以多列显示的，列的宽度由最长名称的宽度决定。

除了列出当前目录的内容，还可以列出系统上任何可用目录的内容。例如，要列出 `/usr` 目录的内容，你将使用命令 `ls /usr`：

```
$ ls /usr
```

X11 doc i486-linuxout lib

sbin dt ibase libexec

X11R6 share

X386 etc include local

spool bin games info man

src dict -r--r-- i486-linux-libc5 interbase openwin

tmp

如上所述，请注意列表中的列数和列宽取决于所显示的最大名称的长度。

当然，你可能在想我们到底为什么要用这样的列表。这里没有信息可以告诉你哪些名称标识文件，哪些名称标识子目录，或者文件有多大。

可以通过使用 `ls` 命令的扩展来确定这些信息：`ls -1`。要了解命令的结构，请参考下一章中 `ls` 命令的完整讨论。在我的家目录中使用 `ls -1` 会产生这些结果：

（此处省略代码块）

注意每个文件都包含引用信息。最重要的信息部分是每个名称的左侧：文件或目录的最后修改日期，对于文件，日期左侧是按字节为单位的文件大小（例如，1024 字节的文件）。

开始搜索的起始目录。例如，指定 `/home` 意味着只搜索 `/home` 的子目录（换句话说，只搜索用户的家目录），而指定 `/` 则意味着将搜索所有内容。

参数是您指定搜索标准的地方。在我们的案例中，我们使用 `-name filename` 来指定我们正在搜索的文件。

动作（actions）部分指示了对找到的文件执行什么操作。通常，你可能想要使用 `-print` 动作，它表示显示文件的完整名称和路径。如果不使用该动作，`find` 命令将执行指示的搜索，但不会显示结果，这违背了该命令的初意。

将这些整合在一起，如果你想在系统中搜索所有名为 `foo` 的文件，可以使用以下命令：

```bash
$ find -name foo -print
```

在我的情况下，结果如下：

```
$ find -name foo -print
/tmp/foo
/home/armand/foo
/home/tdanish/foo
```

> 你会注意到，在上一条命令中，我们尝试搜索整个系统。为了有效地执行此操作，你需要以 root 用户身份登录，以便访问系统上的所有目录。如果你这样做，每当 `find` 尝试搜索你没有权限的目录时，你都会收到“拒绝访问”（permission denied）。

也可以搜索部分文件名。例如，如果你知道要找的文件以 `fo` 开头，那么你可以使用表达式 `fo*` 来识别所有以 `fo` 开头并以任意组合结尾的文件：

```bash
$ find -name 'fo*' -print
/tmp/foo
/var/lib/texmf/fonts
/usr/bin/font2c
/usr/bin/mh/folders
/usr/bin/mh/folder
/usr/bin/mh/forw
/usr/bin/formail
/usr/bin/fontexport
/usr/bin/fontimport
/usr/bin/fold
```

在 `fo*` 周围使用单引号。当你使用该字符时，在整个表达式周围加上单引号是非常重要的。否则，`find` 将给你出一个错误：

```bash
$ find -name fo* -print
find: paths must precede expression
Usage: find [path...] [expression]
```

如果 `find` 命令产生的结果过多，一个屏幕无法显示完，你可以像我们之前对 `ls -l` 命令所做的那样，管道给 `more` 命令：

```bash
$ find -name fo* -print | more
```

# Grep

与通过文件名、类型或日期搜索文件不同，`grep` 被用于查看一个或多个文件的内部内容，以尝试在文件中查找特定模式文本的出现。

考虑一个例子：你知道你创建了一个包含 "radio" 单词的文件，并将其存储在家目录中。然而，你忘记了文件名，想快速检查哪些文件包含 "radio"。这就是 `grep` 派上用场的地方。

假设你正处于家目录，以下命令将搜索 "radio" 并产生如所示的结果：

```bash
$ grep radio *
ab.txt:This is a test of searching for the grep word.
p.txt:On another radio station, he found that
```

注意 `grep` 命令如何为文件中每个 "radio" 单词的出现返回一行。显示文件名，后面跟着一个冒号，然后是该单词所在整行的完整文本。

通常，`grep` 命令的模式为：

```bash
$ grep <text-pattern> <file-list>
```

文本模式可以是一个简单的单词或短语，也可以是更复杂的正则表达式。关于 `grep` 使用正则表达式——一种搜索文本模式的强大方法，可以通过 `grep` 的 man 页。文件列表可以是 shell 允许任何形式。关于构成文件列表的表达式类型的完整讨论，请参考13章“理解 Shell”。

通常，你想检查单个文件的内容，格式如下：

```bash
$ grep <test-pattern> <file-name>
```

或者检查目录中所有文件的内容：

```bash
$ grep <test-pattern> *
```

其中 `*` 是一个表示搜索当前目录下所有文件的表达式。

在最简单的形式中，文本模式是不包含空格的单个单词或单词的一部分。如果你想搜索一个短语（如 "is a test"），你需要将文本包含在引号中：

```bash
$ grep "is a test" *
ab.txt:This is a test of searching for the word radio.
```

正如通过 `more` 或 `less` 命令管道命令结果有时有用一样，`grep` 也是如此。考虑你想列出当前目录下所有修改日期为 5 月 12 日的文件的情况。你可以通过将 `ls -1` 管道给 `grep` 命令来找到这些信息：

| $ ls -1l | grep "May 12" | | | |
| :--- | :--- | :--- | :--- |
| -rw-r-r- | root | root | 19197 May 12 21:17 rfbprotoheader.pdf |
| -rw-r-r- | root | root | 110788 May 12 21:20 rfpprotoA.zip |
| -rw-r-r- | root | root | 17692 May 12 21:03 01.tar.gz |
| -rw-r-r- | root | root | 25222 May 12 19:58 vnc |
| drwxr-xr-x | root | root | 1024 May 12 21:49 java |

# Tar Zip

大多数操作系统（包括 Windows 95 和 Mac）的用户都熟悉压缩包（compressed archives）的概念。压缩包是一个包含一个或多个文件的压缩格式的文件。Linux 提供了 `unzip` 命令来访问 ZIP 压缩包，Unix 世界通常使用 `gzip` 程序来压缩单个文件。

# Tar

`tar` 程序最初用于在磁带（tapes）上创建备份。在目前的形式中，它被广泛用于创建存档。创建一个 tar 存档是简单的：

```bash
$ tar cvf <file-name> <file-list>
```

此命令将创建一个由 `<file-name>` 指定的新存档（通常具有 `.tar` 扩展名），存储 `<file-list>` 中的所有文件。第13章，“理解 Shell”。重要的是，这个过程会将文件复制到存档中，因此原始文件会被删除。你会发现 `tar` 命令后面紧跟着一系列选项。这些选项中的每一个都用于控制不同的行为：

- `c` 表示我们正在创建一个存档（相对于查看已存在的存档或提取存档文件），
- `v` 表示命令应以详细模式运行（这意味着在复制到存档时会显示文件名），
- `f` 表示我们归档到一个文件（相对于磁带）。

例如，如果我们想将当前目录下所有的 `.txt` 文件归档到一个名为 `.tar` 的存档中，我们将使用命令：

```bash
$ tar cvf .tar *.txt
```

注意文件名是如何被列出并复制到存档的。幸运的是，`tar` 将复制所有文件和子目录（如果它是文件列表的一部分）。因此，如果我们有一个目录 `vnc` 并想将该目录的所有内容复制到一个新的 `vnc.tar`，我们可以使用：

```bash
$ tar cvf vnc.tar vnc
```

并获得以下结果：

```
$ tar cvf vnc.tar vnc
vnc/
vnc/LICENCE.TXT
vnc/README
vnc/README.vnc
vnc/Xvnc
vnc/classes/
vnc/classes/DesCipher.class
vnc/classes/animatedImageSource.class
vnc/classes/authenticationPanel.class
vnc/classes/clipboard-Frame.class
vnc/classes/options-Frame.class
vnc/classes/rfbProto.class
vnc/classes/vncCanvas.class
vnc/classes/vncviewer.jar
vnc/vncpasswd
vnc/vncserver
vnc/vncviewer
```

你会发现第一行表示在存档中创建 `vnc` 目录，并将该目录中的文件复制到存档中。

如果我们有一个存档，通常想要查看文件列表或提取文件内容。要查看存档的内容，我们将 `c` 选项替换为 `t`。因此，为了查看刚刚创建的 `vnc.tar` 存档中的文件列表，我们可以使用：

```bash
$ tar tvf vnc.tar
drwx-xr-x root/root      0 1998-05-16 23:55 vnc/
-rw-r-r- root/root     18000 1998-01-23 16:52 vnc/LICENCE.TXT
-rw-r-r- root/root        6142 1998-01-23 16:53 vnc/README
-rw-r-r- root/root        601 1998-01-23 16:28 vnc/README.vncserver
-drwxr-xr-x root/root   1286834 1998-01-23 13:00 vnc/classes/
drwxr-xr-x root/root        0 1998-01-23 16:24 vnc/
-rw-r-r- root/root      7143 1998-01-23 16:24 vnc/classes/DesCipher.class
-rw-r-r- root/root     1329 1998-01-23 16:24 vnc/classes/animated-MemoryImageSource.class
-rw-r-r- root/root     2068 1998-01-23 16:24 vnc/classes/authentica-tionPanel.class
-rw-r-r- root/root     1761 1998-01-23 16:24 vnc/classes/clipboard-Frame.class
-rw-r-r- root/root     3210 1998-01-23 16:24 vnc/classes/options-Frame.class
-rw-r-r- root/root     8309 1998-01-23 16:24 vnc/classes/rfbProto.class *
```

## 第 10 章 • 介绍 Linux 命令

-r--r--r--r-- root/root 7092 1998-01-23 16:24
vnc/classes/vncCanvas.class
-r--r--r--r-- root/root 7100 1998-01-23 16:24
vnc/classes/vncviewer.class
-r--r--r--r-- root/root 20564 1998-01-23 16:24
vnc/classes/vncviewer.jar
-r-xr-xr-x root/root 11433 1998-01-23 13:00 vnc/vncpasswd
-r-xr-xr-x root/root 10795 1998-05-17 00:17 vnc/vncserver
-r-xr-xr-x root/root 49685 1998-01-23 13:00 vnc/vncviewer

注意文件列表是以完整形式列出的，这类似于 `ls -l` 列出目录内容的方式。

要从当前目录提取归档中的内容，我们将 `c` 替换为 `x`：

```
$ tar xf vnc.tar
vnc/
vnc/LICENSE.TXT
vnc/README
vnc/README.vncserver
vnc/Xvnc
vnc/classes/
vnc/classes/DesCipher.class
vnc/classes/animatedMemoryImagesSource.class
vnc/classes/authenticationPanel.class
vnc/classes/clipboardFrame.class
vnc/classes/optionsFrame.class
vnc/classes/rfbProto.class
vnc/classes/vncCanvas.class
vnc/classes/vncviewer.class
vnc/classes/vncviewer.jar
vnc/vncpasswd
vnc/vncserver
vnc/vncviewer
```

## Gzip

虽然 `tar` 用于文件归档，但在上面的示例中它并没有执行任何压缩。Linux 中的压缩通常通过 `gzip` 命令实现。

与 Windows ZIP 归档不同（Windows ZIP 将多个文件压缩成单个压缩归档），`gzip` 只是简单的压缩单个文件，而不会将它们压缩成归档。

例如，如果我们有一个名为 `test.pdf` 的大文件，短期内不会使用它，并想压缩它以节省磁盘空间，我们使用 `gzip` 命令：

```
$ gzip test.pdf
```

这将压缩文件并在文件名末尾添加 .gz 扩展名，将名称改为 `test.pdf.gz`。

在压缩之前，`-l` 显示大小为 110,778 字节：

```
-rw-r-r- 1 root 110778 Jun 5 16:54 test.pdf
```

压缩后，大小已降到 83,729 字节：

```
-rw-r-r- 1 root 83729 Jun 5 16:54 test.pdf.gz
```

正如我们在本章中看到的命令一样，你可以使用任何有效的 shell 文件表达式来列出多个文件。例如，

```
$ gzip *
```

这会压缩当前目录下的所有文件（但不包括子目录中的文件）。

## 解压缩 gzip 文件

要解压 gzip 文件，可以使用带有 -d 选项的 `gzip` 命令：

```
$ gzip -d test.pdf.gz
```

这将解压文件并移除 .gz 扩展名，将文件恢复为原始未压缩状态，文件名为 `test.pdf`。

替代命令 `gunzip` 消除了对使用 -d 选项的需求：

```
$ gzip test.pdf.gz
```

## 结合 gzip 和 tar

由于早期版本的 `tar` 命令不支持压缩归档，因此通常使用 `gzip` 完成。例如，

```
$ tar cvf test.tar *.txt
```
ab.txt
pop.txt

```
$ gzip test.tar
```

这会生成一个名为 `tar.gz` 的压缩归档。

要访问此归档的内容，请先解压归档，然后使用 `tar`：

```
$ gunzip text.tar.gz
$ tar tvf text.tar
```

| 权限 | 所有者 | 组 | 大小 | 日期 | 名称 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| -rw-r-r- | root | root | 48 | 1998-06-05 16:13 | ab.txt |
| -rw-r-r- | root | root | 6 | 1998-06-05 16:13 | pop.txt |

最新版本的 `tar`（包括与所有当前发行版分带的版本）提供了一种直接访问和创建 gzip 压缩 tar 归档的方法。

只需在之前讨论的任何 `tar` 命令中添加 `z` 选项，我们就可以创建压缩归档而不需要第二个命令。

例如，
