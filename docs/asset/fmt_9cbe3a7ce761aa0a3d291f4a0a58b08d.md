
```
server=admin
service=plj
password=**
```

将这些每项更改为正确的值，然后将脚本作为队列的接口安装并使用以下命令开始打印：

```
root# lpadmin -p printername -v /dev/null -i./smbprint.sysv
root# enable printername
root# accept printername
```

例如，如果打印机名为 `hawk_print`，远程服务器为 `HAWK`，打印机共享名为 `MYPRINTER` 访问远程共享不需要密码，则 `smbprint.sys` 的更改将如下：

```
server=HAWK
service=MYPRINTER
password=**
```

设置并启用此打印机所需的命令为：

```
root# lpadmin -p hawk_print -v /dev/null -i./smbprint.sysv
root# enable hawk_print
root# accept hawk_print
```

# 使用 NetBIOS 名称服务解析主机名

Unix 网络管理员经常由于客户端（以及服务器）名称的动态性而抱怨 NetBIOS 名称解析和 Windows 客户端。抱怨的根源在于，除非在 DNS 中配置了 NetBIOS 主机，否则某些 Unix 工具（如 `ping`）将无法通过其 NetBIOS 名称联系机器。

Samba 包含一个 NSS 模块，可查询网络上的 NetBIOS 名称服务以解析主机名。尽管名为 `libns_wins`，但如果无法连接到 WINS 服务器，该库也将使用广播机制解析主机名。WINS 在第 18 章中有详细介绍，因此我们在此不展开。

Samba 默认不构建 `libns_wins` 模块，因为它仅适用于 Linux。但只需要额外执行一个步骤即可在 `source/nsswitch` 目录中创建共享库。从 `source/` 子目录执行以下命令：

```
$ make nss/libns_wins.so
```

`libnss_wins.so` 文件名是 Linux 特有的。在当前的 2.2 版本中，该模块将在 Solaris 等其他平台上编译失败。

一旦构建了该库，我们必须将其拷贝到 `/lib` 目录并按所示设置所有权和权限：

```
root cp -p nsswitch/libnss_wins.so /lib/libnss_wins.so.2
root chown /lib/libnss_wins.so.2
root chgrp /lib/libnss_wins.so.2
root chmod 755 /lib/libnss_wins.so.2
```

`libnss_wins` 模块期望来自 `smb.conf` 的 NetBIOS 名称解析设置，仅使用 `smbd` 和 `winbind`。这将包括：

```
[global]
  name order = wins files
```

最后一步是将其添加到 `/etc/nsswitch.conf`。这意味着应该首先查询 hosts 文件，然后是 wins：

```
hosts: files wins dns
```

假设机器已添加到 DNS 区域，我们可以 ping `cleopatra`：

```
$ ping cleopatra
PING cleopatra (192.168.1.140): 56 bytes of data
64 bytes from 192.168.1.140: icmp_seq=0 ttl=128 time=0.551 ms
64 bytes from 192.168.1.140: icmp_seq=1 ttl=128 time=0.800 ms
```

如果 NetBIOS 解析配置不当，此步骤可能会。

### 总结

在这一小时中，我们检查了 Samba 提供的两个客户端工具。虽然这里介绍的 smbfs 实现是针对 Linux 的，但存在其他版本，包括商业版和开源。挂载 CIFS 文件系统的能力为标准 Unix 工具（如 `vi`、`find`、`rm` 和 `mkdir`）提供了支持。

# 第 13 小时

## 故障排除技术

我发现很有趣的是，这一小时是本书中点之后的第一个小时——如果你是按小时数的话。它也是“第四部分——进入生产环境”之前的最后一个小时。

为什么我等了这么久才介绍 Samba 的故障排除技术呢？我认为故障排除是一个“先有鸡还是有蛋”的问题。当你需要知道如何排除某个软件包的故障时，你并没有足够的信息来自己该做什么。然而，一旦你拥有了这些信息，你不一定需要进行故障排除，因为你可以根据自己的经验定位问题。编写关于追踪和解决损坏的 Samba 配置的方法，其问题在于：在理解这些技术为何有效之前，你必须对事物是如何运作的有一个通用的理解。但是，正如我之前说的，一旦你掌握了这些知识，通常可以自己解决问题。这真的是一个恶性循环。

