
你可以使用 `zpool` 命令删除 ZFS 卷。例如，`zpool destroy data` 将删除上一个输出中创建的 ZFS 卷和池。

如果在创建 ZFS 卷时指定多个设备，这些设备将自动添加到 ZFS 池中，并基于它们创建卷。例如，如果你按照该命令操作，`/dev/sdc` 和 `/dev/sdd` 硬盘将被添加到 `data2` 池中，并创建一个名为 `data2` 的 ZFS 卷（容量为两块硬盘的总和），并挂载到 `/data2` 目录。这等同于 RAID 0 卷，但具有 ZFS 防止文件损坏的益处。

```
[root@server1 ~]# zpool create data2 /dev/sdc /dev/sdd
[root@server1 ~]#
```

要从 `/dev/sde` 和 `/dev/sdd` 硬盘创建 ZFS 池和镜像 ZFS 卷 `data3`，并将该卷挂载到 `/data3`，请在创建时使用 `mirror` 关键字，如下所示：

```
[root@server1 ~]# zpool create data3 mirror /dev/sde /dev/sdf
[root@server1 ~]#
```

`data3` 卷等同于 RAID 1，但在 ZFS 下具有韧性，且卷的总大小与其中一块硬盘的大小相同。

> 注意 24

要创建 ZFS 镜像卷，你需要至少指定两个硬盘设备以防止单块硬盘故障。

要查看组成 `data3` 池的磁盘状态，可以使用以下命令：

```
[root@server1 ~]# zpool status data3
pool: data3
state: DEGRADED
```

status: 一个或多个设备发生了无法恢复的错误。已尝试纠正该错误。应用程序不受影响。

action: 确定设备是否需要更换，并使用 'zpool clear' 清除错误，或使用 'zpool replace' 替换设备。访问 https://openzfs.github.io/openzfs-docs/msg/ZFS-8000-9P

scan: scrub repaired 340K in 00:00:00 with 0 errors on Sep 10

| NAME | STATE | READ | WRITE | CKSUM |
|---|---|---|---|---|
| data3. | DEGRADED | 0 | 0 | 0 |
| mirror-0 | DEGRADED | 0 | 0 | |
| sde | UNAVAIL | 0 | 0 | corrupted data |
| sdf | ONLINE | 0 | 0 | 0 |

```
config:
errors: No data errors
[root@server1 ~]#
```

# 第 6 章 Linux 服务器部署

从上一个示例中可以看出，镜像中的一个磁盘已故障（`/dev/sde`）。在这种情况下，你应该使用 `zpool detach data3 /dev/sde` 将设备从池中分离，更换故障的硬盘，并使用 `zpool attach data3 /dev/sdf /dev/sde` 将磁盘重新附加到镜像中。在此过程中，文件系统仍然可用供供用户读写数据。在重新附加新硬盘后，`zpool status data3` 命令的输出将显示以下内容：

```
[root@server1 ~]# zpool status data3
pool: data3
state: ONLINE
scan: resilved 102K in 00:00:00 with 0 errors on Sep 10
23:47:19 2023
```

```
config:
NAME STATE READ WRITE CKSUM
data3 ONLINE 0 0 0
mirror-0 ONLINE 0 0 0
sde ONLINE 0 0 0
sdf ONLINE 0 0 0
```

```
errors: No data errors
[root@server1 ~]#
```

要从 `/dev/sda`、`/dev/sdb` 和 `/dev/sdc` 硬盘创建一个使用 RAID-Z（等同于具有可变条带的 RAID-5 卷）名为 `data4` 卷并挂载到 `/data4`，请在创建时指定 `raidz` 关键字：

```
[root@server1 ~]# zpool create data4 raidz /dev/sdg /dev/sdh /dev/sdi
[root@server1 ~]#
```

> 注意 25

RAID-Z 卷至少需要三个硬盘来防止单盘故障，需要七个硬盘来防止多盘故障。

> 注意 26

你也可以使用 `raid2`（类似于 RAID-6 的双校验）和 `raid3`（三重校验）来代替 `raidz`。`raid2` 至少需要四个设备，`raid3` 至少需要五个设备。

> 注意 27

具有可变条带的 ZFS 写入性能最高，且几乎不会出现传统 RAID 系统的“RAID 洞”（掉电导致的数据丢失）。随后，可以使用 `zpool status -v` 命令查看 RAID-Z 卷的状态和性能：

