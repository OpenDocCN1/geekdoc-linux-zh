

lp 命令是用于提交打印作业的命令行接口。可以使用 lp 命令输入多个选项来指定目标、副本数量和其他选项。lpadmin 用于配置排队系统以描述打印机、类并设置默认打印机。

## AIX

AIX 提供了非常强大的打印服务集合。IBM 在开发强大的打印系统上投入了大量时间和精力。AIX 可与 BSD 和 SysV 系统互操作。它同时支持 lp 和 lpr 命令。然而，其底层结构与 BSD 和 SysV 系统相当不同。AIX 打印服务利用 /etc/qdaemon 来调度打印作业。qdaemon 的启动和停止由 /etc/inittab 文件控制。/etc/qconfig 文件包含打印服务可用的队列和设备的描述。qdaemon 在启动时以及 qdaemon 刷新时读取 qconfig 文件。/usr/sbin/lpd 守护进程负责接收来自 TCP/IP 的远程打印请求。lpd 守护进程可以在系统启动时启动（在 /etc/inittab 文件中添加条目）或通过命令行启动。

在 AIX 中，可以通过多种不同方式操作打印作业和队列。enq 命令可以启动和停止队列和打印机。它还可以更改作业的优先级，从队列中删除作业，并列出打印机队列的状态。enq 是一个非常有用且功能强大的打印服务命令。

AIX 提供两种 GUI 来设置打印服务。两种 GUI 都易于使用，并且会为你完成所有繁重的工作。SMIT 提供了一个图形界面，允许你配置、启动、停止和操作所有本地打印机和队列。只需输入命令 smit 并在系统管理下选择打印排队按钮即可。另一个 GUI 是基于 Web 的系统管理器（WSM）。WSM 位于 /usr/bin/wsm，它提供了一个基于 Web 的界面来管理 AIX 系统。单击打印机队列图标，你就可以执行 SMIT 中包含的所有类似功能。

enq 可以启动和停止队列和打印机。它还可以更改作业的优先级，从队列中删除作业，并列出打印机队列的状态。

## HPUX

HPUX 基于 SysV 打印服务。它增强了 lpsched 守护进程以将作业分发到远程 BSD 打印机。HPUX 还可以通过 rlpdaemon 接收来自 BSD 系统的远程作业。HP 分布式打印服务（HPDPS）是面向分布式环境的打印管理和管理产品。它与 lp 命令兼容，但提供了扩展的管理功能。系统管理管理器（SAM）提供了一个 GUI 界面，允许配置 lp 打印服务和 HPDPS（图 10.1）。我们建议使用 SAM 在 HPUX 上配置打印服务。

# 图 10.1 SAM 打印机管理。

## RED HAT LINUX

Red Hat 基于 BSD 打印服务。printtool 命令允许系统管理员通过图形界面在 Red Hat 系统上添加、编辑和删除打印机（图 10.2）。printtool 提供发送测试文件的工具并支持 Windows 2000 上的 SMB 打印机服务器。

## SOLARIS

Solaris 打印服务基于 SysV。可以使用“SysV 打印服务”部分中概述的命令完成打印服务的配置。打印服务也可以使用 Admintool 进行配置，Admintool 是一个 GUI 系统管理工具。Admintool 可以添加或删除对打印机的访问（图 10.3）。我们建议使用 Admintool 在 Solaris 系统上添加和删除对打印机的访问。

![](img/415c89a1ede71e11e5040a0038b6916c_429_0.png)

![](img/415c89a1ede71e11e5040a0038b6916c_430_0.png)

图 10.2 Red Hat Linux 打印系统管理器。

## LPRng

LPRng 是一个基于 BSD 的增强型打印服务包。它包含熟悉的 lpr、lpc 和 lprm 命令。它还包括打印队列的动态重定向、单个队列的多个打印机以及大幅增强的安全检查。LPRng 与使用 BSD 服务的远程打印机兼容，并且已移植到 HPUX、Solaris、Linux 和 AIX。

![](img/415c89a1ede71e11e5040a0038b6916c_430_1.png)

图 10.3 Admintool 打印机管理。

