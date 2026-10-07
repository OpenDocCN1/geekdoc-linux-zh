
`tail` 工具与 `head`，但它显示文件的最后十行。如果你输入以下命令，`tail` 将显示上一节 `head` 部分显示的 `months` 中从 3 月到 12 月的内容：

```bash
$ tail months
```

根据调用方式的不同，`tail` 工具可以显示少于或多于行的，根据块或字符计数而非行显示文件的部分，并显示向变化的文件添加的行。关于 `tail` 的更多信息请参阅第二部分第 869 页。

| $ cat days | $ sort days |
| :--- | :--- |
| Monday | Friday |
| Tuesday | Monday |
| Wednesday | Saturday |
| Thursday | Sunday |
| Friday | Thursday |
| Saturday | Wednesday |
| Sunday | |

## 使用 sort 排序显示文件

`sort` 工具按行顺序显示文件内容。如果你有一个名为 `days` 的文件，每个分隔行包含每一每天的名字，`sort` 将按字母顺序显示文件（图 3-5）。

`sort` 工具对于组织数据非常有用。更多信息请参阅第二部分第 856 页的 `sort`。

图 3-5 使用 sort

### 使用 uniq 去除行

`uniq`（唯一）工具显示文件并跳过相邻行。如果在此处理前对文件进行排序，`uniq` 可以确保没有两个行是相同的。关于 `uniq` 的更多信息请参阅第二部分第 893 页。

### 使用 diff 比较两个文件

`diff`（差异）工具比较两个文件并列出它们之间的更改。该工具不会更改你想要转换的内容，只是显示差异。

| cat colors.1 | $ diff colors.1 colors.2 |
| :--- | :--- |
| red | 4d |
| blue | < blue |
| green | > green |
| yellow | |

`diff` 工具产生一系列要添加（a）、删除（d）或更改（c）的行。`diff` 工具假设你想要将第一个文件（`colors.1`）转换为第二个文件（`colors.2`）。`diff` 显示的第一行（`4d`）表示你需要删除第四行（只有当你想要将第二个文件转换为第一个时，后面的数字才重要）。显示的下一行是要删除的行。`<` 符号表示该行来自第一个文件；`>` 符号识别来自第二个文件的。

图 3-6 使用 diff

## 46 第 3 章：工具简介

### 使用 file 创建文件内容

你可以使用 `file` 工具了解 Linux 系统上任何文件的内容，而无需亲自检查。在这个示例中，`file` 报告 `letter-e.z` 包含特定方式压缩的数据：

```bash
$ file letter_e.z
letter_e.gz: gzip compressed data - deflate method . .
```

关于 `echo` 的更多信息请参阅第二部分第 729 页。

### 使用 echo 在终端显示文本

`echo` 工具将你在命令行 `echo` 之后的任何内容复制到终端。示例见图 3-7。

`echo` 工具是学习 shell 和其他 Linux 程序的好工具。在第 5 章（第 107 页），`echo` 用于学习特殊字符。在第 10 章（第 316 页），它用于学习 shell 变量以及如何从 shell 程序向终端发送消息。

```bash
$ echo Hi
Hi
$ echo This is a sentence.
This is a sentence.
$ echo Good morning.
Good morning.
$
```

图 3-7 echo 工具

### 使用 date 显示时间和日期

`date` 工具显示当前的日期和时间。`date` 的示例为：

```bash
$ date
Wed Aug 14 11:23:30 PDT 1996
```

### 通过压缩文件节省空间

当你从互联网下载内容时，经常会遇到压缩文件。下面描述的工具允许你通过几种不同的方式来压缩和解压缩文件。

### 使用 gzip 缩小文件

大文件会占用大量的磁盘空间，而且通过网络从一个系统传输到另一个系统也比小文件耗得多。如果你不需要经常查看大文件的内容，你可能想将其保存在磁带上并从磁盘中删除。然而，如果你对该文件有持续的需求，从磁带中检索副本是不方便的。为了在不完全删除文件的情况下减少磁盘空间占用，你可以压缩（缩小）文件而不丢失任何信息。

