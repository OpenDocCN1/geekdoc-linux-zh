
| 选项 | 描述 |
| :--- | :--- |
| -f | 执行完整的文件系统检查 |
| -a 或 -y | 允许 `fsck` 自动修复任何错误 |
| -A | 检查 `/etc/fstab` 中第六个字段为 1 或 2 的所有文件系统 |
| -Cf | 执行完整的文件系统检查并显示进度行 |
| -AR | 检查 `/etc/fstab` 中第六个字段为 1 或 2 的所有文件系统，但跳过 / 文件系统 |
| -V | 显示详细输出 |

**表 5-6 fsck 命令的常用选项**

要查看 lost+found 目录的内容，只需挂载该设备并查看挂载点正下方的 lost+found 目录内容即可。由于很难通过 inode 号识别丢失的文件，大多数用户会定期删除此目录的内容。请记住，当创建 ext2、ext3 或 ext4 文件系统时，会自动创建 lost+found 目录。

就像你可以使用 `mkfs` 命令创建 ext2、ext3 或 ext4 文件系统一样，你也可以使用 `e2fsck` 命令来检查 ext2、ext3 或 ext4 文件系统。`e2fsck` 命令接受更多选项，并且比 `fsck` 能更彻底地检查文件系统。例如，通过使用 `e2fsck` 命令的 `-c` 选项，你可以检查硬盘上的坏块并将它们添加到文件系统的坏块表中，以便将来不再使用这些块，如下例所示：

```
[root@server1 ~]# e2fsck -c /dev/vg00/data
e2fsck 1.42.8 (20-Jun-2013)
Checking for bad blocks (read-only test): done
/dev/vg00/data: Updating bad block inode.
Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
Pass 4: Checking reference counts
Pass 5: Checking group summary information
/dev/vg00/data: ***** FILE SYSTEM MODIFIED *****
/dev/vg00/data: 11/983040 files (0.0% non-contiguous), 104064/3932160 blocks
[root@server1 ~]# 
```

![](img/c27875544958897d817484d558c208c8_262_0.png)

badblocks 命令可以执行与带有 `-c` 选项的 `e2fsck` 命令相同的功能。

你不能使用 `fsck` 命令来检查 btrfs 文件系统。相反，在卸载 btrfs 文件系统后，你必须使用 **btrfs 命令** 来检查它。例如，命令 `btrfs check /dev/sda5` 将检查位于 `/dev/sda5` 上的已卸载的 btrfs 文件系统。

回顾本章前面提到的内容，当从 `/etc/fstab` 文件中的条目挂载文件系统时，在启动时运行 `fsck` 命令。`/etc/fstab` 中第六个字段为 1 的条目首先被检查，随后是第六个字段为 2 的条目。但是，在许多 Linux 系统上，每次挂载 ext2、ext3 或 ext4 文件系统时，都会定期强制进行一次完整的文件系统检查。根据被检查文件系统的大小，这可能会延迟启动过程几分钟甚至几个小时。要更改此间隔，你可以使用 `tune2fs` 命令的 `-i` 选项，如下所示：

```
[root@server1 ~]# tune2fs -i 0 /dev/vg00/data

tune2fs 1.42.8 (20-Jun-2013)

Setting interval between check 0 seconds

[root@server1 ~]# 
```

` tune2fs` 命令可用于在文件系统创建后更改或“调整”文件系统参数。如前例所示，将检查间隔更改为 0 秒会禁用文件系统检查。

## 硬盘配额

如果 Linux 系统上有多个用户，则必须有足够的硬盘空间来支持每个用户预期存储在硬盘上的文件。然而，如果硬盘空间有限或公司策略限制磁盘使用量，你应该对文件系统的使用施加限制。这些限制称为 **硬盘配额**，可以应用于用户或用户组。此外，配额可以限制用户在特定文件系统上可以创建多少文件和目录（即限制创建的 inode 数量），或者用户在文件系统中可以拥有的所有文件的总大小。有两种类型的配额限制：软限制和硬限制。**软限制** 是用户可以在一定时间内（默认七天）超出的硬盘配额，而 **硬限制** 是用户不能超出的刚性限制。如果 `/etc/fstab` 中有配额条目，配额通常在启动时启用，但之后也可以使用 `quotaon` 和 `quotaoff` 命令分别开启和关闭它们。

默认情况下，Fedora 20 未安装配额支持。要获得配额支持，你必须运行 `yum install quota` 命令，从互联网软件仓库下载并安装 quota 包。之后，你可以执行以下步骤为 `/data` 文件系统设置配额并限制用户 `user1`：

