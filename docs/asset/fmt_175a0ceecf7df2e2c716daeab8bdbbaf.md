
```text
#
# Sample /etc/auto.master file
# (lines which begin with a '#' are comments)
#
/mount/point           map~file              global-options
/home                   auto.home
/usr/local              auto.local
/misc                   auto.misc
```

第一列表示挂载点；第二列列出包含该挂载点映射详情的文件；最后一列包含你希望应用于所有挂载的任何 NFS 选项。

映射文件的外观与 `auto.master` 文件略有不同。例如，这里是 `auto.misc` 文件：

```text
#
# auto.misc
#
# This is an automounter map and it has the following format
# key [ -mount-options-separated-by-comma ] location
# Details may be found in the autofs(5) manpage.
kernel    -ro,soft,intr      ftp.kernel.org:/pub/linux
cd          -fstype=iso9660,ro      :/dev/cdrom
# the following entries are samples to pique your imagination
#floppy     -fstype=auto      :/dev/fd0
#floppy     -fstype=ext2      :/dev/fd0
#e2floppy   -fstype=ext2      :/dev/fd0
#jaz        -fstype=ext2      :/dev/sdc1
```

这里，第一列是键，第二列包含 `mount` 选项，最后一列是挂载源位置。如果位置条目以冒号开头，这是向系统发出的信号，表示该挂载是本地的。因此，`/misc/cd` 将以以下 `mount` 选项挂载 `/dev/cdrom`：

```text
-fstype=iso9660,ro
```

![](img/ec2066d370d3af1a767664d36aa7ddfe_240_0.png)

与 NFS 不同，NFS 要求目录必须已经存在才能进行挂载，而 autofs 服务不需要。对于 `/misc` 挂载点，只需要 `/misc` 目录存在即可。所有子目录将由 autofs 守护进程根据需要创建。

如果在 autofs 运行时更改了任何映射文件，你需要重启 autofs 服务以便它能重新读取配置文件。使用 autofs 操作如下：

```bash
[root@edford /root]# /etc/init.d/autofs reload
```

# 关键技能 7.5 管理配额

在任何多用户环境中，你肯定会遇到一些用户——他们要么拒绝公平竞争，要么对基本礼仪毫无概念——练习着磁盘霸占的艺术，占据了超过合理数量的磁盘空间。

这个问题可以通过几种方式管理。第一种也是最明显的解决方案是恳求和哀求。这很少有效。第二种方法是同伴压力：定期并公开列出那些占用过多磁盘空间的用户所占用的空间量。如果人们稍微在意别人对他们的看法，这可能有效。最后也是最成功的技术是实施磁盘配额，允许每个用户消耗一定量的磁盘空间，不多也不少。执行是由操作系统完成的。

磁盘配额通常是系统管理员的最佳选择，因为配额是自动化的，不需要你面对那些违规的用户。然而，技术和/或政治障碍可能会阻碍其使用。（例如，首席执行官可能不喜欢被告知她只能使用服务器磁盘空间的 5MB。）当然，配额是可选的——没有它们你的系统也会运行得很愉快。它们是否能在你的环境中起作用取决于你和你的管理层。

## 为配额准备磁盘

准备使用磁盘配额分为两步。第一步是在 `/etc/fstab` 文件中进行必要的设置，并在每个想要进行配额控制的分区中添加必要的文件。必须为每个想要进行配额控制的分区重复步骤 1。步骤 2 是运行 `quotacheck` 命令在已配置的每个分区上设置配额。

## 配置单个分区

磁盘配额基于每个用户或每个组的基础工作，每个分区允许拥有自己的配额。例如，所有用户可能在某个分区的主目录上拥有一项配额，而在另一个分区上，他们参与的群组项目拥有另一项配额。

对于你想要设置配额的每个分区，你需要设置 `usrquota` 选项和 `grpquota` 选项，然后重新挂载该分区。

### usrquota 选项

