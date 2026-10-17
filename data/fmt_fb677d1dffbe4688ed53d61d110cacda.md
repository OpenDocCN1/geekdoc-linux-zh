
如前所述，Ubuntu 默认通过 `sudo` 命令赋予第一个创建的用户 root 权限。如果你需要为其他用户添加此功能，可以通过将每个用户添加到 `admin` 组（在 Ubuntu 11.10 或更早版本）或 `sudo` 组（12.04 之后的任何版本），或者通过使用用户管理器工具允许他们管理系统（这可以在编辑用户属性时在“用户权限”选项卡中找到）。Ubuntu 12.04 官方发布说明中的此条注释描述了组的更改：“在 Ubuntu 11.10 之前，使用 `sudo` 工具的管理员访问是通过 `admin` Unix 组授予的。在 Ubuntu 12.04 中，管理员访问将通过 `sudo` 组授予。这使得 Ubuntu 与上游实现版本和 Debian 更加一致。为了兼容性，`admin` 组将在 12.04 中继续提供 `sudo`/管理员访问权限。”

## 磁盘配额

在具有许多用户的大型系统上，你通常需要控制用户可以使用磁盘空间量。磁盘配额专门为此目的设计。配额按分区管理，可以为单个用户和组设置；组配额不需要与组内个人的累计配额一样大。

当创建文件时，用户和组都拥有它们；文件的所有权始终是文件元数据的一部分。这使得基于用户和组的配额易于管理。

## 注意

磁盘配额管理在家庭系统中并不真正有用或需要，在小型办公室系统中也很少使用。在两种情况下，你都不可能看到或实现它。

要管理磁盘配额，你的系统中必须安装了 `quota` 和 `quotatool` 软件包。Ubuntu 的磁盘配额管理默认启用，传统上一直由系统管理员手动启用和配置。系统管理员使用配额命令族，例如使用 `quotacheck` 初始化配额数据库文件，使用 `edquota` 编辑和设置配额，`setquota` 配置磁盘配额，`quotaon` 或 `quotaoff` 控制服务。（其他工具还包括 `warnquota`，用于向超过磁盘空间使用限制限制的用户自动发送邮件。）

## 实现配额

即使在你的 Ubuntu 系统上安装了配额软件包，配额默认也是不启用的。当安装并启用配额时，你可以看到带有用户配额、组配额的分区，或者通过查看 `/etc/fstab` 文件中的第四字段。例如，`/etc/fstab` 中的其中一行显示 `/home` 分区启用了配额：

```
/dev/hda5 /home ext3 defaults,usrquota,1 1
```

启用了配额的分区根目录下将包含 `quota.user` 或 `quota.group` 文件（如果启用了两种类型的配额，则两者都有），文件将包含实际配额。这些文件的权限应该是 `600`，以便用户无法读取或写入它们（否则，用户会更改它们）。……要初始化磁盘配额，必须重新挂载分区。可以通过以下操作轻松完成：

```
matthew@seymour:~ $ sudo mount -o ro remount partition_to_be_remounted
```

可以使用以下工具：

- `quotaon`
- `quotaoff`
- `repquota`
- `quotacheck`
- `edquota`

## 手动配置配额

手动配置配额涉及更改 `/etc/fstab` 中的条，将 `usrquota` 添加到目标分区。作为 root 操作员，你可以如下启用组级配额：

[点击查看代码图片]

```
/dev/hda5 /home ext3 defaults,usrquota,1 1
```

你也可以使用以下启用用户配额：

[点击查看代码图片]

```
matthew@seymour:~ sudo quotaon -av
```

注意：在编辑用户配额时会启动默认系统编辑器（除非你更改了 `EDITOR` 环境变量）。任何用户都可以通过以下命令查看配额：

```
matthew@seymour:~ quota -v
```

## 相关 Ubuntu 命令

你使用这些命令管理 Ubuntu 用户账户：

- `age`—设置或修改密码过期策略
- `chfn`—编辑或创建 `/etc/passwd` 中的用户信息
- `chgrp`—修改组组成
- `chmod`—更改文件权限
- `chown`—更改文件所有者
- `chpasswd`—批量修改密码的命令
- `chsh`—修改用户的 shell
- `groups`—显示现有组组成
- `logame`—显示用户的登录名
- `newsusers`—批量用户管理
- `passwd`—创建或修改密码
- `su`—以其他用户执行 shell 或命令
- `sudo`—管理用户执行权限
- `useradd`—创建、修改或管理用户
- `usermod`—编辑用户的配置文件

