
# Linux 入门指南

序言：Daniel Jebaraj

![](img/42ed1d6a90f762b0fa883c992aa553d5_1_0.png)

# 《简明系列》丛书背后的故事

Daniel Jebaraj，副总裁

Syncfusion 公司

站在最前沿

正如你们中的许多人所知，Syncfusion 是微软平台软件组件的供应商。这使我们处于一个既兴奋又充满挑战的地位：始终处于最前沿。

每当微软发布平台或工具时（如今似乎几乎每隔周就有一次），我们都必须快速地自我学习。

## 信息丰富，但难以消化

在现实中，这意味着产生了大量的书籍订单、博客搜索和 Twitter 扫描。

虽然互联网上的可用信息越来越多，出版的书籍也越来越多（即使是在相对较新的主题上），但一个持续制约我们的方面是：无法找到简洁的技术概述。

我们通常面临两个选择：阅读几本超过 500 页的书，或者在网络上搜索相关的博客文章和其他文章。就像每一个有工作要做、有客户要服务一样，我们觉得这非常沮丧。

## 《简明系列》(Succinctly series)

这种挫败感转化为一种深切的渴望，创作出一系列针对在微软平台上工作的开发者的简明技术书籍。

我们坚信，考虑到这些开发者所拥有的背景知识，大多数主题都可以被转化成 50 到 100 页之间的书籍。

这正是我们决定通过《简明系列》要实现的。难道不是一切美好的事物都源于对改变事物变得更好的深切渴望吗？

## 最好的作者，最好的内容

每位作者都是从一个才华横溢的专家库中精心挑选的，他们与我们有着共同愿景。你现在手中的这本书以及该系列中的其他书籍，都是作者们不懈努力的成果。你将发现原创内容，这些内容保证让你在喝几杯咖啡的时间内就能上手并运行。

## 永久免费

Syncfusion 将致力于制作多个主题的书籍。这些书籍将始终是免费的。

我们发布的任何更新也将是免费的。

## 免费？猫腻在哪里？

这里没有猫腻。Syncfusion 在这项工作中有着切利益。

作为组件供应商，我们独特的主张一直是：我们提供的框架比市场上任何其他供应商都更深、更广。开发者教育极大地帮助我们市场化并击败那些承诺“一键开启 AJAX 支持”或“把月亮变成奶酪！”的竞争对手。

## 让我们知道你的想法

如果你有任何感兴趣的主题、想法或反馈，请随时通过 `succinctly-series@syncfusion.com` 发送给我们。

我们诚挚地希望你喜欢这本书，希望它能帮助你更好地理解所学的课题。感谢阅读。

请在 Twitter 上关注我们，并在 Facebook 上“点赞”我们，帮助我们传播《简明系列》的消息！

## 关于作者

Jason Cannon 于 1999 年开始他的 Unix 和 Linux 系统工程师的职业。从那时起，他在 Xerox、UPS、惠普（HP）和亚马逊等公司利用了他的 Linux 技能。此外，他还担任过小型企业以及财富 500 强公司的技术顾问和独立承包商。

Jason 拥有 CentOS、RedHat Enterprise Linux、SUSE Linux Enterprise Server 和 Ubuntu 的专业经验。他在个人项目中使用过多个 Linux 发行版，包括 Debian、Slackware、CrunchBang 等。除了 Linux，Jason 还有支持专有 Unix 操作系统的经验，包括 AIX、HP-UX 和 Solaris。

他喜欢教他人如何使用和利用 Linux 操作系统的力量。Jason 是《命令行功夫：Bash 脚本技巧》、《Linux Shell 编程技巧》、《Bash 单行命令》以及《Linux 初学者：Linux 操作系统与命令行》的作者。他还是 `http://LinuxTrainingAcademy.com` 的创始人，他在那里写博客并教授在线视频培训课程。

# 第 1 章 引言

## 什么是 Linux?

Linux 是一种类 Unix 的开源操作系统。操作系统的核心是 Linux 内核。它充当了中介角色。

## Linux 发行版

Linux 发行版是 Linux 内核以及相关工具、应用程序的软件包。由于 Linux 内核由不同的组织或个人维护和分发，因此产生了许多不同的 Linux 发行版。这些 Linux 发行版被称为“发行版”。许多 Linux 发行版包含图形用户界面，而有些则只提供命令行界面。Linux 发行版包含的软件包也会根据发行版而有所不同。以下是一些常见的 Linux 发行版：

- Debian
- Slackware
- CrunchBang
- Ubuntu
- Fedora
- openSUSE
- Arch
- CentOS
- Red Hat Linux

# 第 2 章 Linux 目录结构

Linux 文件系统的结构从根目录开始，它像一个树形结构。根目录用符号 `/` 表示。

## 常见的根级目录

在 Linux 中，所有的目录都位于根目录 `/` 下。根目录下有许多子目录，每个目录都有特定的用途。

## `/bin` 二进制文件

`/bin` 目录包含了系统必需的可执行二进制文件。这些程序在单用户或多用户模式下都可以使用。例如，`ls`、`cp`、`mv` 等命令。

## `/lib` 库文件

`/lib` 目录包含了程序所需的共享库文件。这些库文件是 `/bin` 中程序所需要的。

## `/etc` 配置文件

`/etc` 目录包含了系统配置文件。这些文件控制操作系统的如何运行。

## `/home` 用户目录

每个普通用户在 `/home` 下都有自己的子目录。这是用户存储个人文件的地方。例如，`/home/user`。

## `/root` 超级用户目录

`/root` 目录是超级用户（root）的家目录。出于安全考虑，root 的家目录并不放在 `/home` 之下。

## `/dev` 设备文件

`/dev` 目录包含了设备文件。在 Linux 中，硬件设备被视为文件。

## `/mnt` 挂载点

`/mnt` 目录用于临时挂载其他文件系统。

## `/media` 介质

`/media` 目录用于自动挂载插入式介质，如 USB 驱动器或 CD。

## `/var` 可变数据

`/var` 目录包含了经常发生变化的文件，例如日志文件、邮件队列等。

## `/opt` 可选附加软件

`/opt` 目录用于安装可选的第三方软件包。

## `/tmp` 临时文件

`/tmp` 目录用于存放临时文件。这些文件通常在系统重启时被清除。

## `/usr` 用户数据

`/usr` 目录包含了只读的用户数据和程序。它是 Linux 系统中最大的目录之一。

## `/usr/bin` 二进制文件

`/usr/bin` 目录包含了大多数用户程序的二进制文件。它与 `/bin` 类似，但包含更多程序。

## `/usr/lib` 库文件

`/usr/lib` 目录包含了 `/usr/bin` 中程序所需的共享库。

这些顶级目录的通用用途。此列表中包含了一些子目录，以帮助清晰地定义顶级目录的用途。

- `/` Linux 文件系统层次结构的起点，称为根目录。
- `/bin` 二进制文件和其他可执行程序。
- `/boot` 启动操作系统所需的文件。
- `/cdrom` 连接或挂载 CD-ROM（光驱驱器）的地方。
- `/cgroup` 控制组（control groups）层次结构。
- `/dev` 设备文件，通常由操作系统和系统管理员控制。
- `/etc` 系统配置文件。
- `/home` 用户家目录。
- `/lib` 系统库。
- `/lib64` 系统库，64位。
- `/lost+found` 文件系统在执行文件系统检查后用于存储恢复的文件的文件。
- `/media` 用于挂载可移动介质（如 USB 优盘）。
- `/mnt` 用于挂载外部文件系统。
- `/opt` 可选或第三方的虚拟软件。
- `/proc` 进程信息虚拟文件系统。
- `/root` root（超级用户）账户的家目录。
- `/sbin` 系统管理二进制文件。
- `/selinux` 用于显示 SELinux 信息的虚拟文件系统。
- `/srv` 包含系统提供的数据。
- `/srv/www` Web 服务器文件。
- `/srv/ftp` FTP 文件。
- `/sys` 用于显示并有时配置 Linux 内核知的设备和总线的虚拟文件系统。
- `/tmp` 临时空间，通常在重启时清空。
- `/usr` 用户相关的程序、库和文档。
- `/usr/bin` 二进制文件和其他可执行程序。
- `/usr/lib` 库。
- `/usr/local` 本地安装的不属于基础操作系统的软件。
- `/usr/sbin` 系统管理二进制文件。
- `/var` 可变数据，特别是日志文件。
- `/var/log` 日志文件。

如果你遇到了此处未列出的其他顶级目录，它们很可能是系统管理员创建的。

## 应用程序目录结构

应用程序的目录结构可以模仿操作系统。以下是一个安装在 `/usr/local` 的名为 apache 的应用程序示例目录结构。

- `/usr/local/apache/bin` 应用程序的二进制文件和其他可执行程序。
- `/usr/local/apache/etc` 应用程序的配置文件。
- `/usr/local/apache/lib` 应用程序库。
- `/usr/local/apache/logs` 应用程序日志文件。

如果 apache 安装在 `/opt` 中，它看起来像这样：

- `/opt/apache/bin` 应用程序的二进制文件和其他可执行程序。
- `/opt/apache/etc` 应用程序的配置文件。
- `/opt/apache/lib` 应用程序库。
- `/opt/apache/logs` 应用程序日志文件。

另一种常见的应用程序目录结构模式包括将配置和可变数据移出 `/opt`。不是将所有应用程序组件放置在 `/opt/app-name` 中，而是使用 `/etc/opt/app-name` 用于配置文件，使用 `/var/opt/app-name` 用于日志。继续以 apache 示例，这里是这种方法的演示：

- `/etc/opt/apache` 应用程序的配置文件。
- `/opt/apache/bin` 应用程序的二进制文件和其他可执行程序。
- `/opt/apache/lib` 应用程序库。
- `/var/opt/apache` 应用程序日志文件。

应用程序不仅可以隔离在自己的目录中，还可以与其他不属于标准操作系统的应用程序共享共同目录结构。例如，apache 可以可以直接安装到 `/usr/local`。在这种情况下，二进制文件将位于 `/usr/local/bin`，而配置将位于 `/usr/local/etc`。由于 apache 可能不是本地安装的唯一应用程序，它可以与其他程序共享空间。

## 组织目录结构

目录结构可以基于组织，例如公司、小组或团队。例如，如果你为 Widget 公司工作，你可能会在公司的 Linux 服务器上发现一个名为 `/opt/widget` 或 `/usr/local/widget` 的目录。在某些情况下，此基础目录被视为应用程序目录。它将包含类似 `/etc` 和 `/bin` 的常用子目录。这是一个示例：

- `/opt/widget` Widget 顶级目录。
- `/opt/widget/bin` Widget 公司安装或创建的二进制文件和程序。
- `/opt/widget/etc` Widget 公司安装或创建的程序的配置文件。

在该组织目录结构内可以进行进一步的细分。例如，每个应用程序可以接收自己的子目录，如下：

- `/opt/widget` Widget 顶级目录。
- `/opt/widget/apache` Widget 公司安装的 apache 的顶级目录。
- `/opt/widget/apache/bin` apache 二进制文件。
- `/opt/widget/apache/etc` apache 配置文件。

这些是相同主题的变体，但基于公司内部的团队。

- `/opt/sysadmin` 系统管理员团队的顶级目录。
- `/opt/widget/sysadmin` 系统管理员团队的顶级目录。
- `/usr/local/widget/sysadmin` 系统管理员团队的顶级目录。

# 第 3 章 命令行界面

Shell（壳）是一个接受命令并指示操作系统执行这些命令的程序。例如，当你通过网络连接到 Linux 系统时，会启动 shell 并作为你与系统的接口。在这种特定情况下，shell 是命令行解释器。命令行界面通常简称为 CLI。

当你直接通过外接的键盘和显示器连接到 Linux 系统时，你将看到一个文本界面或图形界面，取决于系统的如何配置。在文本界面的情况下，你的体验与通过网络连接到该系统非常相似。当你登录时，命令行 shell 会启动并向你显示一个提示符。

如果你连接到图形模式的系统，你将与图形界面 (GUI) 交互。为了访问命令行，你需要启动终端模拟器应用程序。常见的终端模拟器包括 `xterm`、`GNOME Terminal`、`Konsole` 和 `Eterm`。你的选择取决于个人喜好和可用性，但它们都提供相同的功能——访问命令行。

以下演示了在命令行下登录 Ubuntu Linux 服务器。

```
Ubuntu 14.04 LTS linuxsvr tty1
linuxsvr login:
Password:
Welcome to Ubuntu 14.04 LTS

jason@linuxsvr:~$
```

行 `jason@linuxsvr:~` 是命令行提示符。默认提示符随发行版和 shell 的不同而不同。有很多 shell，其中最常用且受欢迎的是 `Bash`。所有用户都可以按照喜好自定义他们的 shell 提示符。这里的提示符包含用户名、服务器名称和当前目录。波浪号代表家目录，在示例中是 `/home/jason`。你也可以在波浪号后指定用户名，此时它将展开为用户的家目录。例如，`~john` 会展开到 `/home/john`。对于像 wwwdata 这样的应用程序用户，`~wwwdata` 会展开到 `/var/www`。

以下是提示符的示例。

```
[jason@linuxsvr /tmp]
svr:/home/jason
```

```
12:32:19 linuxsvr ~]$
$
```

提示符并不限于单行。以下是跨多行的提示符示例。

```
linuxsvr://home/jason
$
(jason@linuxsvr)-(09:22am)-
~)

Mon 14/12/15 09:22 EST[pts/3][x86_64]
<jason@linuxsvr:~>
zsh 26 %
```

后续示例中的 shell 提示符将简化为美元符号，除非显示整个提示符提供了额外的清晰度。

## 基础命令

在 Linux 中，命令是大小写敏感的并且通常全小写。注意方括号中的项目是可选的。让我们从两个可以在命令行导航系统的命令开始。它们是 `pwd` 和 `cd`。

`pwd` 命令将工作目录显示在你的屏幕上。命令让你跟踪自己在文件系统层次结构中的位置。

`cd [directory]` `cd` 命令将当前目录更改为指定的目录。执行 `cd` 时没有指定目录，它会将当前目录更改为你的家目录。这就是导航系统的方式。

