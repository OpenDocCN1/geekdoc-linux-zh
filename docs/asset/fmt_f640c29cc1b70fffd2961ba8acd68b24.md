
正如所有想要运行的 Shell 脚本一样，复制到 `/etc/cron.*` 文件夹的脚本必须具有可执行权限才能正常工作。

> 如果你好奇当电脑在凌晨 4:02 未运行时，你的每日 Shell 脚本会发生什么，请参阅 `gpasswd` 手页（注：此处原文可能存在逻辑跳跃，已按原文翻译）。

## 组成员身份

为了让普通用户使用他们的组身份，他们必须使用 `newgrp` 命令。调用 `newgrp` 命令时将组名作为参数；如果用户是该组的成员，则用户的组身份将变为指定组的身份。例如，`programmers` 组的成员 `jane` 想要访问属于 `programmers` 组的文件，她在命令行提示符中调用 `newgrp`，并将 `programmers` 作为参数：

```
[jane@workstation20 jane]$ newgrp programmers
[jane@workstation20 jane]$
```

用户可以通过执行不带参数的 `newgrp` 命令来返回他们默认的（即登录时）的组身份：

```
[jane@workstation20 jane]$ newgrp
[jane@workstation20 jane]$
```

## 命令行系统管理

### 使用 cron 管理周期性任务

每个 Linux 和 Unix 系统都包含一个名为 `cron` 的服务，它允许用户根据用户定义的定时选项定期运行运行特定的命令或脚本。该服务提供了一系列独特的任务——定期备份、电子邮件状态报告、主目录清理等。

`cron` 进程列表分为两个级别：系统级列表和用户级列表。系统级 `cron` 进程列表应仅用于管理面向系统的进程；对于所有需要定期运行的个人任务，应使用用户级 `cron` 列表。

### 添加系统级 cron 进程

系统级 cron 进程通常用于定期备份、日志轮转和系统监控等任务。要创建一个系统级 cron 进程，你需要创建一个执行目标任务的脚本，使用 `cp` 或 `mv` 命令将其放入 `/etc` 中一个非常特殊的目录中：

- 复制到 `/etc/cron.hourly` 的 Shell 脚本每天每小时过一分后运行一次。
- 复制到 `/etc/cron.daily` 的 Shell 脚本每天凌晨 4:02 运行一次。
- 复制到 `/etc/cron.weekly` 的 Shell 脚本每周每周日凌晨 4:22 运行一次。
- 复制到 `/etc/cron.monthly` 的 Shell 脚本每月第一天凌晨 4:42 运行一次。

正如所有想要运行的 Shell 脚本一样，复制到 `/etc/cron.*` 文件夹的脚本必须具有可执行权限才能正常工作。

> 如果你好奇当电脑在凌晨 4:02 未运行时，你的每日 Shell 脚本会发生什么，请参阅 `gpasswd` 手页。

## 组成员身份

为了让普通用户使用他们的组身份，他们必须使用 `newgrp` 命令。调用 `newgrp` 命令时将组名作为参数；如果用户是该组的成员，则用户的组身份将变为指定组的身份。例如，`programmers` 组的成员 `jane` 想要访问属于 `programmers` 组的文件，她在命令行提示符中调用 `newgrp`，并将 `programmers` 作为参数：

```
[jane@workstation20 jane]$ newgrp programmers
[jane@workstation20 jane]$
```

用户可以通过执行不带参数的 `newgrp` 命令来返回他们默认的（即登录时）的组身份：

```
[jane@workstation20 jane]$ newgrp
[jane@workstation20 jane]$
```

## 命令行系统管理

### 使用 cron 管理周期性任务

每个 Linux 和 Unix 系统都包含一个名为 `cron` 的服务，它允许用户根据用户定义的定时选项定期运行运行特定的命令或脚本。该服务提供了一系列独特的任务——定期备份、电子邮件状态报告、主目录清理等。

`cron` 进程列表分为两个级别：系统级列表和用户级列表。系统级 `cron` 进程列表应仅用于管理面向系统的进程；对于所有需要定期运行的个人任务，应使用用户级 `cron` 列表。

