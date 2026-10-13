
这会在 /bin 目录下运行 pwd 命令，而不是 shell 内置的 pwd。你会看到 pwd 命令的简短帮助文件，而不是当前目录。如果您对自己的位置有任何疑问，请使用 /bin 目录下的 pwd 命令。

## 使用 find 命令搜索目录中的匹配文件

find 命令是一个功能强大的搜索工具，可用于在硬盘上查找文件。您可以使用简单的 find 命令行轻松地在硬盘上搜索文件。例如，要在 /usr 目录下搜索 spell 命令，请使用以下命令：

```
# find /usr -name spell -print
```

您可以使用 find 命令按日期查找文件，还可以指定时间范围。例如，要查找在过去 100 天内未使用的 /usr/bin 目录中的程序，可以尝试以下操作：

```
# find /usr/bin -type f -atime +100 -print
```

-atime 选项后面跟一个表示天数的数字。要查找 /usr/bin 目录中新建或修改且年龄为一天或更少的文件，可以使用以下选项：

```
# find /usr/bin -type f -mtime -1 -print
```

-mtime 选项后面跟一个天数（本例中为一天或更少），用于查找已修改的文件。find 命令在搜索字符串中也接受通配符（如 * 或 ?），您将在第 5 小时学习到相关内容。作为一个简单示例，您可以使用 find 显示 /usr 目录中的所有 PostScript 文件，方法如下：

```
# find /usr -name '*.ps' -print
```

第 16 小时《图形工具》中的“理解图形格式”部分介绍了 PostScript 文件。

-xdev 是 find 命令的一个方便选项。到目前为止的示例显示的搜索仅限于 /usr 目录。但如果您想从根目录（/）开始搜索怎么办？-xdev 将搜索限制在当前文件系统，本例中为 Linux。如果没有它，find 会愉快地继续通过任何已挂载的 CD-ROM 或您的 DOS 或 Windows 分区进行搜索，可能找到您不感兴趣的文件，从而减慢搜索速度并使搜索输出混乱。

例如，您可以使用 -xdev 选项将 find 命令搜索限制在 Windows 分区。要查找 /mnt/dos 目录下已挂载的 Windows 分区中以 .sys 结尾的所有文件，请按如下方式使用 -xdev 选项：

```
# find /mnt/dos -name *.sys -print -xdev
```

find 命令有许多不同的选项和用途。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_96_0.png)

> 您还可以让 find 命令执行搜索并销毁任务以从计算机中删除选定的文件。有关详细信息，请参阅第 21 小时《基本系统管理》中的“节省磁盘空间”。

虽然 find 能快速搜索硬盘和文件系统，但还有其他快速查找文件（尤其是程序）的方法。继续阅读以了解更多信息！

## 使用 whereis 命令查找文件

whereis 命令可以快速查找文件，并显示文件二进制文件、源代码和手册页所在的位置。例如，以下命令显示 find 命令位于 /usr/bin 目录，其手册页位于 /usr/man/man1 目录：

```
# whereis find
find: /usr/bin/find /usr/man/man1/find.1.gz
```

您还可以使用 whereis 仅查找程序的二进制版本，方法如下：

```
# whereis -b find
find: /usr/bin/find
```

如果您只想查看程序的位置而不查看其文档，这很有用。如果 whereis 找不到您的请求，您会得到一个空返回字符串，例如：

```
# whereis foo
foo:
```

问题的一部分也可能是文件不在 whereis 命令搜索的任何目录中。whereis 查找的目录已硬编码在程序中。虽然这看起来可能是一个缺点，但将搜索限制在已知目录（如 /usr/man、/usr/bin 或 /usr/sbin）可以加快查找文件的速度。

虽然 whereis 比使用 find 定位程序或手册页更快，但您还可以使用一个更快的搜索工具，称为 locate，有关介绍请参见下一节。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_96_1.png)

## 使用 locate 命令定位文件