以下是使用 `pwd` 和 `cd` 命令的示例。记住顺序很重要。

```
$ pwd
/home/jason
$ cd /tmp
$ pwd
/tmp
```

```
Pwd: command not found
$ cd /home
$ pwd
/home
$ cd /var/log
$pwd
/var/log
$ cd
$ pwd
/home/jason
$
```

查看目录内容最常用的方法是使用 `ls` 命令。要查看文件内容，请使用 `cat` 命令。

`ls` `ls` 命令用于列出目录内容。此外，`ls` 还可以显示有关文件和目录的信息，包括权限、大小和类型。

`cat [file]` `cat` 命令用于连接或显示文件。

```
$ pwd
/home/jason
$ ls
Desktop Documents Downloads Music Pictures to-do.txt
$ cat to-do.txt
此文件包含我的待办事项。
* 修剪草坪。
* 统治世界。
$ cd Music
$ ls
JohnColtrane
```

要结束命令行会话，请输入 `exit`、`logout` 或 `Ctrl-d`。

`exit`, `logout`, 或 `Ctrl-d` 退出 shell 或你的当前会话。

```
$ exit
logout
Connection to linuxsvr closed.
```

## 命令行帮助

Linux 操作系统提供了内置文档。要访问这些在线手册（也称为 man 页面），请使用 `man` 命令。man 页面非常适合查找特定命令的可用选项，甚至寻找可以帮助你完成当前任务的命令。

`[command]` `man` 命令显示指定命令的在线手册。

一旦执行了 `man` 命令，你可以使用方向键以及 Page Up（向上翻页）和 Page Down（向下翻页）在 man 页面中导航。你还可以使用回车键向下移动一行，空格键向下移动一页，g 移动到开头，大写 G 移动到 man 页面末尾。输入 q 退出。要学习在查看 man 页面时更多的可用命令，请输入 h 获取帮助。

表 1：导航 man 页面

| 键 | 动作 |
|---|---|
| n| Enter, Down Arrow | 向下移动一行。 |
| | Up Arrow | 向上移动一行。 |
| Spacebar, Page Down | 向下移动一页。 |
| g | 转到开头或顶部。 |
| G | 转到末尾或底部。 |
| q | 退出。 |

```
$ man
What manual page do you want?
$ man ls
LS(1) User Commands LS(1)
NAME
ls - list directory contents
SYNOPSIS
ls [OPTION]... [FILE]...
DESCRIPTION
列出 FILE 的信息（默认是当前目录）。
如果未指定 -fctuvSUX 或 --sort，则按字母顺序对条目排序。
```



Manual page 1s(1) line 1 (press h for help or q to quit)

$

要搜索 man 页面，请向 `man` 命令的 `-k` 选项提供关键字。如果你正在寻找一个可以重启系统的命令，可以搜索 `"reboot"`。一旦获得了包含该关键词的 man 页面列表，你就可以阅读其中最有希望的文档了。

```
$ man -k reboot
grub-reboot (8) - 仅为下次启动设置 GRUB 的默认启动项
halt (8) - 重启或停止系统
poweroff (8) - 重启或停止系统
reboot (2) - 重启或启用/禁用 Ctrl-Alt-Del
reboot (8) - 重启或停止系统
$ man reboot
```

NAME

`reboot`, `halt`, `poweroff` - 重启或停止系统...

某些命令在提供参数 `-h` 或 `--help` 时会打印帮助信息。即使是 `man` 命令也遵循这一约定。

```
$ man -h
Usage: man [OPTION...] [SECTION] PAGE

-C, --config-file=FILE 使用此用户配置文件
-d, --debug 发出调试消息
-D, --default 将所有选项重置为默认值
  --warnings=[WARNINGS] 启用 groff 的警告
```

```
$ man --help
Usage: man [OPTION...] [SECTION] PAGE

-C, --config-file=FILE 使用此用户配置文件
-d, --debug 发出调试消息
-D, --default 将所有选项重置为默认值
  --warnings=[WARNINGS] 启用 groff 的警告
...
$ ls --help
Usage: ls [OPTION]... [FILE]...
```

列出 `FILE`（默认是当前目录）的信息。

如果未指定 `-cftuvUX` 或 `--sort`，则按字母顺序对条目排序。

长选项的强制性参数对于短选项也是强制性的。

`-a`, `--all` 不忽略以 `.` 开头的条目。

根据你对 Linux 目录结构的了解以及 Linux 操作系统附带的文档，你可以开始自己探索命令了。例如，列出 `/bin` 和 `/usr/bin` 的目录内容。挑选一些引起你注意的命令，并使用 `man` 命令查找其中每个命令的作用。

```
$ cd /bin
$ ls
awk diff cat cp date du echo grep groups less more
$ man date
NAME
    date - 打印或设置系统日期和时间
...
$ cd /usr/bin
$ ls
clear crontab cut dos2unix find kill mv pstree pwd sed strings touch ...
$ man clear
```

前面的 `ls` 命令的输出被截断了。在实际上，你可能会在 `/bin` 中找到几十个命令，在 `/usr/bin` 中找到数百个命令。

在继续之前，我想分享最后一个你可能觉得有基础命令。它是 `clear` 命令。如果你想要一个干净的屏幕来工作，那就是 `clear` 命令。

# 第4 章 目录

根据你对 Linux 目录结构的了解以及 Linux 操作系统附带的文档，你可以开始自己探索命令了。例如，列出 `/bin` 和 `/usr/bin` 的目录内容。挑选一些引起你注意的命令，并使用 `man` 命令查找其中每个命令的作用。

## 创建和删除目录

除了通过完整或相对路径引用目录外，你还可以创建新目录。绝对路径以 `/` 开头。相对路径不是。以下是一个示例：

```
$ mkdir testdir
$ls
testdir
$ mkdir testdir/subdir
$ ls -R testdir
testdir
subdir
```

要删除空目录，使用 `rmdir` 命令。要删除目录及其内容，请使用 `rm -rf` 命令。

```
$ rmdir testdir
$ rm -rf testdir
```

## 绝对路径和相对路径

绝对路径以 `/` 开头。相对路径不是。以下是一个示例：

```
$ mkdir testdir
$ls
testdir
$ mkdir testdir/subdir
$ ls -R testdir
testdir
subdir
```

要删除空目录，使用 `rmdir` 命令。要删除目录及其内容，使用 `rm -rf` 命令。

```
$ rmdir testdir
$ rm -rf testdir
```

# 第5 章 查看文件详情

`ls` 命令在第3章中简单介绍。它不仅列出文件和目录，还能提供这些目录的详细信息。`ls` 最常用的选项之一是 `-l`，它显示列表格式。以下是一个示例：

```
$ ls
Desktop Documents Music to-do.txt
$ ls -l
total 20
drw-xr-x 2 jason users 4096 May 3 08:33 Desktop
drw-xr-x 2 jason users 4096 May 3 08:35 Documents
drw-xr-x 2 jason users 4096 May 3 08:38 Downloads
drw-xr-x 3 jason users 4096 Jun 21 21:16 Music
-rw-r---- 1 jason users 73 Jun 22 19:34 to-do.txt
$
```

`ls -l` 提供的信息以一系列字符开头，表示文件或目录的权限。权限将在第6章中介绍。权限字符串后面的数字代表指向该文件或目录的链接数。接着显示所有者，然后是组名。然后显示文件大小。时间戳代表修改时间。最后一项是文件或目录名称。

```
$ ls -l to-do.txt
-rw-r---- 1 jason users 73 Jun 22 19:34 to-do.txt
```

默认情况下，`ls` 不显示以点（`.`）开头的文件或目录。在 Linux 中，此类文件被视为隐藏文件。要用 `ls` 显示隐藏文件，请使用 `-a` 选项来包含所有项目。要以长列表格式显示所有项目，请使用 `-1` 和 `-a`。记住选项可以组合使用。这三个命令是等价的：`ls -1 -a`、`ls -la` 和 `ls -al`。

```
$ ls
Desktop  Documents  Downloads  Music  to-do.txt
$ ls -a
..  .bash_history  bash_logout  bashrc  Desktop  Documents  Downloads
Music  .profile  .ssh  to-do.txt
$ ls -a -l
total 48
drwxr-xr-x 7 users 4096 Jun 22 20:36 .
drwxr-xr-x 6 root 4096 May 4 10:26 ..
-rw-r--r 1 users 3738 Jun 22 19:37 .bash_history
-rw-r---- 1 users 220 Mar 30 2013 .bash_logout
-rw-r---- 1 users 3650 Jun 22 19:41 .bashrc
drwxr-xr-x 2 users 4096 May 3 08:33 Desktop
drwxr-xr-x 2 users 4096 May 3 08:35 Documents
drwxr-xr-x 2 users 4096 May 3 08:38 Downloads
drwxr-xr-x 3 users 4096 Jun 21 21:16 Music
-rw-r---- 1 users 675 Mar 30 2013 .profile
drwx------ 2 users 4096 May 3 12:44 .ssh
-rw-r---- 1 users 73 Jun 22 19:34 to-do.txt
$ ls -al
total 48
drwxr-xr-x 7 users 4096 Jun 22 20:36 .
drwxr-xr-x 6 root 4096 May 4 10:26 ..
-rw------ 1 users 3738 Jun 22 19:37 .bash_history
-rw-r---- 1 users 220 Mar 30 2013 .bash_logout
-rw-r---- 1 users 3650 Jun 22 19:41 .bashrc
drwxr-xr-x 2 users 4096 May 3 08:33 Desktop
drwxr-xr-x 2 users 4096 May 3 08:35 Documents
drwxr-xr-x 2 users 4096 May 3 08:38 Downloads
drwxr-xr-x 3 users 4096 Jun 21 21:16 Music
-rw-r---- 1 users 675 Mar 30 2013 .profile
drwx------ 2 users 4096 May 3 12:44 .ssh
-rw-r---- 1 users 73 Jun 22 19:34 to-do.txt
$ ls -la
total 48
drwxr-xr-x 7 users 4096 Jun 22 20:36 .
drwxr-xr-x 6 root 4096 May 4 10:26 ..
-rw------ 1 users 3738 Jun 22 19:37 .bash_history
-rw-r--r-- 1 jason users 220 Mar 30 2013 .bash_logout
-rw-r--r-- 1 jason users 3650 Jun 22 19:41 .bashrc
drwxr-xr-x 2 jason users 4096 May 3 08:33 Desktop
drwxr-xr-x 2 jason users 4096 May 3 08:35 Documents
drwxr-xr-x 2 jason users 4096 May 3 08:38 Downloads
drwxr-xr-x 2 jason users 4096 Jun 21 21:16 Music
-rw-r--r-- 1 jason users 675 Mar 30 2013 .profile
drwx------ 2 jason users 4096 May 3 12:44 .ssh
-rw-r--r-- 1 jason users 73 Jun 22 19:34 to-do.txt
```

若要在 `ls` 中在文件或目录名称后添加文件类型指示，请使用 `-F` 选项。

```
$ ls
Desktop Documents Downloads link-to-to-do Music program to-do.txt
$ ls -F
Desktop/ Documents/ Downloads/ link-to-to-do@ Music/ program* to-do.txt
$ ls -1F
total 24
drwxr-xr-x 2 jason users 4096 May 3 08:33 Desktop/
drwxr-xr-x 2 jason users 4096 May 3 08:35 Documents/
drwxr-xr-x 2 jason users 4096 May 3 08:38 Downloads/
lrwxr-xr-x 1 jason users 9 Jun 22 21:01 link-to-to-do -> to-do.txt
drwxr-xr-x 3 jason users 4096 Jun 21 21:16 Music/
-rwxr-xr-x 1 jason users 13 Jun 22 21:02 program*/
-rw-r--r-- 1 jason users 73 Jun 22 19:34 to-do.txt
$
```

表 2：文件类型指示

| 符号 | 文件类型 |
| --- | --- |
| / | 目录 |
| @ | 符号链接，`->` 符号之后的文件是链接的目标。 |
| * | 可执行脚本或程序 |
| = | 套接字 |
| > | 门 (Door) |
| \| | 命名管道 |

符号链接（有时称为 symlink 或 link）指向实际文件或目录的位置。符号链接只是一个指针，但你可以像操作实际文件或目录一样对其进行操作。符号链接通常用于创建长路径的快捷方式。符号链接的另一个常见用途如下所示，指向应用程序的当前版本。

```
$ cd /opt/
$ ls -F
1.6.0/ 1.7.1/ 1.7.2/ current@
$ ls -l
total 12
drwxr-xr-x 2 root 4096 Jun 22 21:12 1.6.0/
drwxr-xr-x 2 root 4096 Jun 22 21:11 1.7.1/
drwxr-xr-x 2 root 4096 Jun 22 21:11 1.7.2/
lrwxrwxrwx 1 root 5 Jun 22 21:12 -> 1.7.2/
$
```

要按时间对 `ls` 命令的输出进行排序，请使用 `-t` 选项。它会显示最近修改的项目。如果你想反转顺序，请使用 `-r`。这在你有一个包含许多文件的目录时非常有用。当按时间反向排序时，旧文件将滚出屏幕顶部，而最新的文件将显示在你的提示符上方。

```
$ ls -t
program link-to-to-do to-do.txt Music Desktop
$ ls -lt
total 24
drwxr-xr-x 1 jason users 13 Jun 22 21:02 program
-rw-r---- 1 jason users 73 Jun 22 19:34 to-do.txt
drwxr-xr-x 3 jason users 4096 Jun 21 21:16 Music
drwxr-xr-x 2 jason users 4096 May 3 08:38 Downloads
drwxr-xr-x 2 jason users 4096 May 3 08:35 Documents
drwxr-xr-x 2 jason users 4096 May 3 08:33 Desktop
```

### 空格与特殊字符的转义

尽管文件名和目录名允许包含空格，但最好尽可能避免它们。如果不使用空格，可以考虑使用连字符或下划线。另一个很好的选择是使用驼峰命名法（CamelCase）。例如，不要将文件命名为 `my to do list`，而是命名为 `my-to-do-list`、`my_to_do_list`甚至是 `ToDoList`。

