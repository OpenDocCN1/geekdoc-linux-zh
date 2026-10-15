
```
./current/ch8.doc
./current/ch9.doc
./current/ch10.doc
./current/ch11.doc
./current/ch12.doc
./final/
./final/ch1.doc
./final/ch2.doc
./final/ch3.doc
./final/ch4.doc
./final/ch5.doc
./final/ch6.doc
$ ls -l
total 3010
drw------ 2 sarwar faculty      512 Jan 9 00:02 current
drwx------ 2 sarwar faculty      512 Jan 9 00:03 final
-rw-r--r-- 1 sarwar faculty 2064896 Jan 9 13:48 linuxbook.tar
$ file linuxbook.tar
linuxbook.tar: GNU tar archive
```

你也可以使用以下命令行创建当前目录的 tar 存档。`-` 参数告知 `tar` 存档发送到标准输出，然后重定向到 `linuxbook.tar`。正如第 15 章所讨论的，反引号用于命令替换，即执行 `find` 命令并将其输出替换命令。`-print` 命令的输出（当前目录下所有文件和目录的名称）作为参数传递给 `tar` 命令。这些文件和目录名称被视为 `tar` 命令归档的文件列表。因此，该行的行的效果是在 `linuxbook.tar` 中创建当前目录的 tar 存档。

```
$ tar cvf `find . -print` > linuxbook.tar
tar: ./linuxbook.tar same as archive; not dumped
```

```
./current/
./current/ch1.doc
...
$
```

在接下来的课内练习中，你将使用带有 `c` 选项的 `tar` 命令创建一个目录的存档。

| 课内练习 |
| :--- |
| 19.1. 在你的主目录下为 `labs` 目录层次结构创建一个 tar 存档。使用了哪些命令行？你的存档文件名是什么？ |

## 19.2.2 恢复归档文件

你可以使用 `tar` 命令的 `x` 选项恢复（解包）存档。要恢复第 19.2.1 节创建的存档并将其放在名为 `~/backups` 的目录中，你可以运行以下命令序列。`cp` 命令将存档文件（假设在你的主目录下）复制到恢复归档文件的目录 (`~/backups`) 中。`cd` 命令用于将目标目录更改为当前。最后，使用 `tar` 命令执行恢复。

```
$ cp linuxbook.tar ~/backups
$ cd ~/backups
$ tar xvf linuxbook.tar
./.lastlogin
./current/
./current/ch7.doc
./current/ch8.doc
./current/ch9.doc
./current/ch10.doc
./current/ch11.doc
./current/ch12.doc
```

```
./final/
./final/ch1.doc
./final/ch2.doc
./final/ch3.doc
./final/ch4.doc
./final/ch5.doc
./final/ch6.doc
```

```
$ ls -l
total 3010
drw------ 2 sarwar faculty      512 Jan 9 00:02 current
drw------ 2 sarwar faculty      512 Jan 9 00:03 final
-rw-r--r-- 1 sarwar faculty 2064896 Jan 9 12:38 linux.tar
```

注意 `linux.tar` 文件在解包后仍然保持完好。考虑到结果是合理的，因为考虑到 tar 存档的主要目的是备份文件，如果系统在恢复后但在再次归档之前发生崩溃，它在恢复后也应该保持完好。

## 618 第19章 文件系统备份

```
-rw----- sarwar/faculty 121344 1999-08-23 19:11:22 ./current/ch10.doc
```

| 文件类型和权限 | 登录名/组名 | 文件大小 | 修改日期和时间 | 文件名 |
|---|---|---|---|---|
| | | | | |

![](img/d16a56b1b2a540facbf3aae233584428_639_0.png)

**图 19.3** 在 ~/backups 中恢复 linuxbook.tar

