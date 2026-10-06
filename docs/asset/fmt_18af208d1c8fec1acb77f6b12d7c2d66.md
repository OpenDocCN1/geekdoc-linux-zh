
- 4. 如果你启动 `joe` 后屏幕看起来很奇怪，可能出了什么问题？如何修复？
- 5. 在使用 `joe` 时如何从它获得帮助？
- 6. 你会使用哪些 `joe` 命令来：
  a. 删除一行
  b. 撤销你的上一个命令
  c. 退出 `joe` 编辑器
- 7. `cat` 和 `ls` 实用程序之间有什么区别？`less` 和 `more` 之间有什么区别？
- 8. shell 特殊字符有什么特殊之处？你如何让 shell 处理它们？
- 9. 大多数页面以 NAME 和 SYNOPSIS 开头。尝试以下操作：
10. 在读完本章并在你的系统上进行实验后，你应该熟悉以下内容：

# 文件操作

```
$ ls
memo
$ mv memo memo.0130
$ ls
memo.0130
```

图 3-2 使用 `mv` 为文件重命名

`mv` 实用程序不仅用于重命名文件。请参阅第 78 页的“将文件从一个目录移动到另一个目录”。

## 使用 `lpr` 打印文件

为了让多个人或作业可以使用单台打印机，UNIX 系统提供了一种打印机输出队列机制，每次仅有一个作业被打印。`lpr`（行打印机）实用程序将一个或多个文件放入打印机队列进行打印。在可以访问多台打印机的机器上，你可以使用 `-P` 选项来指示 `lpr` 将文件放入特定打印机的队列中，即使该打印机连接到网络上的另一台机器上。以下命令打印名为 `report` 的文件：

```
$ lpr report
```

下一个命令在名为 `mailbox` 的打印机上打印同一个文件：

```
$ lpr -P Mailroom report
```

你可以使用 `lpq` 工具查看行打印机队列中有哪些打印作业：

```
$ lpq
lpq is ready and printing
Rank Owner Job Files Total Size
active alex 86 (standard input) 954061 bytes
```

在这个示例中，Alex 有一个正在打印的作业，队列中没有其他作业。作业编号（在此情况下为 86）可以使用 `lprm` 工具从打印队列中删除作业并停止其打印：

```
$ lprm 86
```

你可以用一个命令向打印机发送多个文件。以下命令在名为 `laser1` 的打印机上打印三个文件：

```
$ lpr -Plaser1 05.txt 108.txt 12.txt
```

# 第 3 章：实用程序简介

```
$ cat memo

Helen:

我们在 6 月 6 日的会议上
讨论了关于信用的问题。
你对这个问题有任何
进一步的思考吗？

Alex

$ grep 'credit' memo
discussed the issue of credit.
```

图 3-3 使用 `grep` 在文件中查找单词

## 使用 `grep` 查找字符串

`grep`（全局正则表达式打印）实用程序搜索一个或多个文件，以检查其中是否包含指定的字符字符串。该实用程序不会更改它搜索的文件，而是会显示包含该字符串的每一行。

图 3-3 中的 `grep` 命令在文件 `memo` 中搜索包含该字符串的行，并显示单行。

如果 `memo` 包含 `credit`、`creditor` 或 `accreditation` 等单词，`grep` 也会显示这些行，因为它们包含了我们正在搜索的字符串。你不需要将字符串括在引号中，但这样做允许你在搜索字符串中放入空格和特殊字符。

`grep` 实用程序可以执行比在单个文件中查找简单字符串多得多的搜索。更多信息，请参阅第二部分第 751 页的 `grep` 以及附录 A，“正则表达式”。

## 使用 `head` 查看文件顶部

`head` 实用程序显示文件的前十行。它对于提醒特定文件包含的内容有用。如果你有一个名为 `months` 的文件，其中按顺序包含一年的 12 个月份，`head` 会显示从 1 月到 10 月。

