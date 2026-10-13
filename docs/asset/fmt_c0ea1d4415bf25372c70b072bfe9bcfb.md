
```
/usr/bin/gpg
/usr/lib/gnupg
/usr/lib/gnupg/unix
/usr/lib/gnupg/deg
/usr/lib/gnupg/tiger
/usr/share/man1/gpg.1
/usr/share/gpg/
/usr/share/gnupg/options.skel
```

# 在你的 Linux 系统上设置配额 (Quota)

## 概述

Quota 是一种用于监控和限制用户磁盘使用的系统管理工具。...

关于本书的意见意见和建议请邮件至 `gmourani@videotron.ca`

## 第 2 步

现在我们必须在系统的根目录上初始化 `quota.user` 和 `quota.group` 文件，以便在服务器重启期间不会收到关于配额的错误信息。

- 要初始化 `quota.user` 和/或 `quota.group` 文件，请使用以下命令：

```
[root]@deep# edquota -u wahib
```

```
[root]@deep# edquota -g wahib
```

上述步骤仅用于初始化 `quota.user` 和/或 `quota.group` 文件，`edquota (-u)` 命令将编辑用户 `wahib` 的配额，而 `(-g)` 将编辑组 `wahib` 的配额。请注意，你必须使用系统中存在的 UID/GID 来初始化文件。

## 第 3 步

在 `etc/fstab` 文件中为你的配额程序设置好适当的选项并初始化 `quota.users` 和/或 `quota.group` 文件后，你必须重启系统，以便你在 `etc/fstab` 文件和/或 `quota.group` 文件中所做的更改才能生效。

- 要重启系统，请使用以下命令：

```
[root]@deep# reboot
```

## 为用户和组分配配额

系统重启后，你现在可以为系统中的用户或用户组分配配额了。此操作通过 `edquota` 命令执行。`edquota (8)`。

## edquota 程序

`edquota` 程序是一个配额编辑器，它会创建一个临时文件，其中包含超级用户 `root` 使用的磁盘配额，用于为系统中的用户或用户组设置配额。下面的示例显示了如何为系统中的用户或组设置配额。

## 为特定用户分配配额

如果你在系统中有一个登录名为 `wahib` 的用户。以下命令将带你进入编辑器 `vi`，在每个启用了配额的分区上编辑并设置用户 `wahib` 的配额：

### 第 1 步

- 要编辑和修改用户 `wahib` 的配额，请使用以下命令：

```
[root]@deep# edquota -u wahib
```

```
/dev/sda1: blocks in: 6, limits (soft = 0, hard = 0)
inodes in: 5, limits (soft = 0, hard = 0)
```

执行上述命令后，你将在屏幕上看到与用户 `wahib` 相关的行。`Blocks in use` 显示文件在分区上消耗的块总数（以 KB 为单位）。这些参数 `blocks in use, and inodes in use` 由系统自动控制和设置，你不需要设置或更改它们。

### 第 2 步

- 要为用户 `wahib` 分配 5MB 的配额，请在 `vi` 编辑器中更改以下参数：

- `/dev/sda: blocks in: 6, limits (soft = 0, hard = 0)`
- `inodes in: 5, limits (soft = 0, hard = 0)`

读取为：

Quota for user wahib:
```
/dev/sda: blocks in: 6, limits (soft = 5000, hard = 0)
inodes in: 5, limits (soft = 0, hard = 0)
```

`soft limit` (`soft =`) 指定了配额用户允许拥的最大磁盘使用量。

`hard limit` (`hard =`) 指定了配额用户不能超过的磁盘使用绝对限制。请注意，只有在设置了 `grace period` 参数时，`hard limit` 值才生效。

## 宽限期参数

`grace period` 参数允许你在启用配额的文件系统中在强制执行软限制值之前设置一个时间限制（更多信息请见上文的 soft limit）。例如，此参数可以提醒用户某项策略将在其家目录设置 7 天期限的 5MB 磁盘空间配额。你可以将此参数的默认 0 天设置为任何认为合理的时长。

此设置的更改需要以下两个步骤（在我的示例中假设为 7 天）。

### 第 1 步

- 通过以下命令编辑默认宽限期：

```
[root]@deep# edquota -t
```

Time units may be: days, hours, minutes, or seconds

Grace period before enforcing soft limits for users:
```
/dev/sda: block period: 0 days, grace period: 0 days
```

### 第 2 步

- 将宽限期修改为 7 天。在 `vi` 编辑器中更改或设置参数：

Time units may be: days, hours, minutes, or seconds

Grace period before enforcing soft limits for users:
```
/dev/sda: block period: 0 days, grace period: 0 days
```

读取为：

Time units may be: days, hours, minutes, or seconds

Grace period before enforcing soft limits for users:
```
/dev/sda: block period: 7 days, grace period: 7 days
```

注意：命令 `edquota -t` 编辑每个文件系统的软限制。

## 为特定组分配配额

如果你在系统中有一个名为 `webusers` 的组。该命令将带你进入 `vi` 编辑器，在每个已启用的分区上编辑组 `webusers` 的配额：

- 要编辑和修改 `webusers` 的配额，请使用以下命令：

```
[root]@deep# edquota -g webusers
```

Quota for group: webusers
```
dev/sda: blocks in: 6, limits (soft = 0, hard = 0)
inodes in: 6, limits (soft = 0, hard = 0)
```

之后，步骤与上述为特定用户分配配额相同，你修改 `soft =` 参数并保存。

## 为相同值的组分配配额

`edquota` 程序有一个特殊选项 `(-p)`，可以为具有相同值的用户组分配配额。假设你想为 UID 为 500 的用户分配与用户 `wahib` 相同的配额，我们首先编辑并设置 `wahib` 的配额，然后执行：

- 为相同值的组分配配额，使用以下命令：

```
[root]@deep# edquota -p wahib awk -F: '{print $1}' /etc/passwd
```

`edquota` 程序将为 `wahib` 设置的配额复制到 `/etc/passwd` 文件中的所有用户。

## 更多文档

更多详细信息可以阅读以下页面：

- `edquota (8)` - 编辑用户配额
- `quota (1)` - 显示磁盘使用情况和限制
- `manquota (8)` - 扫描文件系统的磁盘使用情况
- `manquot (2)` - 操纵磁盘配额
- `repquota (8)` - 汇总文件系统的配额
- `-quota (3)` - 在远程机器上实现配额

## 命令

下面列出的命令是我们经常使用的，但还有更多命令，你必须检查手册页获取更多详细信息。

## Quota

`Quota` 显示文件系统中用户的磁盘使用情况和限制。

- 要显示使用情况和限制，请使用命令：

```
[root]@deep# quota -u wahib
```

Disk quotas for user wahib (uid 501):
```
Filesystem blocks quota grace quota limit
/dev/sda 6001* 6000 7 0
```

- 要显示你所属组的配额，请使用命令：

```
[root]@deep# quota -g wahib
```

Disk quotas for group wahib (gid 501):
```
Filesystem blocks quota limit grace quota limit grace
/dev/sda 5995* 5000 0 1 0
```

注意：如果指定的用户没有组，将收到以下消息：

Disk quotas for group wahib (gid 501):

## Repquota

`Repquota` 产生文件系统磁盘使用情况和配额的汇总信息，它还会为每个用户打印当前的文件数量和空间大小（以 KB 为单位）。

这里是 `repquota` 的示例输出（你的结果可能不同）：

```
[root@deep /# repquota -a
```
