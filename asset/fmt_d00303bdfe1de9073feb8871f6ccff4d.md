
Either the boot manager didn't get when you installed FreeBSD or something you did in Windows (`fdisk /mbr`, for example) clobbered the FreeBSD boot manager. Fortunately, it is relatively easy to restore.

- Boot from the included DVD or from the installation floppies you created.
- After you have gotten into the `Sysinstall` program, select Configure and then `Fdisk` (see Chapter 2, “Installing FreeBSD,” if you need a refresher on `Sysinstall`).
- 如果你的系统中有多个硬盘，系统会提示你想要在哪个系统上运行 `fdisk`。请选择你的系统启动的主硬盘。
- 当你处于 `fdisk` 中时，只需选择 `W` 来写入更改。你将收到一条警告，告诉你只有在对现有安装进行更改时才应执行此操作。选择 `Yes` 并按回车。
- 当系统询问你如何处理引导加载程序时，请选择主引导记录（Master Boot Record）。

完成此过程后，引导管理器应该就会恢复运行。

## FreeBSD 检测到的内存少于系统实际内存

FreeBSD 并不总是能从 BIOS 获取你系统中正确的内存量。通常，这会导致 FreeBSD 检测到 64MB 的内存，即使你实际上拥有更多内存。

要解决这个问题，你需要在内核配置选项中添加以下选项：

```
"MAXMEM=n"
```

`n` 是你以 KB 为单位的内存量。请记住，在二进制数学中，一个千字节实际上是 1024 字节，而不是 1000 字节。因此，如果你有 512MB 的内存，在这里需要输入数字 524288。

在你做出此更改后，你需要重新构建内核（详见第 18 章“内核配置”，有关重新构建内核的详细信息）。

## FreeBSD 在挂载 CD-ROM 驱动器时报错“设备未配置”

这个问题可能由以下几点引起：

- CD-ROM 驱动器可能是空的；只需插入 CD 并重试。
- 第二种可能性是 ATAPI CD-ROM 驱动器被配置为辅助控制器上的从设备，而控制器上没有主设备。如果是这种情况，你需要将你的 CD-ROM 驱动器重新配置为主设备（你通常可以使用 CD-ROM 驱动器背后的跳线帽进行重新配置）。
- 如果你有一个 SCSI CD-ROM 驱动器，当内核启动时，驱动器可能没有足够的时间响应总线请求。如果是这种情况，请在内核配置文件中找到 `SCSI_DELAY` 行并增加时间。（时间以毫秒为单位。默认设置为 5000，即 5 秒。你可以先尝试将其翻倍到 10000。）然后你还需要重新构建内核（详见第 18 章）。

## 启动问题和其他非安装问题 949

### 程序因信号 11 错误崩溃

这个问题类似于 Windows 中的“非法操作”错误。它基本上意味着程序尝试访问未分配给它的内存。这可能是程序中的 Bug 导致的，或者如果发生在 FreeBSD 自带的工具中，则可能是 FreeBSD 本身的 Bug。

此问题的第三个潜在原因是硬件不稳定。如果在编译软件时问题随机出现，你可以确定旧设备或故障的硬件是罪魁祸首。导致此类问题的常见硬件包括缺陷的 RAM、过热的 CPU（你的 CPU 风扇在转吗？你是否在超频？）、缓存或电源不足。

你可以通过启动不同的操作系统来隔离问题，例如完全从 CD 运行的 Linux 发行版（这意味着你不需要将其安装到硬盘上就可以查看你的 FreeBSD 硬件上是否存在相同的问题）。`Knoix` 可以在 http://www.knoppix.net 免费获取。另一个选项是 `memtest86` (http://www.memtest86.com)，你可以下载并将其制作成可启动 CD，用于诊断潜在问题。

### 运行 top、ps 和其他系统实用程序时出现奇怪错误信息（如“proc mismatch”）

这类错误几乎总是由于你的世界（`world`）和内核（`kernel`）不同导致的，通常是因为它们基于源码的不同状态。问题通常源于使用 `make world` 从源码构建系统，然后没有构建新内核。反之也可能成立：你使用下载的源码构建了新内核，但没有先执行 `make world`。

由于重新构建内核比重新构建世界快得多，简单的解决方案是尝试构建新内核并重启（有关重新构建内核的详细信息请见第 18 章）。

