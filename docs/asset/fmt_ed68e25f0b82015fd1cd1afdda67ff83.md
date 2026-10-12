
```bash
$expect
autoexpect started, file is script.exp
$ ftp ftp.us.kernel.org
Connected to ftp.us.kernel.org.
220
Name (ftp.us.kernel:michael): anonymous
331 Anonymous login ok, send your complete e-mail address as password.
Password:
230 Anonymous access granted, restrictions apply.
Remote system type is UNIX.
Using binary mode to transfer files.
$ ftp > cd /pub/linux/kernel/v2.2
250 CWD command successful.
$ ftp ls
200 PORT command successful.
150 Opening ASCII data connection for file list.
-r--r--r-- 1 merlin merlin 0 Aug 26 00:45 LATEST-IS-2.2.112
-r--r--r-- 1 merlin merlin 27 Jan 26 1999 README
-r--r--r-- 1 merlin merlin 10529549 Jan 26 1999 linux-2.2.0.tar.bz2
-r--r--r-- 1 merlin merlin 344 Jan 26 1999 linux-2.2.0.tar.bz2.sign
-r--r--r-- 1 merlin merlin 13080195 Jan 26 1999 linux-2.2.0.tar.gz
-r--r--r-- 1 merlin merlin 32992 May 13 23:54 patch-2.2.9.gz
-r--r--r-- 1 merlin merlin 344 May 13 23:54 patch-2.2.9.gz.sign
226 Transfer complete.
$ exit
221 Goodbye.
$exit
exit
```

# 第一部分：控制程序 第 2 章

`autoexpect` done, file is `script.exp`

$

此示例创建了一个使用 `ftp` 查找新内核版本的脚本。输出为了节省空间已过编辑。

### autoexpect 记录每一次按键

在 `autoexpect` 运行期间，它会记录你输入的每一个按键。这包括退格键、删除键和方向键。

它还要求告诉它预期的信息必须与接收到的信息完全一致。例如，如果你设置了一个 `expect` 脚本来登录 FTP 服务器，而服务器在每次登录时都会显示不同的当天消息或时间日期戳，那么 `autoexpect` 将无法工作。它依赖于每次运行时都产生相同的输出。

### 控制程序

大多数（但并非所有）Shell 都支持对后台进程进行某种形式的控制。重要功能包括：

- 列出当前后台程序
- 暂停正在运行的程序
- 停止运行的进程
- 将发送到后台的程序调回前景

控制后台程序被称为作业控制（job control）。

### 使用作业控制

使用作业控制来管理多个运行中的程序。你可以从 Shell 命令行通过 `&` 运算符在后台启动程序，也可以通过按下 `Ctrl+z` 挂起程序。Shell 将通过打印一个作业号、后跟一个进程号来响应。

```bash
$ sc &
[1] 2689
```

通过 `Ctrl+z` 发送到后台的运行程序将会消失，Shell 会打印作业号：

```bash
[2]+ Stopped sc
```

# 第一部分 Linux 基础

## 第 2 章 命令

许多程序实例可以启动、挂起或运行。要获取运行中的程序列表，使用 Shell 的 `jobs` 命令：

```bash
$ jobs
[2]+ Stopped sc
[3]- Stopped (tty)) report.txt
```

`jobs` 命令会打印每个程序的作业号以及启动该程序的命令行。要选择性地恢复一个程序，使用 `fg`（前台）命令后接作业号：

```bash
$ fg 3
```

此示例会将文本编辑器返回到显示器。如果你想让挂起的程序在后台恢复，请使用 `bg` 而不是 `fg`：

```bash
$ bg 4
[4]+ xcalcc &
$
```

注意 Shell 会自动添加 `&`，就像你最初输入的一样。

# 使用 ps 和 kill 命令

所有系统进程都由内核分配一个唯一的进程号。要查看运行程序的进程号，使用 `ps`（进程状态）命令。（为了节省空间，这里没有列出编写时运行的所有进程。）此列表显示 `su` 命令以进程号 1658 运行：

```bash
$ ps
...
1658 p0 S 0:00 su
1659 p0 S 0:00 bash
2713 p0 T 0:00 pico report.txt
2714 p0 T 0:00 pico newreport.txt
```

你可以通过 `kill` 命令指定进程号来停止程序：

```bash
$ kill -9 2714
[4]+ Killed pico newreport.txt
```

# 第一部分

# 使用通配符 第 2 章

# 另

- 要了解更多关于控制进程和其他后台程序的信息，请参阅第 538 页。

通过进程号杀死进程来停止后台程序通常是不方便的方法。使用 `kill` 命令，后接 `%` 号以及作业号或命令名称来停止程序，如下：

```bash
$ kill %3
```

```bash
[3]+ Terminated pico report.txt
```

```bash
$ kill %pico
```

```bash
[3]+ Terminated pico report.txt
```

### 使用通配符

通配符用于匹配文件名中的模式。

### 构建表达式

正则表达式用于在文本中搜索复杂的模式。

# 第一部分 Linux 基础

## 第2章 输入命令

要查看系统可接受的 shell 列表，请使用 `chsh -l` (list) 选项：

```
### chsh -l
/bin/bash
/bin/bsh
/bin/sh
/bin/ash
/bin/bsh
/bin/tcsh
/bin/csh
/bin/ksh
/bin/zsh
/usr/bin/pine
```

## 第3章 导航 Linux 文件系统

- 输出当前工作目录
- 使用 `cd` 命令切换目录
- 列出目录
- 查看文本文件
- 创建文件和目录
- 复制文件和目录
- 移动和重命名文件及目录
- 创建符号链接
- 删除文件和目录
- 查找文件和目录
- 使用 GNOME GMC 客户端
- 使用 KDE 文件管理器 kfm
- 搜索文本文件

# 第一部分 Linux 基础

## 第3章 导航 Linux 文件系统

在操作 Linux 时，你应该知道自己在哪里或正要去哪里。本节将展示如何在控制台或终端窗口、GNOME 桌面以及 X KDE 桌面环境 (KDE) 中导航目录。

### 输出当前工作目录

使用 `pwd` (print working directory) 命令可以打印当前、正在运行的目录（即你此时所处的目录）：

```
$ pwd
/home/michael
```

`pwd` 命令的二进制版本可以在 `/bin` 目录下找到，几乎所有的 shell 都内置了 `pwd` 命令。

内置的 `pwd` 命令在每个 shell 的帮助页（manual pages）中均有文档说明；或者从命令行使用。可以使用 `type pwd` 或 `help pwd`。

### 使用 `cd` 命令切换目录

使用 `cd` (change directory) 命令在 Linux 文件系统的目录间导航。通过目录规范或路径名使用此命令移动到指定目录。此命令在每个 Linux shell 中都是内置的，也可以作为快速返回主目录的快捷方式。

```
$pwd
/home/michael
$ cd /usr/bin
$pwd
/usr/bin
$ cd
/home/michael
```

如果你直接输入 `cd`，将返回你的主目录（由 `$HOME` 环境变量指定）。通过输入两个点和一个正斜杠 (..) 并配合 `cd` 命令可以移动到上一级目录，如下：

```
$pwd
/home/michael
$ cd ..
/home
```

### 使用 `ls` 命令列出目录和文件

使用 `ls` (list) 命令列出一个或多个目录的内容。

该命令有超过40 种不同的命令行选项，可以组合使用进行格式化列表。可以使用通配符（Wildcards）来指定特定的文件或目录。

要列出 `/usr/local/` 目录的内容，请输入：
