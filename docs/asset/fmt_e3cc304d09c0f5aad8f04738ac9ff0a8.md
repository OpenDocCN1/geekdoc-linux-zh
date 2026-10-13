
```
# mke2fs -l 'Little Guy' -v -N 128000 /dev/hdb
mke2fs 1.23, 15-Aug-2001 for EXT2 FS 0.5b, 95/08/09
/dev/hdb is entire device, not just one partition!
Proceed anyway? (y,n) y
Filesystem label=Little Guy
OS type: Linux
Block size=1024 (log=0)
Fragment size=1024 (log=0)
128000 inodes, 255528 blocks
12776 blocks (5.00%) reserved for the super user
First data block=1
32 block groups
8192 blocks per group, 8192 fragments per group
4000 inodes per group
Superblock backups stored on blocks:
8193, 24577, 40961, 57345, 73729, 204801, 221185

Writing inode tables: done
Writing superblocks and filesystem accounting information: done

This filesystem will be automatically checked every 37 mounts or 100 days, whichever comes first. Use tune2fs -c or -i to override.
```

请注意，卷现在有了标签，并且索引节点的数量已大幅增加，正如期望的那样。

一次快速的 `fsck` 证明一切如预期：

```
# fsck /dev/hdb
Parallelizing fsck version 1.23 (15-Aug-2001)
e2fsck 1.23, 15-Aug-2001 for EXT2 FS 0.5b, 95/08/09
Little Guy: clean, 11/128000 files, 16094/255528 blocks
```

向文件系统添加新磁盘的大部分工作都是由 `mke2fs`（或其兄弟命令之一）完成的，并且该命令有许多不同的选项。

### 挂载新磁盘

在磁盘格式化并由 `newfs`（或 `mkfs`）添加文件系统骨架后，它可以挂接到文件系统。这是 Unix 与其他计算机系统略有不同的地方，因为与其添加新的驱动器映像，Unix 要求你将新磁盘挂接到现有文件系统。这就是为什么 `mount` 输出显示特定目录的原因。请考虑 `mount` 输出中的以下行：

```
/dev/hda1 on /boot type ext3 (rw)
```

这意味着根（`/`）文件系统上有一个 `/boot` 目录，其内容被新挂载的 `/dev/hda1` 驱动器隐藏。

新挂载的磁盘隐藏现有文件内容这一想法对于理解如何最好地将新磁盘空间添加到系统至关重要。

#### 任务 10.3：向系统添加新驱动器

想象一下，我们可以在启动序列中途停止系统，在事物开始运行后，但在任何非启动磁盘挂载之前。此时，会有一个 `/boot` 目录，但其中没有任何内容。`mount` 命令的工作是将文件系统附加到特定目录。

1. 在新驱动器 `hdb` 添加到系统之前，让我们先看看目录 `/home/taylor`：

```
/home/taylor:
# cd /home/
# ls -a taylor
.               .first_start_kde   .MOOP-random-seed
..              .gconf            .mcoprc
.autorun.lck    .gconfd           .nautilus
.bash_history   .gnome            .sawfish
```

```
.bash_logout      .gnome-desktop   .screenrc
.bash_profile     .gnome_private    .wmrc
.bashrc           .gtkrc            .xauth
.DCOPserver_localhost.localdomain  .ICEauthority  .Xauthority
.DCOPserver_localhost.localdomain_:0  .kde  .xsession-errors
Desktop            .kderc
.emacs             .mcop
```

现在，让我们使用 `mount` 命令将新驱动器挂接到现有系统，以 `/home/taylor` 作为其初始挂载点：

```
# mount /dev/hdb /home/taylor
```

```
# ls -al taylor
```

```
total 17
drwxr-xr-x 3 root root 1024 Feb  1 14:40 .
drwxr-xr-x 3 root root 4096 Jan 24 12:20 ..
drwxr-xr-x 2 root root 12288 Feb  1 14:40 lost+found
```

看到所有文件都消失了令人相当害怕，但它们并没有真正消失，它们在下面，被已挂载的新磁盘的内容覆盖。

2. 为了证明这一点，`umount` 会卸载磁盘，从而允许访问之前的内容：

```
# umount /dev/hdb
```

```
# ls -a taylor
```

```
.first_start_kde  .MCOP-random-seed
..                 .mcoprc
.autorun.lck       .gconfd           .nautilus
.bash_history      .gnome            .sawfish
.bash_logout       .gnome-desktop    .screenrc
.bash_profile      .gnome_private    .wmrc
.bashrc            .gtkrc            .xauth
.DCOPserver_localhost.localdomain  .ICEauthority  .Xauthority
.DCOPserver_localhost.localdomain_:0  .kde  .xsession-errors
Desktop            .kderc
.emacs             .mcop
```

这是一个非常重要的概念，许多 Unix 系统管理员并不清楚：磁盘只能挂载到现有目录上，并且在挂载之前该目录中的任何内容在磁盘再次卸载之前都将无法访问。

3. `mount` 命令支持多种不同的挂载磁盘方法。最重要的标志总结在表 10.2 中。

#### 表 10.2 有用的 mount 标志

| 标志 | 含义 |
|------|---------|
| `-a` | 确保 `/etc/fstab` 中列出的所有设备都已挂载，并在其分离时挂载它们。这可以与 `-t` 结合使用，例如 `mount -a -t ufs`，这将强制挂载 `/etc/fstab` 文件中列出的所有 UFS 文件系统（如果可能）。 |
| `-o opts` | 指定挂载的 `opts` 选项。常见值有 `ro`（只读）、`rw`（读写）、`noatime`（禁用文件访问时间的更新，加快磁盘交互）、`noauto`（磁盘只能显式挂载，而不是通过 `mount -a`）、以及 `noexec`（在磁盘上禁用二进制文件的执行）。 |
| `-r` | 只读挂载（相当于 `-o ro`）。 |
| `-t type` | 将磁盘挂载为 `type` 类型。常见值有 `ext2`、`ext3`、`hfs`、`hfs+`、`nfs`、`ufs`、`iso9660` 和 `xfs`，具体取决于所在的平台。 |
| `-v` | 详细输出。显示更多正在发生的情况。 |
| `-w` | 读写挂载（相当于 `-o rw`）。 |

作为进一步的实验，让我们将一个可执行二进制文件复制到磁盘上，然后以只读方式挂载磁盘以演示一些有趣的行为：