1.  编辑 `/etc/fstab` 文件，为 `/data` 文件系统添加 `usrquota` 和 `grpquota` 挂载选项。生成的 `/etc/fstab` 文件应如下所示：

    ```
    [root@server1 ~]# cat /etc/fstab

    # /etc/fstab
    # Created by anaconda on Mon Aug 2 09:34:19 2015
    #
    # Accessible filesystems, by reference, are maintained under '/dev/disk'
    # See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for info
    #
    /dev/sda1    /    ext4    defaults    1 1
    /dev/sda2    swap    swap    defaults    0 0
    /dev/vg00/data    /data    ext4    defaults,usrquota,grpquota    0 0
    [root@server1 ~]# 
    ```

    你也可以在现代 Linux 内核上使用日志式配额，这会在意外关机期间保护配额数据。要使用日志式配额，只需将第 1 步中的挂载选项 `defaults,usrquota,grpquota` 替换为：`defaults,usrquota,grpquota,aqquota.user,grpjquota=aqquota.group,jqfmt=vfsv0`

2.  以读写方式重新挂载 `/data` 文件系统，以使用 `/etc/fstab` 中的新选项更新系统。执行此操作的命令是：

    ```
    [root@server1 ~]# mount /data -o remount,rw
    [root@server1 ~]# 
    ```

3.  运行 `quotacheck -mavugf -F vfs0` 命令，该命令在系统上查找文件所有权，并使用默认配额格式 (-F vfs0) 为 `/etc/fstab` 中列有配额选项的所有文件系统 (-a) 创建配额数据库 (-f)，为所有用户和组 (-u 和 -g) 提供详细输出 (-v)，即使文件系统正被其他进程使用 (-m)。这会在 `/data/aquota.user` 和 `/data/aquota.group` 文件中创建并放置信息。`quotacheck` 命令的示例输出如下：

    ```
    [root@server1 ~]# quotacheck -mavugf -F vfs0
    quotacheck: Your kernel probably supports journaled quota but you are not using it. Consider switching to journaled quota to avoid running quotacheck after an unclean shutdown.
    quotacheck: Scanning /dev/sda2 [/] done
    quotacheck: Checked 8983 directories and 109416 files
    [root@server1 ~]# 
    ```

    如果你在此阶段在 `quotacheck` 输出的开头收到任何警告，你可以安全地忽略它们，因为它们是尚未使用的、新创建的 `aquota.user` 和 `aquota.group` 文件的结果。

4.  使用 `quotaon -avug` 命令为所有已配置配额的文件系统开启用户和组配额：

    ```
    [root@server1 ~]# quotaon -avug
    /dev/mapper/vg00-data [/data] : group quotas turned on
    /dev/mapper/vg00-data [/data] : user quotas turned on
    [root@server1 ~]# 
    ```

    你还可以为单独的文件系统启用和禁用配额。例如，你可以使用 `quotaon /data` 命令来启用 `/data` 文件系统的配额，并使用 `quotaoff /data` 命令来禁用它们。

5.  使用 `edquota` 命令按以下方式编辑特定用户的配额：`edquota -u <username>`。

    这将启动 vi 编辑器，允许你设置用户在文件系统中可以拥有的块数量（通常，1 块 = 1 千字节）以及用户在文件系统中可以拥有的总 inode 数（文件和目录）的软配额和硬配额。软限制和硬限制为零 (0) 表示没有限制。要设置硬限制为 20MB (=20480KB) 和 1000 个 inode，以及软限制为 18MB (=18432KB) 和 900 个 inode，你可以执行以下操作：

    ```
    [root@server1 ~]# edquota -u user1
    Disk quotas for user user1 (uid 500):
      Filesystem  blocks    soft    hard  inodes  soft    hard
      /dev/mapper/vg00-data    1188      0       0     326      0      0
      ~
      ~
      ~
      ~
      "/tmp/EdP.ac1p5l^" 3L, 216C
    ```
    接下来，在提供的列中填入适当的值，然后保存并退出 vi 编辑器：

    ```
    Disk quotas for user user1 (uid 500):
      Filesystem  blocks    soft    hard  inodes  soft    hard
      /dev/mapper/vg00-data    1188  18432  20480    326    900   1000
      ~
      ~
      ~
      :wq
      "/tmp/EdP.ac1p5l^" 3L, 216C written
    [root@server1 ~]# 
    ```

6.  使用 `edquota -t` 命令编辑用户超出软配额的限制时间。软配额的默认时间限制为七天，但可以按以下方式更改：

    ```
    [root@server1 ~]# edquota -t
    Grace period before enforcing soft limits for users:
    Time units may be: days, hours, minutes, or seconds
      Filesystem  Block grace period  Inode grace period
      /dev/mapper/vg00-data      7days           7days
      ~
      ~
      ~
      "/tmp/EdP.alvzf5^" 4L, 233C
    ```

7.  使用 `repquota` 命令收集数据文件系统中按用户划分的配额报告，以确保配额已正确更新，如下面的输出所示：

    ```
    [root@server1 ~]# repquota /data

    *** Report for user quotas on device /dev/mapper/vg00-data
    Block grace time:  7days;  Inode grace time:  7days
    ```