如果重新构建内核不能解决问题，请重新构建世界（有关构建世界的详情请见第 19 章“跟进 FreeBSD 更新”）。

最后，如果这两个选项都不能解决问题，获取最新的源码（详见第 19 章）、构建世界并重新构建内核应该让你的系统恢复正常。

### 忘记 root 密码

如果你忘记了 root 密码，可以进入单用户模式来恢复它。

要进入单用户模式，重启系统，然后在加载菜单中选择选项 4，“以单用户模式启动 FreeBSD”。当你被询问使用哪种 shell 时，直接按回车使用默认值。你应该会得到如下所示 root 用户提示符：

```
#
```

在提示符处，输入 `mount -u` `/` 然后按回车，以读写模式重新挂载根文件系统。然后，输入 `mount -a` 来挂载所有其他文件系统。你现在可以输入 `passwd root` 来更改 root 账户的密码。（如果不起作用，输入 `/usr/bin/passwd root`。）系统不会要求输入旧密码。直接输入即可。

## 附录 D

### 更多来源

FreeBSD 拥有一个不断扩大的社区。本附录提供了网站、邮件列表等资源。

#### FreeBSD 特有资源

##### 网站

- `www.freebsd.org`: 这是项目的官方网站。它是获取新闻、更新的地方。
- `www.freebsddiary.org`: 该网站是 FAQ 和操作指南的宝库。
- `www.freshports.org`: 获取最新新闻的地方。
- `www.freebsdmall.com`: 购物信息的来源。

##### 邮件列表

###### 通用列表

任何人都可以订阅并参与通用列表。然而，在列表中发布帖子之前，你应该阅读列表指南（它会在你订阅时发送给你）。以下是通用列表及其用途的简要描述。

完整的邮件列表以及其存档的网页搜索界面，可以在 http://www.freebsd.org/community/mailinglists 找到。

`cvs-all`

对 FreeBSD 源码树的所有更改都会发布此列表中。这是一个只读列表，对喜欢阅读大量 C 代码的硬核开发者感兴趣。

`freeBSD-advocacy`

一个讨论 FreeBSD 益处以及推广 FreeBSD 的不同方式的列表。

`freeBSD-announce`

关于 FreeBSD 的重要公告。这是一个只读列表，旨在保持低邮件量。

`freeBSD-arch`

关于系统架构和设计的讨论。

`freeBSD-bugbusters`

FreeBSD 用户讨论 FreeBSD 漏洞数据库工作原理的列表。

`freeBSD-bugs`

FreeBSD 的错误报告。请注意，你不应该直接向此列表发送错误报告。相反，你应该使用 http://www.freeBSD.org/send-pr.html 处的表单（或 FreeBSD 中的 `send-pr` 程序）向漏洞数据库提交问题报告。你提交的问题报告将将发布给该列表的订阅者，并在数据库中进行跟踪。

`freeBSD-chat`

面向 FreeBSD 社区成员的通用性、非技术讨论列表。

`freeBSD-current`

如果你正在跟踪 FreeBSD 的 CURRENT 分支，你需要订阅此列表。除其他外，阅读此列表可以防止你在源码树损坏时执行“编译世界（`make world`）”，这可能导致你的系统无法使用。除非你精通技术并愿意处理此类问题，否则你不应该跟踪 CURRENT。这意味着你不应该向此列表发布通用的“如何做”的问题。只有关于 CURRENT 的技术问题应该发布到此列表。对于其他类型的问题，你可能得不到任何回复，或者可能需要在 `freeBSD-questions` 中重新发布你的问题。

`freeBSD-isp`

使用 FreeBSD 的互联网服务提供者的讨论列表。请注意，此列表面向供应商而非用户。换句话说，如果你在连接 FreeBSD 到你的互联网服务商时遇到问题，这里不是发布问题的地方。

`freeBSD-jobs`

如果你是一个正在寻找工作的 FreeBSD 高手（guru），你可以在此列表中找到职位公告。如果你是雇主并需要 FreeBSD 高手，你可以向此列表发布你的“诚聘良士”广告。

`freeBSD-policy`

此只读列表供 FreeBSD 核心团队讨论 FreeBSD 开发策略的更改。

`freebsd-questions`
