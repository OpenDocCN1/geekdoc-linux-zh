
# ls -l /quota.usr /quota.group  # Red Hat 7.0 及早版本

```
```

或者：

```bash
# ls -l /aquota.user /aquota.group  # 适用于 Red Hat 7.1
```

如果您使用 `linuxx` 启用配额，当您激活更改时，它会询问您是否要运行 `quotacheck`。只需回答 `Yes`，此步骤就会被处理。

无论您如何创建文件，您都需要运行 `quotacheck` 来收集用户的初始信息。这可以通过重启系统或在尚未运行过的情况下手动发布 `quotacheck` 命令来实现。例如，要在根文件系统上初始化配额文件，请使用：

```bash
quotacheck /
```

## 使用 edquota 设置磁盘配额

要指定磁盘配额，您需要运行 `edquota`。`edquota` 将使用 `vi` 编辑编辑 `quota.user` 或 `quota.group` 文件。您可以通过指定 `$EDITOR` 变量来更改编辑器（例如 `EDITOR=path/to/new/editor; export EDITOR`）。

在示例中，我们假设有一个名为 "craig" 的用户，我们想要限制他允许使用的磁盘空间。我们输入以下命令来编辑他的配额记录：

```bash
# edquota -u craig
```

这将启动并显示以下内容：

```
Edit block and inode quota for user craig:
Device /dev/hda2 (/)
Used 60KB, limits: soft=0 hard=0
Used 15 inodes, limits: soft=0 hard=0
```

如果您运行此命令并只看到第一行，那么您可能忘记运行 `quotacheck`。

![](img/af9747d0cc5d061c585d6aea0a227a74_346_0.png)

# 308 第 6 章：高级用户管理

在此示例中，我们的 inode 和文件的软限制（soft limits）和硬限制（hard limits）都设置为 0。这是默认设置，意味着我们目前可以消耗任意数量的 inode 或磁盘块。我们可以 `craig` 目前使用了 60K 的磁盘空间，在该分区上只有 15 个文件（inodes）。我们需要设置一个限制，以便他不超出 20MB 的使用策略。

首先，我们需要详细说明软限制和硬限制的含义：

- **软限制 (Soft Limit)**：这是用户在该分区上可以拥有的最大空间。如果您设置了宽限期（grace period），则它将作为边界阈值。用户将收到其违反配额的通知。如果您设置了宽限期，您还需要设置硬限制。宽限期是用户在系统拒绝代表用户创建新文件或扩展现有文件之前被允许的天数。用户必须保持在软限制之下。
- **硬限制 (Hard Limit)**：只有在您使用宽限期时，硬限制才是必需的。如果启用了宽限期，这将是个人可以使用的绝对限制。任何超出此限制消耗资源的尝试都将被拒绝。如果您不使用宽限期，软限制则是用户可以使用的绝对空间。

在我们的示例中，我们将为用户设置 18MB 的软限制和 20MB 的硬限制。我们还会给 `craig` 一个七天的宽限期来让他清理一下自己的东西。

```
Edit block and inode quota for user craig:
Device /dev/hda2 (/)
Used 60KB, limits: soft=18000 hard=20000
```

（对于 inode 的行）
```
Used 15 inodes, limits: soft=0 hard=0
```

## 312 第 6 章：高级用户管理

当您更改此设置时，所有其他配额设置都将被系统默认值替换。最好先使用此设置，然后根据需要单独为用户设置。

![](img/af9747d0cc5d061c585d6aea0a227a74_351_0.png)

## 配额报告 (Quota Reports)

查看谁在使用最多的磁盘空间报告这总是一件好事。你可以针对用户、用户组或每个分区上的所有用户生成报告。要查看显示所有配额信息的报告，请运行 `repquota -a` 命令：

```
# repquota -a
*** Report for user quotas on device /dev/hda2 () 
Block grace time: 7 days; Inode grace time: 7 days
Block limits File limits
User used soft hard grace used soft hard grace
root - 24 0 0 2 0 0
craig 60 0 0 15 0 0
```

你可以使用 `repquota` 命令显示特定文件系统上所有用户的特定报告：

```
# repquota -u /
```

要查看仅某一个用户的特定信息，可以使用以下配额命令：

```
# repquota -uv craig
Disk quotas for user craig(502):
Filesystem blocks quota limit grace files quota limit grace
/dev/hda2 60 0 0
```

单个用户可以使用 `quota` 命令检查其自己的使用情况，但只有 `root` 用户可以使用 `-u` 选项查看其他用户。

## NFS 文件系统上的配额

NFS 文件系统上的配额基本上相同。NFS 将远程用户翻译为本地用户。你通过 `nfsd` 配置来指定这种翻译如何工作。关于 NFS 驱动器的更多详细信息，请参阅第 7 章。你需要将磁盘配额设置到你计划映射外部用户的用户上。因此，如果你创建了一个名为 `nfsuser` 的本地用户，并将所有远程请求翻译为该用户，那么你需要在挂载的分区上为 `nfsuser` 设置配额限制。这将限制所有进入 NFS 用户的磁盘消耗。

## 认证目标 6.02

## 系统初始化脚本

Red Hat 7.x 遵循标准的 UNIX System VR4 (System 5 Release 4) 方法进行系统启动和状态管理。`init` 守护进程作为第一个进程（其进程 ID 为 1）。`init` 读取其配置文件 `/etc/inittab` 并根据在该文件中看到的内容继续初始化过程。以下是 Red Hat 7.1 的 `/etc/inittab` 列表：

在此处设置默认运行级别（runlevel）。

```
# 5 - X11
# 6 - reboot (不要将 initdefault 设置为此项)
# 3:initdefault:
```

```
# 启动初始化。
si::sysinit:/etc/rc.d/rc.sysinit
```

```
10:0:wait:/etc/rc.d/rc 0
11:1:wait:/etc/rc.d/rc 1
12:2:wait:/etc/rc.d/rc 2
13:3:wait:/etc/rc.d/rc 3
14:4:wait:/etc/rc.d/rc 4
15:5:wait:/etc/rc.d/rc 5
16:6:wait:/etc/rc.d/rc 6
```

```
# 在每个运行级别下运行的项目。
ud:once:/sbin/update
```

```
# 捕捉 CTRL-ALT-DELETE
ca::ctrlialdel:/sbin/shutdown -t3 -r now
```

```
# 当我们的 UPS 告诉我们断电时，我们有几分钟
p::powerfail:/sbin/shutdown -f +2 "Power Failure, System Shut Down"
```

```
# 如果在启动触发前恢复电源，则取消。
pr:12345:powerokwait:/sbin/shutdown -c "Power Restored"
```

```
# 在标准运行级别下运行 gettys
1:2345:respawn:/sbin/mintty tty1
2:2345:respawn:/sbin/mintty tty2
3:2345:respawn:/sbin/mintty tty3
4:2345:respawn:/sbin/mintty tty4
5:2345:respawn:/sbin/mintty tty5
6:2345:respawn:/sbin/mintty tty6
```

```
# 在运行级别 5 中运行 xdm
# xdm 现在是一个独立的服务
x5:respawn:/etc/X11/prefdm --nodemon
```