即使你选择在文件名中使用空格，可能会遇到他人创建的文件。处理包含空格的文件有两种方法：使用引号或转义。要操作名为 `my to do list` 的文件，请用引号括起来，如 `"my to do list"`。要转义文件名，请在空格前加反斜杠，如 `my\ to\ do\ list`。转义就像引号，只不过适用于单个字符。

如果你不确定如何转义文件或目录名称，可以让 `ls` 通过 `-b` 选项为你显示。引用和转义不仅针对空格，还针对其他特殊字符，如 `|`、`&`、'` `;`、空格和制表符。

```
$ ls
my to do list
$ ls -l
total 4
-rw-r--r-- 1 jason users 73 Jun 22 22:16 my to do list
$ ls -1 my to do list
ls: cannot access my: No file or directory
ls: cannot access to: No file or directory
ls: cannot access do: No file or directory
ls: cannot access list: No file or directory
$ ls -1 "my to do list"
```

```bash
-rw-r--r-- 1 jason users 73 Jun 22 22:16 my to do list
$ ls -l my\ o\ do\ list
-rw-r--r-- 1 jason users 73 Jun 22 22:16 my to do list
$ ls -lb
total 4
-rw-r--r-- 1 jason users 73 Jun 22 22:16 my\ o\ do\ list
$
```

# 第 6 章 权限

回看 `ls` 命令提供的长列表，我们现在可以解读给定文件或目录列表的权限了。权限显示在长列表的开头。

```bash
$ ls -l sales.data
-rw-r--r-- 1 jason users 10400 Jun 14 09:31 sales.data
```

权限字符串中的第一个字符揭示了类型。例如，`-` 是普通文件，`d` 是目录，`l` 是符号链接。这些是你会遇到的最常见的类型。然而，下表还列出了其他文件类型。

表 4：文件类型

| 文件类型 | 符号 |
| :--- | :--- |
| 普通文件 | - |
| 块设备文件 | b |
| 字符设备文件 | c |
| 目录 | d |
| 符号链接 | l |
| FIFO (命名管道) | p |
| 套接字 | s |
| 其他文件类型 | ? |

权限字符串中的其余字符代表了三种主要的权限类型：读、写和执行。每个权限由单个字母表示，称为符号。读用 `r` 表示，写用 `w` 表示，执行用 `x` 表示。

表 5：权限

| 权限 | 符号 |
| :--- | :--- |
| 读取 | r |
| 写入 | w |
| 执行 | x |

对于文件而非目录，读、写和执行权限具有直观的含义。读取权限允许你查看文件内容。写入权限允许你修改文件。执行权限允许你运行或作为程序执行一个文件。

当涉及到目录时，读、写和执行权限的含义并不直观。读取权限允许你读取目录中的文件名。写入权限允许通过重命名文件、创建文件和删除文件来更改目录中的项。执行权限允许你 `cd` 进入该目录。查看以下文件权限和目录权限之间的区别。

表 6：文件和目录权限

| 权限 | 文件含义 | 目录含义 |



| :--- | :--- | :--- |

| 读取 | 允许读取文件。 | 允许读取目录中的文件名。 |

| 写入 | 允许修改文件。 | 允许修改目录内的项。 |

| 执行 | 允许执行文件。 | 允许访问目录项的内容和元数据。 |

Linux 中的所有文件都由一个用户和一个组所有。这允许在三组用户上应用独特的权限：用户所有者、组所有者和其他。在修改权限时，这些组可以用单个字母表示：`u` 代表用户所有者，`g` 代表组所有者，`e` 代表其他。此外，字母 `a` 可以代表所有三个权限组。注意，这些字符不会出现在 `ls` 列表中，但在更改权限时可以使用它们。

### 表 7：用户类别

| 类别 | 符号 |
| :--- | :--- |
| 用户 | u |
| 组 | g |
| 其他 | o |
| 所有 | a |

回到我们的原始示例，我们可以查看 `sales.data` 文件的用户和组所有者。用户所有者首先列出，然后是组所有者。在这种情况下，`jason` 是用户所有者，`users` 是组所有者。

```bash
$ ls -l sales.data
-rw-r--r-- 1 jason users 10400 Jun 14 09:31 sales.data
```

每个用户至少是一个组的成员，称为主组。然而，用户可以是许多组的成员。组用于将用户组织成逻辑集合。例如可以创建一个名为 `sales` 的组，包含销售部门的所有员工。你可以将文件的组所有者设置为 `sales` 组，并允许 `sales` 组的成员拥有文件的读写权限，或任何其他权限。

要确定你属于哪些组，请运行 `groups` 命令。如果你将另一个用户的 ID 作为参数提供给 `groups` 命令，将看到该用户所属的组列表。你也可以运行 `id -Gn [user]` 来获得相同的结果。

```bash
$ groups
users sales
$ id -Gn
users sales
$ groups tracy
users projectx dba
$ groups john
users sales manager
```

### 解码权限

现在你有足够的背景信息来开始解码权限字符串了。权限字符串中的第一个字符是类型。接下来的三个字符代表用户即文件所有者可用的权限。接下来的三个字符代表组可用的权限。最后三个字符代表所有其他人的权限。

在这种情况下，顺序是重要的。权限组将始终按此顺序显示：用户、组和其他。在这三个权限组内部，权限类型将按此顺序排列：读、写和执行。如果未授予特定权限，则用连字符 `-` 占据其位置。

是 `ls -l` 显示的权限信息的彩色表示：文件类型为红色，用户权限为绿色，组权限为蓝色，其他权限为紫色。

```bash
$ ls -l sales.data
-rw-r--r-- 1 jason users 10400 Jun 14 09:31 sales.data
```

通过检查前面的示例，你可以确定文件类型是普通文件 `-`，用户所有者允许读写权限 `rw-`，组所有者允许读取权限 `r--`，其他人也允许读取权限 `r--`。用户所有者是 `jason`，组所有者是 `users`。

如果权限字符串末尾出现额外的字符，则应用了另一种控制方法。点 `.` 表示 SELinux 安全增强 Linux 安全上下文已应用到文件或目录。加号 `+` 表示 ACLs 访问控制列表正在使用。SELinux 和 ACLs 超出了本书的范围。如果你在权限上遇到问题，请查看权限字符串末尾的额外字符，可能需要进一步调查。

```bash
$ ls -l sales.data.selinux
-rw-r--r-- 1 jason users 10400 Jun 14 09:31 sales.data.selinux
$ ls -l sales.data.acl
-rw-r--r-- 1 jason users 10400 Jun 14 09:31 sales.data.acl
```

### 修改权限

权限也称为模式 modes。`chmod` 命令是“change mode”的缩写，用于更改权限。`chmod` 命令有两种方法来指定模式。第一种方法是符号模式。符号格式是用户类别权限。以下是使用符号格式的 `chmod` 命令视图。

| 符号 | 描述 |
| :--- | :--- |
| chmod | 命令本身。 |
| ugoa | 用户类别。使用 `u` 表示用户，`g` 表示组，`a` 表示所有。 |
| +=- | 运算符。使用 `+` 添加权限，使用 `-` 删除，或使用 `=` 显式设置。 |
| rwx | 实际权限。使用 `r` 表示读，`w` 表示写，`x` 表示执行。 |

你可以使用用户类别和权限对来添加、删除或设置权限。例如，如果你想为组所有者添加权限，可以指定 `chmod g+w`。

```bash
$ ls -l sales.data
-rw-r--r-- 1 jason users 10400 Jun 14 09:31 sales.data
$ chmod g+w sales.data
$ ls -l sales.data
-rw-r--r-- 1 jason users 10400 Jun 14 09:31 sales.data
```

运行 `chmod g+w sales.data` 后，权限字符串从 `-rw-r--r--` 变为 `-rw-rw--r--`。注意权限按用户、组和其他的顺序显示。组权限现在包含了 `w` 符号，表示已授予写入权限。现在文件的所有者 `Jason` 和 `users` 组的成员可以读写 `sales.data`。以下示例演示了如何删除写入权限。

```bash
$ ls -l sales.data
-rw-rw--r-- 1 jason users 10400 Jun 14 09:31 sales.data
$ chmod g-w sales.data
$ ls -l sales.data
-rw-r--r-- 1 jason users 10400 Jun 14 09:31 sales.data
```

可以一次更改多个权限。例如，你可以使用 `g+wx` 为组添加写和执行权限。

```bash
$ ls -l sales.data
-rw-r--r-- 1 jason users 10400 Jun 14 09:31 sales.data
$ chmod g+wx sales.data
$ ls -l sales.data
-rw-rwxrx-- 1 jason users 10400 Jun 14 09:31 sales.data
```

你也可以同时修改多个权限。例如，如果用户和组没有这些权限，`ug+wx` 将添加。在这种情况下，注意用户所有者在执行 `chmod` 命令之前已经有了写入权限。运行 `chmod` 后，用户所有者仍将写入权限，以及新添加的执行权限。使用 `+` 添加权限始终会在适用时添加权限，它不会剥夺。

```bash
$ ls -l sales.data
-rw-r--r-- 1 jason users 10400 Jun 14 09:31 sales.data
$ chmod ug+wx sales.data
$ ls -l sales.data
-rw-rwxrwx-- 1 jason users 10400 Jun 14 09:31 sales.data
```

如果你想为不同的用户类别设置不同的权限，可以用逗号分隔这些说明。你可以混合组合以产生你所需的权限。例如，`u=rw,g+x` 将为文件所有者设置读、写和执行权限，同时为组添加执行权限。查看以下示例中 `sales.data` 权限是如何变化的。

```bash
$ ls -l sales.data
-rw-r--r-- 1 jason 10400 Jun 14 09:31 sales.data
$ chmod u=rw,g+x sales.data
```

```
$ ls sales.data
-rwxr-xr-- 1 jason users 1040 Jun 14 09:31 sales.data
```

如果你想让文件对所有人可读，且仅可读，请使用 `chmod a=r file`。当你使用等号 `=` 时，当前的权限会被你所指定的内容所替换。在这种情况下，`a=r` 为用户、组和其他用户设置了读取权限。任何写入或执行权限都将被移除。

```
$ ls -l sales.data
-rw-r--r-- 1 jason users 10400 Jun 14 09:31 sales.data
$ chmod a=r sales.data
$ ls -l sales.data
-rw-r--r-- 1 jason users 10400 Jun 14 09:31 sales.data
```

如果你没有在等号后没有指定权限，则该权限将被移除。以下是这种行为的示例说明。

```
$ ls -l sales.data
-rw-r--r-- 1 jason users 10400 Jun 14 09:31 sales.data
$ chmod u=rwx,o= sales.data
$ ls -l sales.data
-rwxr-xr-x 1 jason users 10400 Jun 14 09:31 sales.data
```

### 基于数值的权限

使用 `chmod` 命令指定模式的第二种方法称为模式 mode。理解符号模式将帮助你学习八进制模式。一些 Linux 用户永远不会脱离符号权限。然而，经验丰富的 Linux 用户发现，长远来看，八进制模式更快、更简单；只有几种常用的权限可以被容易记住和回想起。

八进制权限基于二进制数值系统，也称为二进制数值系统。每种权限类型被视为一个位，要么是关闭的用 0 表示，要么是开启用 1 表示。在权限中，顺序是有意义的。权限始终按照读取、写入和执行的顺序排列。如果 `r`、`w` 和 `x` 都被设置为关闭，二进制表示为 `000`。如果它们都被设置为开启，二进制表示为 `111`。要在省略执行权限的情况下读取和写入权限，二进制数为 `110`。

### 表 9：权限的二进制和十进制表示法

| | 读取 | 写入 | 执行 |
|---|---|---|---|
| 关闭的二进制值和十进制值 | 0 | 0 | 0 |
| 读取 | 写入 | 执行 |
|---|---|---|---|
| 开启的二进制值 | 1 | 1 | 1 |
| 开启的十进制值 | 4 | 2 | 1 |

为 `chmod` 命令提供所需权限的十进制值。若要将二进制表示转换为十进制，请记住读取等于 4，写入等于 2，执行等于 1。权限数字通过相加每个权限类型的值来确定。例如，读取和执行权限表示为读取的 4 加上执行的 1，等于 5。从零到七共有八种可能的值，因此被称为八进制 octal。下表演示了所有八可能的权限。

### 表 10：八进制权限

| 权限 | 字符串 | 二进制 | 八进制 |
|---|---|---|---|
| 无权限 | --- | 000 | 0 |
| 仅执行 | -x | 001 | 1 |
| 仅写入 | -w- | 010 | 2 |
| 写入和执行 | -wx | 011 | 3 |
| 仅读取 | r-- | 100 | 4 |
| 读取和执行 | r-x | 101 | 5 |
| 读取和写入 | rw- | 110 | 6 |
| 读取、写入和执行 | rwx | 111 | 7 |

记住权限顺序是有意义的。用户类别始终是这个顺序：用户 user、组 group 和其他 other。一旦确定了每个类别的八进制值，必须按该顺序指定。例如，要获得 `-rwxr-xr--` 权限，使用 `chmod 754 file`。这意味着文件的所有者拥有读取、写入和执行权限；文件组的成员拥有读取和执行权限；而其他人只有读取权限。

### 表 11：给定权限的符号、二进制和十进制表示

| 用户 | 组 | 其他 |
|---|---|---|
| 符号 | rwx | rw- | r-- |
| 二进制 | 111 | 110 | 100 |
| 十进制 | 7 | 6 | 4 |

### 常用权限

该表说明了最常用的权限。这五组权限设置将涵盖大多数权限情况。

### 表 12：常用权限

| 含义 | 八进制 | 符号 |
| --- | --- | --- |
| 允许文件所有者对文件完全控制。系统上的其他人无法访问。 | 700 | -rwx------ |
| 允许系统上的所有人执行文件，但只有所有者可以编辑它。 | 755 | -rwxr-xr- |
| 允许一组人员修改文件并让其他人读取。 | 664 | -rw-rw-r-- |
| 允许一组人员修改文件但不让他读取。 | 660 | -rw-rw---- |
| 允许系统上的所有人读取文件，但只有所有者可以编辑它。 | 644 | -r--r--r-- |