`gzip` 工具可以通过分析文件内容并对其进行更高效的编码来缩小文件大小。新版本的文件看起来完全不同。事实上，新文件包含许多非打印字符，因此你不应该尝试直接读取它。`gzip` 工具特别适用于包含大量重复信息的文件，例如文本和图像数据。许多 Linux 手册页都以 gzipped 格式存储，以节省磁盘空间。

下面的示例显示了一个占用空间较大的文件。这个名为 `letter_e` 的文件共有 800 行，每行都包含 72 字节和一个标记文件结束的 NEWLINE 字符。该文件占据了超过半兆字的磁盘存储。

```bash
$ ls -l
-rw-rw-r-- 1 alex speedy 584000 Jul 31 06:07 letter_e
```

`-l` 选项允许我们显示关于文件的更多信息。上面显示 `letter_e` 的长度为 58400 字节。

下面的 `--verbose`（或 `-v`）选项允许 `gzip` 报告它缩小了多少文件大小；在这种情况下，缩小比例超过了 99%。

```bash
$ gzip -v letter_e
letter_e: 99.6% -- replaced with letter_e.gz
```

```bash
$ ls -l
-rw-rw-r-- 1 alex speedy 2030 Jul 31 06:07 letter_e.gz
```

现在文件长度为 2030 字节。`gzip` 工具重命名了文件——它在名称末尾添加了 `gz`。这种命名约定有助于提醒你该文件是经过压缩的；例如，你不想在不解压缩的情况下直接播放或打印它。`gzip` 工具不会更改文件的修改日期，尽管它完全改变了文件的内容。

在接下来的更真实的示例中，文件 `card2.bm` 包含一张复杂的图形：

```bash
$ ls -l
-rw-rw-r-- 1 jenny speedy 131092 Jul 31 10:48 card2.bm
```

在这里，`gzip` 只能减少约 20% 的文件磁盘存储：

```bash
$ gzip card2.bm
card2.bm      19.7% -- replaced with card2.bm
$ ls -l
-rw-rw-r-- 1 jenny speedy 105261 Jul 31 10:48 card2.bm
```

第二个工具 `compress` 也可以压缩文件，但效果没有 `gzip` 好。`compress` 工具通过在文件名末尾添加 `.Z` 来标记它已处理过的文件。

### 使用 gunzip 和 zcat 扩展文件

你可以使用 `gunzip` 工具来恢复用 `gzip` 或 `compress` 缩小的文件：

```bash
$ gunzip letter_e.gz
$ ls -l
-rw-rw-r-- 1 alex speedy 584000 Jul 31 06:07 letter_e
$ gunzip card2.bm.gz
$ ls -l
-rw-rw-r-- 1 jenny speedy 131092 Jul 31 10:48 card2.bm
```

`zcat` 允许你查看用 `gzip` 或 `compress` 压缩的文件。它等同于针对 `.gz` 和 `.z` 文件的 `cat`；像 `cat` 一样，`zcat` 会解释压缩数据并像文件未压缩一样显示其内容。垂直竖线（`|`），称为管道（第 101 页），将 `zcat` 的输出传递给 `head`，这样你只能看到文件的前两行：

在运行 `zcat` 后，`letter_e.gz` 的内容保持不变——文件仍然以压缩格式存储在磁盘上。

### 注意事项

不要将 `gzip` 和 `gunzip` 与 `zip` 和 `unzip` 工具混淆。后两个用于将包含多个文件的归包打包成单个文件。`unzip` 工具经常用于解压在 DOS 操作系统下创建的 `zip` 归包，而 `zip` 用于构建用于 DOS 的 `zip` 归包。它们在 Linux 中很少用于其他用途。

## 使用 TAR 解压存档软件

