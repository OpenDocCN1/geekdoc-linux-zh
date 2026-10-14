
用户可以是个人，也可以是一个组（以 `%` 标识名称为组）。`host_computer` 通常对于网络上的所有主机为 `ALL`，对于本地机器为 `localhost`，但主机也可以引用为子网或任何特定主机。`sudoers` 行中的命令可以是 `ALL`、特定命令列表，或对特定命令的限制（通过在命令前加 `!` 形成）。`sudoers` 行有许多选项可供使用，并可以使用别名（`aliases`）来简化权限分配。同样，`sudoers` man 页提供了详细信息，这里有几个示例：

如果我们添加以下这一行：

```
%wheel ALL= (ALL) NOPASSWD: ALL
```

那么我们添加到 `wheel` 组的任何用户都可以无需密码执行任何命令。

假设我们想赋予用户 `john` 跨网络权限，使其能够图形界面添加用户。我们会添加以下行：

```
john ALL=/users-admin
```

或者，我们可能只在她的本地计算机上授予权限：

```
john 192.168.1.87=/usr/bin/users-admin
```

如果我们想给编辑器组授予系统范围内的无密码删除文件权限，我们使用以下命令：

```
%editors ALL=NOPASSWD: /bin/rm
```

如果我们想给每个用户授予在本地主机无密码挂载 CD 驱动器的权限，按如下方式操作：

```
ALL localhost=NOPASSWD: /sbin/mount /dev/scd0 /mnt/cdrom /sbin/umount /mnt/cdrom
```

在构建 `sudoers` 文件时可以使用通配符。可以使用别名让定义用户和组变得更容易。`sudoers` 的主页包含了一些示例，`komar.org/pres/sudo/toc.html` 提供了关于大型公司使用 `sudo` 的说明性笔记和注释。`sudo.ws` 上的 `sudo` 主页也是获取额外说明和示例的有用资源。

以下命令将向用户显示他们有权使用的命令列表：

```
mathew@semour:-~$ sudo -l
```

### 添加额外的 sudo 用户

如前所述

## 磁盘配额

在具有许多用户的大型系统中，你通常需要控制用户可以使用的磁盘空间量。磁盘配额（Disk quotas）是专门为此目的而设计的。配额按分区管理，可以为单个用户和组设置；组的配额不需要与组内个人的总配额一样大。

当创建文件时，用户和组都拥有它们；文件的所有权始终是文件元数据的一部分。这使得基于用户和组的配额易于管理。

> 磁盘配额管理在家庭系统中并不真正有用或需要，在小型办公系统中也也极少使用。在这两种情况下，你都不可能看到或实现此功能。

要管理磁盘配额，你必须在系统中安装 `quota` 和 `quotatool` 软件包。Ubuntu 的配额管理默认未启用，传统上由系统管理员手动启用和配置。系统管理员使用 `quota` 系列命令，例如使用 `quotacheck` 初始化配额数据库文件，使用 `edquota` 设置和编辑用户配额，使用 `setquota` 配置磁盘配额，以及使用 `quotaoff` 控制服务（其他工具还包括 `warnquota`，用于向超过磁盘空间限制的用户自动发送邮件）。

## 实现配额

即使在 Ubuntu 系统上安装了配额软件包，配额默认也是未启用的。当安装并启用配额时，可以通过查看 `/etc/fstab` 文件的第四字段来查看哪些分区启用了用户配额、组配额或两者。例如，`/etc/fstab` 中的某行显示 `/home` 分区启用了配额：

```
/dev/hda5    /home    ext3    defaults,usrquota,grpquota 1 1
```

```
matthew@seymour:-$ sudo mount -o ro, partition_to_be_remounted_mount_point
```

底层控制工具（带有 man 页）如下：

- `quotaon`, `quotaoff`—开启或关闭分区的配额

- `repquota`—对用户和组进行摘要状态报告

# 第 12 章 管理用户

- `quotacheck`—更新配额状态（比较新旧磁盘使用表）；在事实发生后运行

- `edquota`—一个基础的配额管理命令

## 手动配置配额

手动配置配额涉及更改系统文件系统表 `/etc/fstab` 中的条目，以便在文件系统的指定部分添加 `userquota` 挂载选项。作为简单文件系统中的一个示例，你可以这样启用配额管理：