```
$ tar tvf unixbox.tar 0 2001-01-09 00:14:56 //
drwx------ sarwar/faculty 0 1999-08-23 19:42:22 //lastlogin
drwx------ sarwar/faculty 0 2001-01-09 00:02:12 ./current/
dr-xr--x sarwar/faculty 204288 1999-08-23 19:11:22 ./current/ch7.doc
dr-xr--x sarwar/faculty 87552 1999-08-23 16:49:31 ./current/ch8.doc
dr-xr--x sarwar/faculty 86016 1999-08-23 17:11:42 ./current/ch9.doc
drwx------ sarwar/faculty 121344 1999-08-23 19:11:22 ./current/ch10.doc
dr-xr--x sarwar/faculty 152576 1999-08-23 16:49:31 ./current/ch11.doc
dr-xr--x sarwar/faculty 347648 1999-08-23 17:11:42 ./current/ch12.doc
drwx------ sarwar/faculty 0 2001-01-09 00:03:13 ./final/
dr-xr--x sarwar/faculty 41984 1999-08-23 19:01:04 ./final/ch1.doc
dr-xr--x sarwar/faculty 54272 1999-08-23 15:54:57 ./final/ch2.doc
dr-xr--x sarwar/faculty 142848 1999-08-23 15:11:26 ./final/ch3.doc
-rw------ sarwar/faculty 86528 1999-08-23 19:45:32 ./final/ch4.doc
dr-xr--x sarwar/faculty 396288 1999-08-23 09:24:01 ./final/ch5.doc
```

## 619 通过 tar 归档和恢复文件

-rwxrwx---- sarwar/faculty 334848 1999-08-23 09:24:15 ./final/ch6.doc $

如果你想在 `~/linuxbook/current` 目录中恢复文件 `ch10.doc`，可以使用以下恢复命令序列。请务必提供要恢复文件的**路径**，而不仅仅是**文件名**。

```
$ cd ~/linuxbook
$ tar -xvf ~/backups/linuxbook.tar ./current/ch10.doc
./current/ch10.doc
```

该 `tar` 命令的输出显示 `ch10.doc` 已恢复到 `~/backups/current` 目录。你可以通过 `ls -l ~/backups/current` 命令确认此结果。

以下命令可以执行将当前目录下的整个层次复制到 `~/linuxbook/backups` 目录的任务。管道左边的 `tar` 命令创建归档，并将其作为输入传递给右边的 `tar` 命令。记住括号内的命令是在子 shell 中执行的。

```
$ tar -cf - . | ( cd ~/linuxbook/backups; tar -xvf - )
/
./ch1.doc
./ch2.doc
./ch3.doc
./ch4.doc
./ch5.doc
./ch6.doc
./ch7.doc
./ch8.doc
./ch9.doc
./ch10.doc
./ch11.doc
./ch12.doc
./ch13.doc
```

## 620 第19章 文件系统备份

```
./ch11.doc
./ch14.doc
./ch15.doc
./ch16.doc
./ch17.doc
./ch18.doc
./ch19.doc
./ch20.doc
./ch21.doc
$
```

在接下来的练习中，你将使用 `tar` 命令的 `t` 和 `x` 选项来查看归档文件的属性以及如何恢复归档文件![](img/d16a56b1b2a540facbf3aae233584428_641_0.png)。

- 19.2. 列出你在练习 19.1 中创建的归档文件的属性，并识别其中所有文件的大小。你使用了什么命令？

- 19.3. 将你在练习 19.1 中创建的归档复制家目录下名为 `backup` 的目录。显示你执行此任务使用的命令。

### 19.2 复制目录层次

你可以使用 `tar` 将一个目录复制到另一个目录。你也可以使用 `cp -r` 命令，但使用该命令的缺点是文件权限和修改时间无法保留。复制的文件和目录的权限由掩码决定，且修改时间被设置为当前时间。此外，并不是所有的 Linux 系统都提供 `r` 选项。

更常见的方法是用 `tar` 命令归档源目录、创建目标目录并在后者中解压（untar）归档目录。通过分组和管道，可以使用一个命令完成整个任务。在下面的会话中，`~/linuxbook/examples` 目录被复制到 `~/linuxbook/backup` 目录。管道左边的 `tar` 命令将归档发送到 stdout，右边的 `tar` 命令在 stdin 上解压归档。使用 `ls` 命令用于确认命令的语义。（注意：在 `cd` 后不要按回车，由于行长度和 examples.backup 文件的路径长度，会自动换行。）