![](img/e6dc042fe420c610acdd193e834a4772_230_0.png)

我们在这一小时将采取的方法是为 Samba 管理员识别一组最佳实践。这些指南将以常见错误信息及其含义的形式呈现，以及当你完全陷入困境时获取帮助的技术和途径。遵循 Unix 和开放/自由软件的传统，这将帮助你站在那些已经修复过损坏服务器并获得成功的人的肩膀上。

## 埃及、Samba 与 Bug

如果更换了汽车引擎，结果最后却发现它只是没油了，这难道没有帮助吗？这看起来像是一个愚蠢的问题，但我见过太多的网络管理员因为没有检查基础问题而浪费时间。基于此，图 13.1 展示了一个分析 Samba 问题的金字塔。

图 13.1 从底到上分析 Samba 问题。

![](img/e6dc042fe420c610acdd193e834a4772_231_0.png)

金字塔底部的主题对于上层的主题是基础性的。如果服务器断开了网络，Windows 客户端无法访问 Samba 盒子上的文件共享，这并不奇怪。这种对故障排除需求的表示并不总是成立（你可以查看日志文件），但在诊断问题时，从底部开始更好。随着我们向上爬，对 Samba 内部机制的参与程度增加，最后到达使用调试器逐行单步源码的高处（或深度，取决于你的观点）。

## 我们可以使用的工具

在寻找问题的根源时，我们有三种基本资源可以使用：

- 现有的文档，例如本书、Samba 自带的 HOWTO，以及邮件列表存档

- 通过 IRC、新闻组和邮件列表等手段与管理员和用户进行交互式通信

- 软件工具，如 Samba 自带的实用程序和网络监控程序

我们将花费大部分时间时间集中在个人故障排除努力上。这并不意味着列表中的前两项不重要。额外的文档和经验丰富的管理员建议可能是无价的。本书无法包含 Samba 社区所拥有的丰富知识。谁知道呢？也许有一天你甚至有机会向某人回报。

## 文档

Samba 2.2 的文档清理投入了大量精力，尽管仍有许多工作要做。变化之一是将转换为一种名为 YODL（另一种其他文档语言）的标记语言到 SGML/DocBook。其产物之一就是《Samba-HOWTO-Collection》书。这个教程和解释集以 PDF 和 HTML 格式提供，两者都包含在 Samba 发行版中。登录 SWAT 时，可以从主页链接到 HTML 版本。

`docs/texts` 目录中存储了许多其他单独文本文件，需要更新和转换。其中被常用的是 `DIAGNOS.txt`。这是 Samba 的原始故障排除指南，尽管它已经很旧了，但许多管理员在尝试追踪问题时仍在使用它。

## 人员

Samba 社区可以是追踪问题的最佳资源之一。你必须记住，你在各种邮件列表和新闻组联系的所有人员他们想要帮助且不需要付费。这包含了许多开发 Samba 的人。这意味着修复问题的最终责任落在你肩上。

![](img/e6dc042fe420c610acdd193e834a4772_232_0.png)

在任何邮件列表或新闻组上发布或回答问题时，你应该遵守共同的网络礼仪。如果没有，你会发现人们提供的帮助有限。然而，如果你在发布时考虑到他人，通常会有回复。你可以在 http://lists.samba.org/ 找到更多关于邮件列表以及如何加入它们的信息。一些可用的列表有：

- `samba@samba.org`——关于安装、配置和维护 Samba 服务器的主要邮件列表。

- `samba-technical@samba.org`——关于 Samba 开发的邮件列表。如果你觉得可以，加入列表并从源码开始工作。

- `samba-bugs@samba.org`——这不是一个邮件列表，而是报告实际 Bug 的地址。此地址用于通用帮助。

许多人发现 IRC 通道的交互性质对于实时调试问题更有帮助。`irc.openprojects.net` 有两个热门频道。`#technical` 频道通常包含 Samba 团队成员并讨论计划。`#samba` 频道可以在遇到配置问题时使用。

Usenet 新闻组 `comp.protocols.smb` 是另一个关于配置和测试 Samba 的信息来源。

## 测试环境

为了正确处理本小时剩下的故障排除方法，我们必须对环境做出一些假设：