`head` 实用程序可以显示任意数的行，因此你可以用它只查看文件的第一行或一屏或更多内容。要指定 `head` 显示的行数，请包含一个连字符后跟 `months` 文件第一行的行数：例如，以下命令仅显示：

```
$ cat months
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
Dec
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

$ head -1 months
Jan
```

图 3-4 使用 `head` 显示文件的前十行

`head` 实用程序还可以根据块或字符数而非行显示文件的部分。关于 `head` 的更多信息，请参阅第二部分第 758 页。

## 使用 `tail` 查看文件末尾

`tail` 实用程序与 `head` ，但它显示文件的最后十行。如果你输入以下命令，`tail` 将显示上一节中显示的 `months` 文件从 3 月到 12 月的内容：

```
$ tail months
```

取决于你的调用方式，`tail` 实用程序可以显示少于或更多的行，根据块或字符数而非行显示文件的部分，并显示正在变化的文件新增的行。关于 `tail` 的更多信息，请参阅第二部分第 869 页。

| $ cat days |
| :--- |
| Monday |
| Tuesday |
| Wednesday |
| Thursday |
| Friday |
| Saturday |
| Sunday |
| $ sort days |
| Friday |
| Monday |
| Saturday |
| Sunday |
| Tuesday |
| Wednesday |

## 使用 `sort` 按顺序显示文件

`sort` 实用程序按行顺序显示文件内容。如果你有一个名为 `days` 的文件，其中每个分隔行包含每周每一天的名称，`sort` 会按字母顺序显示文件。

`sort` 实用程序对于对列表排序有用。在一定限制内，你可以使用 `sort` 对列表进行排序。更多信息请参阅第二部分关于 `sort` 的内容。

## 使用 `uniq` 删除文件中重复行

`uniq`（唯一）实用程序显示文件并跳过相邻的重复行。如果文件在处理前已经过排序，`uniq` 将确保文件中没有两个相同的行。更多信息请参阅第二部分第 893 页的 `uniq`。

## 使用 `diff` 比较文件

`diff`（差异）实用程序比较两个文件并显示它们之间的差异。该实用程序不会更改所比较的任何文件，只是显示将一个文件转换为另一个所需的操作。如果你想比较两个版本的字母或源代码：

| $ cat colors.1 |
| :--- |
| red |
| blue |
| green |
| yellow |
| $ cat colors.2 |
| red |
| blue |
| green |
| $ diff colors.1 colors.2 |
| 4d3 |
| < yellow |

`diff` 实用程序产生一系列添加 `a`、删除 `d` 或更改 `c` 的指令，后跟着需要的操作行。如果你有两个名为 `colors.1` 和 `colors.2` 的文件，包含颜色，`diff` 会比较这两个文件并显示它们的差异。

# 通过压缩文件节省空间

当你从互联网下载内容时，经常会得到压缩文件。下面描述的实用程序允许你通过几种不同的方式对文件进行压缩和解压缩。

## 使用 `gzip` 缩小文件

大文件会占用大量的磁盘空间，并且通过网络从一个系统传输到另一个系统的时间比小文件更长。如果你不需要经常查看大文件的内容，可能希望将其保存在磁带上并将其删除。然而，如果你对该文件有持续需求，从磁带中提取副本是不方便的。为了在不完全删除文件的情况下减少使用的磁盘空间，你可以在不丢失任何信息的情况下压缩（缩小）文件。

`gzip` 工具通过对文件进行分析并更高效地编码来缩小文件。文件的新版本看起来很不同，包含许多非打印字符，因此你不应该尝试直接读取它。`gzip` 工具特别适用于包含大量重复信息的文件，因为许多 Linux 手册页都经过了 `gzip` 压缩处理以节省空间。

下面的示例显示了一个单调的文件。这个名为 `letter_e` 的文件共有 8000 行，每行都包含 72 个 e 和一个标记文件结束的 `NEWLINE`（换行符）字符。该文件占据了超过半兆的磁盘空间。

```bash
$ ls -l
--rw-rw-r-- 1 alex speedy 584000 Jul 31 06:07 letter_e
```