```
LABEL=      / ext3 defaults,usrquota 1 1
```

你还可以使用 `grpquota` 选项启用组级配额。作为 root 操作员，你必须在文件系统的指定部分（使用我们创建用户配额的示例）创建一个名为 `quota.user` 的文件，如下：

```
matthew@seymour:~ sudo touch /quota.user
```

然后你应该使用 `quota` 命令开启配额的使用：

```
matthew@seymour:~ sudo quota -av
```

你可以使用 `edquota` 命令编辑用户配额，以设置文件系统使用的硬限制和软限制。在编辑用户配额时，会启动默认系统编辑器（除非你更改了 `EDITOR` 环境变量，否则为 `vi`）。

任何用户都可以通过以下命令查看自己的配额情况：

```
matthew@seymour:~ quota -v
```

> 注意

Ubuntu 不支持任何允许你配置磁盘配额的图形化工具。`www.tldp.org` 维护有一个配额迷你教程（Quota mini-HOWTO）。

## 相关 Ubuntu 命令

你使用这些命令来管理 Ubuntu 用户账户：

- `ac`—用户账户统计命令

- `change`—设置或修改用户密码过期策略

- `chfn`—创建或修改 `/etc/passwd` 中的用户指纹信息

- `chgrp`—修改组组成

- `chmod`—更改文件权限

- `chown`—更改文件所有权

- `chpasswd`—批量修改用户密码的命令

- `chsh`—修改用户的 shell

- `groups`—显示组组成

- `logname`—显示用户的登录名

- `newusers`—批量用户管理命令

- `passwd`—创建或修改用户密码

- `su`—作为另一个用户执行 shell 或命令

- `sudo`—管理选择执行权限

- `useradd`—创建、编辑或管理用户

- `usermod`—编辑用户的登录配置

## 参考文献

- `http://tldp.org/HOWTO/User-Authentication-HOWTO/`—User-Authentication HOWTO 描述了用户和组信息是如何存储和用于认证的。

- `http://tldp.org/HOWTO/Shadow-Password-HOWTO.html`—ShadowPassword HOWTO 深入了影子密码，甚至讨论了为什么你可能不想使用它们。

- `http://tldp.org/HOWTO/Security-HOWTO/`—必读的 HOWTO，Security HOWTO 是安全问题的概述。本章中创建账户、文件权限和密码安全的章节特别适用。

- `http://tldp.org/LDP/sag/html/index.html`—通用指南，Linux 系统管理员安全指南包含关于限制和监控用户的有趣章节。

- `www.kernel.org/pub/linux/libs/pam`—可插认证模块（PAM）包含了复杂且非常有用的应用程序，可为密码提供额外的安全性和日志记录。Ubuntu 默认安装了 PAM。有效使用 PAM 并不需要理解内部细节。

# 第 13 章

# 任务自动化与 Shell 脚本

## 本章内容

- 任务调度

- Shell 控制

- 编写和执行 Shell 脚本

- 参考文献

在本章中，我们将介绍如何使用任务调度器来实现系统任务的自动化。本章还将介绍创建 shell 脚本的基础知识，shell 脚本是符合 shell 语法的可执行文本文件。Shell 脚本在 Linux 下像任何其他命令一样运行，可以包含复杂的逻辑，也可以是简单的 Linux 命令行指令。你还可以在 shell 程序内部运行其他 shell 脚本。在对 shell 命令行操作进行简要介绍后，本章将讨论了多种 Linux shell 的特性和功能。你将学习如何使用 `bash` 编写并执行简单的 shell 程序，`bash` 是最流行的 Linux shell 之一，也是 Ubuntu 以及大多数其他发行版的默认 shell。

## 任务调度

在 Ubuntu 中有三种调度命令的方法，它们的工作方式各不相同。第一种是 `at` 命令，它可以指定在相对于今天的特定时间和日期运行命令。第二种是 `batch` 命令，它实际上是一个重定向到 `at` 命令的脚本，并设置了一些额外的选项，以便在系统空闲时运行命令。最后一种选择是 `cron` 守护进程，它是 Linux 在给定时间执行任务的方式。

# 使用 at 和 batch 调度以后的任务