编辑 `/etc/fstab` 文件，以便对于每个需要配额的分区，挂载选项中包含 `usrquota` 选项。例如，如果 `/dev/hda5` 挂载到 `/home` 目录，并且你希望该目录具有用户配额，那么 `/etc/fstab` 条目将如下所示：

```text
/dev/hda5    /home    ext3    defaults,usrquota    1    1
```

### grpquota 选项

需要支持组配额的分区应在 `/etc/fstab` 文件中包含 `grpquota` 选项，正如刚才描述的 `usrquota` 选项一样。（注意，同时启用这两个选项是可以接受的。）例如，如果 `/dev/hda5` 挂载到 `/home` 目录，并且你希望该目录具有组配额，那么 `/etc/fstab` 条目将与此类似：

```text
/dev/hda5    /home    ext3    defaults,grpquota    1    1
```

### 重新挂载分区

现在你只需使用 `umount` 和 `mount` 重新挂载该分区。虽然仅做这一操作不会使你的配额系统就绪，但你不能跳过这一步！为了继续这个例子，在 `/dev/hda5` 分区上重新挂载 `/home` 将如下所示：

```bash
[root@tedford /root]# umount /home
[root@tedford /home]# mount /home
```

## 运行 quotacheck 以启用配额

在重新配置并重新挂载分区后，你必须告知 Red Hat Linux 初始化数据库文件，检查文件系统的使用情况，并启用配额。使用 `quotacheck` 命令来执行所有这些操作：

```
[root@tedford /root]# quotacheck -avug
```

`-avug` 选项指示 `quotacheck` 在所有启用配额的运行文件系统中运行，提供详细的输出让你了解其正在做的事情，并且同时支持基于用户和基于组的配额。

![](img/ec2066d370d3af1a767664d36aa7ddfe_242_0.png)

> Red Hat 建议定期重新运行 `quotacheck` 命令。你可以通过每周运行一次“cron”任务来实现这一点（有关 cron 任务的更多信息，请参阅模块 8）。

## 配置配额设置

在用户级或组级创建、修改和删除配额是通过 `edquota` 命令完成的。在本节中，你将查看此命令的用法并运行一些示例。首先，是一些术语：

- **软限制**

  此请求限制应用于用户或组。如果用户的帐户超过软限制，可以施加宽限期，规定帐户可以在软限制以上存在多长时间。在此期间，用户可能会收到其帐户超过限制的警告。

- **硬限制**

  此限制由操作系统强制实施，不能被突破。任何试图在硬限制之外写入数据的尝试都将被拒绝。

- **宽限期（时间限制）**

  当用户的帐户超过软限制时，时钟开始跟踪。宽限期过期后，用户无法访问该帐户。此宽限期的长度应取决于环境。常见的值为一周。为了防止帐户被禁用，用户需要删除或压缩文件，直到其磁盘消耗量低于软限制。

### edquota 的命令行选项

当用于管理基于用户的配额时，`edquota` 命令只有三个选项：

| 选项 | 描述 |

| :--- | :--- |

| `-u login` | 为指定用户设置配额信息。 |

| `-t` | 设置分区的宽限期。将其与 `-u` 或 `-g` 一起使用，分别设置所有用户或组的宽限期。注意：如果同一分区上存在用户/组，它们不能有相同的宽限期。 |

| `-g group` | 为指定 *组* 设置 *配额* 信息。 |

| `-p login` | 允许将某个用户（用户 *login*）的信息克隆到另一个用户。必须与 `-u` 选项一起设置。 |

当你调用 `edquota` 命令时，它会显示你要添加或编辑的特定用户、组或宽限期的配置信息。默认情况下，使用 `vi` 编辑器来显示人类可读的信息。如果你更喜欢其他编辑器，例如 `emacs` 或 `pico`，你可以在运行 `edquota` 之前简单更改 `EDITOR` 环境变量。例如，如果你使用的是 BASH（root 用户的默认 shell），你会输入这个命令：

```
[root@tedford]# export EDITOR=pico
```