## 621 通过 tar 归档和恢复文件

```
$ cd ~/linuxbook/examples; tar -cvf - . | ( cd ~/linuxbook/backup; tar -xvf - )
./lastlogin
./shell/
./shell/demo
...
./shell/copy
./shell/fileinfo
./shell/diff
./shell/testdriver
./shell/time
$ ls -l examples backup
```

examples:

total 3

drwx------ 3 sarwar/faculty 1536 Dec 10 11:39

drwx------ 3 sarwar/faculty 1024 Aug 21 19:59

backup:

total 3

drwx------ 3 sarwar/faculty 1536 Dec 10 11:39

drwx------ 3 sarwar/faculty 1024 Aug 21 19:59

使用此命令行的优点是，所有 Linux 系统都提供了 `cd` 和 `tar` 命令，并且复制的文件具有源文件的访问权限和修改时间。

你也可以使用 `tar` 命令将目录复制到网络上的远程机器。在下面的命令行中，`~/linuxbook/examples` 目录被复制到名为 `upsun` 的远程机器上的 `~/linuxbook/backup` 目录。使用 `rsh` 命令（见第 14 章）在 `upsun` 上执行引号中的命令。由于 `tar` 命令没有以详细模式运行，它是静默运行的，你不会在屏幕上看到任何输出。

```
$ cd ~/linuxbook/examples; tar cf - | rsh upsun "cd ~/linuxbook/backup; tar xf -"
```

## 19.3 TAR 格式的软件发行

公司经常使用 `tar` 命令分发软件，因为形成了一个客户需要复制的单个文件，并且与包含分发软件的未归档目录层次相比，节省了磁盘空间。此外，大多数公司将其分发包（tar 格式）放在其互联网站点上，客户可以通过 `ftp` 命令下载。因此，tar 格式还缩短了复制时间并减少了客户的工作量，客户仅需一个 `gunzip` 命令（或 `wget`），而不需要在必须下载目录层次时使用多个系列命令。

由于图形界面和多媒体格式，软件包的大小日益增大，它们在放在 FTP 站点之前会进行压缩。软件用户在恢复之前需要解压缩下载的文件。

让我们考虑一个从 FTP 站点下载的一个文件 `tcsh-0.06.tar.Z`。为了恢复这个文件，我们需要对其进行解压缩和解包，如下所示：

```
$ uncompress tcsh-0.06.tar.Z
$ tar xvf tcsh-0.06.tar
[命令输出]
```

`~/linuxbook/backups/lb.tar.gz` 文件中的当前目录，第二个命令则从该文件将压缩包归还原到当前目录。

```bash
$ tar -zcf ~/linuxbook/backups/lb.tar.gz
$ tar -zxvf ~/linuxbook/backups/lb.tar.gz
$
```

## 总结

LINUX 具有多种工具（也称为低级备份程序），用于创建文件和目录的存档（备份）副本，包括 `afio`、`cpio`、`dump` 和 `tar`。还有几种 shell 脚本，通常称为高级备份程序，包括 `amanda`、`backup`、`KBackup`、`tbackup`、`lub` 和 `bot`，这些程序允许你执行全量或增量备份。`tar` 命令是最常用的。备份可以磁带或磁盘文件的形式存在。对于磁带备份，用户不仅需要对磁带设备文件具有访问权限，还需要挂载该文件。磁盘备份通常用于软件分发，也可以用于打包大型不活动文件以节省磁盘空间。在 LINUX 网络中，用户可以使用使用 `tar` 和 `rsh` 命令的命令组在远程机器上创建其文件和目录的存档。

## 问题

- 1. 存档（archive）一词的意思是什么？

- 2. `tar` 命令是做什么的？列出它的所有用途。

