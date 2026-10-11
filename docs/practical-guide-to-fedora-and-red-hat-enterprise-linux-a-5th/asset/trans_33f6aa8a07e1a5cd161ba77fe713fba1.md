

**可选** 你可以在同一命令行中结合使用 `gunzip` 和 `tar` 命令，通过管道（`|`）将 `gunzip` 的输出重定向，使其成为 `tar` 的输入：
`$ gunzip -c make-3.80.tar.gz | tar -xvf -`
`-c` 选项使 `gunzip` 通过管道发送其输出，而不是创建一个文件。有关此命令行工作原理的更多信息，请参阅“管道”（第 238 页）和 `gzip`（第 163 页）。
更简单的解决方案是使用 `tar` 的 `-z` 选项。该选项使 `tar` 直接调用 `gunzip`（在创建存档时调用 `gzip`），并将上述命令行简化为
`$ tar -xzvf make-3.80.tar.gz`
以类似的方式，`-j` 选项调用 `bzip2` 或 `bunzip2`。

## 定位命令

**whereis** 和 **apropos** 实用程序可以帮助你找到名称已遗忘或位置未知的命令。当存在同一实用程序或程序的多个副本时，**which** 会告诉你将运行哪个副本。**locate** 实用程序在本地系统上搜索文件。

### which 和 whereis：定位实用程序

当你向 Linux 输入命令时，shell 会在目录列表中搜索具有该名称的程序，并运行它找到的第一个程序。此目录列表称为**搜索路径**。有关如何更改搜索路径的信息，请参阅第 306 页的“PATH：Shell 查找程序的位置”。如果你不更改搜索路径，shell 只搜索标准目录集，然后停止搜索。然而，系统中的其他目录也可能包含有用的实用程序。

**which** **which** 实用程序通过显示实用程序文件的完整路径名来定位实用程序。（第 6 章包含有关路径名和 Linux 文件系统结构的更多信息。）本地系统可能包含几个同名命令。当你键入命令名称时，shell 在你的搜索路径中查找该命令，并运行它找到的第一个命令。你可以使用 **which** 找出 shell 将运行程序的哪个副本。在以下示例中，**which** 报告了 **tar** 命令的位置：
`$ which tar`
`/bin/tar`
当命令似乎以意外方式运行时，**which** 实用程序可能很有帮助。运行 **which** 时，你可能会发现你正在运行一个非标准版本的工具，或者不是你预期的那个工具。*重要*提示：第 198 页的“标准目录和文件”提供了可执行文件标准位置的列表。例如，如果 tar 没有正常工作，并且你发现你运行的是 /usr/local/bin/tar 而不是 /bin/tar，你可能怀疑本地版本已损坏。

### which、whereis 和内置命令

which 和 whereis 实用程序仅报告磁盘上找到的命令名称；它们不报告 shell 内置命令（构建在 shell 中的实用程序；参见第 247 页）。当你使用 whereis 试图找到 echo 命令（既作为实用程序程序存在，也作为 shell 内置命令存在）存储在哪里时，你会得到以下结果：

```
$ whereis echo
echo: /bin/echo /usr/share/man/man1/echo.1.gz
```

whereis 实用程序不显示 echo 内置命令。甚至 which 实用程序也会报告错误的信息：

```
$ which echo
/bin/echo
```

在 bash 中，你可以使用 type 内置命令（第 937 页）来确定某个命令是否为内置命令：

```
$ type echo
echo is a shell builtin
```

whereis whereis 实用程序通过查找标准位置而不是使用你的搜索路径来搜索与实用程序相关的文件。例如，你可以找到与 tar 相关的文件位置：

```
$ whereis tar
tar: /bin/tar /usr/share/man/man1/tar.1.gz
```

在这个示例中，whereis 找到了两个关于 tar 的引用：tar 实用程序文件和 tar 手册页。

### which 与 whereis

给定程序名称，which 按顺序遍历搜索路径中的目录，并定位该程序。如果搜索路径中包含多个具有指定名称的程序，which 只显示第一个（即你将会运行的那个）的名称。

whereis 实用程序遍历标准目录列表，并且独立于你的搜索路径工作。使用 whereis 来定位指定程序的二进制（可执行）文件、任何手册页和源代码；whereis 显示它找到的所有文件。

### apropos：搜索关键字