加快文件搜索速度的一种方法是不要搜索文件目录！您可以通过使用 locate 之类的程序来实现。locate 使用单个文件名和位置数据库，通过查看单个文件而不是遍历硬盘来节省时间。使用 locate 查找文件比 find 命令快得多，因为 locate 直接访问数据库文件，找到任何匹配的文件名并显示其结果。

Locate 使用起来很简单。例如，要查找系统上的所有 PostScript 文件，可以输入以下内容：

```
# locate *.ps
```

文件几乎会立即出现在您的屏幕上。您甚至可能会发现 locate 命令行比 find 命令更容易使用。然而，有一个问题：find 可以“开箱即用”，而 locate 需要系统上所有文件的数据库。但不用担心——该过程几乎是自动的。

安装 OpenLinux 后，locate 数据库每天凌晨 5:50 更新。要立即创建 locate 数据库的更新版本，需要使用 updatedb 命令。确保您以 root 操作员身份登录，或使用 su 命令（参见第 21 小时）。在提示符下，输入以下内容：

```
# updatedb
```

updatedb 命令完成工作可能需要一分钟左右，但完成后，locate 的数据库 locatedb 位于 /var/state 目录中。对于 900MB 的文件，locatedb 大约为 700,000 个字符。使用 locate 命令的唯一缺点是，随着时间的推移，随着您向系统添加或删除文件，其数据库可能会过时。幸运的是，OpenLinux 会自动更新 locate 数据库；有关详细信息，请参阅第 24 小时《调度》。

## 使用 whatis 和 apropos 获取命令摘要

当您首次探索 OpenLinux 系统时，您可能会遇到功能不明确的程序。许多 Linux 程序设计为在命令行上使用 ?, -help 或 -help 选项提供一些帮助，但通常不应在不知道程序用途的情况下运行程序。

whatis 命令可能可以帮助您通过从程序手册页派生的摘要行快速了解程序是什么。例如，要了解 who 是什么，可以输入以下内容：

```
# whatis who
```

您的屏幕会清空，whatis 命令会显示如下摘要：

```
who (1)  - show who is logged on
```

按 Q 退出 whatis 命令。然而，与 locate 命令不同，您必须先使用 makewhatis 命令构建命令摘要数据库，该命令位于 /usr/sbin 目录下。为此，请确保您以 root 身份登录，并输入以下内容：

```
# makewhatis
```

makewhatis 命令与 updatedb 命令类似，需要几分钟时间来构建 whatis 数据库，该数据库称为 whatis，位于 /usr/man/man1 目录下。makewhatis 命令有几个选项，但没有手册页。要查看快速摘要，请使用以下命令：

```
# makewhatis -?
```

您需要定期更新 whatis 数据库以跟踪任何新安装的程序。请参阅第 24 小时，了解如何让 OpenLinux 自动执行此操作的提示。

现在您可以看到 whereis 和 whatis 如何帮助您查找程序或了解它们的作用。但如果您想做某事却记不起哪个程序执行什么操作怎么办？在这种情况下，您可以使用 apropos 命令。

例如，如果您记不起哪个命令用于搜索文件，可以输入以下内容：

```
# apropos search
```

```
apropos (1)      - search the whatis database for strings
badblocks (8)    - search a device for bad blocks
bsearch (3)      - binary search of a sorted array
conflict (8)     - search for alias/password conflicts
find (1)         - search for files in a directory hierarchy
hcreate, hdestroy, hsearch (3) - hash table management
lfind, lsearch (3) - linear search of an array
lkbdb (1)        - search bibliographic databases
lookbib (1)      - search bibliographic databases
lsearch (n)      - See if a list contains a particular element
manpath (1)      - determine user's search path for man pages
strbrk (3)       - search a string for any of a set of characters
strspn, strcspn (3) - search a string for a set of characters
tsearch, tfind, tdelete, twalk (3) - manage a binary tree
```

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_98_0.png)
