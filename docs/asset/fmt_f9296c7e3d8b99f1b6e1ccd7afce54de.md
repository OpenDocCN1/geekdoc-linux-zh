
- `chfn`——创建或修改 `/etc/passwd` 中的用户指纹信息
- `chgrp`——修改组关系
- `chmod`——更改文件权限
- `chown`——更改文件所有者
- `chpassword`——批量修改用户密码的命令
- `csh`——修改用户的 shell
- `groups`——显示现有的组关系
- `logname`——显示用户的登录名
- `newusers`——批量用户管理命令
- `passwd`——创建或修改用户密码
- `su`——以另一个用户的身份执行 shell 或命令
- `sudo`——管理选定用户的执行权限
- `useradd`——创建、修改或管理用户
- `usermod`——编辑用户的登录配置

## 参考文献

- http://tldp.org/HOWTO/User-Authentication-HOWTO/——[User-Authentication] 描述了用户和组信息如何存储以及用于身份验证。
- http://tldp.org/HOWTO/Shadow-Password-HOWTO.html——[Shadow-Password HOWTO] 深入探讨了影子密码的复杂之处，甚至讨论了为什么你可能不想使用它们。
- http://tldp.org/HOWTO/Security-HOWTO/——[Security HOWTO] 这是一个必读的 HOWTO，是对安全问题的良好概述。关于创建账户、文件权限和密码安全的章节特别适用于本章。
- http://tldp.org/LDP/sag/html/index.html——一个通用指南，《Linux 系统管理员安全指南》包含关于限制和监控用户的有趣章节。
- www.kernel.org/pub/linux/libs/pam——可插认证模块 `PAM` 套件包含了复杂且极其有用的应用程序，为密码提供额外的安全性和日志记录。Ubuntu 默认安装 `PAM`。要有效使用它，并不理解 `PAM` 的复杂细节。

# 第 12 章
## 任务自动化与 Shell 脚本

在本章中，我们将介绍如何使用任务调度器自动执行系统上的任务。本章还介绍了创建 shell 脚本（即符合 shell 语法编写的可执行文本文件）的基础知识。Shell 脚本像 Linux 下的任何其他命令一样运行，可以包含复杂的逻辑或简单的系列 Linux 命令行指令。你还可以在 shell 程序内部运行其他 shell 脚本。在简要介绍如何从 shell 命令行工作后，本章将讨论 Linux shell 的特性和功能。你将了解到如何使用 `bash` 编写并执行一个简单的 shell 程序，`bash` 是最流行的 Linux shell 之一，也是 Ubuntu 以及大多数其他发行版的默认 shell。

## 任务调度

在 Ubuntu 中有三种调度命令的方法，它们的工作方式各相同。第一种是 `at` 命令，它指定在相对于今天的特定时间和日期运行命令。第二种是 `batch` 命令，它将你重定向到 `at` 并设置一些额外选项，以便你的命令在系统空闲时运行。最后一种选择是 `cron` 守护进程，它是 Linux 在给定时间执行任务的方式。

## 使用 at 和 batch 调度后执行的任务

如果你有一个耗时任务想要运行，但不想在登录状态下执行它，可以使用 `at` 命令告诉 Ubuntu 稍后运行。

## 本章内容

- 使用 `at`、`batch` 和 `cron` 调度任务
- 基础 Shell 控制
- 编写和执行脚本
- 参考文献

使用 `at` 时，你会看到一个新的提示符，输入你要运行的内容然后按回车。`at>`，你在按下 `Ctrl+D` 之前输入的所有内容都是你想运行的命令。

当指定时间到达时，`at` 会逐个顺序执行每个操作，这意味着后来的命令可以依赖先前命令的结果。在下一个示例中，在晚上 8:00 之后运行，`at` 用于在网络应该处于空闲的时间下载并提取最新版本的 Linux 内核：

```
mathew@seymour:~ at now + 7 hours

at> wget http://www.kernel.org/pub/kernel/v3.0/linux-3.0.tar.bz2

at> tar xvfjp linux-3.0.tar.bz2

at> <EOT>

job 2 2011-07-08 20:01
```

指定 `now + 7 hours` 为你预期的时间：`at` 是晚上 8:00 运行的，因此命令将在凌晨 3:00 之后运行。

如果你有一个更复杂的任务，可以使用 `-f` 参数从文件读取你的命令，如下所示：

```
echo wget http://www.kernel.org/pub/kernel/v3.0/linux-3.0.tar.bz2
```

指定 `now + 7 hours` 为你预期的时间：`at` 是晚上 8:00 运行的，因此命令将在凌晨 3:00 之后运行。

如果你有一个更复杂的任务，可以使用 `-f` 参数从文件读取你的命令，如下所示：

`at` `batch`。你可以将用户名输入到 `@at.deny` 中，每行一个，以停止这些调度作业。

或者，你也可以使用 `@at.allow` 文件；该文件默认并不存在。如果你有一个空的 `@at.allow` 文件，则除了 root 之外，没有任何人允许调度作业。通过 `@at.deny`，你可以将用户名每行一个地添加到 `@at.allow` 中，这些用户就可以调度作业。你应该在 `@at.deny` 或 `@at.allow` 中二选一。当尝试运行 `@at` 或 `batch` 时，Ubuntu 会在 `@at.deny` 中检查其用户名。如果该用户名在其中，或者 `@at.allow` 不存在，Ubuntu 仍会在 `@at.deny` 中检查其用户名。如果其用户名在 `@at.deny` 中或不存在，则该用户不被允许调度作业。

## 使用 Cron 重复运行作业

如果你只是想在未来的某个日期执行单个任务，那么 `at` 和 `batch` 命令就足够了，但如果你想频繁运行某项任务，它们就会变得很有用。相反，`cron` 守护进程用于根据系统（和）用户的请求重复运行任务。`cron` 守护进程的权限与 `@at` 类似：列在 `cron.deny` 文件中的用户不允许使用 `cron`，而列在 `cron.allow` 文件中的用户则可以。一个空的 `cron.deny` 文件意味着所有人都可以设置作业。一个空的 `cron.allow` 文件意味着没有人（除 root 之外）可以设置。

作业有两种类型：系统作业和用户作业，而任何出现在 `cron.allow` 中或未出现在 `cron.deny` 中的用户名都可以运行用户作业。系统作业通过 `/etc/crontab` 文件控制，该文件默认如下：

```
SHELL=/bin/sh

PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

# m h dom dom user      command

25 6 * * * root      cd / && runs-tasks-report /etc/cron.hourly

    test -x /usr/sbin/anacron || ( cd && runs-tasks-report

    > /etc/cron.daily )

47 6 * * 7 root      test -x /usr/sbin/anacron || ( cd && runs-tasks-report

    > /etc/cron.weekly)

52 6 1 * * root      test -x /usr/sbin/anacron || ( cd && runs-tasks-report

    > /etc/cron.monthly)
```
