
# 为普通用户授予系统管理员权限

`su` 命令产生一个新的 shell，同时更改现有用户的 UID 和 GID，并自动更改与用户相关的环境变量，这被称为继承环境。有关环境变量的更多信息，请参见第 4 章。

`su` 命令的语法如下：

```
matthew@semour:-$ username arguments
```

`man su` 提供了更多细节，但 `su` 命令的一些亮点在这里：

- `-c, --command COMMAND`：通过 `-c` 将单个 `COMMAND` 传递给 shell
- `-m, --preserve-environment`：不重置环境变量
- `-l`：为替换的用户进行完整的登录模拟，与指定横杠 `-` 相同

在一种情况下，你使用它但保留你的环境变量（如路径）。在另一种情况下，你继承该用户的环境。当你使用 `su` 变成超级用户时，这种区别并不明显。如果不加上 `-`，路径变量（`path`）不包含 `/bin` 或 `/sbin`，当你直接 `su` 到 root 时，必须始终输入命令的完整路径。

# 为普通用户授予管理员权限

请参考第 11 章中“使用 `vi`”部分介绍的编辑命令。你可以通过执行以下命令来运行 `visudo` 并开始编辑：

```
matthew@semour:~$ sudo visudo
```

默认的 `/etc/sudoers` 文件内容如下：

```
## /etc/sudoers
#
## 此文件必须使用 ‘sudo’命令以 root 身份编辑。
#
## 请参阅 man页获取有关如何编写 sudoers 文件的详情。
Defaults
  env_reset

# 主机别名指定

# 用户别名指定

# 命令别名指定

# 用户权限指定
root  ALL=(ALL) ALL

# 取消注释以允许 sudo 组不需要密码
# （注意，后面的条目会覆盖此设置，因此你可能需要将其
# 移动到更下方）
%sudo ALL=NOPASSWD: ALL

# admin 组的成员可以获得 root 权限
%admin ALL=(ALL) ALL
```

文件中 `sudoers` 行的基本格式如下：

```
user host_computer=command
```

用户可以是单个用户或一个组（名称前的 `%` 标识该名称为组）。`host_computer` 对于网络上的所有主机为 `NORMAL`，对于本地机器为 `localhost`，但主机计算机也可以引用为子网或任何特定主机。`sudoers` 行中的命令可以是 `ALL`、特定命令列表，或对特定命令的限制（通过在命令前加 `1` 形成）。`sudoers` 行有许多可用选项可以使用，并可以使用别名来简化权限分配。再次，`sudoers` 的 `man` 页提供了详情，但这里有几个示例：

如果我们添加以下行：

```
%wheel ALL=(ALL) NOPASSWD: ALL
```

任何添加到 `wheel` 组的用户都可以执行任何命令而无需密码。

假设我们想授予某个用户网络权限，使其能够通过图形化界面添加用户。我们将添加以下行：

```
john ALL=/users-admin
```

或者，我们可能只在其本地计算机上授予权限：

```
john 192.168.1.87=/usr/bin/users-admin
```

如果我们想赋予编辑器组（`editors`）无需密码即可删除文件的权限，我们使用以下命令：

```
%editors ALL=NOPASSWD: /bin/rm
```

如果我们想授予每个用户无需密码即可在本地挂载 CD 驱动器的权限，操作方法如下：

```
ALL localhost=NOPASSWD: /sbin/mount /dev/scd0 /mnt/cdrom /sbin/umount /mnt/cdrom
```

在构建 `sudo` 文件时可以使用通配符。可以使用别名来更容易地定义用户和组。`sudoers` 页包含了一些示例，而 www.komar.org/pres/sudo/toc.html 提供了关于大型公司使用 `sudo` 的说明性笔记和注释。www.sudo.ws/ 的 `sudo` 首页也是获取额外说明和示例的有用资源。

以下命令向用户列出其有权使用的命令列表：

```
matthew@semour:-$ sudo -l
```

## 添加额外的 sudo 用户

