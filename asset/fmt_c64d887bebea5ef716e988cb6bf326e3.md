
你应该注意另外两个语句：`break` 语句和 `exit` 语句。`break` 语句可以终止迭代循环，如 `for`、`until` 或 `repeat`。`exit` 语句可以退出 Shell 程序。你可以可选地在 `exit` 后面使用一个数字。如果当前 Shell 程序是由另一个程序调用的，调用程序可以检查 `$?` 并此做出决定。

# 在 Shell 脚本中使用函数

与其他语言一样，Shell 程序也支持函数。函数是执行特定过程的 Shell 程序的一个部分；你可以在 Shell 中多次使用同一个函数。函数有助于消除在编写 Shell 程序时对编写重复代码的需求。

以下是 `pdksh` 和 `bash` 中函数的格式：

```bash
func(){
  Statements
}
```

你可以如下调用函数：

```bash
func param1 param2
```

`param1`、`param2` 等是可选的。例如，下面的脚本使用 `Displaymonth()` 函数，如果你提供不在 1 到 12 范围内的月份，它会输出错误消息：

```bash
#!/bin/sh
Displaymonth() {
    case $1 in
      01 | 1) echo "Month is January";
      02 | 2) echo "Month is February";
      03 | 3) echo "Month is March";
      04 | 4) echo "Month is April";
      05 | 5) echo "Month is May";
      06 | 6) echo "Month is June";
      07 | 7) echo "Month is July";
      08 | 8) echo "Month is August";
      09 | 9) echo "Month is September";
      10) echo "Month is October";
      11) echo "Month is November";
      12) echo "Month is December";
      *) echo "Invalid parameter";
    esac
}
Displaymonth 8
```

上述程序显示输出：

Month is August

## 相关的 Ubuntu 和 Linux 命令

在使用 Shell 或编写 Shell 脚本时，你可以使用这些命令：

- `csh`——用于更改登录 Shell
- `kibitz`——允许与 Shell 交互
- `mc`——一个名为 Midnight Commander 的可视化 Shell
- `nano`——一种易于使用的文本编辑器
- `shar`——用于创建归档
- `vi`——vi 文本编辑器

# 参考文献

- http://www.linuxgazette.com/issue70/ghost.html——Linux Gazette 上关于“引导 Linux”的文章，包含了关于 BIOS 和 MBR 方面的大量细节。

- http://www.lostcircuits.com/advice/bios/1.shtml——LostCircuits 的 BIOS 指南；包含了所有 BIOS 设置的细节。

- http://www-106.ibm.com/developerworks/linux/library/l-slack.html——通过 IBM 网站提供的关于 Slackware Linux 文章，附带关于 System V BSD 脚本的侧边栏。

- `/src/linux/init/main`——学习 Linux 启动的最佳地点。非常有阅读价值。

- http://sunsite.dk/linux-newbie——Linux 新手管理员指南主页——对 Linux 管理的温和介绍。

- GRUB 手册——一份尚未完成的手册可以在 http://www.gnu.org/software/grub/manual/ 找到。在你的 Ubuntu 系统上，`info grub` 提供了大量信息，示例 `grub.conf`（`/boot/grub/menu.1` 是 `/boot/grub/gr.conf` 的符号链接；使用任何名称均可）位于 `/usr/doc/grub`。

- LILO 用户指南——Werner Altberger 关于 LILO 的权威技术著作，以及它在 Intel PC 上的工作原理。可以在 `/usr/share/doc/l10p*/` 目录下找到 `User_Guide.ps` 文件，可以使用 `gview` 查看内容。Ubuntu 已删除了 LILO；GRUB 现在是支持的加载器。

- “Grub, Glorious Grub”——Hoyt Duff，《Linux Format》杂志，2001年8月；第 58-61页。一个关于 GRUB 加载器的教程。

- http://web.cs.mun.ca/~michael/pdksh/—`pdksh` 主页。

- http://lug.umbc.edu/~mabzug1/bash-httpd.html—Bash-httpd 常见问题，包含 bash Web 服务器最新版本 bash-httpd-0.02 的链接。

- http://www.tcsh.org/—在此处了解更多关于 `tcsh` 的信息。

- http://www.zsh.org/—在此处详细查看 `zsh`。

# 第12 章

## 系统监控工具

## 本章内容

- 基于控制的监控
- 图形化进程与系统管理工具
- KDE 进程与系统监控工具
- 参考

为了保持系统处于最佳状态，你需要能够对其进行密切监控。在运行时间至关重要且任何系统故障都会导致高昂成本的企业环境中，这种监控是必不可少的。无论是检查进程是否有执行任务，还是密切关注 CPU 和内存使用，Ubuntu 都提供了丰富的实用，可以根据你的需要提供多或或少的反馈。本章将介绍一些基础监控工具，以及让系统运行更长时间的策略。某些监控工具涵盖了网络连接、内存和硬盘使用情况，但它们都应该是你系统管理员工具箱中的一员。最后，你将学习如何结合图形和命令行工具来操作活跃的系统进程。

## 基于控制的监控

熟悉 Unix 系统管理的人已经知道大多数 Unix 发行版中都有 `ps` 或进程显示命令。由于 Linux 与 Unix 关系紧密，它也受益于该命令，允许你快速查看系统上当前运行的进程，以及它们的所有者和资源消耗情况。

尽管 Linux 内核有自己独特的架构和内存管理，但它也受益于许多 Unix 发行版增强型的 `/proc` 文件系统。通过 `/proc` 文件系统，你可以直接与内核通信，以获取当前正在发生情况的深度视图。开发者倾向于将 `/proc` 文件系统作为从内核获取信息的一种，并让程序将其转换为更易人类读的格式。`/proc` 文件系统超出了本书的范围，但如果你想直观地了解它包含的内容，请访问 http://en.tldp.org/LDP/Linux-Filesystem-Hierarchy/html/proc.html，那里有一个非常深入的指南。

进程也可以在命令行进行控制，这很重要，因为你有时只有一个命令行界面。每当启动应用程序或进程（无论是从命令行还是点击图标）时，来自内核的进程都会被分配一个称为进程 ID（简称 `PID`）的标识数字。如果进程是通过命令行启动的，该数字将显示在 shell 中。

```
$ gedit &
```

[1] 6193

在此示例中，`gedit` 已在后台启动，(`bash`) `shell` 报告了一个作业号（在本例中为 `{1}`）。作业号或作业控制是 shell 特有的功能，允许不同形式的进程控制，例如将程序挂起并发送到后台，并将后台作业调回前台（如果你没有使用 `bash`，可以查看你 shell 的 man 页获取更多信息）。

显示的第二个数字（在本例中为 6193）代表进程 ID。你可以像这样使用 `ps` 命令来快速获取进程列表：

```
$ ps
PID TTY TIME CMD
6176 pts/0 00:00:00 bash
6193 pts/0 00:00:00 gedit
```

注意，并不是所有的输出都是 PID。但正如你所看到的，输出包含了进程 ID（缩写为 `PID`）以及其他信息，例如运行进程的名称。对于任何 Unix 命令，都有许多选项；`proc` 的 man 页有一个完整的列表。最有用的选项是 `aux`，它提供了一个所有进程的友好列表。你还应该知道 `ps` 并不是通过轮询内存工作的，而是通过查询 `/proc` 或进程文件系统实现的。（`ps` 是本节开头提到的接口之一）。

`/proc` 目录包含几个文件——其中一些包含不断更新的硬件信息（如电池量等）。Linux 系统管理员经常将 `ps` 的输出通过管道传递给命令族中的成员来显示进程信息，如下：
