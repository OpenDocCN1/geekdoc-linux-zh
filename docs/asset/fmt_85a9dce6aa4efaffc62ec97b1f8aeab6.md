
根据系统和系统管理员的不同，可能存在其他文件。重点在于，每个用户的环境可以通过使用 `/etc/skel` 中的文件全局设置，并通过允许用户修改其 `/home` 目录中的文件进行单独设置（或不允许，取决于系统管理策略）。

系统记录所有用户登录，以及 `su` 和 `sudo` 命令的所有使用情况，供系统管理员审查。(`init`、`syslogd` 和 `klogd` 应用程序创建这些日志。)现代安全监控程序（或你创建的简单脚本）可以扫描这些文件（如 `/var/log/messages`）以检测异常并标记可能的安全违规行为。

# 磁盘配额

在拥有大量用户的大型系统中，你需要控制用户可访问的磁盘空间量。磁盘配额旨在实现此目的。按每个分区管理的配额可以为个人用户和组设置；组的配额不必像组内个人的总配额那么大。

创建文件时，用户和组都拥有它们；文件的所有权始终是文件元数据的一部分。这使得基于用户和组的配额易于管理。

> 磁盘配额管理从未在主家系统上执行，并且在小型办公系统上也很少（如果有的话）执行。

要管理磁盘配额，你的系统上必须安装配额软件包；它通常默认安装。Fedora 中的配额管理默认未启用，传统上由系统管理员手动启用和配置。系统管理员使用一系列配额命令，例如使用 `quotacheck` 初始化配额数据库文件，使用 `edquota` 设置和编辑用户配额，使用 `setquota` 配置磁盘配额，以及使用 `quotaon` 或 `quotaoff` 控制该服务。 （其他实用程序包括 `warnquota`，用于自动向超过磁盘空间使用限制的用户发送电子邮件。）

## 实施配额

再次强调，即使你的系统上安装了配额软件包，配额也可能默认未启用。当配额安装并启用后，你可以看到哪些

通过查看 `/etc/fstab` 文件中的第四个字段，可以判断分区是否启用了用户配额、组配额，或者两者兼有。例如，`/etc/fstab` 中的一行显示 `/home` 分区已启用配额：

```
/dev/hda5       /home       ext3       defaults,usrquota,grpquota 1 1
```

启用了配额的分区根目录下会包含 `quota.user` 或 `quota.group` 文件（如果启用了两种类型的配额，则两个文件都会存在），这些文件将包含实际的配额设置。这些文件的权限应设置为 600，以防止用户读取或写入它们。 （否则，用户可能会修改它们，从而为他们的音乐文件和互联网艺术收藏提供充足的空间。）为了初始化磁盘配额，必须重新挂载这些分区。这可以通过以下命令轻松完成：

```
# mount -o ro,remount partition_to_be_remounted mount_point
```

底层的控制台工具（附带手册页）包括：

- `quotaon`、`quotaoff`——在分区上开关配额。
- `repquota`——生成用户和组的汇总状态报告。
- `quotacheck`——更新配额状态（比较新的和旧的磁盘使用率表）；它在 `fsck` 之后运行。
- `edquota`——一个非常基础的配额管理命令。

### 手动配置配额

手动配置配额涉及修改系统文件系统表 `/etc/fstab` 中的条目，以将 `usrquota` 挂载选项添加到文件系统的所需部分。例如，在一个简单的文件系统中，可以这样启用配额管理：

```
LABEL=/        /        ext3        defaults,usrquota        1 1
```

通过使用 `grpquota` 选项，也可以启用组级配额。作为 root 操作员，您必须在文件系统的指定部分创建一个名为 `quota.user` 的文件（以创建用户配额的示例为例），如下所示：

```
# touch /quota.user
```

然后，您应该使用 `quotaon` 命令启用配额的使用：

```
# quotaon -av
```

接着，您可以使用 `edquota` 命令编辑用户配额，以设置文件系统使用的硬性限制和软性限制。当编辑用户的配额时，系统将启动默认的系统编辑器（除非您更改了 `EDITOR` 环境变量，否则默认为 `vi`）。

任何用户都可以通过以下命令查看他们自己的配额：

```
$ quota -v
```

> **注意**
>
> Fedora Core 不支持任何用于配置磁盘配额的图形工具。在 http://www.ltlp.org/HOWTO/mini/Quota.html 上维护有一份配额迷你 HOWTO。

> **相关的 Fedora 命令**
>
> 您将在 Fedora 中使用这些命令来管理用户账户：
>
> - `ac`—用户账户统计命令
> - `chage`—设置或修改用户密码过期策略
> - `chfn`—创建或修改 `/etc/passwd` 中用户的 finger 信息
> - `chgrp`—修改组成员身份
> - `chmod`—更改文件权限
> - `chown`—更改文件所有权
> - `chpasswd`—批量修改用户密码的命令
> - `chsh`—修改用户的 shell
> - `groups`—显示现有的组成员身份
> - `loginname`—显示用户的登录名
> - `newusers`—批量用户管理命令
> - `passwd`—创建或修改用户密码
> - `su`—作为其他用户执行 shell 或命令
> - `sudo`—管理特定用户执行权限
> - `system-config-users`—Fedora 的图形化用户管理工具
> - `useradd`—创建、修改或管理用户
> - `userinfo`—Fedora 的图形化 `chfn` 命令
> - `usermod`—编辑用户的登录配置
> - `userpasswd`—Fedora 的图形化用户密码命令

## 参考

http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/_User-Authentication-HOWTO.html—用户身份验证 HOWTO 描述了用户和组信息是如何存储和用于身份验证的。

http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Shadow-Password-HOWTO.html—影子密码 HOWTO 深入探讨了影子密码的细微之处，甚至讨论了您为什么可能不想使用它们。

http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/_Security-HOWTO.html—一份“必读”的 HOWTO，安全 HOWTO 是对安全问题的良好概述。特别适用于本章的是关于创建账户、文件权限和密码安全的章节。

http://www.secinf.net/unix_security/Linux_Administrators_Security_Guide/—这是一份通用指南，Linux 系统管理员安全指南中有关于限制和监控用户的有趣章节。

http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Config-HOWTO.html—如何自定义某些特定的用户设置？软件配置 HOWTO 提供了一些建议。

http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Path.html—如何知道真实的路径？路径 HOWTO 阐明了这个问题。如果您想引导用户访问他们的数据和应用，您需要理解路径。

http://www.courtesan.com/sudo/—`sudo` 命令是一种强大而优雅的方式，可以将特定命令的权限委派给普通用户。

http://www.kernel.org/pub/linux/libs/pam/index.html—可插拔身份验证模块（PAM）是复杂且非常实用的应用程序，为密码提供额外的安全性和日志记录。Fedora Core 默认安装了 PAM。有效地使用 PAM 并不需要了解其内部细节。

http://localhost/localhost/—您的 Fedora Core 系统包含了几乎涵盖此处所有内容的 man 和 info 页面。使用 `man -k` 可以根据关键字进行搜索。

# 第 14 章

## 任务自动化

- 在启动时运行服务
- 手动启动和停止服务
- 计划任务
- 基本 Shell 控制
- 编写和执行 Shell 脚本
- 参考

在本章中，您将学习在系统上自动执行任务的五种方法：将它们制作成在系统启动时运行的服务，将它们制作成您手动启动和停止的服务，安排它们在特定时间运行，在 shell 上将多个命令连接在一起，以及编写将一切组合在一条命令下的自定义脚本。