`-l` 选项允许 `gzip` 显示更多关于文件的信息。上面的输出显示 `letter_e` 长度为 58400 字节。

下面的 `--verbose`（或 `-v`）选项允许 `gzip` 报告它缩小了多少文件大小；在这种情况下，缩小幅度超过了 99%。

```bash
$ gzip -v letter_e
letter_e: 99.6% ---rw-rw-r-- 1 alex speedy 2030 Jul 31 06:07 letter_e
```

现在文件只有 2030 字节长。`gzip` 工具还重命名了文件。这种这种命名有助于提醒你该文件是压缩过的；例如，在不先解压缩的情况下，你可能不想显示或打印它。`gzip` 工具不会更改与文件相关的修改日期，尽管它更改了文件的内容。

在接下来的更真实的示例中，文件 `card2.bm` 包含一张复杂的计算机图形：

```bash
$ ls -l
--rw-rw-r-- 1 jenny speedy 131092 Jul 31 10:48 card2.bm
```

在这里，`gzip` 只能减少 20% 的文件磁盘存储：

## 第 3 章：实用程序介绍

```bash
$ gzip -v card2.bm
card2.bm: 19.7% -- replaced with card2.gz
$ ls -l
-rw-rw-r-- 1 jenny speedy 105261 Jul 31 10:48 card2.bm.gz
```

另一个实用程序 `compress` 也可以压缩文件，但通常效果没有 `gzip` 好。`compress` 工具会在已压缩的文件名后加上 `.Z` 标记。

## 使用 `gzip` 和 `zcat` 扩展文件

你可以使用 `gzip` 工具来恢复用 `gzip` 或 `compress` 缩小的文件：

```bash
$ gunzip letter_e.gz
$ ls -l
-rw-rw-r-- 1 alex speedy 584000 Jul 31 06:07 letter_e
$ gunzip card2.bm.gz
-rw-rw-r-- 1 jenny speedy 131092 Jul 31 10:48 card2.bm
```

`zcat` 工具允许你查看用 `gzip` 或 `compress` 压缩的文件。它是 `.gz` 和 `.z` 文件的 `cat` 等替；与 `cat` 不同，`zcat` 会解释压缩数据并显示文件内容，就像它未压缩一样。竖线 `|`（称为管道，第 101 页）将 `zcat` 的输出传递给 `head`，这样你只会看到文件的前两行：

```bash
$ zcat letter_e.gz | head -2
eeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee
eeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee
```

运行 `zcat` 后，`letter_e.gz` 的内容保持不变——文件仍然以压缩格式在磁盘上。

> **注意**
>
> 不要将 `gzip` 与 `zip` 和 `unzip` 工具混淆。后者用于打包和解包包含多个压缩成单个文件的 zip 归档。`unzip` 工具通常用于解包在 DOS 操作系统中创建 zip 归档，而 `zip` 用于构建供 DOS 使用的 zip 归档。它们在 Linux 中很少用于其他目的。

## 使用 `tar` 解压归档软件

`tar` 工具用于许多用途。它的名字代表 "tape archive"（磁带归档），因为它最初的功能是创建并制作磁带归档。现在它被用于创建单个文件，这些文件在解压后会创建一个带有任意级别子目录和子文件的目录。`tar` 文件通常用 `gzip` 压缩，以提高存储和处理的效率。你从互联网下载的文件经常就是这种格式。

## 查找实用程序和其他文件

经过 `tar` 处理并用 `gzip` 压缩的软件通常具有 `.tar` 后缀扩展名。

## 获取用户和系统信息

$ apropos sort

- MIT X Consortium (1) - MIT X 联盟信息
- X Standards (1) - MIT X 联盟标准
- bsearch (3) - 对排序数组进行二分查找。
- comm (1) - 逐行比较两个排序的文件
- look (1) - 在排序列表中查找行
- mksort (8) - 对标准输入进行排序，允许任意长度的行
- pathmerge (8) - 合并排序路径的文件
- qsort (3) - 对数组排序
- scandir, alphasort (3) - 扫描目录中的匹配项
- sort (1) - 对文本文件的行进行排序
- sq (1) - 压缩排序后的单词列表
- unsq - 解压缩排序后的单词列表
- uniq (1) - 排序列表中的重复行

