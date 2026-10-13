
whatis (1)      . 搜索 whatis 数据库中的完整单词。
zgrep (1)      . 搜索可能已压缩的文件以查找
  → 正则表达式
zipgrep (1)    . 搜索可能为 zip 文件的
  → 正则表达式

你在屏幕上看到来自 whatis 数据库的程序列表。读完列表后按 Q 键。apropos 命令使用此数据库搜索你输入的关键字。如果你保持 whatis 数据库为最新状态，就能够使用 apropos 来帮助你找到所需的程序。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_99_0.png)

> 你也可以使用 man 命令的 -K 选项来做与 apropos 相同的操作，但搜索速度慢，并且会在搜索结果中逐个显示手册页。例如，要搜索处理 PostScript 的任何程序，可以尝试以下操作：
> 
> # man -K PostScript
> 
> 这可能会在你使用 Q 退出之前产生以下输出：
> 
> /usr/man/man7/unicode.7? [ynq] n
> /usr/man/man7/suffixes.7? [ynq] n
> /usr/man/man7/groff_char.7? [ynq] n
> /usr/man/man1/convert.1? [ynq] n
> /usr/man/man1/xv.1? [ynq] n
> /usr/man/man1/xdvi.1? [ynq] n
> /usr/man/man1/dvips.1? [ynq] n
> /usr/man/man1/afm2tfm.1? [ynq] n
> /usr/man/man1/ps2pk.1? [ynq] n
> /usr/man/man1/ps2frag.1? [ynq] q

## 读取目录和文件

现在你已经了解了目录导航、搜索文件以及如何查找有关程序的更多信息，我将向你介绍其他可用的基本 Linux 命令。本节向你展示如何列出目录的内容、制作硬盘目录以及读取文件的内容。你将学习这些命令的基本形式以便入门。

## 使用 ls 命令列出目录

ls（list directory）命令是最常用的程序之一。在最简单的形式中，ls 会列出当前目录中的几乎所有文件。但这个名字很短的命令，可能拥有比任何其他程序都多的命令行选项（截至上次统计超过 75 个）！

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_100_0.png)

为什么 Linux 命令这么多，为什么它们的名字这么短？如果你最初不熟悉 Linux，很快就会发现数百个程序拥有短小、起初难以理解的名字，如 cd、pwd、df、du、ls、as、ar、at、w 等等。不要被吓到！相反，要感谢 Linux 继承了这一丰富的传统 UNIX 工具集合。UNIX 的哲学是，一个好的程序很小并且做一件事做得非常好；操作系统的强大之处在于将多个程序的输出组合起来协同工作。许多命令名称是为了节省输入而选择的。为什么要输入长程序名，而一两个字母就足够了？此外，许多早期的 UNIX 用户通过非常慢的（110 波特）终端线路与远程 UNIX 计算机通信，简短、精确的命令传输速度更快。要更好地欣赏这些简短的命令名称，请阅读第 6 小时。

在简单形式中，ls 会列出当前目录中的文件，如以下示例所示：

```
[home/bball]$ ls
News          axhome        nsmail        search
author.msg    documents     reading       vultures.msg
auto          mail          research
```

示例列出了我的主目录中的文件。

你也可以使用 -m 选项以单行、逗号分隔的方式列出文件：

```
# ls -m
News, author.msg, auto, axhome, documents, mail, nsmail, reading,
=> research, search, vultures.msg
```

如果你不喜欢这种列表方式，可以使用 -x 选项将文件水平排序，而不是默认的垂直排序，如下所示：

```
# ls -x
News          author.msg    auto           axhome         documents
mail          nsmail        reading        research       search
vultures.msg
```

这些都是文件，还是有几个目录？一种方法是使用 -F 选项来判断：

```
# ls -F
News/         axhome        nsmail/       search*
author.msg    documents/    reading/      vultures.msg
auto/         mail/         research/
```

```
# ls -aF
./
../
.Xauthority
.Xdefaults
.addressbook
.addressbook.lu
.bash_history
.bash_logout
.bash_profile
.bashrc
.desksdefaults
.dt/
.dtprofile*
.festival_history
.forward
.fvwm2rc95*
.index/
.mailcap
.mailrc
.mime_types
.ncftp
.nedit
.neditdb
.netscape/
.newsrc
.oldnewsrc
.pinerc
.procmail/
.procmailrc
.tin
.xinitrc*
News/
.author.msg
auto/
axhome/
documents/
mail/
nsmail/
reading/
research/
search*
vultures.msg
```

