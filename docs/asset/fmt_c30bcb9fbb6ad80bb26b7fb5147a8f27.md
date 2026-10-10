
## D-1: 检查文件系统错误

| 操作步骤 | 目的 |
| --- | --- |
| 1 在 `tty2` 上以 `root` 身份登录 | （如有必要。） |
| 2 输入 `df` | 查看系统上存在的文件系统。 |
| 3 输入以下命令：<br>`dumpe2fs -h /dev/hda4` | 查看 `/dev/hda3` 文件系统的 `inode` 信息。 |
| 4 输入以下命令：<br>`fsck -t ext3 /dev/hda4` | 读取警告信息。 |
| 按 `N` | 退出 `fsck` 命令。 |
| 5 输入 `umount /newmount` | 从 `hda3` 分区卸载文件系统。 |
| 输入 `mount` | 验证文件系统是否已正确卸载。 |
| 6 输入以下命令：<br>`fsck -t ext3 /dev/hda4` | 检查文件系统是否存在错误。 |
| 7 输入以下命令：<br>`fsck -Cf -t ext3 /dev/hda4` | 在检查文件系统时显示进度完成条。 |
| 8 输入 `e2fsck -c /dev/hda4` | 在检查文件系统之前应用日志。 |
| 9 输入以下命令：<br>`tune2fs -i 0 /dev/hda4` | 更改强制检查的间隔以避免其发生。 |
| 10 输入 `mount /dev/hda4` | |
| 11 将活动 B-1 中的软磁盘插入电脑的软盘驱动器 | |
| 输入 `debugfs -w /dev/fd0` | 进入编辑模式下的文件系统调试器。 |

## 文件系统管理 5-43

- 12 输入 `inittab` 编辑软磁盘上 `inittab` 文件的 `inode`。
- 当提示更改文件模式时，按 `ENTER`。
- 按 `ENTER` 接受显示的值。
- 重复此操作以修改用户 ID（`User ID`）、组 ID（`Group ID`）等，直到提示更改链接计数（`Link Count`）。
- 13 当提示更改链接计数时，输入 `0`。
- 按 `ENTER` 为 `inittab` 文件赋予一个为 `0` 的无效链接计数。
- 对所有剩余选项按 `ENTER` 以接受显示的值。
- 14 按 `Q` 退出 `debugfs` 命令。
- 15 输入以下命令：检查软磁盘是否存在错误。

```
fsck -f -t ext2 /dev/fd0
```

- 在每个错误处按 `Y` 允许 `fsck` 修复错误。
- 16 再次运行该命令查看是否仍有任何错误。
- 17 弹出软磁盘

## 磁盘配额

如果您的系统中有多个用户，则必须有足够的磁盘空间来支持每个用户预期存储的文件。然而，如果磁盘空间有限，或者公司策略限制了磁盘使用，您应该对文件系统使用设置限制。

这些限制被称为磁盘配额（`quota`），可以应用于用户或用户组。配额限制了用户可以创建的文件和目录数量（即限制创建的 `inode` 数量），或者用户可以拥的所有文件的总大小。

配额限制有两种类型：

- 软限制（`Soft limits`）：允许用户在一定时间内扩展它们（默认为七天）。
- 硬限制（`Hard limits`）：是强制性的，将防止用户超过它们。

如果 `/etc/fstab` 中存在配额条，配额通常在启动时启用，但也可以使用 `quota` 和 `quotaoff` 命令开启或关闭。

要设置配额，您编辑 `/etc/fstab` 并限制用户 `"user"`，需要执行以下步骤：

- 1. 编辑 `/etc/fstab` 文件，为文件系统添加 `usquota` 和 `grquota` 挂载选项。`/etc/fstab` 应该如下：
```bash
[localhost root]# # cat /etc/fstab

LABEL=/               ext3

default,usquota,grquota  1 1

none                   /dev/pts  devpts gid=5,mode=620

0 0                    /proc     defaults

0 0                    /dev/shm   tmpfs defaults

0 0                    /dev/hdc2  swap      defaults

0 0                    /dev/cdrom /mnt/cdrom  iso9660 noauto,owner, kudzu,ro

0 0                    /dev/fd0   /mnt/floppy auto      noauto,owner, kudzu
```

