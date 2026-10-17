
# grep CONFIG_QUOTA /usr/src/linux/.config

```
```

你应该看到类似下面的输出：

```
CONFIG_QUOTA=y
```

如果你得到：

```
CONFIG_QUOTA=n
```

那么你的内核没有启用配额支持。如果你没有任何输出，说明你没有安装配置好的自定义内核源码树。这不是问题，因为原版红帽 7.x 内核包含了配额支持，并且在内核中默认启用。

如果你有自定义内核，请使用 `menuconfig` 或 `make xconfig` 启用配额支持。该选项位于文件系统部分下。只需开启配额支持并重新构建安装你的新内核。

## 安装 Quota rpm

为了完成此工作，你需要重启到新内核并安装 `quota` rpm。

首先，检查系统是否已安装了 `quota` rpm。可以使用以下命令进行检查：

```
[root@notebook ~1]# rpm -qa | grep quota
quota-2.00pre3-7
```

有几种方法可以获取并安装 `quota` rpm 文件。最直接的方法是挂载你的 Red Hat CD-ROM 并切换到 `rpms` 目录：

```
mount /dev/cdrom
cd /mnt/cdrom/RedHat/RPMS
```

使用以下命令加载 `quota` rpm：

```
rpm -Uvh quota-2.00pre3-7
```

这将告诉 `rpm` 使用 `-U` 更新（如果不存在之前的版本的 `quota` rpm 则进行安装）、详细模式安装（`-v`），并使用一系列哈希符号（`-h`）来指示安装软件期间的当前进度。你也可以通过 FTP 或 HTTP 获取程序包，或者使用 Red Hat 7.x 自带的 Gnome rpm 并点击 Web Find。这将在互联网上搜索 `quota` 包并安装它。

获取 rpm 的最佳选择是发行版光盘。CD 中的 `quota` 版本是 Red Hat 针对你的特定版本测试过的版本。它应该运行得非常完美。

一旦安装了 `quota`，你可以使用以下命令及其关联管理器：

- `quotaon /fs` 为 `/fs` 文件系统启用配额。
- `quotaoff` 禁用配额跟踪。
- `edquota name` 编辑用户 `name` 的配额设置。也可用于设置默认值。
- `quota` 允许用户查看其当前的资源消耗情况和限制。

## 设置与管理磁盘配额

- `repquota` 为所有启用了配额的文件系统生成所有用户的磁盘消耗报告。
- `quotacheck` 扫描文件系统的配额使用情况。初始化配额数据库。

你可以通过以下任一方式获取这些任一程序的详细信息：

```
# man program
```

或者：

```
# info program
```

下一步是确保在启动期间开启并检查配额。

### /etc/rc.d/rc.sysinit 配额处理

第 4 节描述的 `etc/rc.d/init.d/rc.sysinit` 脚本用于在 Linux 系统启动时提供系统初始化服务。脚本中包含了启用配额服务的命令。具体来说，此脚本会运行 `quotacheck` 以确保磁盘消耗记录是准确的，并运行 `quotaon`（对 `/etc/fstab` 中指定的所有文件系统启用配额）。

虽然你可以手动运行 `quotaon` 和 `quotaoff`，但通常没有必要。Red Hat 7.x 的 `/etc/rc.d/init.d/rc.sysinit` 确保在启动时启用配额。当机器关机时，Red Hat 会对所有文件系统执行有序卸载。当每个启用了配额的文件系统被卸载时，内核中关于该文件系统的用户、组、文件和节点资源消耗的最新信息将写回分区。

### 修改 /etc/fstab

`/etc/fstab` 文件用于告知 Linux 你希望在启动时挂载的文件系统。该文件的选项（options）列用于设置文件系统挂载选项。这些选项在每个文件系统被上线（挂载）时会传递给 `mount` 命令。若要为文件系统启用配额，你必须更新 `/etc/fstab` 中该文件系统的选项条，以指示你想启用配额，并且你希望跟踪用户、组或两者的配额。配额仅基于文件系统启用。它们不能在目录上设置。

以下是编辑前的 `fstab` 示例：

| Device | Mount point | Filesys | Options | Fck |
| --- | --- | --- | --- | --- |
| LABEL=/ | | ext2 | defaults | 1 1 |
| /dev/cdrom | /mnt/cdrom | iso96660 | noauto,owner,ro | 0 0 |
| /dev/fd0 | /mnt/floppy | auto | noauto,owner | 0 0 |
| none | /proc | proc | | 0 0 |
| none | /proc/pts | devpts | gid=5,mode=620 | 0 0 |
| /dev/hda5 | swap | swap | defaults | 0 0 |
| /dev/hda1 | /win | vfat | uid=500,gid=500,owner,rw | 0 0 |
| /dev/hda6 | /home | ext2 | defaults | 0 0 |

在前面的示例中，我们只能在根文件系统（LABEL=/）和 `/home` 文件系统上启用配额。要在系统中启用用户配额跟踪，请在选项列列出的值中添加关键字 `usquota`。同样，使用 `grpquota` 选项禁用组配额跟踪。使用 `vi` 或你喜欢的编辑器更新 `/etc/fstab`。

在我们的示例中，我们将为根文件系统同时添加用户配额和组配额：

| Device | Mount point | Filesys | Options | Fck |
| --- | --- | --- | --- | --- |
| LABEL=/ | | ext2 | exec,dev,suid,rw,usquota,grpquota | 1 1 |
| /dev/cdrom | /mnt/cdrom | iso96660 | noauto,owner,ro | 0 0 |
| /dev/fd0 | /mnt/floppy | auto | noauto,owner | 0 0 |
| none | /proc | proc | | 0 0 |
| none | /proc/pts | devpts | gid=5,mode=620 | 0 0 |
| /dev/hda5 | swap | swap | defaults | 0 0 |
| /dev/hda1 | /win | vfat | uid=500,gid=500,owner,rw | 0 0 |
| /dev/hda6 | /home | ext2 | defaults | 0 0 |

注：OCR 文本在 341-344 页包含重复部分，已合并唯一内容。

# 第 6 章：高级用户管理

图 6-5

![](img/af9747d0cc5d061c585d6aea0a227a74_345_0.png)

验证运行 `quotacheck` (`aquota.group`) 是否正常。我在我的系统上更新配额文件使用的命令示例为：

```bash
# convertquota -u -g /
```

现在我们可以使用以下命令开启配额：

```bash
# quotaon -u -g /
```

## 手动管理配额

如果您选择不使用 `linuxconf` 工具来创建配额，则需要手动创建 `/quota.user` 和 `/quota.group`。若要手动操作，请在分区的根目录下创建空文件，并设置安全权限，使得只有 root 用户具有读写权限。例如：

```bash
# touch /quota.user /quota.group      # RedHat 7.0 及早版本
# chmod 600 /quota.user /quota.group
```

或者：

```bash
# touch /quota.user /quota.group      # RedHat 7.1
# chmod 600 /quota.user /quota.group
```

当您运行 `quotacheck -avug` 时，此步骤将自动为您完成。`quotacheck` 的选项有：

- `-a`: 通过检查 `/etc/mntab` 扫描所有已启用配额的文件系统。
- `-v`: 执行详细扫描。否则 `quotacheck` 将处于静默运行模式。
- `-u`: 扫描用户配额。
- `-g`: 扫描组配额。

## 设置和管理磁盘配额

这将检查所有用户、组和分区的当前配额信息。它将这些信息存储在配额分区的根目录下。如果您没有手动创建这些文件，它们现在会被创建，并应该设置了相应的安全警告，但为了安全起见，您应该再次检查：

```bash
```
