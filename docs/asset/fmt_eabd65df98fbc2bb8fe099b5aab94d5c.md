
- `sbin/`。该目录包含对系统运行并非至关重要，但如果没有它们，系统功能将受到极大削弱的二进制文件。例如，该目录中可用的某些二进制文件包括`crond`、`l1pd`、`edquota`、`makewhatis`和`traceroute`。

- `bin/`。大多数应用程序的二进制文件都存存在此目录中。

- `etc/`。该目录包含应用程序的配置文件。

- `tmp/`。该目录是应用程序的临时存储空间。

此外，`/usr`还包含了一些没有系统级对应项的目录。其中一些目录列在此处：

- `X11`或`X1R6/`。该目录代表`X`窗口应用程序层次结构。

- `dict/`。该目录包含一个字典。

- `doc/`。该目录包含`/usr/bin`中应用程序的文档。

- `games/`。该目录包含游戏程序。

- `include/`。该目录包含用于软件开发的文件。

- `info/`。该目录供`info`命令使用。对于某些应用程序，可以使用`info`命令代替`man`命令。

## 第 3 章 LINUX 发行版与安装

- `man/`。该目录包含帮助手册页（`man` pages）。

- `src/`。该目录包含应用程序的源代码。Linux 内核存储在此。

`/usr/share`目录包含可以在各种应用程序之间共享的数据。`/usr`目录可以包含各种实用，如`awk`、`emacs`、`gettext`、`lyx`和`vim`。此外，该目录还可以包含此处列出的子目录：

- `afterstep/`
- `automake/`
- `games/`
- `icons/`
- `magic`
- `termino/`
- `zoneinfo`

然而，某些信息和应用程序针对特定的计算机网络。例如，你需要不同的应用程序来运行办公版和家庭版局域网。`/usr/local`目录为这些信息提供了存储。`/usr/local`目录通常是一个完整的文件系统。因此，`/usr/local`目录可能会包含`bin`、`etc`、`games`、`include`、`info`、`lib`、`man`、`sbin`和`src`目录。有时，共享和专有的配置文件位于`/usr/local/share`目录。人们还会将Web服务器等应用程序存储在`www`下，将数据库存储在`mysql`下。

## 总结

在本章中，你学习了各种Linux发行版，如`Red Hat`、`MandraSoft`、`Debian`、`Core`和`SuSE`。接下来，你学习了Linux的不同安装方法。你可以通过光盘、`NFS`、硬盘驱动器和`FTP`安装Linux。你还可以使用`Kickstart`特性来自动化安装过程。使用`Kickstart`，你可以自动化语言、键盘、时区、软件包和鼠标选择等任务。

## 检验你的理解程度

第 3 章

接下来，你查看了Linux中的文件系统和驱动器分区。你学习了`fdisk`和`cfdisk`工具，它们用于管理系统中的分区。我详细讨论了两种流行的启动加载程序：`LILO`和`GRUB`。`LILO`是Linux最常用的启动加载程序。`LILO`可以引导内核。它将内核相关信息存储在纯文本文件中。你可以使用`LILO`启动`MS DOS`、`Linux`、`FreeBSD`等。`GRUB`是一种可以通过链式加载加载各种自由操作系统和专有操作系统的启动加载程序。`GRUB`的设计旨在解决启动个人计算机的复杂性问题。

最后，你探索了Linux文件系统。`/`是文件系统的根目录。根目录包含几个标准目录。我们对这些标准目录以及每个目录的内容进行了详细的考虑。

## 检验你的理解程度

### 单选题

1. `Red Hat`安装程序使用________文件来确定`/RedHat/RPMS`目录中每个待安装软件包类别的可用程序包。

   - a. `/RedHat/comps`
   - b. `/RedHat/comp`
   - c. `/RedHat/base/comps`
   - d. `/RedHat/base/comp`

2. ________和________软件包组Linux操作系统基础系统的一部分。

   - a. `libc`
   - b. `termcap`
   - c. `lib`
   - d. `termpack`

3. 选择配置文件的三个主要部分。

   - a. 系统信息 (`System info`)
   - b. `RedHat`软件包
   - c. 安装后`shell`命令
   - d. 安装前`shell`命令