```
[root@server1 ~]# zpool status data4
pool: data4
state: ONLINE
config:
```

``` # CompTIA Linux+ 与 LPIC-1：Linux 认证指南

| NAME | STATE | READ | WRITE | CKSUM |
|---|---|---|---|---|
| data4 | ONLINE | 0 | 0 | 0 |
| raid1-0 | ONLINE | 0 | 0 | 0 |
| sdg | ONLINE | 0 | 0 | 0 |
| sdh | ONLINE | 0 | 0 | 0 |
| sdi | ONLINE | 0 | 0 | 0 |

errors: No data errors

```
root@server1:~# iostat -v data4
| pool | capacity | operations | read | write |
|---|---|---|---|---|
| data4 | 220K | 8.6G | 0 | 11 | 10.5K |
| raid1 | 220K | 8.6T | 0 | 11 | 10.5K |
| /dev/sdg | | | 0 | 10 | 25.2K | 83.6K |
| /dev/sdh | | | 0 | 10 | 25.1K | 83.6K |
| /dev/sdi | | | 0 | 10 | 24.8K | 83.6K |

```

root@server1 ~]#

```

对于 ZFS 的常规管理，你使用 `zfs` 命令来管理 ZFS 系统的特性。`zfs` 命令允许你设置各种特定的 ZFS 功能、目录配额、自动压缩以及许多特定的目录特性和性能选项。此外，你可以在现有的 ZFS 卷上配置作为 ZFS 卷的结构。这些子目录是 ZFS 数据集，可以使用任何 ZFS 设置和特性进行配置。例如，如果你创建一个目录 `/data/research`，可以运行以下命令指定将 research 子目录视为 ZFS 数据集：

```
[root@server1 ~]# zfs create data4/research
[root@server1 ~]#
```

要查看可 ZFS 管理的 ZFS 数据集列表，可以运行 `zfs list`：

```
[root@server1 ~]# zfs list
| NAME | USED | AVAIL | REFERENT | MOUNTPOINT |
|---|---|---|---|---|
| data4 | 228K | 8.6G | 42.6K | /data4 |
| data4/research | 38.6K | 8.6T | 38.6K | /data4/research |
|[root@server1 ~]#
```

注意 `zfs list` 输出包含了 `data4` ZFS 卷。这是因为 `data4` 卷也被视为一个数据集，以确保它可以与卷中的其他数据集分开管理。要查看你可以修改的 `data4/research` 数据集的属性，可以使用 `zfs get` 命令：

```
[root@server1 ~]# zfs get all data4/research | less
| NAME | PROPERTY | VALUE | SOURCE |
|---|---|---|---|
| data4/research type | filesystem | | |
| data4/research creation | | Sat 10 23:48 2023 | |
| data4/research used | | 38.6K | | |
| data4/research available | | 214M | | |
| data4/research referenced | | 38.6K | | |
| data4/research compress | | 1.00x | | |
| data/research/ mounted | yes | - | |
| data/research/ quota | none | default | |
| data/research/ reservation | none | default | |
| data/research/ recordsize | 128K | default | | |
| data/research/ mountpoint | /data/research/ | default | | |
| data/research/ sharenfs | off | default | | |
| data/research/ checksum | on | default | | |
| data/research/ compression | off | default | | |
| data/research/ atime | on | default | | |
| data/research/ services | on | default | | |
| data/research/ exec | on | default | | |
| data/research/ setuid | off | default | | |
| data/research/ readonly | off | default | |
```

## CompTIA Linux+ 和 LPIC-1：Linux 认证指南

注意：在 5.15 版本中多个默认设置发生了变化，请确保这不会影响您的部署：
- 元数据的 DUP ( -m dump)
- 启用无空洞模式 (-O no-holes)
- 启用空闲树 (-R free-space-tree)

```
Performing full TRIM /dev/sdc (1.00GiB) ...
Label: (null)
UUID: bafaccc8-7b1f-4e87-8f7f-alab672621f0
Node size: 16384
Sector size: 4096
Filesystem size: 4.00TiB
Block group profiles:
Data: RAID1 102.38MiB
Metadata: RAID1 102.38MiB
System: RAID1 8.00MiB
SSD detected: no
zoned device:
Incompat features: extref, skinny-metadata, no-holes
Runtime features: free-space-tree
Checksum: crc32c
Number of devices: 2
Devices:
ID SIZE PATH
1 2.00TiB /dev/sdb
2 2.00TiB /dev/sdc
[root@server1 ~]#
```