Linux 操作系统的许多新手倾向于使用宽松的权限。他们有时并不仔细思考所需的权限，而是通过使用 `777` 或 `666` 权限来“给所有人所有权限”。每当你看到一个具有 `777` 或 `666` 权限的文件或目录时，请知道总有更好的权限集可以使用。

向文件或目录授予不必要的权限不仅具有安全影响，还可能导致这些文件或目录引入意外的更改。如果每个文件都有 `777` 权限，那么 Linux 系统上的任何人都可以编辑该文件。这可能导致某人在实际上只想用编辑器查看文件内容时，不小心保存了更改。

此外，系统上的用户可能会故意利用弱权限来提升权限，访问他们不应该访问的数据，甚至破坏数据。他们可能会向脚本或程序中插入恶意代码，并等待系统上的其他人执行它。记住，系统上的任何人都可以执行该文件，因为所有权限包括执行权限都已授予。

如果有多个人需要对文件进行写入访问，请利用组并限制他人的访问。将避免 `777` 和 `666` 权限模式视为最佳实践。

### 组操作

让我们来看一个多人需要访问同一个文件的情况。例如，销售团队的成员需要更新一个名为 `sales.report` 的文件，可以使用 `chgrp` 命令将文件的组所有者设置为名为 `sales` 的 Linux 组。接下来，如果你不想让系统上的其他人读取它，可以将权限设置为 664 `rw-r--r--` 甚至 660 `rw-rw--`。从技术上讲，774 `rwxr-xr-x` 和 770 `rwxrwx--` 也可以，但由于 `sales.report` 不是一个可执行程序，使用 664 `rw-r--r--` 或 660 `rw-rw--` 是合理的。

当创建一个文件时，它会被设置为当前用户的主组。你可以使用 `newgrp` 命令来覆盖此行为，但记住新文件将继承此设置。

```
$ ls -l sales.data
-rw-r--r-- 1 jason users 10400 Jun 14 09:31 sales.data
$ chmod a=r sales.data
$ ls -l sales.data
-rw-r--r-- 1 jason users 10400 Jun 14 09:31 sales.data

$ ls -l sales.data
-rw-r--r-- 1 jason users 10400 Jun 14 09:31 sales.data
$ chmod u=rwx,o= sales.data
$ ls -l sales.data
-rwxr-xr-x 1 jason users 10400 Jun 14 09:31 sales.data
```

### 目录权限

Linux 新手遇到的常见问题是目录权限错误。目录权限可以阻止访问文件。如果你确定文件权限设置错误，请查看父目录。通过在当前目录运行 `ls -1 .`、使用 `cd` 进入父目录并重复这些步骤，向文件系统的根目录移动直到找到问题。

```
$ ls -ld directory/
drwxr-xr-x 2 jason 4096 Sep 29 22:02 directory/
$ ls -ld directory/
total 0
-rwx--r-- 1 jason 0 Sep 29 22:02 testprog
$ chmod 400 directory
$ ls -ld directory/
d------ 2 jason 4096 Sep 29 22:02 directory/
$ ls -ld directory/
ls: cannot access directory/testprog: Permission denied
total 0
-??????? ? ? ? testprog
$ directory/testprog
su: directory/testprog: Permission denied
$ chmod 500 directory/
$ ls -ld directory/
d-x------ 2 jason 4096 Sep 29 22:02 directory/
$ ls -1d directory/
total 0
-rwx--r-- 1 jason 0 Sep 29 22:02 testprog
$ directory/testprog
This program ran successfully.
```

### 默认权限与文件掩码

文件创建掩码称为 umask 决定了新文件和目录的默认权限。umask 通常由系统管理员设置；然而，个人用户可以在其账户初始化文件中使用 umask 语句来覆盖该设置。

如果不应用掩码，新目录将获得 777 `rwxrwxrwx` 权限，新文件将获得 666 `rw-rw-rw-` 权限。当 umask 应用于这些基础权限时，它会禁用或屏蔽某些权限。例如，umask 为 000 将禁用或屏蔽零位。在这种情况下，新目录获得 777，新文件获得 666 权限。在另一个极端，umask 为 777 会禁用所有权限位。在这种情况下，新文件和目录获得 000 权限。

`umask [-S] [mode]` 如果指定了模式，则将创建掩码设置为该模式。如果省略了模式，则将显示当前模式。使用 `-S` 参数允许 umask 以符号表示法显示或设置模式。



快速估算 `umask` 模式如何影响默认权限的一种快捷方法是：对于目录，从 `777` 中减去八进制 `umask` 模式；对于文件，则从 `666` 中减去。以下是一个 `022` `umask` 的示例，这通常是 Linux 发行版或系统管理员使用的默认 `umask`。

### 表 13：创建权限估计

| 文件 | 目录 |

|---|---|---|

| 基础权限 | 666 | 777 |

| 减去 umask | -022 | -022 |

| 创建权限 | 644 | 755 |

使用 `002` `umask` 非常适合与用户组成员共同工作。当创建文件或目录时，该权限允许组内成员操作这些文件和目录。

### 表 14：创建权限估计

| 文件 | 目录 |

|---|---|---|

| 基础权限 | 666 | 777 |

| 减去 umask | -002 | -002 |

| 创建权限 | 664 | 775 |

这是另一个可以用于与组内成员工作的 `umask`。通过使用 `007`，不会向组外用户授予任何权限。

### 表 15：创建权限估计

| 文件 | 目录 |

|---|---|---|

| 基础权限 | 666 | 777 |

| 减去 umask | -007 | -007 |

| 创建权限 | 660 | 770 |

再次提到，使用这种减法方法是一个很好的估算。你可以看到，当 `umask` 为 `007` 时，该方法失效了。为了每次都能获得准确的结果，你需要将八进制权限转换为二进制值。从那里开始，对 `umask` 使用位取反（NOT）操作，然后对基础权限执行位与（AND）操作。另一种思考此方式是：`umask` 禁用了指定的值。`022` 的 `umask` 实际上意味着“禁用组的写位”。`007` 的 `umask` 意味着“禁用所有的所有位”。

下表包含了由八种掩码设置产生的权限。最常用且实用的 `umask` 模式是 `022`、`002`、`077` 和 `007`。

### 表 16：umask 及其产生的权限

| 文件权限 | 目录权限 | 二进制 | 八进制 |

|---|---|---|---|

| rw- | rwx | 000 | 0 |

| rw- | rw- | 001 | 1 |

| r-- | r-x | 010 | 2 |

| r-- | -- | 011 | 3 |

| -w- | -wx | 100 | 4 |

| -w- | -w- | 101 | 5 |

| --- | --x | 110 | 6 |

| --- | --- | 111 | 7 |

### 特殊模式

当使用 `umask` 命令查询当前设置时，它返回四个字符而不是三个。以下示例显示 `umask` 明确设置为 `022`，但 `umask` 返回 `002`。

```
$ umask 022
$ umask 002
```

到目前为止，你只引入了用户、组和其他用户的权限。然而，有一类被称为 `setuid`、`setgid` 和 `sticky`（粘滞位）的特殊模式。这些特殊模式通过在通常用于 `chmod` 的八进制数字前面加上一个字符来声明。这里的关键点是得知道 `umask 022` 等同于 `chmod 755`。同样，`644` 等同于 `chmod 644`。

`setuid` 权限允许程序以文件所有者的身份运行，而不是执行它的用户的身份。该权限的一个示例是 `passwd` 命令。`passwd` 命令允许用户更改自己的密码，但修改 `/etc/passwd` 和 `/etc/shadow` 文件需要超级用户权限。

使用八进制模式在前面加上数字 `4` 以启用 `setuid` 权限。对于符号模式，使用 `u+s`。

```
$ ls -ld /usr/bin/passwd
-rwxr-xr-x 1 root root 47032 Jul 26 /usr/bin/passwd
$ chmod 4555
$ ls -l
-r-sr-xr-x 1 jason users 0 Jun 7
```

与 `setuid` 权限类似，`setgid` 权限允许程序以文件组的身份运行，而不是执行它的用户的组。使用此类权限的 Linux 命令是 `locate`。当在目录上使用 `setgid` 时，它会导致该目录中的新条目以与目录相同的组创建。对于组，在目录上使用 `setgid` 可以防止有人无意中在默认组中创建文件，而不是预期的组。使用八进制模式在前面加上数字 `2` 以启用 `setgid` 权限。对于符号模式，使用 `g+s`。

```
$ ls -ld /usr/bin/locate
-rwx-s--x 1 root root 35548 Oct 10 /usr/bin/locate
$ chmod 2555
$ ls -l
-r-xr-xr-x 1 jason users 0 Jun 7
$ mkdir salesdir
$ chgrp salesdir
$ chmod g+s salesdir
$ ls -ld salesdir/
drwxr-xr-x 2 jason users 4096 Jun 7
$ touch salesdir/file-before-setgid
$ ls -1 salesdir/
total 0
-rw-r--r-- 1 jason users 0 Jun 7 file-before-setgid
$ chmod g+s salesdir
$ ls -ld salesdir
drwxrwxr-x 2 jason users 4096 Jun 7
```

粘滞位（sticky bit）防止用户删除另一个用户的文件，即使他或她通常拥有权限。最常见使用粘滞位的地方是 `/tmp` 和 `/var/tmp` 目录。使用粘滞位时，在前面加上数字 `1`。对于符号模式，使用 `+t`。

```
$ ls -ld /tmp
drwxrwxrwt 1 root 20480 Jun 6 18:17 /tmp
$ ls -ld /var/tmp
drwxxrrxr 4 root 4096 Jun 7 16:46 /var/tmp
$ chmod 1777 tmp
$ ls -ld tmp
drwxrwxrwt 2 jason users 4096 Jun 7 16:50 tmp
```

### 表 17：特殊模式

| 权限 | 八进制 |

|---|---|

| setuid | 4 |

| setgid | 2 |

| sticky | 1 |

### 编辑文件

`nano` 是一个极其简单但功能足够的文本编辑器。它没有高级的编辑功能，但如果你想对文件进行简单的更改，它一定能胜任。要编辑现有文件或创建新文件，请运行 `nano file-name`。加载时，你将看到文件内容以及屏幕底部的可用命令列表。光标 `^` 代表 Ctrl 键。例如，退出编辑器输入 `Ctrl-x`，保存文件输入 `Ctrl-o`。需要帮助时输入 `Ctrl-g`。

除了屏幕底部列出的导航命令外，你还可以简单地使用方向键、Page Up 和 Page Down 键以及 Home 和 End 键。要添加内容，直接输入即可。删除内容只需使用 Delete 和 Backspace 键。要删除整行，使用 `Ctrl-k`。

```
GNU nano 2.2.6
File: to-do.txt
```

- 此文件包含我的待办事项列表。

- 修草坪。

- 统治世界。

> [ 读取 3 行 ]

^G 帮助 ^O 写入 ^R 读取文件 ^Y 上一页 ^K 剪切文本 ^C 位置

^X 退出 ^J 对齐 ^W 查找 ^V 下页 ^U 取消文本 ^T 进入 Shell

### Vim 编辑器

如果你正在一个具有高级编辑功能且可以在命令行使用的编辑器，请使用 `vi` 或 `Emacs`。在 Linux 系统上，当你尝试使用 `vi` 时，你实际上在使用 `Vim`（improved 的缩写）。`vi` 通常是指向 `Vim` 的软链接。`Vim` 编辑器兼容 `vi` 编辑器中的命令，`vi` 最初是为 Unix 操作系统创建的。`Vim` 包含了 `vi` 不具备的额外功能：语法高亮、通过网络编辑文件的能力、多级撤销和重做以及分屏。学习 `Vim` 或 `vi` 的优势之一是将按键映射应用到其他命令，例如 `man`、`more`、`less` 和 `view`。

### 命令模式

`vi` 和 `Vim` 编辑器的一个独特特性是模式的概念。`Vim` 有三种模式：命令模式、插入模式和行模式。`Vim` 启动时处于命令模式。要随时返回命令模式，只需按下 Escape 键。在命令模式下，发送到编辑器的按键不会出现在文件中，而是被解释为命令。命令模式允许你在文件中导航、执行搜索、删除文本、复制文本、粘贴文本等操作。

| 键 | 动作 |

| --- | --- |

| k | 向上移动一行。 |

| j | 向移动一行。 |

| h | 向左移动一个字符。 |

| l | 向右移动一个字符。 |

| w | 向右移动一个单词。 |

| b | 向左移动一个单词。 |

| ^ | 到行首。 |

| $ | 到行尾。 |

命令区分大小写。例如，小写的 `l` 将光标向右移动一个字符，大写的 `L` 将光标移动到窗口底部。尽管原始 `vi` 编辑器不允许使用方向键，但 `Vim` 可以。尽管你可以使用方向键，但有人认为原始 `vi` 的按键绑定更快，因为你的手不需要离开主行。

### 插入模式

插入模式允许你在文件中实际输入文本。要进入插入模式，按下 `i`、`I`、`a` 或 `A`。输入所需的文本后，可以按下 Escape 键返回命令模式。

| 键 | 动作 |

|---|---|

| i | 在当前位置插入。 |

| I | 在行首插入。 |

| a | 在光标位置后追加。 |

| A | 在行尾追加。 |

### 行模式

行模式（有时称为命令行模式）通过在命令模式下输入冒号 `:` 来访问。行模式允许你保存文件、退出编辑器、替换文本并执行某些形式的导航。以下是你可能想要熟悉的一些常用的行模式命令。

### 表 20：Vim 行模式命令

| 键 | 动作 |

|---|---|

| :w | 写入或保存文件。 |

| :w! | 强制保存文件，即使没有设置写入权限。 |

| :q | 退出编辑器。如果文件有未保存的更改，则执行失败。 |

| :q! | 不保存文件直接退出。 |

| :wq! | 写入并退出。 |

| :x | 等同于 :wq! |

| :n | 将光标置于第 n 行。 |

| $: | 将光标置于文件的最后一行。 |

| :set nu | 打开行号显示。 |

| :set nonu | 关闭行号显示。 |

| :help [子命令] | 内置帮助文档。 |

### 重复命令