`tar` 工具用于许多用途。它的名字是 tape archive（磁带存档）的缩写，因为它的原始功能是创建和读取磁带存档。今天，它用于创建单个文件，这些文件在解压后会创建一个带有任意级别子目录和文件的目录。`tar` 文件通常用 `gzip` 压缩，以提高存储和处理的效率。你从互联网下载的文件经常是这种格式。

### 查找工具和其他文件

经过 `tar` 处理并用 `gzip` 压缩的软件通常具有 `.tar.gz` 或 `.tgz` 扩展名。较新版本的 `tar` 内置了压缩功能。

## 获取用户和系统信息 51

```
$ apropos sort
MIT X Consortium (1) - MIT X Consortium information
X Standards (1) - MIT X Consortium Standards
search (3) - binary search of a sorted array.
come - compare two sorted files by line
look (11) - find lines is a sorted list
mksort (8) - sort the standard input, allowing arbitrarily long
pathmerge (8) - merge sorted paths files
qs (3) - sorts an array
scandir, asphalos (3) - scan a directory for matching entries
sort (1) - sort lines of text files
sq (3) - squeeze a sorted word list
unsq - unsqueeze a sorted word list
uniq (1) - remove duplicate lines from a sorted list
```

图 3-8 的 `apropos` 工具

```
$ man -t sort | lpr
```

管道（`|`）将 `man` 的输出传递给 `lpr` 进行打印。

### 获取用户和系统信息

这些实用程序允许你找出是谁正在使用系统以及系统是如何运行的。如果你在没有连接网络的单用户机器上运行 Linux，可能想跳过本章的其余部分。如果你已经设置好发送和接收电子邮件，请阅读“使用管道发送和接收电子邮件”（第 57 页）。

要找出是谁在用电脑，可以使用几个实用程序之一，它们在提供的细节和支持的选项上有所不同。最古老的实用程序 `who` 会生成一个短列表，列出每个人正在使用的终端连接以及该用户登录系统的时间。

两个实用程序 `w` 和 `finger` 显示了更详细的信息（例如每个用户的全名以及他们正在运行的命令行）。如果你的计算机连接到本地局域网，还可以使用 `finger` 工具来检索远程系统上的用户信息（见第 7 章）。

### 使用 who

`who` 显示当前登录的用户列表。在图 3-9 中，`who` 的第一列显示 Alex 和 Jenny 已经登录。（每个人都出现了两次，是因为他们都在 X Window 系统图形用户界面内各运行着登录 shell。）第二列显示每个人正在使用的终端标识。第三列显示登录的日期和登录用户。最后一列（如果存在）会识别正在使用的 X 显示器或该用户登录的远程计算机名称。

| S who | | | | |
|---|---|---|---|---|
| alex | tty1 | Aug | 2 05:55 |
| alex | tty0 | Aug | 2 05:55 (x) |
| jenny | tty2 | Aug | 2 05:56 |
| jenny | tty1 | Aug | 2 05:56 (:1.0) |

图 3-9 的 `who` 工具

`who` 显示的信息对于你想与安装环境中的某人通信非常有用。如果该人已登录，你可以使用 `write`（第 54 页）或 `talk`（第 55 页）立即建立通信。如果 `who` 没有显示该人登录，或者你不需要立即通信，可以发送 Linux 系统邮件（第 57 页）。

如果你需要找出你正在使用的终端或你登录的时间，可以使用命令 `who am i`。

| S who am i | | | | |
|---|---|---|---|---|
| speedyalex | tty0 | Aug 7 | 05:55 (x) |

### 使用 finger

你可以使用 `finger` 显示当前正在使用系统的人员列表。除了登录信息，`finger` 还提供每个用户的全名，以及关于用户正在使用的终端行、用户最近在键盘上输入内容的时间、用户登录的时间以及关于用户所在位置的信息。如果你的计算机连接到本地局域网，`finger` 工具还可以用于检索远程系统上的用户信息（见第 7 章）。例如，在图 3-10 中，`hls` 显示了用户所在位置。在 `finger` 的输出中，星号（*）表示该用户通过网络登录。`mesg` 工具的描述在第 56 页。