### 添加系统级 cron 进程

系统级 cron 进程通常用于定期备份、日志轮转和系统监控等任务。要创建一个系统级 cron 进程，你需要创建一个执行目标任务的脚本，使用 `cp` 或 `mv` 命令将其放入 `/etc` 中一个非常特殊的目录中：

- 复制到 `/etc/cron.hourly` 的 Shell 脚本每天每小时过一分后运行一次。
- 复制到 `/etc/cron.daily` 的 Shell 脚本每天凌晨 4:02 运行一次。
- 复制到 `/etc/cron.weekly` 的 Shell 脚本每周每周日凌晨 4:22 运行一次。
- 复制到 `/etc/cron.monthly` 的 Shell 脚本每月第一天凌晨 4:42 运行一次。

正如所有想要运行的 Shell 脚本一样，复制到 `/etc/cron.*` 文件夹的脚本必须具有可执行权限才能正常工作。

> 如果你好奇当电脑在凌晨 4:02 未运行时，你的每日 Shell 脚本会发生什么，请参阅 `gpasswd` 手页。

## 组成员身份

为了让普通用户使用他们的组身份，他们必须使用 `newgrp` 命令。调用 `newgrp` 命令时将组名作为参数；如果用户是该组的成员，则用户的组身份将变为指定组的身份。例如，`programmers` 组的成员 `jane` 想要访问属于 `programmers` 组的文件，她在命令行提示符中调用 `newgrp`，并将 `programmers` 作为参数：

```
[jane@workstation20 jane]$ newgrp programmers
[jane@workstation20 jane]$
```

用户可以通过执行不带参数的 `newgrp` 命令来返回他们默认的（即登录时）的组身份：

```
[jane@workstation20 jane]$ newgrp
[jane@workstation20 jane]$
```

在你创建一个组后，你可以通过调用 `gpasswd` 命令并使用 `-A` 选项，提供用户名和组名作为参数，为普通用户授予管理权限。例如，要给用户 `joe` 授予 `programmers` 组的管理权限，你输入以下命令：

```
[root@workstation20 joe]$ gpasswd -A joe programmers
[root@workstation20 joe]$
```

用户 `joe` 现在拥有 `programmers` 组的管理权限，可以添加和删除用户、设置密码或清除该组的密码。

要添加用户，`joe` 使用带有 `-a` 选项的 `gpasswd` 命令，提供要添加的用户名及其所管理的组名作为参数。例如，如果 `joe` 将 `jane` 添加到 `programmers` 组，他输入以下命令：

```
[joe@workstation20 joe]$ gpasswd -a jane programmers
[joe@workstation20 joe]$
```

用户 `jane` 现在是 `programmers` 组的成员，直到 `joe` 将其移除。要将 `jane` 从 `programmers` 组中移除，`joe` 调用带有 `-d` 选项的 `gpasswd` 命令，将要移除的用户 `jane` 和要从中移除的组作为参数：

```
[jane@workstation20 joe]$ gpasswd -d jane programmers
[jane@workstation20 joe]$
```

有关 `gpasswd` 命令为 root 用户提供的额外功能信息（包括使用组密码的能力），请参阅 `gpasswd` 手页。

## 修改组成员身份

为了让普通用户使用他们的组身份，他们必须使用 `newgrp` 命令。调用 `newgrp` 命令时将组名作为参数；如果用户是该组的成员，则用户的组身份将变为指定组的身份。例如，`programmers` 组的成员 `jane` 想要访问属于 `programmers` 组的文件，她在命令行提示符中调用 `newgrp`，并将 `programmers` 作为参数：

```
[jane@workstation20 jane]$ newgrp programmers
[jane@workstation20 jane]$
```

用户可以通过执行不带参数的 `newgrp` 命令来返回他们默认的（即登录时）的组身份：

```
[jane@workstation20 jane]$ newgrp
[jane@workstation20 jane]$
```

## 命令行系统管理
