
最后，请注意物理安全。如果潜在的攻击者可以获得你系统的物理访问权限，那么获取完全访问权限将变得轻而易举。将所有服务器保存在锁好的房间内，并确保只有授权的人员才能访问客户端。

## 配置和使用 Tripwire

`Tripwire`是一种检查普通系统二进制文件完整性并向你或通过电子邮件报告任何更改的工具。`Tripwire`是确保你的二进制文件未被木马程序替换的良好工具。木马程序是无意中被安装为（预期的）程序文件名的恶意程序，它们可能会对被攻破的系统造成破坏性影响。

`Tripwire`有两个版本：开源版本和商业产品。`Tripwire`的免费版本可以在 Ubuntu 仓库中找到。你可以在`www.tripwire.org`了解它们的差异。

要初始化`Tripwire`，请使用其`-init`选项，如下所示：

```
matthew@semour:-$ sudo tripwire -init
Please enter your local passphrase:
Pars policy file: /etc/tripwire/tw.pol
Generating the database...
*** Processing Unix File ***
```

`Wrote database file: /var/lib/tripwire/shuttle2.twd`

数据库已成功生成。

注意，并非所有输出都在这里显示。在`Tripwire`创建其数据库（你文件系统的快照）后，请使用此基线结合`/etc/tripwire`目录下配置的策略和设置来监控你的系统状态。（详情请参阅`tripwire`手页。）例如，你可以让`Tripwire`在命令行中检查你的系统并生成报告，如下：

```
matthew@semour:-$ sudo tripwire -m c
```

此处没有显示输出，但在示例中显示了报告。输出可以重定向到文件，但报告会保存于`/var/lib/tripwire/report/hostname-YYYYMMDD-HHMMSS.twr`（换句话说，使用你的主机名称、日期、月份、日期、小时和秒）。你可以使用`twprint`实用程序读取此报告，如下：

```
matthew@semour:-$ sudo twprint-print-report -r \
/var/lib/tripwire/report/shuttle2-20020919-181049.twr | less
```

### 病毒

`Tripwire`支持其他选项，例如通过电子邮件发送报告，它应该由你系统的调度表`/etc/crontab`在非工作时间作为计划任务运行。（在性能较弱的计算机上，可能会消耗大量资源。）`Tripwire`软件包还包含一个`twadmin`实用程序，你可以用它微调或更改设置或策略，以执行其他管理职责。

如果你想使用`Tripwire`，计划花些时间阅读文档。它强大但并不简单。我们建议从`man`手页和`tripwire.com`网站开始。

### 设备

永远不要宣称你已将网卡（`NIC`）设为混杂模式。混杂模式（可以通过使用`config=promisc`选项在接口上设置）用于监控跨网络流量，并允许你监控入侵你网络的人员的行为。`tcpdump`命令在程序运行时也会将指定的接口设置为混杂模式；遗憾的是，`ifconfig`命令不会报告`tcpdump`正在运行这一事实！

记住对正确的事使用正确的工具。虽然你可以使用网络网桥将网络连接到互联网，但这不是一个好的选择。网桥几乎已经过时，因为它们会转发经过它们的任何数据包，当网桥连接到互联网时这并不好。路由器允许你过滤中继的数据包。

在优秀的人手中，Linux像`Windows`一样容易受到病毒攻击。这可能让你感到惊讶，特别是如果你是因为其安全记录而切换到`Linux`的。然而，`Windows`和`Linux`的区别在于，在`Linux`上更容易防御病毒。事实上，只要你足够机灵且勤奋，就永远不必担心它们。原因如下：

- `Linux`将当前目录放在你的可执行路径之外，因此输入`ls`运行的是`/bin/ls`，而不是当前目录中任何名为`ls`的程序。
- `root`用户只能感染你有访问权限的文件，这通常是用户主目录下的文件。这是在不需要时不要使用`sudo`的最重要原因之一。
- `Linux`强制你手动标记文件为可执行文件，因此你不会误运行一个名为`myfile.txt exe`的文件（你你以为它是文本文件）。
- 通过拥有多个常用的网络浏览器和邮件客户端，`Linux`具有多样性带来的优势：病毒无法针对你的平台和90%的用户。

