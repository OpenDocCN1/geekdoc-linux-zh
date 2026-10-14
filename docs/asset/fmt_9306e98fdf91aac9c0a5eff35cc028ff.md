
手动配置配额涉及更改系统文件 `/etc/fstab` 中的条目，为所需的文件系统部分添加 `usrquota` 选项。作为简单文件系统中的示例，可以这样启用配额管理：

```
LABEL=/ ext3 defaults,usrquota 1 1
```

也可以通过使用 `grpquota` 选项启用组配额。作为 root 操作，你必须在指定的文件系统中创建一个（使用我们创建用户配额的示例）名为 `quota.user` 的文件，如下：

```
# touch /quota.user
```

使用 `quotaon` 命令开启配额的使用：

```
# quotaon -av
```

你可以使用 `edquota` 命令编辑用户配额，以设置文件系统使用的硬限制和软限制。编辑用户配额时，将启动默认的系统编辑器（除非更改了 `EDITOR` 环境变量，否则为 `vi`）。

任何用户都可以通过以下命令查看配额：

```
$ quota -v
```

> 注意
>
> Ubuntu 不支持任何配置磁盘配额的图形化工具。一个 Quota mini-HOWTO 维护在 http://www.tldp.org/HOWTO/mini/Quota.html。

# 第 10 章 管理用户

## 相关的 Ubuntu 命令

- `ac` - A 用户账户统计命令
- `change` - Sets 设置或修改用户密码过期策略
- `chfn` - 创建或修改 `/etc/passwd` 中的用户指纹（finger）信息
- `chgrp` - 修改组组成关系
- `chmod` - 更改文件权限
- `chown` - 更改文件所有者
- `chpasswd` - 批量修改用户密码的命令
- `chsh` - 修改用户的 shell
- `groups` - 显示现有的组组成
- `logname` - 显示用户的登录名
- `newusers` - 批量用户管理命令
- `password` - 创建或修改用户密码
- `su` - 以另一个用户的身份执行 shell 或命令
- `sudo` - 管理选定的执行权限
- `useradd` - 创建、修改或管理用户
- `usermod` - 编辑用户的登录配置

## 参考

- http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/_User-Authentication-HOWTO.html—《用户认证 HOWTO》描述了用户和组信息如何存储以及如何用于验证。
- http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Shadow-Password-HOWTO.html—《Shadow-Password HOWTO》深入探讨了影子密码的复杂之处，并讨论了为什么你可能不想使用它们。
- http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/Security_HOWTO.html—这是一个必读的 HOWTO，《Security HOWTO》是对安全问题的良好概述。其中关于创建账户、文件权限和密码安全的章节特别适用于本章。
- http://www.secifin.net/unix/security/Linux/Administrators_Security_Guide/—这是一本通用指南，《Linux 系统管理员安全指南》在限制和监控用户方面有有趣的章节。
- http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Config-HOWTO.html—如何自定义某些用户特定的设置？《Config 软件配置》提供了一些建议。
- http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Path.html—如何知道真实的路径？《Path HOWTO》对这个问题进行了阐明。如果你想引导用户访问他们的数据和应用程序，就需要理解路径。
- http://www.courtesan.com/sudo/—`Superuser DO` 命令是一种强大且优雅的方法，可以向普通用户授予特定命令的权限。
- http://www.kernel.org/pub/linux/libs/pam/index.html—可插认证模块（PAM）套件包含了复杂且非常有用的应用程序，为密码提供额外的安全性和日志记录。Ubuntu 默认安装了 PAM。要有效地使用 PAM，并不需要理解其复杂的细节。

# 第 11 章 自动化任务

## 本章内容

- 启动时运行服务
- 开始启动加载过程
- 手动启动和停止服务
- 任务调度
- 基础 Shell 控制
- 编写并执行 Shell 脚本
- 参考

在本章中，你将学习自动化系统的五种方法：将它们设置为系统启动时运行的服务、将它们设置为手动运行和停止的服务、调度它们在特定时间运行、在 shell 中将多个命令连接在一起，以及编写将所有内容归类到一个命令下的自定义脚本。

