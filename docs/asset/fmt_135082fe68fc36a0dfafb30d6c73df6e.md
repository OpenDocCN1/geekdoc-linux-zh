
Pass 2: Checking structure

Pass 3: Checking connectivity

Pass 4: Checking reference counts

Pass 5: Checking summary

# 285
# 第 5 章 Linux 文件系统管理

`/dev/mapper/vg00-data`: clean, 2293700 free, 2293760 inodes `[root@server1]#`

## 表 5-6 fsck 命令的常用选项

| 选项 | 说明 |
| :--- | :--- |
| `-f` | 执行完整检查 |
| `-y` | 允许用户对提示回答是 |
| `-A` | 检查 `fstab` 中列出的文件系统 |
| `-C` | 执行检查并显示进度 |
| `-V` | 显示详细输出 |

如果 `fsck` 发现损坏的文件，它会提示用户是否要修复。为了避免这些提示，可以使用表 5-6 中出的 `-y` 选项。要查看 `lost+` 目录的内容，可以使用 `badblocks` 命令。记住，在挂载 `ext`、`ext3` 或 `ext4` 文件系统时会自动创建 `lost+` 目录。然而，在许多 Linux 系统中，每次挂载 `ext`、`ext3` 或 `ext4` 文件系统时，都会强制执行一次文件系统检查。这可能会导致启动延迟几分钟甚至几小时，取决于文件系统的大小。要将其更改为更长的间隔（例如 20 天），你可以使用 `tune2fs` 命令的 `-i` 选项，如下所示：

```
[root@server1]# tune2fs -i 20d /dev/vg0/data

tune2fs 1.4.38 (1-Jan-2020)
```

将检查间隔设置为 1728000 秒

`tune2fs` 命令可以在文件系统创建后更改或“调整”文件系统参数。将自动文件系统检查的间隔设置为 0 将禁用文件系统检查。

## 磁盘配额

如果 Linux 系统上有多个用户，系统必须具有足够的硬盘空间来支持每个用户期望存储的文件。然而，如果硬盘空间有限或公司限制了磁盘使用，你应该对文件系统使用实施限制。这些限制被称为磁盘配额，可以应用于

## 第 5 章 Linux 文件系统管理 263

针对用户或用户组。此外，配额可以限制用户在特定文件系统上创建的文件和目录数量（即限制 inode 数量），或者用户在文件系统上可以使用的所有文件的总大小。有两种类型的配额：`软限制`（soft limits）是用户可以在带有警告的情况下在特定时间内（默认为七天）进行扩展的磁盘配额，而`硬限制`（hard limits）是用户无法越的硬性配额。如果 `/etc/fstab` 中存在条目，配额通常在启动时启用，但之后也可以使用 `quota` 命令和 `quotaoff` 命令分别开启或关闭。

要为 `/data` 文件系统设置配额并限制用户，可以执行以下步骤：

- 编辑 `/etc/fstab`，为 `/data` 文件系统添加 `usquota` 和 `grpquota` 挂载选项。`/etc/fstab` 文件中生成的行应该像如下所示：

```bash
[root@server1] ~# grep data /etc/fstab
/dev/vg00/data ext4 defaults,usquota,grpquota 0 0
[root@server1] ~#_
```

> 注意：在现代 Linux 内核上，你可以使用日志配额（journal quotas），这可以在意外关机期间保护配额数据。要使用日志配额，请将步骤 1 中的 `defaults,usquota,grpquota` 挂载选项替换为 `defaults,usrjquota=aquota.user,grpquota=aquota.group,jqffmt=vfsv0`。

- 将 `/data` 文件系统重新挂载为读写，以使用 `/etc/fstab` 中的新选项更新系统，如下：

```bash
[root@server1] ~# mount /data -o remount,rw
[root@server1] ~#_
```

- 运行 `quotacheck -mavug -F vfsv0` 命令，该命令会在系统中查找 `/etc/fstab` 中列出的配额选项的文件系统的默认配额格式 (`-F vfsv0`)，为所有用户和组 (`-u` 和 `-g`) 提供详细输出 (`-v`)，即使文件系统正在被其他进程使用 (`-m`)。这会在 `/data/aquota.user` 和 `/data/aquota.group` 文件中创建位置信息。`quotacheck` 命令的示例输出所示：

```bash
[server1]# quotacheck -mavug -F vfs0
quotacheck: Your kernel probably supports journaled quota you are not using it. Consider switching to journaled quota
to avoid running quotacheck after an unclean shutdown.
quotacheck: Scanning /dev/mapper/vg00-data [/datal] done
quotacheck: Checked 4 directories and 17 files
[server1 ~]#
```

> 注意：如果在在此阶段 `quotacheck` 输出的开头收到任何警告，可以安全地忽略它们，因为它们是新创建的尚未使用的 `aquota.user` 和 `aquota.group` 文件。

- 使用 `quotaon -avug` 命令对所有配置了配额的文件系统启用用户和组配额：

```bash
[server1]# quotaon -avug
/dev/mapper/vg00-data [/datal]: group quotas turned on
/dev/mapper/vg00-data [/datal]: user quotas turned on
[server1 ~]#
```

> 注意：你也可以为单个文件系统启用和禁用配额。例如，你可以使用 `quotaon /datal` 命令启用 `/datal` 文件系统的配额，并使用 `quotaoff /datal` 命令禁用它们。

- 使用 `edquota` 命令如下所示编辑某些用户的配额：`edquota -u <username>`。这将调出 `vi` 编辑器并允许你设置用户在文件系统上可以使用的块（通常 1 块 = 1 千字节）以及用户在文件系统上可以拥有的 inode（文件和目录）总数的软配额和硬配额。软限制和硬限制为 0 (0) 表示没有限制。要设置硬限制为 20MB (=20480KB) 和 1000 个 inode，以及软限制为 18MB (=18432KB) 和 900 个 inode，你可以执行以下操作：

```bash
[root@server1 ~]# edquota -u user1
Disk quotas for user user1 (uid 1000):
Filesystem blocks soft hard inodes soft hard
/dev/mapper/vg00-datal 1188 0 0 326 0 0
```

接下来，在提供的列中放置适当的值，然后保存并退出 `vi` 编辑器：

```
Disk quotas for user user1 (uid 1000):
Filesystem blocks soft hard inodes soft hard
/dev/mapper/vg00-datal 1188 18432 20480 326 900 1000
```
:wq
"tmp/EdP.aclpsv" 3L, 216C
[root@server1 ~]#

- 6. 使用 `edquota -u -t` 命令编辑用户超出软配额的限制。软配额的默认限制为七天，可以如下进行更改：

```bash
[root@server1 ~]# edquota -u -t
Grace period before enforcing limits:
Time units may be: days, hours, minutes, or seconds
Filesystem
/dev/mapper/vg00-datal
```

- 7. 使用 `quota` 命令收集 `/data` 文件系统的报告，以确保配额已正确更新，如下所示：

```bash
[root@server1 ~]# repquota /datal
```

## 264 第 5 章 Linux 文件系统管理

```bash
[root@server1 ~]# edquota -u -t
Grace period before enforcing limits:
Time units may be: days, hours, minutes, or seconds
Filesystem
/dev/mapper/vg00-datal
```
