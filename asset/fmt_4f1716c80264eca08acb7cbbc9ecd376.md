
你可以使用 `edquota` 命令编辑用户配额，以对文件系统的使用设置硬限制和软限制。编辑用户配额时，将启动默认的系统编辑器（除非你更改了 `EDITOR` 环境变量，否则默认为 `vi`）。

> 注意
> Red Hat 支持的任何图形化工具已不再用于配置磁盘配额。配额 mini-HOWTO 维护在 http://www.tldp.org/HOWTO/mini/Quota.html。

# Red Hat 和 Linux 命令

你将使用这些命令在 Red Hat Linux 中管理用户账户：

- `ac`—用户账户统计命令
- `chage`—设置或修改用户密码过期策略
- `chfn`—在 `/etc/passwd` 中创建或修改用户指纹信息（finger information）
- `chgrp`—修改组组成关系
- `chmod`—更改文件权限
- `chown`—更改文件所有者
- `chpasswd`—批量修改用户密码
- `chsh`—修改用户的 shell 终端
- `groups`—显示现有的组组成关系
- `logname`—显示用户的登录名
- `newusers`—批量用户管理命令
- `passwd`—创建或修改用户密码
- `redhat-config-users`—Red Hat 的图形化用户管理工具
- `su`—以另一个用户的身份执行 shell 或命令
- `sudo`—管理选定的执行权限
- `useradd`—创建、修改或管理用户（此处原文应为创建）
- `userinfo`—Red Hat 的图形化 `chfn` 命令
- `usermod`—编辑用户的登录配置
- `userpasswd`—Red Hat 的图形化用户密码命令

# 引用