当你打开电源开关后，启动过程从执行存储在名为 BIOS 的芯片中的代码开始；无论你安装了什么操作系统，此过程都会发生。Linux 启动过程始于引导加载程序（boot loader）代码启动 Linux 内核，并在登录提示符出现时才结束。

作为系统管理员，你将使用在本章中学到的技能来控制你的系统服务并管理计算机上的运行级别（runlevels）。理解系统服务和状态的管理对于理解 Linux 的工作原理（特别是多用户环境中）至关重要，并将帮助你解开 Ubuntu 配置文件的神秘之纱。此外，对于所有水平的管理员来说，良好掌握处理任务调度的 `cron` 守护进程也是关重要的。

本章也是 Shell 脚本基础的介绍，即按照符合 shell 语法编写的可执行文本文件。Shell 脚本像任何其他命令一样运行，可以包含复杂的逻辑或一系列简单的 Linux 命令行指令。你还可以在 shell 程序内部运行其他 shell 脚本。在简要介绍如何在 shell 操作后，本章还讨论了几种 Linux shell 的特性和功能。

如果一切顺利，BIOS 将寻找一个可启动卷，例如软盘、CD-ROM、硬盘、RAM 磁盘或其他介质。可启动卷包含由引导加载程序应用程序（`GRUB` 或 `LILO`，尽管 Ubuntu 不提供 `LILO`）写入卷的特殊十六进制值。现代 BIOS 允许在选择用于启动的设备时具有很大的灵活性（例如，先软盘，然后是 CD-ROM，最后是硬盘），并从找到第一个设备启动。

## 开始启动加载过程

> 注意
>
> 如果 BIOS 检测到硬件问题，启动过程将失败，BIOS 将通过系统扬声器发出几声蜂鸣。这些“蜂鸣代码”指示了 BIOS 遇到的问题。代码因制造商而异，对该阶段发生问题的诊断不在本书范围内，且不涉及 Linux。如果遇到问题，你应该查阅主板手册或联系制造商。

接下来，BIOS 在可启动卷的分区扇（称为主引导记录 MBR）上寻找引导代码。MBR 包含引导器代码和分区表——可以将其视为引导的索引，以及关于如何启动的简单说明。如果 BIOS 找到了加载器，它将其加载到内存中。此时，BIOS 的工作完成，并将系统控制权交给引导加载程序。

引导加载程序在磁盘上定位 Linux 内核并将其加载到内存中。在该任务完成后，引导加载程序将系统控制权交给 Linux 内核。你可以看到这一过程是如何在一个许多不同的操作系统与相同的硬件工作的的基础上。

> 注意
>
> Linux 非常灵活，可以从 CD-ROM 上的多个镜像、通过 PXE（读作 "pix"）或 NetBoot 通过网络、或者在通过串口或网络连接控制台的无头服务器上进行启动。目前正致力于为 http://www.coreboot.org/ 创建一种特殊的 Linux BIOS，这将加速启动过程，因为 Linux 不需要典型 BIOS 提供的服务。

## 加载 Linux 内核

从总体来说，内核管理系统资源。作为用户，你并不直接与内核交互，而是与你使用的应用程序交互。Linux 将每个应用程序称为一个进程，内核为每个进程分配一个进程 ID（PID）。首先，Linux 内核加载并运行一个 `init` 进程，它被称为“所有进程之父”，因为它启动了后续每一个进程。

> 注意
>
> 如果安装了 Linux 内核文档，关于 Linux 内核加载时发生事件序列的详细信息可以在文件 `/usr/src/linux-2.6/init/main.c` 中找到。

启动过程的下一步是从屏幕上的消息开始的，显示 Linux 内核正在加载，随后屏幕将打印出一系列消息，显示每个命令的状态。如果发生失败，则会显示错误消息。在启动时向内核传递 `-quiet` 选项可以抑制其中许多消息。

如果启动过程在此处停止，系统将处于空闲状态且屏幕将为空白。为了让系统对用户有用，我们需要启动系统服务。这些服务是一些允许我们与系统交互的应用程序。

### 系统服务与运行级别 (Runlevels)

`init` 命令将 Ubuntu 引导到特定的系统状态，通常称为运行级别（runlevel）。