大多数命令可以通过在它们前面加上数字来重复。例如，要将光标向下移动三行，输入 `3j`。要插入 20 次相同的文本，输入 `20i` 后跟所需的文本，完成后按下 Escape 键。插入操作将重复 20 次。要插入一行下划线，输入 `80i`。

### 额外命令

下表列出了在命令模式下使用的一些按键组合。

### 表 21：Vim 模式—删除文本

| 键 | 动作 |

|---|---|

| x | 删除一个字符。 |

| dw | 删除一个单词。 |

| dd | 删除一行。 |

### 表 22：Vim 模式—更改文本

| 键 | 动作 |

|---|---|

| ci | 更改一个字符。 |

| cw | 更改一个单词。 |

| cc | 更改整行。 |

| c$ | 更改到行尾。 |

### 表 23：Vim 模式—复制与粘贴

| 键 | 动作 |

|---|---|

| yy | 复制（yank）当前行。 |

| yw | 复制（yank）一个单词。 |

| p | 粘贴（yank）之前剪切的文本。 |

### 表 24：Vim 模式—撤销与重做

| 键 | 动作 |

|---|---|

| u | 撤销。 |

| r | 重做。 |

### 表 25：Vim 模式—搜索

| 键 | 动作 |

|---|---|

| /pattern | 开始正向搜索。 |

| ?pattern | 开始反向搜索。 |

### 表 26：Emacs 基础快捷键

| 键 | 动作 |

|---|---|

| C-h | 帮助。 |

| C-x C-c | 退出。 |

| C-x C-s | 保存文件。 |

| C-h t | 内置教程。 |

| C-h <key> | 描述 <key>。 |

| C-u N <command> | 重复 <command> N 次。 |

### 表 27：Emacs 快捷键—导航

| 键 | 动作 |

|---|---|

| C-p | 到上一行。 |

| C-n | 到下一行。 |

| C-b | 向后移动一个字符。 |

| C-f | 向前移动一个字符。 |

| M-f | 向向前一个单词。 |

| M-b | 向后移动一个单词。 |

| C-a | 到行首。 |

| C-e | 到行尾。 |

| M-< | 到文件开头。 |

| M-> | 到文件结尾。 |

### 表 28：Emacs 快捷键—删除文本

| 键 | 动作 |

|---|---|

| C-d | 删除一个字符。 |

| M-d | 删除一个单词。 |

### 表 29：Emacs 快捷键—复制与粘贴

| 键 | 动作 |

|---|---|

| C-k | 剪切（或复制）当前行的剩余部分。 |

| C-y | 粘贴（yank）之前剪切的文本。 |

| C-x u | 撤销。多级撤销重复。 |

### 表 30：Emacs 快捷键—搜索

| 键 | 动作 |

|---|---|

| C-s | 开始正向搜索。输入要查找的内容并按 C-s 移动到下一个出现处。按回车停止搜索。 |

| C-r | 开始反向搜索。 |

### 图形化编辑器

`Nano`、`Vim` 和 `Emacs` 非常适合在命令行编辑文件。然而，如果你正在使用 GUI，你有更多选择，但不要认为在学习 `Vim` 或 `Emacs` 上付出的精力在图形环境下是徒的。`Vim` 的图形界面版本是 `gvim`。`Emacs` 会检测并以图形模式启动。

如果你正在寻找文字处理器，可以考虑 `LibreOffice` 或 `AbiWord`。`LibreOffice` 是一个办公套件，不仅包含文字处理器，还带有电子表格程序、数据库应用程序和演示文件软件。

Linux 系统也有专用的编辑器。如果你正在寻找 IDE 或源代码编辑器，可以考虑 `jEdit`、`Geany`、`Kate` 或 `Sublime Text`。下表列出的编辑器仅为部分示例。

### 表 31: 图形化编辑器

| 编辑器 | 说明 |

|---|---|

| gVim | Vim 的图形版本。 |

| Emacs | Emacs 的图形版本。 |

| gedit | 用于 GNOME 桌面环境的类似记事本的编辑器。 |

| KEdit | KDE 桌面环境的默认文本编辑器。 |

| AbiWord | 文字处理器。 |

| LibreOffice | 办公套件。 |

| jEdit | 程序员文本编辑器。 |

| Geany | 一个小型且快速的 IDE。 |

| Kate | 多文档编辑器。 |

| Sublime Text | 源代码编辑器。 |

## 第 8 章 删除、移动和重命名文件与目录

可以使用 `rm` 命令删除文件和目录。

`rm file` 删除文件。

`rm -r directory` 使用 `rm` 删除目录时需要 `-r` 参数。`-r` 参数告诉 `rm` 递归删除文件和目录。

`rm -f file` 使用 `-f` 选项进行删除，且不提示确认。

通配符形式的搜索模式可以用于 `rm` 和 `ls` 等命令。常用的通配符是星号（*）和问号（?）。星号匹配任意内容，而问号匹配单个字符。记住，带有点的文件和目录被视为隐藏，不会被星号匹配。要在搜索中包含隐藏文件，请以点开头搜索。

```
$ ls Desktop Downloads Music todo.txt
$ ls t*
ls cannot access t*: No such file or directory
$ ls g*goals.txt
$ ls g?
ls cannot access g?: No such file or directory
$ ls -d .*
.bash_history .bashrc .profile
$ rm .hidden
```

`cp` 命令用于复制文件和目录。要创建副本，运行 `cp source_file destination_file`。你也可以通过在 `cp` 命令末尾指定目标目录将一个或多个文件复制到目录中。

`cp source_file destination_file` 将 `source_file` 复制到 `destination_file`。

`cp source_file... destination_directory` 将 `source_files` 复制到 `destination_directory`。

`cp -i source_file destination_file` 使用 `cp` 的 `-i` 选项以交互模式运行。如果 `destination_file` 存在，`cp` 将给你机会中止操作或通过覆盖 `destination_file` 继续执行。

`cp -r source_directory destination_directory` `cp` 的 `-r` 选项导致 `source_directory` 递归复制到 `destination_directory`。如果 `destination_directory` 存在，则将源目录复制到目标目录中。否则，将创建一个包含 `source_directory` 内容的 `destination_directory`。



```
$ ls
1file
$ cp 1file 2file
$ ls
1file 2file
$ mkdir 1dir
$ cp 1file 2file 1dir
$ ls 1dir/
1file 2file
$ cp -i 2file 1file
cp: overwrite '1file'? n
$ cp -r 1dir 2dir
$ ls 2dir/
1file 2file
$ cp 1dir 3dir
cp: omitting directory '1dir'
$ mkdir 3dir
$ cp -r 1dir 2dir 3dir
$ ls 3dir
1dir 2dir 3dir
|-- 1dir
|-- 1file
|-- 2file
|-- 2dir
|-- 1file
|-- 2file
2 directories, 4 files
```

要将文件和目录移动另一个另一个，请使用 `mv` 命令。此外，`mv` 也用于重命名文件和目录。

`mv source destination` 将 `source` 移动到 `destination`。如果 `destination` 是目录，则 `source` 将移动到 `destination` 中。如果 `destination` 不是目录，则 `source` 将重命名为 `destination`。

`mv -i destination` 使用 `-i` 选项以交互模式运行。如果 `destination` 存在，`mv` 将给你机会中止操作或通过覆盖 `destination` 继续执行。

在下面的示例中，使用 `mv` 命令将 `1dir` 重命名为 `1dir-renamed`。接下来，将 `1file` 重命名为 `2file` 并移动到 `1dir-renamed` 目录。如果你没有为 `mv` 指定 `-i` 选项，它将在不提示的情况下覆盖现有文件。这通过将 `1file` 移动到 `2file` 得到演示。`2file` 是一个现有文件。

```
$ ls -F
1dir/ 1file 2dir/ 2file 3dir/
$ mv 1dir 1dir-renamed
$ ls -F
1dir-renamed/ 1file 2dir/ 2file 3dir/ file1
$ mv 1file file1
$ ls -F
1dir-renamed/ 2dir/ 2file 3dir/
$ ls -F
1dir-renamed/
1file 2file file1
$ cat 1dir-renamed/1file
The contents of 1file.
$ cat 1dir-renamed/2file
The contents of 2file.
$ mv 1dir-renamed/1file 1dir-renamed/2file
$ cat 1dir-renamed/2file
The contents of 1file.
$ ls -F 1dir-renamed/
2file file1
$ mv -i 1dir-renamed/2file/file1
mv: overwrite '1dir-renamed/file1'? n
$
```

# 第 9 章 查找、排序和比较文件与目录

要在 Linux 系统上定位文件或目录，你可以使用 `find`。你可以通过名称、大小、权限、修改时间来查找文件。但是，如果你运行 `find / -name some_name`，`find` 将检查系统上的每一个文件，这可能是一个缓慢的过程。另一个可用于查找项的工具叫做 `locate`。

`locate pattern` 显示匹配模式的文件和目录。

`locate` 命令检查一个索引（或数据库），该数据库由名为 `updatedb` 的进程每天更新一次。这种方法的优点是它非常快，因为不需要实时检查文件和目录。缺点是它不是实时的。`locate` 命令对于查找旧于一天的文件或目录非常棒，但它找不到刚刚创建的项目。此外，`locate` 和 `updatedb` 有时未安装或启用。

### 表 32: 常用 find 命令

| 命令 | 说明 |
|---|---|
| `find -name` | 按名称显示项。 |
| `find -iname` | 与 `name` 相同，但不区分大小写。 |
| `find -ls` | 对每个项执行 `ls`。 |
| `find -mtime` | 显示旧于指定天数的项。 |
| `find -size` | 按大小显示项。 |
| `find -type d` | 显示目录。 |
| `find -exec` | 对每个项运行命令。 |
| `find {}` | 找到的项占位符。 |

`find` 命令检查提供路径中的每个文件和目录，以确定其是否匹配给定的表达式。在不带参数运行 `find` 时，假设路径为当前目录。

```
$ ls Desktop Downloads Music todo.txt
.bash_history .bashrc .profile
.hidden
.viminfo
$ find -name
.bash_history .bashrc .profile
.hidden .viminfo
$ find -name *
.bash_history .bashrc .profile
.hidden .viminfo
$ find -name t*
.bash_history .bashrc .profile
.hidden .viminfo
$ find -name g*
.bash_history .bashrc .profile
.hidden .viminfo
$ find -name g?
.bash_history .bashrc .profile
.hidden .viminfo
$ find -name g????
.bash_history .bashrc .profile

hidden .viminfo
$ ls -d .*
.bash_history .bashrc .profile
.hidden .viminfo
```

### 表 33: 常用 sort 选项

| 选项 | 说明 |
|---|---|
| `sort` | 对文本排序。 |
| `sort -k FIELD_NUM` | 按“键”排序。按 `FIELD_NUM` 列排序。 |
| `sort -r` | 反向排序。 |
| `sort -u` | 唯一排序。不显示重复项。 |

使用 `sort` 命令对文件内容排序。

```
$ find -mtime 1
.bashrc .viminfo
$ find -size +2M
/Music/Johntrane/giantsteps.mp3
$ find -type d -newer-do
/Music/Johntrane
$ find -name *|exec;
```

High Performance MPEG 1.0/2.5 Audio Player for 1, 2 version 1.12; copyright by Michael Hipp and others free software (LGPL/GPL) without any warranty best wishes

Directory: ./Music/Johntrane/

Playing MPEG stream of 1...

Title: Giant Steps

MPEG 1.0 layer III, 192 kbit/s, 44100 Hz

[0:00] Decoding of giantsteps.mp3 finished.

$

| 州 | 城市 |
| :--- | :--- |
| 亚利桑那 | 菲尼克斯 |
| 科罗拉多 | 丹佛 |
| 乔治亚 | 亚特兰大 |
| 印第安纳 | 印安纳波利 |
| 印第安纳 | 印安纳波利 |
| 印第安纳 | 印安纳波利 |
| 田纳西州 | 纳什维尔 |
| 怀俄明州 | 谢延 |
| $ sort random random-states | |
| 亚利桑那 | 菲尼克斯 |
| 科罗拉多 | 丹佛 |
| 乔治亚 | 亚特兰大 |
| 印第安纳 | 印安纳波利 |
| 田纳西州 | 纳什维尔 |
| 怀俄明州 | 谢延 |
| $ sort -k2 -u random-states | |
| 乔治亚 | 亚特兰大 |
| 怀俄明州 | 谢延 |
| 科罗拉多 | 丹佛 |
| 印第安纳 | 印安纳波利 |
| 田纳西州 | 纳什维尔 |
| 亚利桑那 | 菲尼克斯 |
| $ | |

比较

你可以使用 `diff`、`sdiff` 和 `vimdiff` 命令来比较文件和目录。`diff` 命令仅显示差异，`sdiff` 并排显示两个文件并高亮显示差异，而 `vimdiff` 则使用 Vim 编辑器显示差异。只需提供要比较的命令项即可。

```
$ cat random-states
Arizona Phoenix
Colorado Denver
Georgia Atlanta
Indiana Indianapolis
$ cat random-states.bak
Arizona Phoenix
Colorado Denver
```

Georgia Savannah Denver

Indiana Indianapolis

```
$ diff random-states random-states.bak
3c3
```

```
< Georgia Atlanta
---
> Georgia Savannah
$ diff random-states random-states.bak
Arizona Phoenix Phoenix
Colorado Denver Denver
Georgia | Georgia Savannah
Indiana Indianapolis Indiana
$ diff random-states random-states.bak
Arizona Arizona Phoenix
Colorado Colorado Denver
Georgia | Georgia Savannah
Indiana Indiana Indianapolis
```

random-states 1,1 All random-states.bak 1,1 All

"random-states.bak" 4L, 104C

$ tree

```
|-- dir1
|   -- file1
|-- dir2
|   -- file1
|   -- file2
```

2 个目录，3 个文件

$ diff dir1 dir2: file2

仅在 dir2

$

在 `diff` 输出中，`<` 符号后的文本属于第一个文件，而 `>` 符号后的文本属于第二个文件。此外，`diff` 还以简写格式提供差异信息。第一个数字代表第一个文件的行号。下一个字符将 `c` 表示更改、`d` 表示删除或 `a` 表示添加。最后一个数字代表第二个文件的行号。

