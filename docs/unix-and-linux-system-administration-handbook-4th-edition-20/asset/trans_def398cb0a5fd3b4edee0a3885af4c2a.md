

# ZFS 架构

该系统将在未来几十年内被广泛模拟。悬而的问题是，我们需要等多久才能在其他系统中获得 ZFS 风格的特性。尽管 ZFS 是开源软件，遗憾的是其目前的许可条款阻止了它被纳入 Linux 内核。

Oracle 的 Btrfs 文件系统项目（“B-树文件系统”）正式命名为“Btrfs”，尽管很难不让人联想到“butter face”（黄油脸），其目标是在 Linux 平台上重现许多 ZFS 的进展。它已经作为技术预览包含在当前的 Linux 内核中。Ubuntu 和 SUSE 用户可以分别尝试安装 `btrftools` 和 `btrprogs` 包。然而，Btrfs 尚未达到生产就绪，而且由于 Oracle 收购了 Sun，Btrfs 和 ZFS 的确切功能尚不确定。

# ZFS 架构

图 D 显示了 ZFS 系统主要对象及其相互关系的示意图。

图 D ZFS 架构

![](img/579efec8c67772f31ecf34844bbb71a2_313_0.png)

ZFS 的“池”（pool）类似于其他系统中的“卷组”（volume group）。每个池由“虚拟设备”组成，这些设备可以是原始存储设备（磁盘、分区、镜像组或 RAID 阵列）。ZFS 在精神上与 RAID 5 相似，它使用一个或多个校验设备为阵列提供冗余。然而，ZFS 将这种方案称为 RAID-Z，并使用变长条带来消除 RAID 5 空洞。所有到存储池的写入都分布在池的虚拟设备上，因此，只包含单个设备的池实际上是 RAID 0 的实现，尽管此配置中的设备并不要求具有相同的大小。

遗憾的是，目前的 ZFS RAID 略显脆弱，你无法向阵列中添加新设备，也无法永久删除某个设备。在大多数 RAID 实现中，设备的大小是相同的；你可以强迫 ZFS 接受混合大小，但最小设备的大小决定了整个阵列的大小。若要在与 ZFS 结合时高效地使用不同大小的磁盘，你必须预先对磁盘进行分区，并将剩余区域定义为单独设备。

尽管你可以将未分区的磁盘交给 ZFS 管理，但 ZFS 会在这些磁盘上秘密写入 GPT 风格的分区表，并将每个磁盘的所有空间分配给其第一个分区。ZFS 的大部分配置和管理通过两个命令完成：**zpool** 和 **zfs**。我们使用 zpool 来构建和管理池以及从池创建的实体，主要是文件系统以及用作交换空间和数据库存储的卷。

# 存储：示例：为 Solaris 添加磁盘

第一步是链接磁盘并将其添加到新的存储池中：

```
solaris$ zpool create demo db1
```

在深入 ZFS 细节之前，让我们先从一个高层示例开始。假设你已经为 Solaris 系统添加了块新磁盘，并且该磁盘显示为 `/dev/cdb1`。`format` 命令会向你显示一个系统磁盘菜单，你可以从中识别出该磁盘。第二步是……ZFS 标记磁盘，创建池 "demo"，在池池内创建一个文件系统，并将该文件系统挂载为 `/demo`。该文件系统将在系统启动时自动挂载。

```
solaris$ ls -a /demo
```

如果我们能简单地将新磁盘添加到现有的根池（默认名为 "rpool"），将会更加令人印象深刻。命令是 `sudo zpool add rpool db1`。遗憾的是，根池只能包含一个虚拟设备。然而，其他池可以通过这种方式进行扩展。

# 文件系统与属性

ZFS 会在新的存储池上自动创建文件系统，因为默认情况下 ZFS 文件系统不消耗特定的空间。所有位于池中的文件系统都可以从池的可用空间中提取。与相互独立的传统文件系统不同，ZFS 文件系统是分级结构，并以各种方式与其父子文件系统交互。你使用 `zfs create` 创建新的文件系统。

```
solaris$ sudo zfs create demo/new_fs
solaris$ zfs list -r demo
NAME        USED AVAIL REFER MOUNTPOINT
demo        100K  488G  21K   /demo
demo/new_fs  19K   488G  19K   /demo/new_fs
```

`zfs` 的 `-r` 参数使其能够递归处理子文件系统。大多数其他 zfs 子命令也支持 `-r`。非常有用的是，ZFS 在我们创建新文件系统后会自动挂载它。为了模拟固定大小的传统文件系统，你可以调整文件系统的属性以添加“预留”（在存储池中为文件系统预留的空间量）并使用配额（quota）。这种调整是 ZFS 管理的关键之一，而且对于习惯了其他系统的管理员来说，这是某种范式的转变。在这里，我们将两个值都设置为 1GB：

```
solaris$ sudo zfs set reservation=1g demo/new_fs
solaris$ zfs set quota=1g demo/new_fs
solaris$ zfs list -r demo
NAME        USED AVAIL REFER MOUNTPOINT
demo        1.00G  487G  21K   /demo
demo/new_fs  19K   1024M  19K   /demo/new_fs
```

新的配额反映在 `/demo/new_fs` 的 AVAIL 列中。同样，预留立即显示在 `demo` 的 USED 列中。

新的配额反映在 `/demo/new_fs` 的 AVAIL 列中。同样，预留立即显示在 `demo` 的 USED 列中。

这两个属性更改是纯粹的记录。对实际存储池的唯一更改是为 `/demo/new_fs` 预留空间。大多数 ZFS 操作、创建新的存储池和文件系统都是轻量级的。使用这种空间管理系统，你可以轻松地组合多个文件系统，以确保集合大小不会超过阈值；你不需要在单个文件系统上设置限制。你必须设置配额和预留属性来正确模拟固定大小的文件系统。光有预留只能确保文件系统有足够的增长空间，无法限制文件。

# 属性继承

许多属性会被子文件系统继承。例如，如果我们想将 demo 池的根挂载到 `/opt/demo` 而不是 `/demo`，只需设置 `mountpoint` 参数：

```
solaris$ zfs set mountpoint=/opt/demo demo
solaris$ zfs list -d
NAME        USED AVAIL REFER MOUNTPOINT
demo        1.00G  487G  21K /opt/demo
demo/new_fs  19K   1024M  19K /opt/demo/new_fs
solaris$ ls /opt/demo
new_fs
```

使用 `zfs get` 查看特定属性的有效值；`zfs get all` 则导出所有属性。`SOURCE` 列告诉每个属性为何具有特定值：`local` 表示属性是显式设置的，`-` 表示该属性是只读的。如果属性值是从祖先文件系统继承的，`SOURCE` 将显示该继承的细节，如下：

```
solaris$ zfs get all demo/new_fs
solaris$ zfs get all demo
NAME PROPERTY VALUE SOURCE
demo/new_fs type filesystem
demo/new_fs creation Wed Mar 17 17:50 2010
demo/new_fs available 1024M
demo/new_fs referenced 19K
demo/new_fs compressratio 1.0x
demo/new_fs mounted yes
demo/new_fs quota 1G local
demo/new_fs reservation 1G local
demo/new_fs mountpoint /opt/new_fs inherited from demo
<更多, 大约 40 个>
```

