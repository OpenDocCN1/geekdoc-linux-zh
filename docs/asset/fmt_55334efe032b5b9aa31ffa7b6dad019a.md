
## 安装后 OES 组件配置

在安装 OES 期间，可以修改每个 OES 组件的配置。安装后也可以访问相同的配置页面。这些页面可以通过 YaST 中的特定组件模块访问。

YaST 可以从终端或图形环境中访问。从终端访问 YaST，执行 `yaast`。从图形环境中访问 YaST，执行 `yast2` 或从应用程序菜单启动 YaST 启动器。

YaST 分为如下：

- 软件
- 硬件
- 系统
- 网络设备

## OES Linux 安装后的常用任务

- 网络服务
- 安全与用户
- 杂

在每个类别下，都有用于配置 OES Linux 特定组件的模块。其中许多模块用于配置传统的 SLES 组件，例如系统语言以及日期和时间。然而，也可以通过 YaST 进行 OES 特有的组件管理。表 2.2 列出了这些 OES 特有模块的位置。

| YAST 类别 | OES 组件 |
|---|---|
| 系统 | Novell 存储服务 (NSS)<br>Novell 集群服务 (NCS)<br>存储管理服务 (SMS) |
| 网络服务 | NCP 服务器<br>NetStorage<br>Novell 健康监控<br>Novell QuickFinder<br>Novell Samba<br>Virtual Office<br>eDirectory<br>eGuide<br>iFolder 2.x<br>iManager<br>iPrint |
| 安全与用户 | Linux 用户管理 |

有关如何使用这些模块的信息，请查看本书书的目录，或参考在线 OES 文档。

## 使用 Red-Carpet 更新 OES Linux 组件

完成 OES Linux 的安装后，使用 OES 在线更新工具——Red-Carpet check OES 更新是一个好主意。

Red-Carpet（或称为配套的终端地毯）可以从 YaST 的“软件”类别访问。从该类别，可以使用“在线更新”模块开始更新过程。如果是您首次执行在线更新，将要求使用您的 Novell ID 和密码注册服务器，这些信息您在购买此产品时应该收到。

激活后，您应该能够轻松选择可用的 OES 补丁并将其应用到新服务器上。有关此过程的更详细说明，请参阅第 6 章的“更新 OES Linux”部分。

## 使用 SUSE Linux Enterprise Server 9 工作

### 瞬时访问

使用 SUSE Linux Enterprise Server (SLES) 需要了解登录过程，包括本地账户文件、系统账户以及身份标识管理。

使用控制台 shell 或图形化环境是在 SLES 机器上工作的两种可能方法。

熟悉 SLES 安装环境需要对文件系统布局有深入的了解。本章记录并解释了基本的的文件系统组件。还描述了基础的文件系统权限。

SLES 帮助系统包含了对 `man` 和 `info` 页的使用。

在控制台会话中编辑文本文件通常使用 `vi` 编辑器完成。文中解释了 `vi` 的模式，并提供了 `vi` 常用命令表。

尽管使用 SUSE Linux Enterprise Server (SLES) 的完整指南超出了本书的范围，但为了成功部署 OES Linux，理解 Linux 和基础的 Linux 功能是必要的。

# 第 3 章：使用 SUSE Linux Enterprise Server 9 工作

本章将讨论基本的 Linux 概念，例如理解登录过程、使用命令行和图形化环境、熟悉文件系统、使用可用的帮助系统以及文本编辑工具。精通 Linux 的管理员可能想跳到第 6 章“SUSE Linux Enterprise 管理”以获取更深入的 SLES 信息，但浏览本章作为 SUSE 特有工具和环境的介绍可能会有所帮助。如果您是 Linux 新手，本章应该可以您入门，但它的目的并不是一份全面的或初级 Linux 指南。

如果您想更深入研究 Linux 基础或 SLES 管理，Novell 的认证 Linux 专业人员 (CLP) 和认证 Linux 工程师 (CLE) 项目非常值得关注。有关 Novell SUSE Linux 认证选项的更多信息，请参见附录 A，“CLE 认证选项”。

## 在 Linux 中登录