`diff` 命令使用管道 `|` 来表示同一行的更改。`<` 符号表示该行仅存在于第一个文件中，而 `>` 符号表示该行仅存在于第二个文件中。

# 第10 章 I/O 重定向

Linux 操作系统具有一个称为 I/O 流的概念。三个默认的 I/O 流是标准输入、标准输出和标准错误。当一个进程启动时，它会连接到这三个 I/O 流，也称为标准流。默认情况下，标准输入来自你的键盘，而标准输出和标准错误显示在你的屏幕上。按照习惯，标准输出用于正常输出，而标准错误留给错误消息。

每个流都被分配了一个文件描述符。文件描述符由一个数字引用并代表一个打开的文件。标准输入被分配文件描述符 `0`，标准输出分配文件描述符 `1`，标准错误分配文件描述符 `2`。这实际上意味着你的键盘和显示器可以替代实际文件。这种抽象层允许你将通常显示在屏幕上的输出保存到文件中。它还允许你从文件向命令发送输入。你可以将一个命令的输出作为另一个命令的输入。

表 34：标准流

| 文件描述符 | 缩写 | 流 |
| :--- | :--- | :--- |
| 0 | stdin | 标准输入 |
| 1 | stdout | 标准输出 |
| 2 | stderr | 标准错误 |

许多 Linux 命令允许你通过指定文件作为参数或接受标准输入来提供输入。在没有文件的情况下，许多命令期望标准输入。文件以及标准输入都以文件结束 `EOF` 标记终止。你可以通过按键盘输入 `Ctrl-d` 来产生此 `EOF` 标记。

作为这种行为的示例，让我们来看 `sort` 命令。要让 `sort` 在文件上操作，请在下面的示例提供该文件作为参数：

```
$ cat test.txt
e
a
c
b
d
$ sort test.txt
a
b
c
```

要让 `sort` 在标准输入上操作，在不带任何参数的情况下运行 `sort` 命令并开始输入文本。完成后，输入 `Ctrl-d` 发送 `EOF` 字符。你提供的标准输入将会被排序。

```
$ sort
a
b
c
d
<Ctrl-d>
a
b
c
d
e
$
```

要将一个命令的标准输出作为另一个命令的标准输入发送出去，请在命令之间使用管道 `|`。下面的示例演示了如何将 `cat text.txt` 的输出发送给 `sort` 命令作为输入。

```
$ cat test.txt | sort
a
b
c
d
e
$
```

要将文件的内容作为标准输入，使用小于号 `<` 将命令与文件分开。

```
$ sort < test.txt
a
b
c
d
```

要将命令的输出重定向到文件，使用大于号 `>` 后跟文件名。如果文件不存在，它将被创建。如果它已存在，它将被覆盖。

```
$ sort > sorted.txt
$ cat sorted.txt
a
b
c
d
e
```

要将命令的输出追加到文件，使用双大于号 `>>` 后跟文件名。如果文件不存在，它将被创建。如果它已存在，输出将被追加到其中。

```
$ sort >> sorted.txt
$ cat sorted.txt
a
b
c
d
e
```

要从文件重定向命令的输入，使用小于号 `<` 后跟文件名。文件的内容将用用作标准输入。

```
$ sort < test.txt
a
b
c
d
```

重定向命令的输出到文件，使用大于号 `>` 后跟文件名。如果文件不存在，它将被创建。如果它已存在，它它覆盖。

重重重重重到文件。

```
$ sort > sorted.txt
$ cat sorted.txt
a
b
c
d
e
```

重定向命令的输入从文件，使用小于号 `<` 后跟文件名。文件的内容将用用作标准输入。

```
$ sort < test.txt
a
b
c
d
```

。你也可以同时重定向输入和输出。下面的示例演示了从 `test.txt` 重定向输入并将输出重定向到 `sorted.txt`。

```
$ sort < test.txt
重定向到重定向。
```

### 表 35：重定向 I/O

| 操作符 | 格式 | 动作 |
| :--- | :--- | :--- |
| > | `cmd > file` | 创建或覆盖文件标准输出。 |
| >> | `cmd >> file` | 创建或追加文件标准输出。 |
| < | `cmd < file` | 使用文件作为标准输入。 |

默认情况下，输入重定向操作描述符 `0`，输出重定向操作描述符 `1`。你可以通过紧跟操作符的声明文件描述符。如果文件描述符没有紧跟操作符，它将被解释为命令行上的另一个项。

为了将错误消息重定向到文件而将标准输出显示在你的屏幕上，使用 `2>`。你也可以将输出重定向到另一个文件。

```
$ ls test.txt no-such-file

ls: cannot access no-such-file: No such directory

test.txt

$ ls test.txt no-such-file 2>errors

test.txt

$ cat errors

ls: cannot access no-such-file: No such directory

$ ls test.txt no-such-file 1>normal-output 2>errors

$ cat normal-output

test.txt

$ cat errors

ls: cannot access no-such-file: No such directory

$
```

不仅你可以将输出重定向到文件，你还可以使用 `&` 号后跟文件描述符将其重定向到另一个文件描述符。使用这种方法，你可以使用 `2>&1` 合并标准输出和标准错误。不要使用空格。

输出意味着，“将 `ls` 命令的标准输出发送到 `combined-output` 文件”。等等，“将 `ls` 命令的标准输出发送到 `combined-output` 文件并追加标准错误到标准输出。”所有输出都将发送到 `combined-output` 文件，因为标准错误被重定向到了标准输出，而标准输出被重定向到了 `combined-output`。

```
$ ls test.txt no-such-file > combined-output 2>&1

$ cat combined-output

ls: cannot access no-such-file: No such directory

test.txt

$
```

如果你不想将命令的输出显示在你的屏幕上或将其保存到文件中，你将输出重定向到空设备 `/dev/null`。这个特殊文件简单地丢弃任何发送到它的输入。空设备有时被称为“黑洞”或“比特桶”。下面的示例将 `sort` 的错误重定向到空设备。

```
$ ls test.txt no-such-file

ls: cannot access no-such-file: No such directory

test.txt

$ ls test.txt no-such-file 2>/dev/null

test.txt

$
```



## 第 11 章 额外的命令行概念

环境变量是一个键值对。程序可以使用环境变量中的数据来决定在某些情况下的行为。例如，可以通过通过设置 `PAGER` 环境变量的值来更改用于显示帮助页（man pages）的默认命令。

环境变量是大小写敏感的；但按照惯例，它们使用大写字母。要查看已知环境变量的值，请运行 `echo $VAR_NAME` 或 `printenv VAR_NAME`。你可以不带参数地使用 `env` 或 `printenv` 命令来显示当前设置的所有环境变量。

```
$ echo $HOME

/home/jason

$ printenv HOME

/home/jason

$ printenv

SHELL=/bin/bash

TERM=xterm

USER=jason

MAIL=/var/mail/jason

PATH=/usr/local/bin:/usr/bin:/usr/local/games:/usr

PWD=/home/jason

LANG=en_US.UTF-8

PS1=$

SHLV=1

HOME=/home/jason

LOGNAME=jason

OLDPWD=/home/jason

$ env

SHELL=/bin/bash

TERM=xterm

USER=jason

MAIL=/var/mail/jason

PATH=/usr/local/bin:/usr/bin:/usr/local/games:/usr

PWD=/home/jason

LANG=en_US.UTF-8

PS1=$

SHLV=1

HOME=/home/jason

LOGNAME=jason

OLDPWD=/home/jason

$
```

当启动一个进程时，它会继承父进程导出的环境变量。仅设置的环境变量只会影响当前运行的进程，除非显式地导出（`export`）。在下面的示例中，`PAGER` 环境变量被设置为当前 shell 的 `less`。如果在没有导出该变量的情况下启动了子进程（例如另一个 Bash shell 实例），则该环境变量不会被继承。当导出了 `PAGER` 并启动新的 Bash shell 时，该变量对该进程可用。要删除一个环境变量，请使用 `unset` 命令。

```
$ echo $PAGER

$ PAGER=less

$ echo $PAGER

less

$ bash

$ echo $PAGER

$ exit

exit

$ export PAGER=less

$ bash

$ echo $PAGER

less

$ exit

exit

$ echo $PAGER

less

$ unset

$ echo $PAGER
```

| 变量 | 用途 |
| :--- | :--- |
| `EDITOR` | 用于编辑文件的程序。 |
| `HOME` | 用户的家目录。 |
| `LOGNAME` | 当前用户的 ID 或登录 ID。 |

表 36: 常用环境变量

| 变量 | 用途 |
| :--- | :--- |
| `MAIL` | 用户在本地系统上的邮箱位置。 |
| `OLDPWD` | 旧的或上一个工作目录。 |
| `PATH` | 命令的搜索路径。 |
| `PAGER` | 用于分页查看文件的程序。 |
| `PS1` | 主提示符字符串。 |
| `PWD` | 当前工作目录。 |
| `USER` | 当前用户的 ID 或登录 ID。 |

### 别名 (Aliases)

你可以在命令行中使用称为别名（aliases）的键盘快捷键。通过为经常重复使用、很长、难以输入或难以记忆的命令创建别名，你可以节省一些时间。你可以使用别名来修复常见的拼写错误。有些人使用别名让 Linux 的行为变得像他们熟悉的另一种操作系统一样。

`alias [alias_name=[value]]` 不带任何参数时，`alias` 命令会列出环境中的别名。因此使用 `alias alias_name=value` 来创建一个新的别名。

`unalias alias_name` 删除 `alias_name`。使用 `unalias -a` 删除所有别名。

```
$ alias ls='ls -l'

$ alias

alias ls='ls -l'

$ ls -l

total 32

drwxr-xr-x 2 jason 4096 Jun 21 22:01 Desktop

drwxr-xr-x 2 jason 4096 Jun 21 22:01 Documents

drwxr-xr-x 2 jason 4096 May 17 13:37 Downloads

-rw-rw-r-- 1 jason 274 Jun 28 14:52 goals.txt

drwxr-xr-x 3 jason 4096 Jun 21 22:05 Music

drwxr-xr-x 2 jason 4096 Jun 21 22:01 Pictures

-rw-rw-r-- 1 jason 73 Jun 29 02:30 to-do.txt

$ ls -l

total 32

drwxr-xr-x 2 jason 4096 Jun 21 22:01 Desktop

drwx-xr-x 2 jason 4096 Jun 21 22:01 Documents

drwx-xr-x 2 jason 4096 May 17 13:37 Downloads

-rw-rw-r-- 1 jason 274 Jun 28 14:52 goals.txt

drwx-xr-x 3 jason 4096 Jun 21 22:05 Music

drwx-xr-x 2 jason 4096 Jun 21 22:01 Pictures

-rw-rw-r-- 1 jason 73 Jun 29 02:30 to-do.txt

$ alias=$usr/local/bin/backup-database.sh

$ $
```

开始数据库备份。
...
Database backup complete.

```
$ alias

alias bu=$usr/local/bin/backup-database.sh

alias ll='ls -l'
```

别名仅对你的当前会话有效。因此，如果你创建了一个别名、注销并重新登录，该别名将不可用。要让它们在会话之间持久化，需要将其放入初始化文件。

### 实例化文件 (Initialization Files)

为了在会话之间持久化别名，需要将它们保存在初始化文件中。要保存这些命令，需要将它们保存在 `.bashprofile`。通常 Bash 会使用 `source` 命令读取并执行文件 `.bashrc`。如果你想在执行之前检查它，可以使用 `if` 语句检查文件是否存在。

```
$ cat ~/.bashprofile

if -f ~/.bashrc ]; then

  source ~/.bashrc

fi

# source11 
```
```bash
$ echo "alias11='ls -l'" >> ~/.bashrc
# 以 # 号开头的行是注释。
# 将自定义内容放入文件。
```
```bash

$ cat ~/.bashrc

# 以 # 号开头的行是注释。

# 将自定义内容放入文件。

alias11='ls -l'

$ source11

$ alias11

ls -l

$
```

### Shell 历史 (Shell History)

你在命令行执行的命令保存在 shell 历史中。你的历史保留内存中，直到会话结束。此时，历史会被保存到 `.bash_history`。不同的 shell 使用不同的文件，但它们通常包含命令。你可以设置 `HISTSIZE` 环境变量来控制保存到历史中的命令数量。默认值为 500。当 `history` 命令不带参数执行时，它会显示历史命令列表。

`!N` 重复第 N 行命令。

`!!` 重复上一条命令。

`!pattern` 重复以 pattern 开头的最近一次命令。

```
$ history

1 ls

2 diff random-states random-states.bak

3 history

$ !

1 ls

2 diff random-states random-states.bak

$ echo $SHELL

/bin/bash

$ !!

echo $SHELL

/bin/bash

$ id

id=jason
```

你可以通过输入 Ctrl-r 来搜索 shell 历史。这会启动一个反向搜索，用 (reverse-i-search) ':' 表示，并允许你输入历史命令的一部分来检索。通过遍历历史中匹配搜索内容的其他命令，继续按 Ctrl-r。当你找到想要执行的命令时，按回车。如果你想在执行之前更改命令行，请按 Esc。要完全放弃反向搜索，输入 Ctrl-c。

```
$ diff random-states random-states.bak

3c3

< Georgia Atlanta

---

> Georgia Savannah

(reverse-i-search)'di': diff random-states random-states.bak

3c3

< Georgia Atlanta

---

> Georgia Savannah $
```

### Tab 补全 (Tab Completion)

要调用补全功能，只需输入命令并按 Tab 键。补全尝试完成部分输入的命令。如果有多种可能性，按两次 Tab 可以显示这些选项。你可以随时继续输入并按 Tab 。

除了补全命令外，你可以使用 Tab 补全来完成文件名和目录名。当文件或目录作为 `ls`, `cat`, `rm` 等命令的参数使用时，这非常有用。

```
### 输入 jo[Tab][Tab] 结果为：

$ jo

jobs join
```

