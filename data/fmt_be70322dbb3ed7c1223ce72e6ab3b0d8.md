
```bash
#!/bin/sh
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
*) echo "Invalid parameter"; esac
```

你需要在每个条件下的语句用双分号（`;;`）结束。如果不这样做，下一个条件下的语句也会被执行。

`tcsh` 中 `case` 语句的格式如下：

```tcsh
switch ($str)
case str1|str2:
    Statements
case str3|str4:
    Statements
default:
    Statements
```

你可以为每个条件指定一组离散值——例如 `str1`、`str2` 等，也可以使用通配符指定一个值。最后一个条件应该是 `default`，如果都不满足其他条件，则执行它。对于指定的每个条件，将执行所有关联语句。

之前为 `pdksh` 和 `bash` 显示的根据给定月份数字输出月份名称的示例可以在 `tcsh` 中这样写：

```tcsh
#!/bin/tcsh
set month = 5
switch ($month)
case 1: echo "Month is January";
case 2: echo "Month is February";
case 3: echo "Month is March";
case 4: echo "Month is April";
case 5: echo "Month is May";
case 6: echo "Month is June";
case 7: echo "Month is July";
case 8: echo "Month is August";
case 9: echo "Month is September";
case 10: echo "Month is October";
case 11: echo "Month is November";
case 12: echo "Month is December";
default: echo "Oops! Month is October!";
end
```

你需要在每个条件下的语句用 `break` 结束。如果不这样做，下一个条件下的语句也会被执行。

## break 和 exit

`break` 语句用于终止循环或 `switch` 语句。`exit` 语句用于终止脚本或 shell。

## 在 Shell 中使用函数

函数是一个可以重用的代码块。函数用于组织和简化脚本。

以下是在 `pdksh` 和 `bash` 中定义函数的示例：

```bash
hello() {
    echo "Hello, World!"
}
```

调用函数时，只需使用其名称：

```bash
hello
```

你还可以使用 `$1`、`$2` 等向函数传递参数。

```bash
greet() {
    echo "Hello, $1!"
}
greet "Alice"
```

参考 411

大量的信息和一个示例 `grub.conf` 文件（`/boot/grub/menu.1st` 是 `/boot/grub/grub.conf` 的符号链接；使用任一名称）可以在 `/usr/doc/grub` 中找到。

《LILO 用户指南》——Werner Almesberger 关于 Linux 加载器（LILO）的权威技术专著，以及它在基于 Intel 的 PC 上如何工作。查看 `/usr/share/doc/lilo*` 目录下的 `User_Guide.ps` 文件，可以通过 g 客户端查看。LILO 已从 Fedora 中移除；GRUB 是该发行版支持的默认启动器。

“使用 Red Hat 的 chconfig 管理 Initscripts”——Billy Ball 著，《Linux Journal》，2001 年 4 月；第 128–132 页。

“Grub，光荣的 Grub”——Hoyt Duff，《，《Linux Format》，2001 年 8 月；第 58–61 页。一个关于 GRUB 启动器的教程。

http://www.redhat.com/docs/manuals/linux/RHL-9-Manual/custom-guide/s1-services-serviceconf.html——Red Hat 使用 system-config 服务客户端（当时称为 redhat-config-service）的指南。

http://www.linuxbase.org/spec/refspecs/LSB_1.0.0/GLB/sysinit.html——Linux 标准基准（LSB）对系统初始化的描述；这是标准所在。

http://www.gnu.org/software/bash/bash.html——GNU 软件项目中的 bash 主页。

http://www.tldp.org/LDP/abs/html/——Mendel Cooper 的《高级 Bash 脚本指南》。

http://www.linuxnewbie.org/nhf/intel/shells/basic.html——在此网站学习基础 shell 命令。

http://www.cs.princeton.edu/~jlk/li—“新 Korn Shell—ksh93，”——David G. Korn、Charles J. Northrop 和 Jeffrey Korn 一篇关于 pern shell 的文章。

http://web.cs.mun.ca/—michael/pdksh/——pdksh 主页。

http://lug.umbc.edu/~mazbug1/bash-httpd.html——Bash-httpd 常见，包含指向最新版本 bash 网络服务器 bash-httpd-0.02 的链接。

http://www.tcsh.org/——在此处了解 tcsh。

http://www.zsh.org/——在此处详细查看 zsh。

![](img/c4a0ea5ab3561ff33a8da88887702720_448_0.png)

# 第 16 章

# 本章内容

# 系统资源

- 系统监控工具

- 参考文献

# 系统监控工具

为了让你的系统处于最佳状态，你需要对它进行严密监控。在运行时间至关重要的企业环境中，任何系统故障都可能导致真实的资金损失，这种监控是必不可少的。无论是检查进程是否有任何错误的守护进程，还是严密关注 CPU 和内存使用情况，Fedora 都提供了丰富的工具，可以根据你的需要提供多或少的反馈。在本章中，我们将查看一些基础监控工具，以及让系统运行更长时间的策略。某些监控工具涵盖了网络连接、内存和硬盘使用情况，但它们都应该在你系统管理员工具箱中占有一席。最后，你将学习如何结合图形和命令行工具来操作活跃的系统进程。

# 控制台监控

熟悉 UNIX 系统管理的人已经知道许多 UNIX 变体中常见的 `ps` 或进程显示命令。由于 Linux 与 UNIX 密切相关，它也受益于此命令，允许你快速查看系统上当前运行的进程，以及所有者及其资源消耗情况。

尽管 Linux 内核有自己独特的架构和内存管理，但它受益于对 `/proc` 文件系统的增强使用，这是许多 UNIX 变体中的虚拟文件系统。通过 `/proc` 文件系统，你可以直接与内核通信，获取当前正在发生什么的深度视图。开发者倾向于将 `/proc` 文件系统作为从内核获取信息，并让程序将其转换为人类易读的格式。`/proc` 文件系统是本书范围，但如果你想更好地了解它包含的内容，应该前往 http://en.tldp.org/LDP/Linux-System-Hierarchy/html/proc.html 查看一份优秀且深入的指南。

进程也可以在命令行进行控制，这很重要，因为你有时只有命令行界面。每当应用程序或命令启动时（无论是从命令行还是通过点击图标），来自内核的进程会被分配一个称为进程 ID（简称 PID）的标识号。如果程序是通过命令行启动的，该数字将显示在 shell 中。

```
$ xsview &
```

```
[1] 11670
```

在此例中，`xview` 客户端在后台启动（在这种情况下，`(bash)` shell 报告了一个作业号 `[1]`）。作业号或作业控制是 shell 特有的功能，允许不同形式的进程控制，例如将程序发送或挂起到后台，并将后台作业检索回后台。
