
这有助于解释最后一个指令。当百分号 (`%`) 在用户名称名前时，它指定了一个组。下一行指定了 `admin` 组的权限。第一个 `ALL` 指定所有系统；替代方案是替换 `localhost` (`ALL`) 允许所有用户名。这不是问题，因为该行将访问限制在 `admin` 组的用户。最后，`ALL` 支持对所有命令的管理访问。

```
%admin ALL=(ALL) ALL
```

如果你有足够的信心禁用密码要求，以下内容将允许 `admin` 组的用户无密码访问所有管理命令：

```
%admin ALL=(ALL) NOPASSWD: ALL
```

然而，我不建议这种更改，因为它移除了一个防止管理员错误的保护措施。现在你准备好自定义此文件了。

# Wheel 组的授权

`/etc/sudoers` 文件可以使用 `visudo` 命令进行编辑；访问此命令需要管理权限。因此在 Ubuntu 中，你将运行以下命令来用文本编辑器打开 `/etc/sudoers`：

```
$ sudo visudo
```

现在你准备好进行更改了。例如，如果你在 `/etc/group` 中创建了一个名为 `power` 的组，并允许该组的成员重启系统，请添加

## 第 10 章：用户、组和管理员管理

接下一行。`localhost` 意味着 `power` 组的成员只能在本地系统上重启——换句话说，他们无法远程登录并重启该系统。

```
%power localhost=(ALL) /sbin/reboot
```

这是对 `/etc/sudoers` 配置文件的极佳介绍。`man sudo` 命令提供了关于该配置文件的详尽手册。

## 配额配置 (QUOTA CONFIGURATION)

配额用于限制用户或组消耗磁盘空间的能力。这有助于防止一小部分用户垄断磁盘容量，并可能干扰其他用户或整个系统。互联网服务提供商 (ISP)、网络托管公司、FTP 站点以及企业文件服务器通常使用磁盘配额，以确保其系统的持续可用性。

如果没有配额，一个或多个用户可以在 FTP 服务器上上传文件并占用分区上的所有可用空间。一旦分区满，所有用户都将极度拒绝访问磁盘。这也是将不同的文件系统目录挂载到不同分区上的原因之一。例如，如果仅为根目录（`/`）和交换空间（`swap`）配置了分区，上传操作可能会填满根目录（`/`）中的所有空间。如果根目录（`/`）至少没有剩余空间，系统可能会变得不稳定甚至崩溃。

为用户和组设置配额有两种方法：可以根据节点（inodes）或字节大小的磁盘块来设置限制。每个 Linux 文件都需要一个索引。换句话说，可以根据文件数量或绝对大小设置限制。可以为不同的文件系统设置不同的配额。例如，如果 `/home` 和 `/tmp` 目录挂载在单独卷或分区上，每个用户可以对 `/home` 和 `/tmp` 目录拥有不同的配额。

如果尚未安装该包，您可以使用 `sudo aptitude install` 命令进行安装。

## `/etc/fstab` 中的配额

如第 5 章所述，`/etc/fstab` 文件用于指定 Linux 在启动过程中如何挂载文件系统。该文件的“Options”（选项）列配置了 Linux 如何挂载目录，这也可以对用户和组配额进行配置。

> **注意：** 在编辑如 `/etc/fstab` 等关键配置文件之前，请务对其进行备份！如果任何更改导致灾难性故障，您可以在救援模式下恢复系统并还原原始配置文件。

来自 Hardy Heron 的 `/etc/fstab` 配置文件的相关部分，其中包含 `/home` 目录卷的用户和组配额设置，如图 10-6 所示。

## Ubuntu 服务器管理

| /etc/fstab <挂载点> <type> <options> <dump> <pass> |
| # <文件系统> <挂载点> <type> <options> |
| proc /proc | | | |
| /mapper/ubuntahubardyserver-root proc | defaults | 0 0 |
| UUID=41c7a8d2-23f1-40b9-bc78-1d0025c4dff9 / | ext3 | reltime, error s=remount-o / | 1 |
| /dev/sda1 / | ext3 | reltime | | |
| UUID=e3c6e6d-62e4-45f6-9bb5-8d31bd1d3dc3c /home | | | | |
| /mapper/ubuntahubardyserver-swap_1 | | | | |
| UUID=c333b8e0-f423-40f1-b6d1-f9e8bf43d20 /home | ext3 | reltime, usrquota,grpquota | 0 | |
| UUID=959fd625-a7c2-410c-bc59-72061fc27c91 swap | sw | | | |
| /dev/scd0 /media/cdrom | udf | udf,iso8660 user,noauto,utf8 | 0 0 |