| S finger | Name | Tty | Idle | Login | Office |
||---|---|---|---|---|
| jenny | Jenny Chen | 2 | 13:25 | Aug 2 | |
| jenny | Jenny Chen | p1 | 4:00 | Aug 2 | |
| alex | Alex Watson | 1 | 13:26 | Aug 2 | |
| alex | Alex Watson | p0 | 7 | Aug 2 | |
| hls | Helen Simpson | p2 | 19:17 | Aug 2 | |

图 3-10 的 `finger` 工具

```
$ finger alex
Login: alex Name: Alex Watson
Directory: /home/alex Shell: /bin/zsh
On since Wed 7 05:55 (cal) on tty1, idle 13:39
On since Wed 7 05:55 (PDT) on ty0
```

图 3-11 `finger` 的另一种用法

你还可以通过 `finger` 指定用户来获取关于该人的更多信息。图 3-11 显示了关于用户的详细信息。Alex 正在登录并活动使用终端（如果他没有登录，`finger` 将报告他空闲了多久）。你还可以通过 `finger` 获取更多信息，你应该联系分机 1693。你可能会发现创建一个计划会有很大帮助；计划可以包含你选择的信息，例如你的日程、兴趣、电话号码或地址。如果 Alex 没有登录，`finger` 将报告他上次使用系统的时间。

如果你不知道某人的名字，可以使用 `finger` 工具来获取。例如，你可能知道某人姓 Simpson，但可能猜不到她的名字是 Helen。`finger` 工具还可以通过名字或姓氏搜索 Helen 的信息。以下命令可以找到你需要的信息，以及系统中其他名为 Helen 或 Simpson 的用户信息。`finger` 是敏感的。

```
$ finger helen
Login: hls

$ finger simpson
Login: hls
```

### w

`w` 工具显示当前登录的用户列表。在图 3-12 中，第一列 `w` 显示 Alex、Jenny 和 Scott 已登录。第二列显示每个人使用的终端标识。第三列显示每个人登录的位置（即 X 显示器或远程计算机）；某些版本的 `w` 不显示此列。第四列显示每个人登录的日期和时间。第五列指示每个人空闲了多久（即自上次按下键盘以来经过的分钟）。接下来两列提供了每个人在当前会话期间以及在当前运行任务上使用的处理器度量。最后一列显示每个人正在运行的命令。

| W | | | | | |
|---|---|---|---|---|---|
| User | tty | from | login | idle | JCPU | what |
| alex | tty1 | | 5:55am | 13:45 | 1 | -zsh |
| alex | tty0 | | 5:55am | 27 2:55 | 0 | 0 |
| jenny | tty2 | | 5:56am | 13:44 | 0 | nvi |
| jenny | tty1 | | 5:56am | 36 | 3 | ntmp.txt |
| scott | tty2 | bravo | | 7:17pm | 3 | w |

图 3-12 的 `w` 工具

## 与其他用户通信 55

```
$ write alex
Hi Alex, are you there? o
```

图 3-13 开始向 Alex 写入信息

从一个终端到另一个终端的行（图 3-14）。Alex 和 Jenny 建立了一项约定：当你准备好让对方输入时，输入 `o`（代表 over，结束）；当你准备好注销时，输入 `oo`（代表 over and out，离开）。你可以使用这种约定、另一种约定，或者完全不使用。当你想要停止与另一个用户的通信时，在行的开头按下 CONTROL-D。按下 CONTROL-D 会写入一个退出信号（quit），在对方的终端上显示 EOF（文件结束），并让你返回到 shell。另一个用户也必须执行此操作。

```
$ write Alex
Hi Alex are you there? o
Message from alex@speedy on type 3 at 08:20 ...
Yes Jenny, I'm here. o
```

图 3-14 Alex 使用 `write` 响应

### 使用 talk 与另一用户通信
