
```
[root@btrfs ~]$ btrfs filesystem usage /data
Overall:
    Device size:               80.00GiB
    Device allocated:         3.77GiB
    Device unallocated:        76.23GiB
    Device missing:            0.00B
    Used:                      576.00KiB
    Free (estimated):         26.41GiB (min: 26.41GiB)
    Free (statfs, df):         19.74GiB
    Data ratio:                3.00
    Metadata ratio:            3.00
    Global reserve:            3.25MiB (used: 0.00GiB)
    Multiple profiles:         no
Data,RAID1C3: Size:1.00GiB, Used:0.00GiB (0.00%)
    /dev/ssd                  1.00GiB
    /dev/sde                  1.00GiB
    /dev/sdf                  1.00GiB
Metadata,RAID1C3: Size:256.00MiB, Used:176.00KiK (0.07%)
    /dev/ssd                  256.00MiB
    /dev/sde                  256.00MiB
    /dev/sdf                  256.00MiB
System,RAID1C3: Size:32.00MiB, Used:16.00MiB (0.05%)
    /dev/sda                  32.00MiB
    /dev/sde                  32.00MiB
    /dev/sdf                  32.00MiB
Unallocated:
    /dev/sda                  1.00GiB
    /dev/sdb                  7.97GiB
    /dev/sde                  7.97GiB
    /dev/sdf                  7.97GiB
    /dev/sdg                  9.00GiB
    /dev/sdh                  9.00GiB
    /dev/sdi                  8.00GiB
    /dev/sdj                  8.00GiB
```

图 4.13 - 未平衡的使用

虽然这只是一个小问题，但它未来可能会产生影响。幸运的是，解决方案很简单——执行 `btrfs balance`。该命令将重新平衡数据。

注意

为了确保数据良好平衡，建议在添加或删除设备时始终对系统进行平衡，即使存在细微差异。这种做法对于保持文件系统的性能至关重要。`ol8_developer` 仓库中的 `btrfsmaintenance` 软件包是自动执行所需 Btrfs 维护任务的极佳工具。

Btrfs 的功能比旧的 XFS 技术强大得多。这包括子卷、快照和配额。Btrfs 子卷是一项极出色的工具，允许用户在单个 Btrfs 文件系统中创建多个快照或子文件。这些子卷在文件系统层级结构中作为不同的目录显示，它们共享相同的存储空间并可以进行独立管理。

子卷的灵活性和多功能使其成为各种用途的理想选择，例如创建备份或隔离文件系统的部分以便更于管理。快照则特别有用，因为它们提供了文件系统在特定时间点的只读副本。通过快照，用户可以将文件或整个子卷恢复到之前的状态，或者轻松地创建可以移动到另一个系统的可复制备份。

子卷还允许用户更高效地管理磁盘空间。例如，用户可以为某个特定的应用程序或项目创建一个子卷，并限制其使用在特定的容量范围内，以防止其占用文件系统过多的空间。此外，还可以通过为不同的子卷分配不同的权限，或为不同的用户或组创建单独的子卷来实现访问控制。本配方将介绍如何执行这些操作。

## 准备工作

本配方需要一个 Btrfs 文件系统，并将使用上一个配方创建的数据文件系统进行示例。

## 如何操作...

在本配方中，我们将执行以下操作：

- 1. 在 `/data` 中创建一个子卷并挂载它。
- 2. 在子卷上设置配额。
- 3. 创建快照。
- 4. 启用压缩。

创建子卷非常简单，通过使用 `btrfs` 命令并指定子卷的完整路径即可完成：

```
btrfs subvolume create /data/vol1
```

创建完成后，只需将其添加到 `fstab` 中即可，这次在第四列中声明子卷名称。如下所示，其中使用子卷 `vol1` 挂载了 `/data/vol1`：

```
root@btrfs ~# edit /etc/fstab

# /etc/fstab
# Created by anaconda on Sun May 14 01:31:56 2023
# accessible filesystems, by reference, are maintained under '/dev/disk/'.
# See man fstab(5), finds(8), mount(8) and/or bklkid(8) for more info.

# After editing this file, run 'systemctl daemon-reload' to update system
# units generated from file.

UUID=55ed0c6b-06b5-49a0-a94b-35cdf368bf49 btrfs subvol=root      0 0
UUID=55ed0c6b-06b5-49a0-a94b-35cdf368bf49 btrfs subvol=boot     0 0
UUID=55ed0c6b-06b5-49a0-a94b-35cdf368bf49 btrfs subvol=home    0 0
UUID=55ed0c6b-06b5-49a0-a94b-35cdf368bf49 btrfs subvol=var       0 0
UUID=55ed0c6b-06b5-49a0-a94b-35cdf368bf49 btrfs subvol=root      0 0
UUID=55ed0c6b-06b5-49a0-a94b-35cdf368bf49 btrfs subvol=var_log  0 0
UUID=66b9a6b4-ff75-4f63-a2f7-ce9f8e8fa32 btrfs subvol=data      0 0
UUID=55ed0c6b-06b5-49a0-a94b-35cdf368bf49 btrfs subvol=home    0 0
UUID=1d1c19d4-abbf-46c8-a93e-feb826f669 btrfs swap           0 0
root@btrfs ~#
```

图 4.15 - btrfs 中的子卷

现在子卷已经挂载，让我们添加一个配额将其限制在 5 GB。要做到这一点，我们首先需要为该卷创建配额功能。使用以下命令完成：

```
btrfs quota enable /data
```

接下来，我们需要为子卷分配配额限制。这将限制定义的子卷大小。我们使用 `limit` 选项，如下命令所示：

```
btrfs qgroup limit 5g /data/vol
```

你可以使用 `btrfs qgroup show` 命令配合 `-ref` 选项来查看卷中定义了哪些配额：

```
root@btrfs ~# btrfs qgroup show -ref /data/vol
groupid         rfer        excl        max_rfer      max_excl
-------------------------------------------------------------
0/256            16.0KiB      16.0KiB      5.0GiB       none
root@btrfs ~#
```

图 4.16 - 设置配额

现在我们已经设置了配额，让我们为备份创建一个快照。我们需要一个存放备份的地方，所以使用以下命令为备份创建一个子卷：

```
btrfs subvolume create /data/backup
```