- 2. 重新挂载文件系统为读写，以使用 `/etc/fstab` 中的新选项更新系统。执行此操作的命令是：
```bash
[localhost root]# mount -o remount,rw

[localhost root]#
```

- 3. 在文件系统根目录下创建名为 `aquota.user` 和 `aquota.group` 的两个文件。对于文件系统，您应该创建 `/aquota.user` 和 `/aquota.group`。随后，运行 `quotacheck -mavug` 命令，该命令查找文件所有权并根据 `/etc/fstab` 列出的配额选项更新配额数据。`quotacheck` 切换 `-a`（所有文件系统）、`-v`（详细输出）、`-u` 和 `-g`（针对所有用户组）、`-m`（即使文件系统被其他进程使用）。这会在文件系统根目录下创建两个文件：`/aquota.user` 和 `/aquota.group`。您将看到以下输出：
```
[root@localhost root]# touch /aquota.user

[root@localhost root]# touch /aquota.group

[root@localhost root]# quotacheck -mavug

quotacheck: Scanning /dev/hdc1 [/ done

quotacheck: Checked 22249 directories and 337809 files

[root@localhost root]# _
```

- 4 使用 `quotaon/` 命令文件文件配额（使用 `quotaoff/` 命令关闭）。
- 5 使用 `edquota -u <username>` 命令编辑某些用户的配额。这将打开编辑器，允许您为用户可以拥有的块数（通常 1 块 = KB）以及用户可以拥有的 `inode` 总数（文件和目录）设置软配额和硬配额。
```
[root@localhost root]# edquota -u user1

Disk quotas for user user1 (uid 500):

Filesystem blocks soft hard inodes soft

hard

/dev/hdal 1188 0 0
```

## 文件系统管理 5-45

```bash
[root@localhost root]# touch /aquota.user

[root@localhost root]# touch /aquota.group

[root@localhost root]# quotcheck -mavug

quotacheck: Scanning /dev/hdc1 [/ done

quotacheck: Checked 22249 directories and 337809 files

[root@localhost root]# _
```

- 4 使用 `quotaon/` 命令文件系统配额（使用 `quotaoff/` 命令关闭）。
- 5 使用 `edquota -u <username>` 命令编辑某些用户的配额。这将打开编辑器，允许您为用户可以拥有的块数（通常 1 块 = KB）以及用户可以拥有的 `inode` 总数（文件和目录）设置软配额和硬配额。
```
[root@localhost root]# edquota -u user1

Disk quotas for user user1 (uid 500):

Filesystem blocks soft hard inodes soft

hard

/dev/hdal 1188 0
```

软限制为 0 表示没有限制。以下输出设置了 20 MB (20480 KB) 的硬限制以及 18 MB (18432 KB) 的软限制。在列中输入适当的值，然后保存并退出 `vi` 编辑器：
```
[root@localhost root]# edquota -u user1

Disk quotas for user user1 (uid 500):

Filesystem blocks soft hard inodes soft

hard

/dev/hdal 1188 0 0
```

## 文件系统管理 267

## CompTIA+ 认证目标

用户超出的时间限制：天、分钟或秒。

软限制为 0 表示没有限制。以下输出设置了 20 MB (20480 KB) 的硬限制以及 18 MB (18432 KB) 的软限制。在列中输入适当的值，然后保存并退出 `vi` 编辑器：
```
[root@localhost root]# edquota -u user1

Disk quotas for user user1 (uid 500):

Filesystem blocks soft hard inodes soft

hard

/dev/hdal 1188 0 0
```

## 文件系统管理 268

## D-2: 建立磁盘配额

执行吧！

### 操作步骤

### 目的