如所述，默认情况下，Ubuntu 通过 `sudo` 命令为第一个创建的用户授予 root 访问权限。如果你需要为其他用户添加此功能，可以通过将每个用户添加到 `admin` 组，或者使用“用户管理器”（User Manager）工具允许他们管理系统，该工具可以在编辑用户属性时在“用户权限”（User Privileges）选项卡中找到。

# 磁盘配额

在具有许多用户的大型系统中，你通常需要控制用户可以使用磁盘空间量。磁盘配额（Disk quotas）专门为此设计。配额按每个分区进行管理，可以为单个用户和组设置配额；组的配额不需要等于组内个人配额的总和。

当文件被创建时，用户和组都拥有这些文件；文件的所有权始终是文件元数据的一部分。这使得基于用户和组的配额易于管理。

## 注意

磁盘配额管理在家庭级系统中并不真正有用或需要，而且在小型办公系统中也极少使用。在这两种情况下，你都不可能看到或实现此功能。

要管理磁盘配额，你必须在系统中安装 `quota` 和 `quotool` 软件包。Ubuntu 默认不启用配额管理，传统上由系统管理员手动启用并配置。管理员使用配额系列命令，例如使用 `quotacheck` 初始化配额数据库文件，使用 `dequota` 设置和编辑用户配额，使用 `setquota` 配置磁盘配额，以及使用 `quotaon` 或 `quotaoff` 控制服务。（其他工具包括 `warnquota`，用于自动向超过磁盘使用限制的用户发送邮件。）

## 实现配额

即使在 Ubuntu 系统上安装了配额软件包，配额默认也是未启用的。当安装并启用配额后，你可以查看分区是否具有用户配额、配额组，或者查看 `/etc/fstab` 文件的第四字段。例如，`/etc/fstab` 中的某一行显示为 `/home` 分区启用了配额：

```
/dev/hda5 /home ext3 defaults,usrquota,grpquota 1 1
```

启用了配额的分区根目录下会有 `quota.user` 或 `quota.group` 文件（如果启用了两种类型，则两个都有），文件将包含实际的配额。这些文件的权限应为 600，以便用户无法对其进行读写。（否则，用户将更改它们以允许访问）。通过 `man` 命令查看关于这些文件的 `quota.user` 或 `quota.group` 文件（如果启用了两种类型，则两个都有）：

```
/LABEL=/ ext3 defaults,usrquota 1 1
```

启用了配额的分区根目录下会有 `quota.user` 或 `quota.group` 文件（如果启用了两种类型，则两个都有），文件将包含实际的配额。这些文件的权限应为 600，以便用户无法对其进行读写。（否则，用户将更改它们以允许访问）。通过 `man` 命令查看关于这些文件的 `quota.user` 或 `quota.group` 文件（如果启用了两种类型，则两个都有）：

```
matthew@semour:-$ mount
```

通过使用以下命令启用配额的工具：

- `quotaon`——在分区上启用配额。
- `quotaoff`——在分区上禁用配额。
- `man` 页面提供了关于配额的详情。
- `quotacheck`——检查并修复配额数据库。
- `repquota`——配额状态报告。

## 手动配置配额

手动配置配额涉及更改 `/etc/fstab` 中的条目，为分区添加配额选项。在简单的文件系统中，可以通过以下方式启用配额：

```
matthew@semour:-$ quotaon
```

组级配额也可以通过以下方式启用：

```
matthew@semour:-$ quotaon -av
```

任何用户都可以以下命令查看自己的配额：

```
matthew@semour:-$ quota -v
```

> 注意 Ubuntu 不支持任何图形化工具来配置磁盘配额。配额迷你 HOWTO 维护在 www.tldp.org/Quota.html。

# 相关命令

使用这些命令管理用户账户：

- `ac`——账户统计。
- `change`——设置或修改密码过期策略。
- `chfn`——创建或修改 `/etc/passwd` 中的 `finger` 信息。
- `chgrp`——修改组关系。
- `chmod`——更改文件权限。
- `chown`——更改所有者。
- `chpasswd`——批量修改密码的命令。
- `chsh`——修改用户的 shell。
- `groups`——显示现有的组关系。
- `logname`——创建用户的登录名。
- `newusers`——批量用户管理。
- `passwd`——创建或修改用户密码。