4. 可安装软件包列表可以在________文件中找到。

   - a. `/RedHat/base/comps`
   - b. `/RedHat/comps`
   - c. `/RedHat/base/packages`
   - d. `/RedHat/packages`

5. 在`Kickstart`安装期间，使用哪个按键组合查看系统日志控制台？

   - a. `Alt+F1`
   - b. `Alt+F2`
   - c. `Alt+F3`
   - d. `Alt+F4`

6. 哪个目录包含帮助手册页？

   - a. `/etc`
   - b. `/dev`
   - c. `/bin`
   - d. `/usr`

7. 哪个目录包含帮助手册页？

   - a. `/etc`
   - b. `/dev`
   - c. `/bin`
   - d. `/usr`

## 答案

### 单选题答案

1. `/RedHat/base/comps`
2. `libc`, `termcap`
3. 系统信息、`RedHat`软件包、安装后`shell`命令
4. `/RedHat/comps`
5. `Alt+F3`
6. `/usr`
7. `/bin`

## 一般管理

### 第 4 章

## 查找信息

有时，你需要搜索特定的文件——例如在某日期后修改的文件——以生成统计表示等。Linux提供的搜索命令可以有效地从系统中提取此类信息。管理员为此目的使用的某些命令有`grep`、`find`、`locate`、`finger`、`which`、`whereis`和`updated`。

## find

`find`命令在目录及其子目录下搜索文件。`find`命令通过评估表达式搜索目录树。

`find`的语法如下：

```
find [path] [expression]
```

`[path]`参数指定搜索匹配`[expression]`文件的目录。如果没有指定路径，则使用当前目录搜索文件。同样，如果没有给出表达式，则使用表达式`-print`，它会将输出打印到屏幕上。如果搜索成功，`find`命令返回状态`0`。如果发生错误，则返回大于`0`的值。例如，要在当前目录搜索所有`.txt`扩展的文件，执行以下命令：

```
find *.txt
```

同样，要查找根目录下在过去三天内访问过的所有文件，执行以下命令：

```
find -atime 3
```

你可以使用`find`命令搜索可能因未经授权的用户活动或某些病毒活动产生的文件。在入侵检测的情况下，此命令也可用于检测特定期间内修改的文件。

# 第 4 章 LINUX 系统管理

`grep`命令的输入可以以后文件名、另一个命令的输出或直接作为参数的形式提供。`grep`命令接受多个参数来对输入数据进行搜索。`grep`命令的语法所示：

```
grep [options] [search_text] [filenames]
```

这里列出了`grep`命令的一些重要参数：

- `-n`. 此参数返回包含搜索短语的行以及行号。
- `-v`. 此参数返回不包含搜索短语或单词的输出。
- `^<word>`. 此参数返回所有以`<word>`开头的行。
- `<word>$`. 此参数返回所有以`<word>`结尾的行。

## slocate

`slocate` (安全位置定位) 命令是`GNU Locate`命令的安全增强版本。`Secure locate`提供了一种安全的方法，用于索引和快速搜索计算机上的文件。它使用增量编码来压缩数据库以加快搜索速度。该命令还存储了文件的权限和所有权详情，以便用户无法查看其没有权限访问的文件。`slocate`命令的语法如下：

```
slocate [options] [path] [search_string]
```

## finger

`finger`命令显示有关用户的信息。以下列表告诉您`finger`命令的选项及其显示的用户信息。

## 通用管理

### 第 4 章

- `-s`. 此选项显示用户的登录名、真实姓名、终端名称、写入状态、空闲时间、登录时间、办公室位置和办公电话。登录时间以月、日、小时和分钟的形式显示。未知设备以及不存在的空闲和登录时间将以单个星号显示。
- `-l`. 此选项显示多行格式的输出，列出`-s`选项描述的所有信息。该选项还显示用户主目录的详情、电话号码、登录`shell`、邮件状态以及用户目录下的`.plan`、`.project`和`.forward`文件的内容。

假设你创建了一个名为`John`的用户，并想查看他的信息。要做到这一点，你可以执行以下命令：

```
-ls john
```

上一个命令的输出看起来所示：

```
Login: john             Name: (null)
Directory: /home/john  Shell: /bin/bash
Never logged in.
No mail.
No Plan.
```

当未授权的用户使用`finger`命令时，可能会泄露用户信息。因此，应该限制其使用。