安装并启动 SLES 服务器后，您将看到文本或图形登录提示符。输入正确的用户名和密码将让您获得服务器的访问权限。对于管理员来说，理解如何授予访问以及如何配置 SLES 用户账户是重要的。在实施如 Linux 用户管理 (LUM) 等 OES 组件之前，拥有这些知识也是重要的。下一节将简要讨论本地用户账户以及本地验证过程的工作原理。

## 本地账户文件

在 SLES9 服务器上，本地用户账户定义在 `/etc/passwd` 文件中，如图 3.1 所示。该文件中定义的每个用户必须具有某些属性，服务器使用这些属性来确定用户权限和登录名称等。`/etc/passwd` 的格式是每行一个账户。

`passwd` 文件中的每行由五个字段组成，用冒号隔开。这些字段为用户账户被操作系统视为有效提供了必要的属性。每个字段的作用在表 3.1 中记录，对应于 `jdoe:x:1000:100:John Doe:/home/jdoe:/bin/bash` 条目。

## 在 Linux 中登录

图 3.1

一个 `/etc/passwd` 文件的示例。

```
root@lxoes1:~\File Edit View Terminal Tabs Help
lxoes1:~ # head /etc/passwd
root:x:0:0:root:/root:/bin/bash
demon:x:1:1:bin:/bin:/bin/bash
daemon:x:2:2:Damon:/var/spool/lpd:/bin/bash
lp:x:4:7:lp:/var/spool:/
mail:x:8:12:Mail daemon:/var/spool/mailqueue:/bin/false
news:x:9:9:News system:/dev/null
uucp:x:10:14:ucp system:/etc/uccp:/bin/bash
games:x:11:11:Games:/var/games:/bin/bash
man:x:12:12:Manual pages:/var/man:/bin/bash
atd:x:25:25:Batch jobs:/var/atd:/bin/bash
lxoes1:~ #
```

表 3.1

`/etc/passwd` 条目的解释

| 字段项 | 描述 |
| --- | --- |
| jdoe | 用户名。 |
| x | 密码字段。如果此字段为 "x"，则启用影子密码。 |
| 1000 | 此账户的数值用户 ID (UID)。 |
| 100 | 此账户的数值组 ID (GID)。 |
| John Doe | GECOS 字段。通常用于用户的全名。 |
| /home/jdoe | 用户主目录。 |
| /bin/bash | 用户默认 shell。 |

如果 `/etc/passwd` 中的第二个字段为 "x"，则启用影子密码。影子密码提供了更安全的环境，并允许密码老化选项。当使用密码时，有一个额外的文件用于存储加密密码。该文件是 `/etc/shadow`。表 3.2 解释了该文件的字段，对应于 `jdoe:Aztge5TrGn:1202:0:38:7`。

表 3.2:

表 3.2

`/etc/shadow` 条目的解释

| 字段项 | 描述 |
| jdoe | 用户名。 |
| Aztge5TrGn | 加密密码。 |
| 1202 | 密码上次更改日期。此值是 1970 年 1 月 1 日到密码更改之天的数。 |
| 0 | 密码可以更改的天数。 |
| 38 | 密码过期后必须更改的天数。 |
| 7 | 密码过期前警告用户更改密码的天数。 |
| <blank> | 禁用日期。此值是 1970 年 1 月 1 日到账户禁用的天数。 |

在 `/etc/passwd` 文件中，第四字段包含指定用户主组的 GID。当用户创建文件和目录时，新的文件系统对象获得用户所有者组所有者。用户所有者是创建文件系统的 UID。组所有者是创建对象时用户主组的 GID。（在查看文件列表时，UID 和 GID 数字都会转换为用户名和组名。）本地组定义在 `/etc/group` 文件中。表 3.3 显示了 `users:x:100:tjohnson,mblack` 条目的字段及其定义。）

表 3.3

| 字段项 | 描述 |
| --- | --- |
| users | 组名。 |
| x | 加密密码。此字段中的 "x" 表示正在使用影子组文件。 |
| 100 | 数值组 ID (GID)。 |
| tjohnson,mblack | 当前组的次要成员。 |

## 登录 Linux

可以使用多种实用程序来创建和修改本地用户账户及组。在 SLES 中，可以使用 YaST 工具轻松创建这些账户。（有关 YaST 的信息可以在第 6 章中找到。）用户也可以使用多种命令行工具向系统添加用户和组。表 3.4 列出了其中的一些实用程序。

# 表 3.4