```
[1]+ Running      ./db-backup.sh &
$ ls r*

random-states random-states.bak

### 输入 cat[Space][Tab][Enter] 导致：

$ cat random-states

Tennessee Nashville

Wyoming Cheyenne

Indiana Indianapolis

Indiana Indianapolis

Arizona Phoenix

Colorado Denver

Indiana Indianapolis

Georgia Atlanta

$
```

### 续行 (Line Continuation)

如果你想创建一个视觉上跨越多行但作为单个命令的命令行，请在每个需要延续的行末尾使用反斜杠 `\`。当反斜杠出现在命令行的末尾时，它充当续行符。如果你在命令提示符处使用它，延续的行将以大于符号 `>` 前缀。你在阅读文档或检查 shell 脚本时可能会遇到这种情况。

```
$ diff \\
> random-states \\
> random-states.bak

3c3

< Georgia Atlanta

---

> Georgia Savannah

$ diff random-states random-states.bak

3c3

< Georgia Atlanta

---

> Georgia Savannah

$ 
```

## 第 12 章 进程与作业 (Processes and Jobs)

`ps` 命令用于列出 Linux 系统上当前运行的进程。如果你在不带任何参数的情况下运行 `ps`，它将显示以你身份运行并与你的终端相关的进程。如果你两次连接到 Linux 服务器，你将看到 `ps` 命令的不同输出。对于第一个会话，可能会看到以下内容，它使用的是 `pts/0`（伪终端 0）。

```
$ ps

PID TTY         TIME CMD

1309 pts/0     00:00:00 bash

1635 pts/0     00:00:00 ps
```

以下是第二次连接时 `ps` 的输出，它使用的是 `pts/1`。

```
$ ps

PID TTY         TIME CMD

1721 pts/1     00:00:00 bash

1821 pts/1     00:00:00 ps
```

如果你想显示所有运行的进程，无论关联的终端或锁，请使用命令 `ps -u username`。

```
$ ps -u jason

PID TTY         TIME CMD

1308 ?           00:00:00 sshd

1309 pts/0     00:00:00 bash

1720 ?           00:00:00 sshd

1721 pts/1     00:00:00 bash
```

要查看系统上运行的每一个进程，使用命令 `ps -e`。

```
$ ps -e | head

PID TTY         TIME CMD

1 ?             00:00:00 init

2 ?             00:00:00 kthread

3 ?             00:00:00 ksoftirqd/0

6 ?             00:00:00 migration/0

7 00:00:00 watchdog/0

8 00:00:00 cuset

9 00:00:00 khelper

10 00:00:00 kdevmpfs

11 00:00:00 netns
```

默认情况下，`ps` 提供的信息相当稀疏。通常在在使用 `ps` 时，你会提供额外的参数来显示更详细的信息。以下是与 `ps` 配合使用的一些常用选项。

### 表 37：常用的 PS 选项

| 选项 | 说明 |
|---|---|
| `-e` | 显示所有进程。 |
| `-f` | 使用完整格式列表。 |
| `-u <username>` | 显示用户的进程。 |
| `-p <PID>` | 显示进程 ID (PID) 的进程信息。 |
| `-H` | 以层级结构（树形）显示进程。 |
| `--forest` | 使用 ASCII 艺术以层级结构显示进程。 |

下表说明了组合上述选项的一些实用方法。

### 表 38：常用的 PS 命令

| 命令 | 说明 |
|---|---|
| `ps -e` | 显示所有进程。 |
| `ps -ef` | 使用完整格式列表显示所有进程。 |
| `ps -EH` | 以树形格式显示所有进程。 |
| `ps -e -forest` | 使用 ASCII 艺术以树形格式显示进程。 |
| `ps -u <username>` | 显示用户运行的进程。 |
| `ps -fp <PID>` | 为进程 ID (PID) 显示完整格式列表。 |

以下演示了各种 `ps` 命令的输出。

```
$ ps

PID TTY TIME CMD

1309 pts/0 00:00:00 bash

2096 pts/0 00:00:00 ps

$ ps -f

UID PID PPID C TIME TTY TIME CMD

jason 1309 1308 0 15:15 pts/0 00:00:00 -bash

jason 2102 1309 0 15:45 pts/0 00:00:00 ps -f

$ ps -1309

PID TTY TIME CMD

1309 pts/0 00:00:00 bash

$ ps -fp 1309

UID PID PPID C TIME TTY TIME CMD

jason 1309 1308 0 15:15 pts/0 00:00:00 -bash

$ ps -e | head

PID TTY TIME CMD

1 ? 00:00:00 init

2 ? 00:00:00 kthread

3 ? 00:00:00 ksoftirqd/0

6 ? 00:00:00 migration/

7 ? 00:00:00 watchdog/0

8 ? 00:00:00 cuset

9 ? 00:00:00 khelper

10 ? 00:00:00 kdevmps

11 ? 00:00:00 netns

$ ps -11 | head

UID PID PPID C TIME TTY TIME CMD

root 1 0 0 15:14 ? 00:00:00 /sbin/init

root 2 0 0 15:14 ? 00:00:00 [kthread]

root 3 2 0 15:14 ? 00:00:00 [ksoftirqd/0]

root 6 2 0 15:14 ? 00:00:00 [migration/0]

root 7 2 0 15:14 ? 00:00:00 [watchdog/0]

root 8 2 0 15:14 ? 00:00:00 [cuset]

root 9 2 0 15:14 ? 00:00:00 [khelper]

root 10 2 0 15:14 ? 00:00:00 [kdevtmpfs]

root 11 2 0 15:14 ? 00:00:00 [netns]

$ ps -fu www-data

UID PID PPID C TIME TTY TIME CMD

www-data 1060 1057 0 15:15 ? 00:00:00 /usr/sbin/apache2 -k start

www-data 1061 1057 0 15:15 ? 00:00:00 
```

```bash

$ ps

PID TTY TIME CMD

1309 pts/0 00:00:00 bash

2096 pts/0 00:00:00 ps

$ ps -f

UID PID PPID C TIME TTY TIME CMD

jason 1309 1308 0 15:15 pts/0 00:00:00 -bash
```



`jason 2102 1309 0 15:45 pts/0 00:00:00 ps -f`

`$ ps -1309`

```
PID TTY TIME CMD
1309 pts/0 00:00:00 bash
```

`$ ps -fp 1309`

```
UID PID PPID C TIME TTY TIME CMD
jason 1309 1308 0 15:15 pts/0 00:00:00 -bash
```

`$ ps -e | head`

```
PID TTY TIME CMD
1 ? 00:00:00 init
2 ? 00:00:00 kthread
3 ? 00:00:00 ksoftirqd/0
6 ? 00:00:00 migration/
7 ? 00:00:00 watchdog/0
8 ? 00:00:00 cuset
9 ? 00:00:00 khelper
10 ? 00:00:00 kdevmps
11 ? 00:00:00 netns
```

`$ ps -11 | head`

```
UID PID PPID C TIME TTY TIME CMD
root 1 0 0 15:14 ? 00:00:00 /sbin/init
root 2 0 0 15:14 ? 00:00:00 [kthread]
root 3 2 0 15:14 ? 00:00:00 [ksoftirqd/0]
root 6 2 0 15:14 ? 00:00:00 [migration/0]
root 7 2 0 15:14 ? 00:00:00 [watchdog/0]
root 8 2 0 15:14 ? 00:00:00 [cuset]
root 9 2 0 15:14 ? 00:00:00 [khelper]
root 10 2 0 15:14 ? 00:00:00 [kdevtmpfs]
root 11 2 0 15:14 ? 00:00:00 [netns]
```

`$ ps -fu www-data`

```
UID PID PPID C TIME TTY TIME CMD
www-data 1060 1057 0 15:15 ? 00:00:00 /usr/sbin/apache2 -k start
www-data 1061 1057 0 15:15 ? 00:00:00
```

### 作业 (Jobs)

默认情况下，当你从命令行中执行一个程序时，它在前台运行。许多命令运行时间从几分之一到几秒不等。然而，你可能想在后台执行一个程序并继续工作。要在后台启动程序，请在命令末尾加上 `&`。这些后台程序和进程通常被称为作业 (jobs)。

当程序在后台启动时，在显示新提示符之前会返回两个数字。这两部分信息是作业号（在括号 `[]` 中）和进程 ID (PID)。可以通过前面的百分号 `%` 来引用作业号。以下示例演示了在后台启动多个进程。

```
$ ./long-running-proc &
[1] 2793
$ ./long-running-proc &
[2] 2795
$ ./long-running-proc &
[3] 2807
$ ./long-running-proc &
[4] 2809
$ jobs
[1] Done /long-running-proc &
[2] Running /long-running-proc &
[3]- Running /long-running-proc &
[4]+ Running /long-running-proc &
```

`top` 命令将位于任何 Linux 系统上；然而，你可能需要安装 `top` 来查看。在 `ps` 命令的输出中，你会注意到 `+` 号和 `-` 号。`+` 号表示当前作业，而 `-` 号被认为是上一个作业。当前作业是最后一个在后台启动的任务，或者是最近一个在前台运行期间被停止的进程。你可以使用双百分号（`%%` 或百分号后加加号 `+`）来引用当前作业。可以使用百分号后加减号 `-` 来访问上一个作业。在使用 `fg` 和 `bg` 命令时，除非显式指定了不同的作业，否则将操作当前作业。

在 `jobs` 命令的上述输出中，作业号 1 被报告为已完成（done），而其他作业处于运行（running）状态。shell 会在显示新提示符之前报告作业状态。shell 不会中断你当前的命令行（即使它是空闲）来报告作业已完成。要显示新提示符，请按回车键。如果你的任何作业已完成，将在你的新提示符出现前显示状态。以下是该行为的示例。

```
$ <ENTER>
$ <ENTER>
[2] Done ./long-running-proc &
$ jobs
[3]- Running ./long-running-proc &
[4]+ Running ./long-running-proc &
$
```

要将作业返回到前台，请使用 `fg` 命令后跟百分号和作业号。执行相同任务的简便方法是在命令行上输入百分号后跟作业号。因此，`fg %2` 和 `%2` 是等价的。

记住当前作业可以通过 `%%` 或 `%+` 引用。此外，除非提供了另一个作业，否则 `fg` 命令对当前作业操作。以下四个命令是相同的。

```
$ fg
$ fg %%
$ fg %+
$ %%
```

以下演示了将作业号三 调入前台。

```
$ jobs
[3]- Running ./long-running-proc &
[4]+ Running ./long-running-proc &
$ fg %3
./long-running-proc &
```

要暂停或挂起前台进程，请输入 Ctrl-z。被挂起的作业可以在后台或前台恢复。要在后台恢复挂起的作业，请输入作业规范后跟一个和符号（&），或使用 `bg` 命令后跟该规范。如果你想让最近一次挂起的进程在后台运行，可以省略作业规范，因为 `bg` 将对当前作业操作。要在前台恢复作业，使用 `fg` 命令或直接输入作业规范。以下演示了这些方法。

```
$ jobs
[1] Running /long-running-proc &
[2] Running /long-running-proc &
[3]- Running /long-running-proc &
[4]+ Running /long-running-proc &
$ %2
./long-running-proc
^Z
[2]+ Stopped /long-running-proc
$ fg %3
./long-running-proc
^Z
[3]+ Stopped /long-running-proc
$ jobs
[1] Running /long-running-proc &
[2]- Stopped /long-running-proc &
[3]+ Stopped /long-running-proc &
[4] Running /long-running-proc &
$ bg
[3]+ /long-running-proc &
$ jobs
[1] Running /long-running-proc &
[2]+ Stopped /long-running-proc &
[3] Running /long-running-proc &
[4]- Running /long-running-proc &
$
```

要杀死一个在前台运行的作业，请使用 Ctrl-c。要杀死一个已后台化的作业，请使用 `kill` 命令。`kill` 命令接受作业规范或进程 ID（PID）作为参数。除了作业号外，要出 PID 请使用 `jobs` 命令的 `-l` 选项。

```
$ jobs
[1] Running /long-running-proc &
[2] Running /long-running-proc &
[3]- Running /long-running-proc &
[4]+ Running /long-running-proc &
$ fg %1
```

```
./.long-running-proc
^C$ jobs
[2] Running      ./long-running-proc &
[3]- Running      ./long-running-proc &
[4]+ Running      ./long-running-proc &
$ kill %3
[3]- Terminated   ./long-running-proc
$ jobs -l
[2]- 2914 Running  ./long-running-proc &
[4]+ 2918 Running  ./long-running-proc &
$ kill 2914
[2]- Terminated   ./long-running-proc
$
```

`kill` 命令向运行中的进程发送信号。然而，默认信号是终止（termination）。终止信号被称为 SIGTERM 或简称为 TERM。要显示信号列表及其对应的数字，请使用 `kill -1` 命令。要向进程发送特定信号，请在 `kill` 命令后跟上一个连字符和信号名称或数字。

```
$ kill -1 | grep SIGTERM
11) SIGSEGV 12) SIGUSR2 13) SIGPIPE 14) SIGALRM 15) SIGTERM
$ kill 123
$ kill-SIGTERM 234
$ kill -TERM 345
$ kill -15 456
```

如果进程在发送 TERM 信号后没有终止，请使用 KILL 信号。SIGKILL 对应的数字是 9。

```
$ ps | grep cannot-stop-me
2994 pts/1 00:00:00 cannot-stop-me
$ kill 2994
$ ps | grep cannot-stop-me
2994 pts/1 00:00:00 cannot-stop-me
$ kill -9 2994
$ ps | grep cannot-stop-me
$
```

## 第 13 章 切换用户

在命令行切换用户，使用 `su` 命令。在不带任何参数的情况下，`su` 将切换到超级用户账户，也称为 root。或者，你可以执行 `su root`。切换用户不会改变你当前的工作目录或环境变量，除非你在 `su` 后面指定一个连字符（hyphen）。通过指定连字符，你模拟了作为该用户登录系统。例如，`su - root`。

`su [username]` 切换到用户名或成为超级用户。

常用的 `su` 选项：

- `-` 连字符用于提供一个与用户直接登录时所预期的环境。
- `su -c command` 指定一个要执行的命令。如果命令长于一个单词，则需要加引号。

```
$ su - root
$ su - username
```

### Sudo 用

`sudo` 命令允许用户以另一个用户（通常是超级用户）身份执行命令。使用 `sudo` 替代 `su` 的一个优势是你不需要知道 root 密码，并且对哪些命令可以执行有完全的控制权。`su` 命令与 `sudo` 类似，但你应该注意这些差异：`su`（切换用户）请求新用户的密码，而 `sudo` 请求当前用户的密码，或者可能不需要密码。

如果你想知道自己是哪个用户，请运行 `whoami` 命令。

### 使用 Sudo

以下是使用 `sudo` 命令的常用方法。

- `sudo -l` 列出可以使用 sudo 执行的可用命令。
- `sudo command` 以超级用户身份执行命令。
- `sudo -u root` 与 sudo 命令相同。
- `sudo -u user` 以用户身份执行命令。
- `sudo su` 切换到超级用户账户。
- `sudo su -` 切换到超级用户账户，并提供用户登录时预期的环境。
- `sudo su - username` 切换到用户名账户，并提供以该用户名登录时预期的环境。

```
$ sudo -l
User user may run the following commands on this host:
(root) NOPASSWD: /etc/init.d/apache2
(fred) NOPASSWD: /opt/fredsApp/bin/start
(fred) NOPASSWD: /opt/fredsApp/bin/stop
(root) /bin/su - oracle
$ sudo /etc/init.d/apache2 start
* Starting web server apache2
$ sudo -u fred /opt/fredsApp/bin/start
Fred's app started as user fred.
$ sudo su - oracle
[sudo] password for jason
oracle@linuxsvr~$ whoami
oracle
oracle@linuxsvr~$ exit
$ whoami
jason
$
```

`sudo -l` 的输出显示可以使用 sudo 执行哪些命令以及使用哪个账户。在上例中，对于带有 NOPASSWD 前缀的命令，sudo 不会提示密码。这种配置可能用于通过 cron 自动执行需要提升权限的任务。

# 第14 章 安装软件

在 Linux 系统上安装软件最常见的方法是通过使用软件包。软件包不仅包含安装在系统上的文件，还包含了称为元数据（metadata）的附加信息。这些元数据可以包括此类信息：以预安装和安装后脚本形式提供的完成安装所需的步骤、每个文件的权限信息、软件包的描述、版本、软件包维护者，以及为了正常运行所需的任何额外软件包。

要安装、升级或删除软件包，请使用包管理器。当你告诉包管理器安装给软件包时，它不仅会安装该包，还会根据软件包的元数据安装任何其他所需的包（称为依赖项）。包管理器还维护着软件包信息数据库。包管理器记录了安装了哪些软件包、安装了哪些版本以及哪些文件属于哪些软件包。

### 基于 RPM 的发行版

RPM 是 RPM Package Manager（RPM 包管理器）的递归缩写；但它最初是 RedHat Package Manager。基于 RPM 的发行版包括 Red Hat Linux (RHEL)、CentOS、Fedora、Oracle Linux 和 Scientific Linux。你可以直接使用 `rpm` 命令操作 RPM 软件包，也可以使用另一个名为 `yum` 的命令行工具。

- `yum search-pattern` 搜索 search-pattern。
- `yum install [-y] package` 安装 package。使用 -y 选项对你的问题回答“yes”。
- `yum remove package` 或卸载 package。
- `yum info [package]` 显示有关软件包的信息。

要搜索可用软件，请使用 `yum search search-pattern`。

```
yum search web browser
Loaded plugins: refresh-packagekit, security
============================ N/S Matched: web, browser ====================
icedtea-web.i686 : OpenJDK Java 浏览器的额外 Java 组件
      : 插件和 Web Start 实现