## 参考文献

- http://tldp.org/HOWTO/User-Authentication-HOWTO/—User-Authentication HOWTO 描述了用户和组信息是如何存储和用于认证的。
- http://tldp.org/HOWTO/Shadow-Password-HOWTO.html—Shadow-Password 深入探讨了密码的奥秘并解释了为什么你可能不想使用它们。
- http://tldp.org/HOWTO/Security-HOWTO/—一个必读的 HOWTO，Security HOWTO 是安全问题的良好概述。本章特别适用于关于账户、文件权限和密码安全的章节。
- http://tldp.org/LDP/sag/html/index.html—一个通用指南，Linux 系统管理员安全指南包含关于限制和监控用户的有趣章节。
- www.kernel.org/pub/linux/libs/pam—可插件认证模块（PAM）套件包含了复杂且非常有用的应用程序为密码提供额外的安全保护和日志。Ubuntu 默认安装了 PAM。要有效地使用 PAM，并不需要理解其复杂的细节。

## 第 14 章 任务自动化与 Shell 脚本

### 本章内容

- 使用 `at`、`batch`、`cron` 和 `rtcwake` 调度任务
- 基础 Shell 控制
- 编写和执行 Shell 脚本
- 参考文献

在本章中，我们将介绍如何使用任务调度器在你的系统上实现任务自动化。本章还介绍了创建 shell 脚本的基础知识，shell 脚本是按照符合 shell 语法编写的可执行文本文件。Shell 脚本像 Linux 下的任何其他命令一样运行，可以包含复杂的逻辑，也可以简单的 Linux 命令行指令。你还可以在 shell 程序内部运行其他 shell 脚本。在简要介绍如何从 shell 命令行工作后，本章讨论了多种 Linux shell 的特性和功能。你将学习如何使用 `bash` 编写并执行一个简单的程序，`bash` 是流行的 Linux shell 之一，也是 Ubuntu 等其他发行版的默认 shell。

## 调度任务

在 Ubuntu 中有三种调度命令的方法，它们的工作方式各不相同。第一种是 `at` 命令，它指定在今天之后的特定日期和时间运行命令。第二种是 `batch` 命令，它实际上是一个脚本，会将你的操作重定向到 `at` 命令，并设置一些额外的选项，在系统空闲时运行你的 cron 任务。最后一种选择是 `cron` 守护进程，它是 Linux 在指定时间执行任务的方式。

## 使用 at 和 batch 调度后后任务

如果你有一个耗时较的任务想要运行，但你不想在登录状态下执行它，可以使用 `at` 命令告诉 Ubuntu 稍后运行，你必须先安装它。该包名与工具名相同：`at`。要使用 `at`，你需要告诉它你想在何时运行，然后按回车键。随后你将看到一个以 `at>` 开头的新提示符，在你按下 Ctrl+D 之前输入的所有内容将是你想让 `at` 执行的命令。

当指定时间到达时，at 会逐个且按顺序执行每个操作，这意味着后执行命令可以依赖于先执行命令的结果。在接下来的示例中，在晚上 8:00 之后运行，`at` 用于在网络应该空闲的时间下载并提取最新的 Linux 内核：

点击此处查看代码图片

```
matthew@semour:~$ at now + 7 hours
at> wget http://www.kernel.org/pub/linux/kernel/v3.0/linux-3.0.tar.bz2
at> tar xvfjip linux-3.0.tar.bz2
at> <EOT>
job 2 at 2011-07-08 20:01
```

将 `now + 7 hours` 指定为时间可能不像你预期的那样：at 会在晚上 8:00 执行“现在”，因此命令将在凌晨 3:00 运行。

如果你有一个更复杂的任务，可以使用 `-f` 参数让 `at` 从文件中读取内容，如下所示：

点击此处查看代码图片

```
echo wget http://www.kernel.org/pub/linux/kernel/v3.0/linux-3.0.tar.bz2\
tar xvfjip linux-3.0.tar.bz2 > myjob.job
at -f myjob.job tomorrow
```

如你所见，at 对它接收的时间格式非常灵活；你可以通过三种方式指定时间：