- 3. 系统中磁带驱动器的设备文件名称是什么？这些文件的访问权限是什么？

- 4. 给出一个创建当前目录的 tar 存档的命令。给出一个压缩存档并将存档保留在主目录的备份目录中的命令。

- 5. 给出一个在 `~/backups` 目录下恢复问题 4 中备份文件的命令。

- 6. 给出一个将你的家目录复制到名为 `home.back` 的目录的命令，并保留访问权限和文件修改时间。

- 7. 为什么在创建目录层次结构的备份副本时，`tar` 命令优于 `cp -r` 命令？

- 8. 假设你从 FTP 站点下载了一个文件 `linuxbook.tar.gz`。正如名称所示，这是一个压缩格式的 tar 存档。给出还原该存档并将其安装到你的 `~/linuxbook` 目录的命令序列。

- 9. 使用单行命令行完成问题 8 中概述的任务。

# 第 20 章

软件开发的 LINUX 工具

# 学习目标

* 总结不同层次的计算机编程语言

* 讨论解释型语言和编译型语言以及编译过程

* 简述软件工程生命周期

* 讨论用于 C 的 LINUX 程序生成工具，以执行以下任务：编辑、缩进、编译、处理模块化软件、创建库、源码管理和版本控制

* 描述用于 C 程序的静态分析 LINUX 工具：验证代码的可移植性和进行剖分析

* 讨论用于 C 程序的动态分析 LINUX 工具：调试、跟踪和性能监控

* 涵盖命令和原语：`admin`, `ar`, `gcc`, `ci`, `co`, `cvs`, `delta`, `emacs`, `gdb`, `get`, `grep`, `help`, `ident`, `indent`, `make`, `rcsmerge`, `nm`, `rcs`, `ranlib`, `rlog`, `strip`, `time`

## 20.1 引言

典型的 LINUX 系统支持多种高级编程语言，包括解释型和编译型。这些语言包括 C、C++、Pascal、Java、LISP 和 FORTRAN。然而，LINUX 平台的大多数应用软件都是用 C 语言开发的，而 LINUX 操作系统也是用 C 语言编写的。这一系列软件工程工具可用于用这种语言开发软件。许多此类工具也可以用于其他编程语言（特别是 C++）的开发。

LINUX 操作系统拥有丰富的软件工程工具，用于程序生成以及程序的静态和动态分析。它们包括编辑源码、缩进源码、编译和链接、处理模块化软件、创建库、C 程序的静态分析工具（验证代码的可移植性和剖分析）、C 程序的动态分析工具（调试、跟踪和性能监控）。涵盖的命令和原语 `admin`, `ar`, `gcc`, `ci`, `co`, `cvs`, `delta`, `emacs`, `gdb`, `get`, `grep`, `help`, `ident`, `indent`, `make`, `rcsmerge`, `nm`, `rcs`, `ranlib`, `rlog`, `strip`, `time`。

一个典型的 LINUX 系统支持多种高级语言，包括解释型和编译型。这些语言包括 C、C++、Pascal、Java、LISP 和 FORTRAN。然而，LINUX 平台的大多数应用软件都是用 C 语言开发的，而 LINUX 操作系统也是用 C 语言编写的。这一系列软件工程工具可用于用这种语言开发软件。许多此类工具也可以用于其他编程语言（特别是 C++）的开发。

LINUX 操作系统拥有丰富的软件工程工具，用于程序生成以及程序的静态和动态分析。它们包括编辑源码、缩进源码、编译和链接、处理模块化软件、创建库、C 程序的静态分析工具（验证代码的可移植性和剖分析）、C 程序的动态分析工具（调试、跟踪和性能监控）。涵盖的命令和原语 `admin`, `ar`, `gcc`, `ci`, `co`, `cvs`, `delta`, `emacs`, `gdb`, `get`, `grep`, `help`, `ident`, `indent`, `make`, `rcsmerge`, `nm`, `rcs`, `ranlib`, `rlog`, `strip`, `time`。