| 操作步骤 | 目的 |
| --- | --- |
| 1 在 `tty2` 上以 `root` 身份登录 | （如有必要。） |
| 2 输入 `df` | 查看系统上存在的文件系统。 |
| 3 输入以下命令：<br>`dumpe2fs -h /dev/hda4` | 查看 `/dev/hda3` 文件系统的 `inode` 信息。 |
| 4 输入以下命令：<br>`fsck -t ext3 /dev/hda4` | 读取警告信息。 |
| 按 `N` | 退出 `fsck` 命令。 |
| 5 输入 `umount /newmount` | 从 `hda3` 分区卸载文件系统。 |
| 输入 `mount` | 验证文件系统是否已正确卸载。 |
| 6 输入以下命令：<br>`fsck -t ext3 /dev/hda4` | 检查文件系统是否存在错误。 |
| 7 输入以下命令：<br>`fsck -Cf -t ext3 /dev/hda4` | 在检查文件系统时显示进度完成条。 |
| 8 输入 `e2fsck -c /dev/hda4` | 在检查文件系统之前应用日志。 |
| 9 输入以下命令：<br>`tune2fs -i 0 /dev/hda4` | 更改强制检查的间隔以避免其发生。 |
| 10 输入 `mount /dev/hda4` | |
| 11 将活动 B-1 中的软磁盘插入电脑的软盘驱动器 | |
| 输入 `debugfs -w /dev/fd0` | 进入编辑模式下的文件系统调试器。 |

- 12 输入 `inittab` 编辑软磁盘上 `inittab` 文件的 `inode`。
- 当提示更改文件模式时，按 `ENTER`。
- 按 `ENTER` 接受显示的值。
- 重复此操作以修改用户 ID（`User ID`）、组 ID（`Group ID`）等，直到提示更改链接计数（`Link Count`）。
- 13 当提示更改链接计数时，输入 `0`。
- 按 `ENTER` 为 `inittab` 文件赋予一个为 `0` 的无效链接计数。
- 对所有剩余选项按 `ENTER` 接受显示的值。
- 14 按 `Q` 退出 `debugfs` 命令。
- 15 输入以下命令：检查软磁盘是否存在错误。

```
fsck -f -t ext2 /dev/fd0
```

- 在每个错误处按 `Y` 允许 `fsck` 修复错误。
- 16 再次运行该命令查看是否仍有任何错误。
- 17 弹出软磁盘

## D-2: 建立磁盘配额

执行吧！

- 1 编辑 `/etc/fstab` 文件，为文件系统添加 `usquota` 和 `grquota` 挂载选项。`/etc/fstab` 应该如下：
```bash
[localhost root]# # cat /etc/fstab

LABEL=/               ext3

default,usquota,grquota  1 1

none                   /dev/pts  devpts gid=5,mode=620

0 0                    /proc     defaults

0 0                    /dev/shm   tmpfs defaults

0 0                    /dev/hdc2  swap      defaults

0 0                    /dev/cdrom /mnt/cdrom  iso9660 noauto,owner, kudzu,ro

0 0                    /dev/fd0   /mnt/floppy auto      noauto,owner, kudzu
```

- 2 重新挂载文件系统为读写，以使用 `/etc/fstab` 中的新选项更新系统。执行此操作的命令是：
```bash
[localhost root]# mount -o remount,rw

[localhost root]#
```

- 3 在文件系统根目录下创建名为 `aquota.user` 和 `aquota.group` 的两个文件。对于文件系统，您应该创建 `/aquota.user` 和 `/aquota.group`。随后，运行 `quotacheck -mavug` 命令，该命令查找文件所有权并根据 `/etc/fstab` 列出的配额选项更新配额数据。`quotacheck` 切换 `-a`（所有文件系统）、`-v`（详细输出）、`-u` 和 `-g`（针对所有用户组）、`-m`（即使文件系统被其他进程使用）。这会在文件系统根目录下创建两个文件：`/aquota.user` 和 `/aquota.group`。你将看到以下输出：
```
[root@localhost root]# touch /aquota.user

[root@localhost root]# touch /aquota.group

[root@localhost root]# quotacheck -mavug

quotacheck: Scanning /dev/hdc1 [/ done

quotacheck: Checked 22249 directories and 337809 files

[root@localhost root]# _
```

- 4 使用 `quotaon/` 命令文件系统配额（使用 `quotaoff/` 命令关闭）。
- 5 使用 `edquota -u <username>` 命令编辑某些用户的配额。这将打开编辑器，允许您为用户可以拥有的块数（通常 1 块 = KB）以及用户可以拥有的 `inode` 总数（文件和目录）设置软配额和硬配额。
```
[root@localhost root]# edquota -u user1

Disk quotas for user user1 (uid 500):

Filesystem blocks soft hard inodes soft

hard

/dev/hdal 1188 0 0
```