正如你所见，以句点（.）开头的名称的文件或目录，除非明确请求所有文件，否则 ls 不会显示。使用 -F 选项是一种查看列表中的文件和目录的方法，但如果你有彩色显示器或使用彩色 X11，可以让 ls 以不同颜色显示文件、目录或可执行文件。要做到这一点，使用 --color 选项如下：

```
# ls --color
```

在 X11 中，使用 xterm 终端，目录为蓝色，程序为绿色，普通文件为黑色。你也可以自定义不同类型文件使用的颜色。

例如，要使所有图形文件，如 PCX 或 GIF 图形，以红色显示，并且所有以 .txt 结尾的文本文件以紫色显示，创建一个名为 LS_COLORS 的 shell 环境变量，或系统或用户定义的值，定义颜色并导出变量如下：

```
# LS_COLORS="*pcx=31:*gif=31:*txt=35";export LS_COLORS
```

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_101_0.png)

> ls 手册页列出了默认颜色。你可以将自定义定义放在你的 .bashrc 文件中，以便下次登录 OpenLinux 时使用。作为 root 操作员，你也可以为所有用户指定系统范围的默认颜色。请参阅第 6 小时，了解如何为 OpenLinux 系统上的所有用户定义 LS_COLORS 和其他环境变量。

## 长目录列表

你想了解有关文件的更多信息吗？你可以使用 ls -l 选项使用长格式列表，例如：

```
# ls -l
total 2086
-rw-r--r-- 1 bball users 256382 Dec 30 15:42 162317art.zip
drwx------ 6 bball users 1024 Dec 17 22:35 Desktop
drwxr-xr-x 24 bball users 1024 Dec 2 15:09 Office40
```

```
drwxr-xr-x 22 bball users 1024 Dec 2 11:23 Office50
-rw-r--r-- 1 bball users 29360 Dec 30 14:38 Sheet.as
-rw-r--r-- 1 bball users 705 Dec 30 15:15 Sheet.wk3
-rw-r--r-- 1 bball users 2360 Dec 30 15:15 Sheet.x14
-rw-r--r-- 1 bball users 5632 Dec 30 15:20 Sheet.x15
-rw-r--r-- 1 bball users 2950 Dec 17 20:37 XWP
drwxr-xr-x 5 bball users 1024 Mar 24 19:58 aim
drwxr-xr-x 4 bball users 1024 Dec 30 15:15 axhome
drwxr-xr-x 2 bball users 1024 Dec 23 23:15 documents
drwxr-xr-x 2 bball users 1024 Dec 11 11:06 graphics
drwxr-xr-x 6 bball users 1024 Dec 1 11:19 lg
drwxrwxrwt 2 bball users 1024 Dec 9 16:34 mail
drwx------ 2 bball users 1024 Nov 8 10:56 nsmail
drwxr-xr-x 3 bball users 1024 Nov 16 10:22 rvpayer5.0
drwxr-xr-x 5 bball users 1024 Nov 4 10:49 so50
drwxr-xr-x 2 bball users 3072 Dec 30 15:43 ty12
-rw-r--r-- 1 bball users 12004 Dec 30 12:37 worth.as
-rw-r--r-- 1 bball users 1533 Dec 30 13:09 worth.csv
-rw-r--r-- 1 bball users 227985 Dec 30 13:08 worth.dif
-rw-r--r-- 1 bball users 4905 Dec 30 13:12 worth.sc
-rw-r--r-- 1 bball users 8110 Dec 30 13:09 worth.slk
-rw-r--r-- 1 bball users 1533 Dec 30 13:09 worth.txt
```

正如你所见，有八个不同的列。第一列是文件的权限标志，在第 22 小时“处理文件和文件系统”中介绍。这些标志通常显示文件的类型，以及谁可以读取、写入（修改或删除）或运行该文件。

下一列显示链接数，在第 5 小时讨论。接下来是所有者名称，然后是组名。所有者和组在第 22 小时讨论。接下来列出文件大小，然后是时间戳，说明文件或目录的创建或最后修改时间。最后一列显然是每个文件的名称。

## 指定其他目录

你也可以通过在命令行上指定目录或路径名，使用 ls 命令查看其他目录的内容。例如，如果你想查看 /usr/bin 目录中的所有文件（你可能会看到比这些更多的文件），请使用以下命令：

```
# ls /usr/bin
arch dd gzip netstat stty
ash df hostname nisdomainname su
awk dmesg kill ping sync
basename nsdomainname ksh ps tar
bash doexec ln pwd tcsh
bsh domainname login red touch
cat echo ls rm true
chgrp ed mail rmdir umount
chmod egrep mkdir rpm uname
```