- [http://www.tldp.org/HOWTO/User-Authentication-HOWTO/index.html](http://www.tldp.org/HOWTO/User-Authentication-HOWTO/index.html)—User-Authentication-HOWTO 描述了用户和组信息是如何存储和用于认证的。
- [http://www.tldp.org/HOWTO/Shadow-Password-HOWTO.html](http://www.tldp.org/HOWTO/Shadow-Password-HOWTO.html)—Shadow-Password-HOWTO 深入探讨了影子密码（shadow passwords）的深奥之处，甚至讨论了为什么你可能不想使用它们。
- [http://www.tldp.org/Security-HOWTO.html](http://www.tldp.org/Security-HOWTO.html)—Security-HOWTO 一个“必读”HOWTO，是对安全问题的良好概述。特别适用于本章关于创建账户、文件权限和密码安全的章节。
- [http://www.tldp.org/LDP/lasag/](http://www.tldp.org/LDP/lasag/)—这是一个通用指南，《Linux 系统管理员安全指南》在限制和监控用户方面有重叠章节。
- [http://www.tldp.org/LDP/lasag/index.html](http://www.tldp.org/LDP/lasag/index.html)—LSAG 管理工具索引是查看某些管理工具的好地方，但它绝不是详尽列表。
- [http://www.tldp.org/Config-HOWTO/4.html#config](http://www.tldp.org/Config-HOWTO/4.html#config)—你如何自定义某些针对特定用户的设置？Config HOWTO 配置指南提供了一些建议。
- [http://www.tldp.org/mini/Path.html](http://www.tldp.org/mini/Path.html)—人们如何知道真实的路径？Path HOWDS 对此问题进行了阐明见解。如果你想引导用户找到他们的数据和应用程序，就需要理解路径。
- [http://www.coursean.com/sudo/](http://www.coursean.com/sudo/)—`sudo` 命令是一种强大且优雅的方法，可以将特定命令的权限委托给普通用户。
- [http://www.kernel.org/pub/linux/libs/pam/index.html](http://www.kernel.org/pub/linux/libs/pam/index.html)—可插认证模块（PAM）是复杂且高度实用的应用程序，为密码提供了额外的安全性和日志。PAM 在 Red Hat 中默认启用。为了有效地使用它，并没有必要理解其所有的复杂细节。
- [http://www.enteract.com/-lspit/linux.html](http://www.enteract.com/-lspit/linux.html)—“加固 Linux 机器”；修改 Pam 配置以使用 MDS 密码，创建并使用神秘的 wheel 组。
- [http://localhost/localdomain](http://localhost/localdomain)—你的 Red Hat 系统包含许多关于此处涵盖的内容的帮助页。使用 `man -k` 根据关键词进行搜索。

# 管理文件系统

Linux 文件系统不仅仅是硬盘或软盘的格式，不仅仅是磁盘本身和格式化过程。文件系统是存储设备上数据的结构和组织。换句话说，它是数据如何在文件、磁盘驱动器和可移动介质中组织和存储的。

在本章中，你将学习文件系统的结构以及如何操作文件系统。你还学习了 Linux 可以使用的文件系统的背景和历史。本章提供了关于默认设置的一些基本信息，以及你如何调整这些设置以更好地匹配你的系统及其需求。在章节末尾，你将学习如何构建一个测试文件系统，以便你可以安全地探索所有文件系统命令，而不会对系统造成任何损坏。

# Red Hat Linux 文件系统基础

Red Hat Linux 文件系统像所有的 UNIX 文件系统一样，不仅用于存储数据，还存储有关文件的元数据，例如文件所有者、文件关联权限以及其他属性。

Red Hat Linux 文件系统比大多数人想要了解的要复杂得多。它的特征模仿了常见 UNIX 系统中的特征，以及研究或实验文件系统中包含的特征。在本章的这一部分，你将学习文件系统是什么、它是如何工作的以及如何操作它。

- Red Hat Linux 文件系统
- 创建文件系统
- 挂载文件系统
- 卷管理
- 调整文件系统
- 其他系统
- 字符设备、块设备和特殊设备

# 引用

- User-Authentication-HOWTO 描述了用户和组信息是如何存储和用于认证的。
- Shadow-Password-HOWTO 深入探讨了影子密码的深奥之处，甚至讨论了为什么你可能不想使用它们。
- Security-HOWTO 一个“必读”HOWTO，是对安全问题的良好概述。特别适用于本章关于创建账户、文件权限和密码安全的章节。
- 这是一个通用指南，《Linux 系统管理员安全指南》在限制和监控用户方面有重叠章节。
- LSAG 管理工具索引是查看某些管理工具的好地方，但它绝不是详尽列表。
- 你如何自定义某些针对特定用户的设置？Config HOWTO 配置指南提供了一些建议。
- 人们如何知道真实的路径？Path HOWDS 对此问题进行了阐明见解。如果你想引导用户找到他们的数据和应用程序，就需要理解路径。
- `sudo` 命令是一种强大且优雅的方法，可以将特定命令的权限委托给普通用户。（注：原文为 SUUser 疑为笔误，已译为 sudo）
- 可插认证模块（PAM）是复杂且高度实用的应用程序，为密码提供了额外的安全性和日志。PAM 在 Red Hat 中默认启用。为了有效地使用它，并没有必要理解其所有的复杂细节。
- “加固 Linux 机器”；修改 Pam 配置以使用 MDS 密码，创建并使用神秘的 wheel 组。
- 你的 Red Hat 系统包含许多关于此处涵盖的内容的帮助页。使用 `man -k` 根据关键词进行搜索。

# 管理文件系统

Linux 文件系统不仅仅是硬盘或软盘的格式，不仅仅是磁盘本身和格式化过程。文件系统是存储设备上数据的结构和组织。换句话说，它是数据如何在文件、磁盘驱动器和可移动介质中组织和存储的。

在本章中，你将学习文件系统的结构以及如何操作文件系统。你还学习了 Linux 可以使用的文件系统的背景和历史。。本章提供了关于默认设置的一些基本信息，以及你如何调整这些设置以更好地匹配你的系统及其需求。在章节末尾，你将学习如何构建一个测试文件系统，以便你可以安全地探索所有文件系统命令，而不会对系统造成任何损坏。

# Red Hat Linux 文件系统基础

Red Hat Linux 文件系统像所有的 UNIX 文件系统一样，不仅用于存储数据，还存储有关文件的元数据，例如文件所有者、文件关联权限以及其他属性。

Red Hat Linux 文件系统比大多数人想要了解的要复杂得多。它的特征模仿了常见 UNIX 系统中的特征，以及研究或实验文件系统中包含的特征。在本章的这一部分，你将学习文件系统是什么、它是如何工作的以及如何操作它。

- Red Hat Linux 文件系统
- 创建文件系统
- 挂载文件系统
- 卷管理
- 调整文件系统
- 其他系统
- 字符设备、块设备和特殊设备

# 引用

- User-Authentication-HOWTO 描述了用户和组信息是如何存储和用于认证的。
- Shadow-Password-HOWTO 深入探讨了影子密码的深奥之处，甚至讨论了为什么你可能不想使用它们。
- Security-HOWTO 一个“必读”HOWTO，是对安全问题的良好概述。特别适用于本章关于创建账户、文件权限和密码安全的章节。
- 这是一个通用指南，《Linux 系统管理员安全指南》在限制和监控用户方面有重叠章节。
- LSAG 管理工具索引是查看某些管理工具的好地方，但它绝不是详尽列表。
- 你如何自定义某些针对特定用户的设置？Config HOWTO 配置指南提供了一些建议。
- 人们如何知道真实的路径？Path HOWDS 对此问题进行了阐明见解。如果你想引导用户找到他们的数据和应用程序，就需要理解路径。
- `sudo` 命令是一种强大且优雅的方法，可以将特定命令的权限委托给普通用户。（注：原文为 SUUser 疑为笔误，已译为 sudo）
- 可插认证模块（PAM）是复杂且高度实用的应用程序，为密码提供了额外的安全性和日志。PAM 在 Red Hat 中默认启用。为了有效地使用它，并没有必要理解其所有的复杂细节。
- “加固 Linux 机器”；修改 Pam 配置以使用 MDS 密码，创建并使用神秘的 wheel 组。
- 你的 Red Hat 系统包含许多关于此处涵盖的内容的帮助页。使用 `man -k` 根据关键词进行搜索。

# 文件系统分区

文件系统分区是在物理驱动介质上逻辑组织区块的方式，是计算机整体文件系统的部分。没有通用的分区格式。除了常用的 DOS 分区格式（Linux 也使用），Red Hat 还提供了支持以下分区类型：

- Acorn
- Alpha OS（编译进内核）
- Amiga

## 第 10 章 管理文件系统

- Atari
- Macintosh（编译进内核）
- BSD（编译进内核）
- Minix（编译进内核）
- SunOS/Solaris（编译进内核）
- Unixware 分片（编译进内核）
- SGI（编译进内核）
- Windows 逻辑磁盘管理器
- DEC Ultrix，现由惠尔士-惠普所有

> 注意
> 如果你愿意在互联网上搜索，可能会找到其他模块和支持；请尝试在 http://freshmeat.net/ 和 http://www.google.com/linux/ 上搜索关键字 filesystems。正如开源操作系统一如既往的，任何才华横溢且有进取心的人都可以编写自己的文件系统模块。

## 网络文件系统和磁盘文件系统

我们可以将文件系统分为大类：可以通过网络使用的文件系统和本地磁盘文件系统。在使用 Red Hat Linux 时，你将获得处理这两种类型系统的所有应用程序。

网络文件系统物理上存储在本地计算机以外的地方，看起来就像是挂载在你的计算机上一样。

> 注意
> 挂载（Mounting）是 UNIX 将文件系统（也称为卷）附加到挂载点文件系统树的方法。使用 `mount` 命令将在本章稍后部分介绍。

一些常见的网络文件系统类型有：

- NFS—网络文件系统由 Sun 开发并被广泛使用。它没有内置安全机制，因为它最初设计是用于在友好的网络上运行的。虽然被某些人认为存在问题，但它很容易实现。它通常用于 UNIX 节点之间。Red Hat 支持此文件系统的客户端和服务器端安装。
- Coda—与 NFS 类似，Coda 支持离线操作和安全缓存（在网络连接丢失时保留本地副本）。Red Hat 仅提供与 Coda 的兼容性；实际的客户端和服务器代码从 http://www.coda.cs.cmu.edu/ 获取。
- InterMezzo—与 Coda 的功能类似，InterMezzo 是一个 GPL 项目。服务器守护进程可以 http://www.intermezzo.org/ 获取。
- NCP—用于挂载 Novelle 网络卷，其用法更详细地可以在 http://www.tidp.org/LDP/nag2/x-087-2-ipx.ncpfs.client.html 中的《Linux 网络管理员指南》中描述。
- SMB—面向网络的的服务器消息协议由微软开发。Linux 的实现被称为 Samba，目前运行得相当良好。它通常用于 Linux 和 Windows 节点之间。Netatalk 是 Macintosh 的等效软件。

文件系统存在于物理设备上；它们是你的台式机或笔记本电脑中的硬盘。一些常见的文件系统类型有：

- FAT 是微软开发的一种面向磁盘的、基于表的（链表）文件系统。它经常被扩展以添加新功能。微软的企业级文件系统被称为 NTFS。（你将在本章稍后部分“DOS 文件系统”中学习更多关于该系统的知识）。
- ext2、ext3 和 ReiserFS 是基于 inode（索引节点）的。（你将在本章稍后部分“Reiser 文件系统”中了解 ReiserFS。）

> 注意
> ext2/ext3 文件系统中构成一个文件的信息始于 inode。

JFS（来自国际商业机器公司的日志日志文件系统）和 XFS（来自 Silicon Graphics, Inc.）文件系统供 Red Hat Linux 使用，但主要作为这些现有文件系统迁移到 Linux 的辅助工具。

日志文件系统在驱动器数据上添加了日志（或隐藏文件）。由于数据写入磁盘的方式，内核在决定将数据放在何处时可能会持有部分数据。如果你的计算机发生故障，这些缓存数据将会丢失。日志文件系统会保留这些数据，直到内核决定正式将其写入磁盘。如果发生系统故障，特殊应用程序（`fsck`）会知道数据从未写入，并确保它被写入到正确的位置。这确保了数据不会丢失。日志文件系统实际上比这要复杂得多，但它们的机制超出了本章的讨论范围。如 ext3、ReiserFS、JFS 和 XFS 等日志文件系统是对较旧的非日志文件系统的重大改进。

## 查看你系统的文件系统

你安装的 Red Hat Linux 可能拥有其自身独特的一组可用的虚拟文件系统模块。你可以使用以下命令查看你的系统现在可以访问的文件系统（并验证你的内核对这些文件系统的支持）：

```bash
# cat /proc/filesystems
```