```
$ man -t sort | lpr
```

管道 `|` 将 `man` 的输出传递给 `lpr` 进行打印。

## 获取用户和系统信息

这些实用工具可以让你找出谁正在使用系统以及系统是如何运行的。如果你在未连接网络的单用户机器上运行 Linux，你可能想跳过本章的其余部分。如果你已设置发送和接收电子邮件，请阅读“使用 pine 发送和接收电子邮件”（第 57 页）。

要找出是谁正在使用计算机系统，可以使用几个实用工具之一，它们提供的细节和选项各不相同。最旧的 `who` 会生成一个简短的用户列表，以及每个人正在使用的终端连接和登录系统的人。

两个较新的实用工具 `w` 和 `finger` 提供了更详细的信息（例如用户的全名以及每个用户正在运行的命令行）。如果你的计算机连接到局域网，`finger` 工具还可以用于检索远程系统上用户的信息（见第 7 章）。

## 使用 `who`

`who` 显示当前登录的用户列表。在图 3-9 中，`who` 的第一列显示 Alex 和 Jenny 已经登录。（每个人出现两次，因为他们都是 X 窗口系统图形界面内运行的第二个 shell。）第二列显示每个人 person登录的终端标识。第三列显示用户登录的日期和时间。在最后一列中，`present` 标识正在使用的 X 显示器或用户登录的远程计算机名称。

```
$ who
alex tty1 Aug 2 05:55
alex tty0 Aug 2 05:55 (x)
jenny tty2 Aug 2 05:56
jenny tty1 Aug 2 05:56 (:1.0)
```

图 3-9 `who` 工具

`who` 显示的信息对于你想与安装地上的某人通信非常有用。如果对方已登录，你可以使用 `write`（第 54 页）或 `talk`（第 55 页）立即建立通信。如果 `who` 没有显示对方已登录，或者你不需要立即通信，可以向其发送 Linux 系统邮件（第 57 页）。

如果你需要找出你正在使用哪个终端或你登录的时间，可以使用命令：

```
$ who am i
speedy!alex tty0 Aug 7 05:55 (x)
```

## 使用 `finger`

你可以使用 `finger` 显示当前正在使用系统的人员。除了登录名外，`finger` 还提供每个用户的全名，以及关于用户所在的终端行、用户上一次在键盘上输入内容的时间、用户登录的时间以及用户所在的信息（如果终端显示在系统数据库中）。如果用户通过网络登录，远程系统的名称将显示为用户的位置。例如，在图 3-10 中，用户 `hls` 从远程系统 `bravo` 登录。Helen 终端 (TTY) 名称前的星号 (*) 表示她已阻止他人直接向她的终端发送消息（使用第 56 页描述的 `mesg` 工具）。

| 登录名 | Tty | 空闲时间 | 登录时间 | 办公室 | 电话 |
|---|---|---|---|---|---|
| jenny Chen | 2 | 13:25 | Aug 2 05:56 | | |
| jenny Chen | p1 | 4:00 | Aug 2 05:55 | [ :1.0 ] | | |
| alex Watson | 1 | 13:26 | Aug 2 05:55 | [ x ] | | |
| alex Watson | p0 | 7 | Aug | | | |
| hls Helen Simpson | *p2 | Aug 19:17 | [ bravo ] | | |

图 3-10 `finger` 工具示例

```
$ finger alex
Login: alex Name: Alex Watson
Directory: /home/alex Shell: /bin/zsh
On Wed Aug 7 05:55 (cal) on tty1, idle 13:39
On Wed Aug 7 05:55 (PDT) on tty0 from x
Mail last read Wed 7 19:31 1996 (PDT)
Plan:
```

## 与其他用户通信