尽管如此，`Linux`仍然容易成为病毒的载体。如果你运行邮件服务器，你的`Linux`机器可以向`Windows`机器发送受病毒感染的邮件。基于`Linux`的服务器是安全的，但`Windows`会被病毒攻击。

在这种情况下，为你的机器考虑病毒扫描器。你有几个选择，包括免费和商业性的。最流行的免费套件是`Clam AV` (`www.clamav.net`)，`Central Command`、`BitDefender`、`F-Secure`、`Kaspersky`、`McAfee`等都在竞争提供商业解决方案。查看

## 配置你的防火墙

始终使用`UFW`管理防火墙。`UFW`默认是禁用的。在定义规则后，使用以下命令启用它。

在此表中，你将看到在终端使用的`UFW`命令。

| 使用 UFW 命令 | 执行的操作 |
|---|---|
| `enable` | 启用防火墙 |
| `disable` | 禁用防火墙 |
| `reload` | 重新加载防火墙以确保更改生效 |
| `default allow` | 设置默认策略 |
| `default deny` | 设置默认策略 |
| `logging on`|`off` | 切换日志记录 |
| `allow ARGS` | 添加允许规则 |
| `deny ARGS` | 添加拒绝规则 |
| `reject ARGS` | 添加拒绝规则 |
| `limit ARGS` | 添加限制规则 |
| `delete RULE` | 删除规则 |
| `status` | 显示防火墙状态 |
| `status numbered` | 以编号列表显示防火墙状态 |

要查看激活的规则，使用以下命令：

```
matthew@semour:-$ sudo ufw status
```

要查看带编号的规则，使用以下命令：

```
matthew@semour:-$ sudo ufw status numbered
```

要按编号删除规则，使用以下命令：

```
matthew@semour:-$ sudo ufw delete 1
```

要按定义删除规则，使用以下命令：

```
matthew@semour:-$ sudo ufw delete allow 80
```

要查看详细状态，使用以下命令：

```
matthew@semour:-$ sudo ufw status verbose
```

![](img/71b571561538b2a14c3bd347f4fcb569_431_0.png)

图 18.1 GUFW 图形界面。

![](img/71b571561538b2a14c3bd347f4fcb569_431_1.png)

图 18.2 GUFW 预的服务选项。

`AppArmor` 401

## AppArmor

`AppArmor`是一种强制访问控制（`MAC`）系统。它比闻名的`SELinux`（`www.nsa.gov/research/selinux/`）简单得多，后者是由美国国家安全局（`NSA`）创建的`MAC`系统。`AppArmor`的设计目的是通过限制特定程序仅使用预定义的资源且仅限这些资源，来限制程序的功能。这是通过配置文件（`profiles`）实现的，配置文件会在启动时加载到内核中。它可以在投诉模式（`complain mode`）下运行，此时会记录有关不安全操作的信息，但不采取任何行动；也可以在强制模式（`enforce mode`）下运行，此时策略和限制将生效。

这是对`AppArmor`的简要介绍。如需更完整的介绍，请查看本章末尾“参考文献”部分的链接。

默认情况下，`AppArmor`的作用很小。你可以通过安装`apparmor-profiles`包从 Ubuntu 仓库安装一些额外的配置文件。这些配置运行在投诉模式下，并将问题记录在`/var/log/messages`中。

要释放`AppArmor`的威力，你需要在`/etc/apparmor.d`中编辑或创建文本文件。配置文件以其所限制的应用程序命名，包括应用程序在文件系统中的完整路径。此处显示的`sbin.syslogd`示例，它限制了系统日志守护进程：

```
# $ID$
#-
#
# Copyright (C) 2002-2005 Novell/SUSE
#
# This program is free software; you can redistribute it and/or
# modify it under the terms of version 2 of the GNU General Public
#
# License published by the Free Software Foundation.
#
#
```

```
#include <tunables/global>

/sbin/syslogd flags=(complain) {
#include <abstractions/base>
#include <abstractions/nameservice>
#include <abstractions/consoles>

  capability sys_tty_config,
  capability dac_override,
  capability dac_read_search,
  capability setuid,
  capability setgid,
```

18