elinks.i686 : 文本模式 Web 浏览器
firefox.i686 : Mozilla Firefox Web 浏览器
lynx.i686 : 文本式 Web 浏览器
仅匹配名称和摘要，使用 "search all" 匹配所有。
```

```
$ yum search firefox
Loaded plugins: refresh-packagekit, security
==================================== N/S Matched: firefox ====================
firefox.i686 : Mozilla Firefox Web 浏览器
```

仅匹配名称和摘要，使用 "search all" 匹配所有。
$
```

要安装软件，请使用命令 `yum install package`。安装软件需要超级用户权限。在安装或删除软件之前，使用 `sudo` 或通过 `su` 命令切换到 root 账户。

```
$ sudo yum install firefox
Loaded plugins: refresh-packagekit, security
Setting up Install Process
Resolving Dependencies
--> Running transaction check
--> Package firefox.i686 0:24.5.0-1.el16.centos will be installed
--> Finished Dependency Resolution
```

依赖关系已解析

| Package | Arch | Version | Repository | Size |
|-------|------|---------|------------|------|
| firefox | i686 | 24.5.0-1.el16.centos | updates | 47 M |

事务摘要

安装 1 个 软件包

总下载大小: 47 M

安装大小: 80 M

此操作是否允许 [y/N]: y

正在下载软件包:



```
firefox-24.5.0-1.el16.centos.i686.rpm | 47 MB 00:14
Running rpm_check_debug
Running Transaction Test
Transaction Test Succeeded
Running Transaction
Installing : firefox-24.5.0-1.el16.centos.i686 1/1
```

```
Verifying : firefox-24.5.0-1.el66.centos.i686 1/1

Installed:
firefox.i686 0:24.5.0-1.el16.centos

Complete!
$
```

要卸载软件包，请使用命令 `yum remove package`。与安装软件一样，卸载软件需要超级用户权限。

```
$ sudo yum remove firefox
Loaded plugins: refresh-packagekit,
Setting up Remove Process
Resolving Dependencies
--> Running transaction check
--> Package firefox.i686 0:24.5.0-1.el16.centos will be erased
--> Finished Dependency Resolution
```

依赖关系已解析

| Package | Arch | Version | Repository | Size |
|---|---|---|---|---|
| Removing: firefox | i686 | 24.5.0-1.el16.centos | @updates | 80 M |

事务摘要

删除 1 个 软件包

安装大小: 80 M

此操作是否允许 [y/N]: y

正在下载软件包:

Running rpm_check_debug

Running Transaction Test

Transaction Test Succeeded

Running Transaction

```
Erasing : firefox-24.5.0-1.el16.centos.i686 1/1
Verifying : firefox-24.5.0-1.el16.centos.i686 1/1
```

Removed:

firefox.i686 0:24.5.0-1.el16.centos

Complete!

$
```

## 使用 rpm 命令

你也可以通过 `rpm` 命令与 RPM 包管理器交互。

- `rpm -qa` 列出所有已的软件包。
- `rpm -qf /path/to/file` 列出包含 file 的软件包。
- `rpm -ivh package.rpm` 安装名为 `package.rpm` 的软件包。

```
$ rpm -qa | sort | head

acl-2.49.el16.i686

acpid-1.0.10.el16.i686

aic94xx-firmware-30.el16.noarch

alsa-lib-1.0.22.el16.i686

alsa-plugins-pulsaudio-1.0.21.el16.i686

alsa-utils-1.0.22.el16.i686

anaconda-3.215-1.0.el16.centos.i686

anaconda-yum-plugins-1.0-5.el16.noarch

apache-tomcat-apis-0.1-el16.noarch

apr-1.3.9-5.el2.26

$ rpm -qf /usr/bin/sudo

sudo-1.8.63p-12.el16.i686

$ sudo rpm -ivh SpiderOak-5.1.3-1.i386.rpm

Preparing...

########################### [100%]

1:SpiderOak ########### [100%]

$ rpm -ql sudo | head

/etc/pam.d/sudo

/etc/pam.d/sudo-i

/etc/sudo-ldap.conf

/etc/sudo.conf

/etc/sudoers

/etc/sudoers.d

/usr/bin/sudo

/usr/bin/sudoedit

/usr/bin/sudoreplay

$
```

## 基于 DEB 的发行版

基于 Debian 的 Linux 发行版使用 DEB 软件包格式。流行的 Debian 发行版包括 Debian、Elementary OS、Linux Mint 和 Ubuntu。基于 Debian 的发行版的包管理器称为 APT，即高级软件包工具。APT 被拆分为几个小命令。最常用的 APT 命令是 `apt-cache` 和 `apt-get`。

- `apt-cache search search-pattern` 搜索 `search-pattern`。
- `apt-get install [-y] package` 安装 `package`。使用 `-y` 选项对你的问题回答“yes”。
- `apt-get remove package` 或卸载 `package`。
- `apt-cache show [package]` 显示有关软件包的信息。

要搜索可用软件，请使用 `apt-cache search search-pattern`。

```
$ apt-cache search web browser

Loaded plugins: refresh-packagekit, security

============================ N/S Matched: web, browser ====================

icedtea-web.i686 : OpenJDK Java 浏览器的额外 Java 组件

      : 插件和 Web Start 实现

elinks.i686 : 文本模式 Web 浏览器

firefox.i686 : Mozilla Firefox Web 浏览器

lynx.i686 : 文本式 Web 浏览器

仅匹配名称和摘要，使用 "search all" 匹配所有。

$ apt-cache search firefox

Loaded plugins: refresh-packagekit, security

==================================== N/S Matched: firefox ====================

firefox.i686 : Mozilla Firefox Web 浏览器

```

仅匹配名称和摘要，使用 "search all" 匹配所有。
$
```

要安装软件，请使用命令 `apt-get install package`。安装软件需要超级用户权限。在安装或删除软件之前，使用 `sudo` 或通过 `su` 命令切换到 root 账户。

```
$ sudo apt-get install firefox
Reading package lists...
Building dependency tree
Reading state information...
The following NEW packages will be installed:
libdbusmenu-gtk4 xul-ext-ubox firefox
After this operation, 82.4 MB of additional disk space will be used.
Do you want to continue [Y/n]? y
Fetching archive...
Get:1 http://archive.ubuntu.com/ubuntu/precise-updates/main libdbusmenu-gtk4 amd64 0.6.2-ubuntu.2 [31.2 KB]
Get:2 http://archive.ubuntu.com/ubuntu/precise-updates/main firefox amd64 29.0+build1-ubuntu.12.4 [36.0 MB]
Get:3 http://archive.ubuntu.com/ubuntu/precise-updates/main xul-ext-ubox all 2.7-ubuntu0.12.4 [5.8 KB]
Fetched 36.1 MB in 23s (153 KB/s)
Selecting previously unselected package libdbusmenu-gtk4
(Reading database ... 102882 files and directories currently installed)
Unpacking libdbusmenu-gtk4
Selecting previously unselected package firefox
Unpacking firefox
Selecting previously unselected package xul-ext-ubox
Unpacking xul-ext-ubox
Processing triggers for desktop-file-utils...
```

```json
Setting up libdbusmenu-gtk4 (0.6.2-ubuntu.2)
Setting up firefox (29.0+build1-ubuntu.12.4) ...
```

update-alternatives: using /usr/bin/firefox to provide /usr/bin/gnome-www-browser (gnome-www-browser) in auto mode.

update-alternatives: using /usr/bin/firefox to provide /usr/bin/x-www-browser (x-www-browser) in auto mode.

请重启所有运行中的 firefox 实例，否则您将遇到问题。

正在设置 xul-ext-ubufox (2.7-ubuntu0.12.04.1) ...

正在处理 lib-nsl-lconfig 触发器，现在正在延迟处理

$
```

要卸载软件包，请使用命令 `apt-get remove package`。与安装软件一样，移除软件需要超级用户权限。

```
$ sudo apt-get remove firefox
Reading package lists... Done
Building dependency tree
Reading state information... Done
以下软件包将被移除：
firefox
0 个已升级，0 个新安装，1 个要移除，193 个未升级。
执行此操作后，将释放 81.8 MB 的磁盘空间。
您确定要继续吗 [Y/n]? y
(正在读取数据库 ... 目前已安装 10324 个文件和目录)
正在移除 firefox ...
正在处理 man-db 触发器 ...
正在处理 desktop-file-utils 触发器 ...
正在处理 bamdaemon 触发器 ...
正在重建 /usr/share/applications/bamf.index ...
正在处理 gnome-menus 触发器 ...
$
```

## 使用 dpkg 命令

除了 APT 工具，您还可以使用 `dpkg` 命令直接与包管理器交互。

- `dpkg -l`: 列出所有已安装的软件包。
- `dpkg -S /path/to/file`: 列出包含该文件的软件包。
- `dpkg -i package.deb`: 安装名为 `package.deb` 的文件包。
- `dpkg -L package`: 列出所有属于该软件包的文件。

```
$ dpkg -l | head
Desired=Unknown/Install/Remove/Purge/Hold
| Status=Not/Inst/Conf-files/Unpacked/half-inst/conf/Half-inst/trig-aWait/Trig-pend
// Err?=(none)/Reinst-required (Status,Err: uppercase=bad)
||/ Name Version Description
+++======================================================
ii accountservice 0.6.15-2ubuntu.9 query and manipulate user information
ii acpid 1.2.0.10-1ubuntu3 Advanced Configuration and Power Interface event daemon
ii adduser 3.11ubuntu2 add and remove users and groups
ii adium-theme-ubuntu 0.3.2-0ubuntu1 Adium message style for Ubuntu
ii alsa-base 1.0.25+dfsg-ubuntu1.1 ALSA driver configuration
```

```
$ dpkg -s /usr/bin/sudo
sudo: /usr/bin/sudo is not found (Wait, the original says $ dpkg -s /usr/bin/sudo, let's stick to text text)
$ sudo dpkg -i spiderok_5.1.3_i386.deb
Previously selected package spiderok.
(正在读取数据库 ... 目前已安装 153942 个文件和目录.)
正在解包 spiderok (from spiderok_5.1.3_i386.deb) ...
正在设置 spiderok (1:5.3) ...
正在处理 man-db 触发器 ...
正在处理 desktop-file-utils 触发器 ...
正在处理 bamdaemon 触发器 ...
正在重建 /usr/share/applications/bamf.index ...
正在处理 gnome-menus 触发器 ...
$ dpkg -l sudo | head
/
```

```
/etc
/etc/sudoers.d
/etc/sudoers.README
/etc/pam.d
/etc/pam.d/sudo
/etc/sudoers
/etc/init.d
/etc/init.d/sudo
/usr
$
```