图 10-6 带有静态选项的 `/etc/fstab`

与过去的发行版不同，`/etc/fstab` 中的行换行到下一行是可以接受的。请注意 `usrquota` 和 `grpquota` 配额是如何应用于 `/home` 目录卷的。如果您没有 `/home` 分区，则对顶级根目录（`/`）的配额设置将生效。您可以通过重启系统或重新挂载文件系统来测试 `/etc/fstab` 的更改。例如，如果您刚刚为 `/home` 目录文件系统添加了 `usrquota` 和 `grpquota` 条目，可以使用 `mount -o remount /home` 命令进行测试。以下来自 `/etc/mtab` 文件的节选说明了结果（以下代码代表一行）：

```
/dev/mapper/ubuntahubardyserver-home /home ext3 rw,relatime,usrquota,grpquota 0 0
```

## 配额管理命令

在激活配额之前，必须创建适当的配额文件。对于用户和组配额，您需要在激活配额之前在选定的系统中创建 `user` 和 `quota.group` 文件。您不再需要手动创建这些文件；一旦重新挂载了目标目录，适当的 `quotacheck` 会自动创建它们。对于之前描述的 `/home` 目录，您将使用以下命令：

```
$ sudo mount -o remount /home
$ sudo quotacheck -cug /home
```

所示的 `quotacheck` 包含以下命令选项：

- `-c`: 创建配额文件
- `-u`: 扫描用户
- `-g`: 扫描组
- `-m`: 重新挂载文件系统

## 第 10 章：用户、组和管理员管理

所示的 `quotacheck` 包含以下命令选项：

- `-c`: 创建配额文件
- `-u`: 扫描用户
- `-g`: 扫描组
- `-m`: 重新挂载文件系统

## 配额宽期 (Quota Grace Periods)

宽期是用户允许超过软限制的天数。在宽期结束后，用户必须降至软限制以下。所有用户的默认宽期为七天，且用户无法自定义。要更改宽期，请运行 `edquota -t` 命令。当我对用户运行此命令时，我看到如下输出：

强制软限制之前的宽期：
时间单位可以是：天、小时或秒

| 文件系统 | 块宽期 | 节点宽期 |
| /dev/mapper/ubuntahubardyserver-home | 7days | 7days |

7 和 days 之间没有空格。这是配额期的一个特性。数字与 `edquota` 工具不识别的单位之间（例如 `7days`，而不是 `7 days`）。您可以在编辑配置时添加空格，但当保存配额时，`edquota` 会删除这些空格。

`edquota` 允许您使用已配置好的用户配额作为新用户的模板。要使用此功能，您需要运行带有 `-p` 切换的 `edquota` 命令；例如，以下命令将为用户 `donna` 配置的配额应用到 `michael`、`randy` 和 `sandy`：

```
$ edquota -up donna michael randy
```

配额可以为组配置，并且为组创建一个专用目录是很有用的。要这样做，请运行带有 `-g group_name` 参数的 `edquota`，其中 `group_name` 在 `/etc/group` 文件中指定。

# 第10章：用户、组和管理员管理

269

## 配额报告

作为管理员，你可能想查看关于谁使用了最多磁盘空间的报告。你可以针对用户、组以及卷中有文件的所有人生成报告。要查看显示所有用户配额信息的报告，请运行 `sudo repquota -a health` 命令。你将看到所有用户的配额列表。

如果你有多个带有配额的文件系统，可以使用 `quota` 命令隔离特定的文件系统。例如，如果你想查看 `/home` 目录所在文件系统的配额报告，请运行以下命令：

```
$ sudo repquota -u /home
```

或者，如果你想查看用户 `donna` 的配额信息，请运行以下 `quota` 命令：

```
$ sudo quota -uv donna (uid 1001):
```