402 第 18 章 机器安全

```
/dev/log wl,
/var/lib/*/dev/log wl,

/dev/tty* w,
/dev/xconsole rw,
/etc/syslog.conf r,
/sbin/syslogd remix,
/var/log/** rw,
/var/run/syslogd.pid krwl,
/var/run/utmp rw,
/var/spool/compaq/nic/messages_fifo rw,
```

即使不知道语法，你也可以从这个文件中看出，配置文件是支持注释的简单文件，支持绝对路径和通配符（文件模式匹配），允许或禁止特定的能力（`capabilities`），以及文件系统中的哪些位置和程序可以被访问或使用。

每条规则都指定了列表中特定的权限：

- `r` - 读取
- `w` - 写入
- `ux` - 无限制执行
- `Ux` - 无限制执行并清理环境
- `px` - 离散配置执行
- `Px` - 离散配置执行并清理环境
- `ix` - 继承执行
- `m` - 允许在`mmap(2)`调用中使用`PROT_EXEC`
- `l` - 链接

这些权限列在行的末尾。

`Genprof`是一个帮助生成或更新配置文件的程序。你只需提供可执行文件的名称（如果它不在路径中，则提供路径），并可能可选地提供路径的路径，如下：

```
mathew@seymour~$ sudo genprof google-chrome
```

你会被要求启动该程序并运行一段时间。完成后，你将获得一个机会来选择对每个函数的访问应该被允许还是拒绝。该程序会在`/etc/apparmor.d`中写入一个文本文件，使用程序名称及其路径（在本例中为`opt.google.chrome.google-chrome`，我是直接从 Google [`www.google.com/chrome?platform=linux`] 安装的，因此你的系统上不存在 `AppArmor`）。随后，你可以根据需要编辑该文本文件，如果你想从投诉模式切换到强制模式，就必须这样做。

403 制定灾难恢复计划

当你有一组涵盖了你所需的配置文件后，这些是你最常使用的命令：

```
start:
matthew@semour-:$ sudo service apparmor start
```

```
stop:
matthew@semour-:$ sudo service apparmor stop
```

```
reload:
matthew@semour-:$ sudo service apparmor reload (or restart)
```

```
show status:
matthew@semour-:$ sudo service apparmor status
```

我们刚刚触及了`AppArmor`的表面，但希望我们已经为你提供了足够的信息，激发你进一步阅读的兴趣。`AppArmor`仍然很新并且在不断变化。在线文档是跟进变化的最佳方式。“参考文献”部分包含了一些几个好的起点地点。

## 制定灾难恢复计划

没有人喜欢为最坏的情况做打算，这就是为什么

# 第 19 章

## 本章内容

# 性能优化

- 硬盘
- 内核
- MySQL
- 参考文献

鉴于如今通用硬件升级的费用非常低廉，从硬件中挤榨出额外的性能听起来像是一项毫无意义的任务。在某种程度上，这确实是事实；对于我们大多数人来说，买一台新电脑比花费几个小时去争取 5% 的速度提升要便宜得多。但如果速度提升是 20% 呢？如果是 50% 呢？

通过优化系统可以获得的收益取决于你运行的是哪种任务，但对每个人都有适合自己的方法。在接下来的几页中，我们将介绍优化 `Apache` Web 服务器、`KDE` 和 `GNOME` 桌面系统、`MySQL` 和 `PostgreSQL` 数据库服务器等的快速优化方法。

在开始之前，你需要理解“优化”并不是一个绝对术语：如果我们优化了一个系统，我们提高了它的性能，但它的性能仍然可能进一步提高。我们并不热于从系统中获得 99.999% 的性能，因为优化遵循收益递减规律——基础性的改变差异最大，但之后，需要越来越多的工作量来获得日益递减的速度改进。

# 硬盘

许多 `Linux` 用户喜欢在底层进行捣鼓以提高电脑性能，而 `Linux` 为你提供了一些非常棒的工具来实现这一点。虽然追求稳定的养护者通常告诉我们“不要修理坏掉的东西”，但热爱实验的改装狂热者经常说“修它，直到它坏掉为止”。在本节中，你将学习许多用于调优或“微调（tweak）”你系统的命令。

