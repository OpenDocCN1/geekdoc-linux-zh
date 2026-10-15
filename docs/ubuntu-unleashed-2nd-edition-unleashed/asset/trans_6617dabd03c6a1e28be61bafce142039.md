
http://www.gnu.org/software/bash/bash.html—GNU 软件项目上的 bash 主页。

http://www.tldp.org/LDP/abs/html/—Mendel Cooper 的《Advanced Bash-Scripting Guide》。

http://www.linuxinnewbie.org/nhf/intel/shells/basic.html—在此站点学习基本 shell 命令。

http://www.cs.princeton.edu/~jlk/jl/—David G. Korn、Charles J. Northrup 和 Jeffery Korn 关于 korn shell 的文章“新 Korn Shell—ksh93”。

http://web.cs.mun.ca/~michael/pdksh/—pdksh 主页。

http://lug.umbc.edu/~mabzug1/bash-httpd.html—Bash-httpd FAQ，其中包含指向 bash web 服务器 bash-httpd-0.02 最新版本的链接。

http://www.tcsh.org/—在此了解有关 tcsh 的更多信息。

http://www.zsh.org/—在此更详细地了解 zsh。

## CHAPTER 16

## 系统资源

## 系统监控工具

要使系统保持最佳状态，您需要能够对其进行密切监控。在企业环境中，这种监控至关重要，因为系统正常运行时间至关重要，任何系统故障都可能造成真正的金钱损失。无论是检查进程中是否有任何异常守护进程，还是密切关注 CPU 和内存使用情况，Ubuntu 都提供了大量实用程序，旨在为您提供您想要的尽可能少或尽可能多的反馈。在本章中，我们将介绍一些基本的监控工具，以及旨在让系统更长时间保持运行的一些策略。一些监控工具涵盖网络连接、内存和硬盘使用情况，但所有这些都应成为您的系统管理员工具包的一部分。最后，您将学习如何使用图形和命令行工具的组合来操作活动系统进程。

### 基于控制台的监控

熟悉 UNIX 系统管理的人已经知道 ps 或进程显示命令，该命令常见于大多数 UNIX 变体。由于 Linux 与 UNIX 关系密切，它也受益于此命令，使您能够快速查看系统上当前正在运行的进程，以及它们的所有者和它们的资源消耗情况。

尽管 Linux 内核具有自己独特的架构和内存管理，但它也受益于对 /proc 文件系统的增强使用，/proc 文件系统是许多 UNIX 变体中发现的虚拟文件系统。通过 /proc 文件系统，您可以直接与内核通信，以深入了解当前正在发生的情况。开发人员倾向于使用 /proc 文件系统作为从内核获取信息的方式，并将其程序操纵为更易于人类阅读的格式。/proc 文件系统超出了本书的范围；但如果您想更好地了解其包含的内容，请前往 http://en.tldp.org/LDP/Linux-Filesystem-Hierarchy/html/proc.html 获取一份优秀且深入的指南。

### 本章内容

- 系统监控工具
- 参考

进程也可以在命令行上进行控制，这一点很重要，因为您有时可能只有命令行界面。每当从命令行启动应用程序或命令，或通过单击图标启动时，来自内核的进程都会被分配一个称为进程 ID 的标识号，简称为 PID。如果程序通过命令行启动，该数字会显示在 shell 中：

```
$ xosview &
[1] 5918
```

在此示例中，xosview 客户端已在后台启动，(bash) shell 报告了 shell 作业号（本例中为 [1]）。作业号或作业控制是 shell 特有的功能，允许不同形式的进程控制，例如将程序发送到后台或挂起，以及将后台作业检索到前台。 （如果您未使用 bash，请参阅 shell 的 man 页面以获取更多信息。）

显示的第二个数字（本例中为 5918）代表进程 ID。您可以使用 ps 命令像这样快速列出您的进程：

```
$ ps
  PID TTY      TIME     CMD
 5510 pts/0    00:00:00 bash
 5918 pts/0    00:00:00 xosview
 5932 pts/0    00:00:00 ps
```

请注意，这里并未显示显示的所有输出。但是，正如您所看到的，输出包括进程 ID，缩写为 PID，以及其他信息，例如正在运行程序的名称。与任何 UNIX 命令一样，提供了许多选项；proc man 页面有完整列表。最有用的选项之一是 aux，它提供所有进程的友好列表。您还应该知道，ps 的工作方式不是通过轮询内存，而是通过 interrogation Linux /proc 或进程文件系统。 （ps 是本节开头提到的接口之一。）

/proc 目录包含相当多的文件——其中一些包含不断更新的硬件信息（例如电池电量水平等）。Linux 管理员经常将 ps 的输出通过 grep 系列命令之一来显示特定程序的信息，也许是这样的：

```
$ ps aux | grep xosview
USER     PID %CPU %MEM   VSZ   RSS TTY      STAT START   TIME COMMAND
andrew  5918  0.3  1.1  2940  1412 pts/0    S   14:04   0:00 xosview
```