> 注意 29

如果在执行 `mkfs.btrfs` 命令时省略 -m 和 -d 选项，默认会对数据使用 RAID 0，对元数据使用 RAID 1。

你可以通过文件系统内的任何设备将文件系统挂载到点目录；例如，你可以使用 `mount /dev/sdb /storage` 命令，也可以使用 `mount /dev/sdc` 命令将 BTRFS 文件系统挂载到 `/storage` 目录。同样，你可以在 `/etc/stab` 中添加 `/dev/sdb /storage btrfs defaults 0` 行或 `/dev/sdc /storage btrfs defaults 0` 行，以确保在启动时自动挂载 BTRFS 文件系统。

BTRFS 文件系统压缩允许使用挂载选项。例如，`mount -o compress=lz /dev/sdb /storage` 命令将使用 LZ 压缩挂载示例中的 BTRFS 文件系统，而 `/etc/stab` 中的 `/dev/sdc /storage btrfs defaults,compress=lz 0` 行则会在启动时以 LZ 压缩方式进行挂载。

> 注意 30

虽然 ZFS 和 BTRFS 支持多种压缩算法，但由于速度快，Lempel-Ziv-Oberhmer (LZO) 是生产环境中的优选。

在创建 BTRFS 文件系统后，可以使用 `btrfs` 命令对其进行管理。由于 BTRFS 不具备 ZFS 那样的自动功能，你可以检查上一个示例中未挂载的 BTRFS 文件系统，并使用以下命令自动修复任何错误：

```
[root@server1 ~]# btrfs check /dev/sdb
Opening filesystem to check...
Checking filesystem on /dev/sdb
UUID: bfafcc88-7b1f-4e87-8f7f-alab672621f0
[1/7] checking root items
[2/7] checking extents
[3/7] checking free space
[4/7] checking roots
[5/7] checking only csums items (without verifying them)
[6/7] checking root refs
[7/7] quota groups skipped (not enabled on this FS)
found 147456 bytes used, no error found
total bytes: 0
total tree bytes: 147456
total fs tree bytes: 32768
total extent tree bytes: 16384
tree space bytes: 123336
file data blocks allocated: 0
referenced 0
[root@server1 ~]#
```

# 第 6 章 Linux 服务器部署

## 注意 31

可以使用 `btrfs` 命令代替 `btrfs check` 命令。例如，`btrfs /dev/sdb` 执行的任务与上一个示例中的 `btrfs` 命令相同。

`btrfs` 命令还可以用于显示 BTRFS 配置和使用情况。例如，`btrfs filesystem show /dev/sdb` 可以显示包含 `/dev/sdb` 设备的 BTRFS 文件系统的配置，而 `btrfs df /storage` 命令将显示挂载在 `/storage` 目录的 BTRFS 文件系统的使用信息。BTRFS 卷类似于 ZFS 数据集，可以分离到它们自己的挂载点。要为挂载到存储器目录的 BTRFS 文件系统创建卷备份，可以使用 `btrfs subvolume create /storage/backup` 命令，并使用 `compress=lzo /dev/sdb /backup` 命令将其挂载到 `/backup`（前提是 BTRFS 文件系统中的设备之一是设备）。

你可以在 BTRFS 文件系统挂载并在线运行时添加和扩展 BTRFS 文件系统。例如，要向之前创建并挂载到 `/storage` 的 RAID 1 BTRFS 文件系统添加 `/dev/ssd` 和 `/dev/side` 设备，根据生成的配置，你可以遵循以下命令：

```
[root@server1 ~]# btrfs device add /dev/ssd /dev/side /storage
Performing full device TRIM /dev/ssd (2TiB)
Performing full TRIM /dev/side (2TiB) ...
[root@server1 ~]# btrfs filesystem balance /storage
Done, had relocate 3 of chunks
[root@server1 ~]# btrfs show /dev/sdb
Label: (null)
UUID: bafaccc8-7b1f-4e87-8f7f-alab672621f0