然而，在你对 `Linux` 进行任何底层工作之前，请记住几点。首先，在开始之前对你的系统进行基准测试。`Linux` 并没有提供完善的基准测试应用程序，而且现有工具的可用性变化很快。你可以在网上搜索 `Linux` 基准测试程序的最新信息。如果你是系统管理员，可能会选择创建自己的基准测试。其次，一次只调整一种设置，这样你就能判断哪些是有效的、哪些无效的以及哪些会导致崩溃。这些微调中的某些可能无效，可能会导致你的机器死机，但如果你一次只实施一个，你会发现撤销导致问题的更改会容易得多。

始终准备一个可用的启动盘，例如 Ubuntu 的 Live CD 或 DVD。请记住，你个人对尝试任何这些微调承担所有风险。如果你不理解自己在做什么，或者对自己撤销任何调整的能力没有信心，那么 Ubuntu 的默认设置对于大多数人来说运行良好，真的不需要调整；就像大多数人可以原样地使用和享受他们的汽车一样。然而，有些人喜欢拆解他们的汽车并制造改装车；他们喜欢弄坏并修复它们。本章就是为这类人准备的。如果你认为自己无法修好，就不要冒冒险弄坏它。

# 使用 BIOS 和内核调优硬盘驱动器

一种调优方法允许调整 `BIOS` 中的设置。由于 `BIOS` 不是 `Linux`，而且每个 `BIOS` 看起来都不同，请务必查阅你的主板说明书以获取最佳可能的设置，并确保 `BIOS` 正确检测到所有驱动器。一次只更改一个设置。

`Linux` 在启动过程中提供了与 `BIOS` 设置进行交互的有限手段（主要是覆盖它们）。在本节中，你将学习这些命令。

其他选项在下述列表中，并在 `BOOTPROMPT HOWTO` 和内核文档中有更详尽的概述。这些命令可以用于强制 `IDE` 控制器并进行正确配置。然而，因人而异（YMMV），这些并不适用于所有人。

- `idex=dma`——这强制为主总线（`x=0`）或次要总线（`x=1`）开启 `DMA` 支持。
- `idex=autotune`——此命令尝试调优接口以获得最佳性能。
- `hdx=ide-scsi`——此命令启用 `IDE` 驱动器的 `SCSI` 仿真。某些 `CD-RW` 驱动器在写入模式下正常工作需要此项，它也可能为普通的 `CD-R` 驱动器提供一些性能改进。
- `idebus=xx`——可以是 20 到 66 之间的任何数字，会尝试自动检测，但如果 `dmesg` 显示没有正确检测到，或者你在 `BIOS` 中将其设置了不同的值（超频），可以手动设置。大多数 `PCI` 控制器都接受 33。
- `pci-biosirq`——某些主板可能会导致 `Linux` 生成错误信息，说你应该使用此项。在 `dmesg` 中查看它；如果你没看到，就不需要使用它。

这些选项可以像输入其他选项一样输入 `/etc/lilo.conf`、`/boot/grub/grub.conf` 或 `GRUB2` 的 `/boot/grub/grub.cfg` 中。

# hdparm 命令

`root` 用户使用 `hdparm` 工具设置和调优 `IDE` 硬盘的设置。你可以借此调优驱动器以获得最佳性能。在之前需要内核补丁和安装相关支持程序后，`hdparm` 程序现在包含在 Ubuntu 中。你应该只对只读挂载的文件系统进行实验，因为某些设置在使用不当时可能会损坏某些文件系统。`hdparm` 命令也适用于 `CD-ROM` 驱动器和某些 `SCSI` 驱动器。

命令的通用格式为：

```
matthew@semour:~$ hdparm [options] device
```

以下命令测试：

```
matthew@semour:~$ hdparm -T /dev/sda
```

你必须将 `/dev/sda` 替换为你的磁盘的位置。以下命令运行计时测试：

```
matthew@semour:~$ hdparm -t /dev/sda
```

以下命令运行缓冲读取测试：

```
matthew@semour:~$ hdparm -t /dev/sda
```

以下命令运行无缓冲读取测试：

```
matthew@semour:~$ hdparm -c /dev/sda
```