当你不知道执行特定任务所需的命令名称时，可以使用 apropos 配合关键字进行搜索。此实用程序在所有手册页的简短描述行（顶行）中搜索关键字，并显示包含匹配项的手册页。使用 -k（关键字）选项调用的 man 实用程序提供与 apropos 相同的输出（它是同一个命令）。

apropos 使用的名为 whatis 的数据库在 Fedora/RHEL 系统首次安装时并不存在，但由 cron（第 565 页）使用 makewhatis 自动构建。（cron 实用程序运行 /etc/cron.weekly/makewhatis.cron 脚本以构建 whatis 数据库。）如果你定期关闭系统（例如笔记本电脑），可能不会运行该脚本。如果 apropos 没有产生任何输出，请以 root 身份运行命令 makewhatis -w。

以下示例展示了使用 who 关键字调用 apropos 时的输出。输出包括每个命令的名称、包含它的手册部分以及手册页顶部的简短描述。此列表包括你需要的实用程序（who），并标识了你可能发现有用的其他相关工具：

```
$ apropos who
at.allow [at] (5) - determine who can submit jobs via at or batch
at.deny [at] (5) - determine who can submit jobs via at or batch
atwhois (1) - client for the whois service
dapwhooami (1) - LDAP who am i? tool
w (1) - Show who is logged on and what they are doing
who (1) - show who is logged on
whoami (1) - print effective userid
```

### whatis

whatis 实用程序类似于 apropos，但只查找实用程序名称的完整单词匹配：

```
$ whatis who
who (1) - show who is logged on
```

### locate：搜索文件

locate 实用程序在本地系统上搜索文件：

```
$ locate motd
/etc/motd
/lib/security/pam_motd.so
/usr/share/doc/pam-1.1.0/html/sag-pam_motd.html
/usr/share/doc/pam-1.1.0/txts/README.pam_motd
/usr/share/man/man8/pam_motd.8.gz
```

在使用 locate 之前，updatedb 实用程序必须构建或更新 locate 数据库。通常，数据库每天由 cron 脚本（第 565 页）更新一次。

如果你不在网络上，请跳过本章的其余部分

> 提示 如果你是未连接到网络的系统上唯一的用户，你可能想跳过本章的其余部分。如果你不在网络上但已设置为收发电子邮件，请阅读第 174 页的“电子邮件”。

## 获取用户和系统信息

本节介绍提供关于谁在使用系统、这些用户在做什么以及系统运行情况的信息的实用程序。要了解谁在使用本地系统，你可以采用几种实用程序中的一种，它们在提供的详细信息和支持的选项方面有所不同。最古老的实用程序 **who** 生成本地系统上已登录用户的列表、每个人正在使用的设备以及每个人登录的时间。

![](img/f28adb66a7398a382f0505e0ba74a872_209_0.png)

**图 5-10 who 列出已登录的用户**

**w** 和 **finger** 实用程序显示更多细节，例如每个用户的完整姓名以及每个用户正在运行的命令行。如果你的计算机连接到网络，可以使用 **finger** 实用程序获取远程系统上用户的信息。第 172 页的表 5-1 总结了这些实用程序的输出。

### who：列出系统上的用户

**who** 实用程序显示已登录用户的列表。在图 5-10 中，**who** 显示的第一列表明 Alex 和 Jenny 已登录。（Alex 从两个位置登录。）第二列显示每个用户的终端、工作站或终端仿真器所连接的设备。第三列显示用户登录的日期和时间。可选的第四列显示（在括号中）远程登录所在的系统名称；此列未显示在图 5-10 中。

**who** 显示的信息在你希望与安装地点的用户沟通时很有用。当用户已登录时，你可以使用 **write**（第 172 页）立即建立通信。如果 **who** 没有列出该用户，或者你不需要立即沟通，你可以向该人发送电子邮件（第 174 页）。

如果 **who** 的输出在屏幕上滚动消失，你可以通过管道（`|`，第 158 页）重定向输出，使其成为 **less** 的输入，后者一次显示一页输出。你也可以使用管道重定向输出通过 **grep** 来查找特定名称。

如果你想知道正在使用哪个终端或登录时间，可以使用命令 **who am i**：

![](img/f28adb66a7398a382f0505e0ba74a872_209_1.png)

### finger：列出系统上的用户

可以使用 **finger** 显示系统上已登录用户的列表。除了用户名外，**finger** 还提供每个用户的完整姓名，以及有关用户终端连接的设备、用户最近键入内容的时间、用户登录时间以及联系方式的信息

