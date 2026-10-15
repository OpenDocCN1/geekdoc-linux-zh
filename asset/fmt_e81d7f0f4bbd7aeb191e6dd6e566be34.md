
由于它们共享一些技术基础，Btrfs 和 ZFS 之间的比较是不可避免的。然而，Btrfs 并不是 ZFS 的克隆，也没有复制 ZFS 的架构。例如，你可以像其他文件系统一样通过运行 `mount` 命令或在 `/etc/fstab` 中列出它们来挂载 Btrfs 卷。

尽管 Btrfs 卷及其子卷存在于统一命名空间，但它们之间没有层级关系。要创建一组 Btrfs 子卷，你必须单独修改每一个。Btrfs 命令不是递归的，且卷属性是不可的。这与其说是缺失，不如说是一种设计选择：为什么要用可以用脚本模拟的功能加载文件系统？Btrfs 以多种方式反映了这种对简单的偏好。例如，Btrfs 存储池只能包含一种配置的磁盘组（例如 RAID 5），而 ZFS 池可以包含多个磁盘组以及缓存磁盘、意图日志和备用盘。

软件领域常见的，对于相对优劣的争论往往变得激烈并关注风格差异。然而，两个系统之间的几个重要差异高出了挑剔和个人喜好的水平。

- 在更改硬件配置方面，Btrfs 是明显的获胜者；ZFS 在此未战。你可以随时添加或删除磁盘，甚至更改 RAID 类型，Btrfs 在保持在线的同时相应地重新分配数据。在 Btrfs 中，如果不将数据导出到外部媒体并重新开始，这种更改是不可能的。
- 即使内存密集型（如去重），ZFS 在内存充足的情况下运行最好。2GB 是建议的最低配置。对于虚拟机来说，这是一个很大的内存。
- ZFS 在独立 SSD 上缓存频繁读取数据对于很多情况来说是一个特性，Btrfs 目前对此没有答案。
- 截至 2017 年，Btrfs 的校验 RAID 实现（RAID 5 和 6）尚未准备好用于生产。这不是我们的观点；这是开发者的官方说法。这是一项重大功能。

# 设置和存储转换

在本节中，我们演示了几个与之前节中 ZFS 显示类似的常用 Btrfs 过程。我们首先为一组配置为 RAID 1（镜像）的 1TB 硬盘设置 Btrfs：

```
$ sudo mkfs.btrfs -L demo -d raid1 /dev/sdb /dev/sdc
```

- Label:
- UUID: 16384
- Sector size: 4096
- Filesystem size: 1.91TiB
- Block group profiles:
  - Data: RAID1 1.00GiB
  - Metadata: RAID1 1.00GiB
  - System: RAID1 8.00MiB
- SSD detected: no
- Incompat features: extref, skinny-metadata
- Number of devices: 2
- Devices: ID SIZE PATH
  - 1 978.00GiB `/dev/sdb`
  - 2 978.00GiB `/dev/sdc`

## Btrfs：“精简版 Zfs

```
$ sudo mkdir /mnt/demo
$ sudo mount LABEL=demo /mnt/demo
```

我们可以在挂载命令命令行指定任何组件设备，但最简单的方法是使用我们分配给组的标签“demo”。

`btrfs` 文件系统的使用情况显示了这些磁盘上空间当前的使用情况：

```
$ sudo btrfs filesystem usage /mnt/demo
```

- 总体：
  - 设备大小: 1.91TiB
  - 设备已分配: 4.02GiB
  - 设备未分配: 1.91TiB
  - 设备缺失: 0.00GiB
  - 已用: 1.25MiB
  - 空闲（估计）: 976.96MiB (最小: 976.96GiB)
  - 数据比例: 2.00
  - 元数据比例: 2.00
  - 全局预留: 16.00MiB (已用: 0.00GiB)
- 数据,RAID: Size:1.00GiB, Used:512.00KiB
  - `/dev/sdb`: 1.00GiB
  - `/dev/sdc`: 1.00GiB
- 元数据,RAID: Size:8.08MiB, Used:112.00KiB
  - `/dev/sdb`: 1.00GiB
  - `/dev/sdc`: 1.00GiB
- 系统,RAID: Size:8.00MiB, Used:16.00KiB
  - `/dev/sdb`: 8.00MiB
  - `/dev/sdc`: 8.00MiB
- 未分配:
  - `/dev/sdb`: 975.99GiB
  - `/dev/sdc`: 975.99GiB

这里值得注意的是，数据、元数据和系统块在 RAID 1 组中的初始分配非常小。磁盘空间保留在了一个没有内在结构的未分配池中。我们请求的镜像并不是强制应用于整个磁盘，而仅适用于活动正在使用的块。与其说这是一种僵化的结构，不如说这是在块组上实施的一项策略。

这种区别是理解 Btrfs 如何适应变化的需求和硬件配置的关键。当我们在新文件系统中存储一些文件并添加第三块磁盘时，会发生以下情况：

```
$ mkdir /mnt/demo/usr
$ cd /usr; tar cf - . | (cd /mnt/demo/usr; sudo tar xfp -)
$ sudo btrfs device add /dev/sdd /mnt/demo
```

## 第 20 章 存储

```
$ sudo btrfs filesystem usage /mnt/demo*4
总体:
<输出中省略>
数据,RAID1: Size:3.00GiB, Used:2.90GiB
/dev/sdb 3.00GiB
/dev/sdc 3.00GiB
元数据,RAID1: Size:1.00GiB, Used:148.94MiB
/dev/sdb 1.00GiB
/dev/sdc 1.00GiB
系统,RAID1: Size:8.00MiB, Used:16.00KiB
/dev/sdb 8.00MiB
/dev/sdc 8.00MiB
未分配:
/dev/sdb 973.99GiB
/dev/sdc 973.99GiB
/dev/sdd 978.00GiB
```

新磁盘 `/dev/sdb` 已变为存储池可用，但现有的块组保持原样，因此它们没有一个引用新磁盘。未来的分配将自动利用这块磁盘。如果我们愿意，可以转换 Btrfs 以在磁盘之间平衡数据：

```
$ btrfs balance start --full-balance /mnt/demo
未应用任何过滤器启动。
完成，已重定位 5 个 5 个块。
```

RAID 级别之间的转换也是一种平衡的形式。现在我们有三块磁盘可用，可以转换为 RAID 5：

```
$ btrfs balance start -convert=raid5 -mconvert=raid5 /mnt/demo
完成，已重定位 5 个 5 个块。
```

如果我们在转换期间查看了使用数据，将看到 RAID 1 和 RAID 5 的块组同时处于活动状态。删除磁盘的工作原理类似；Btrfs 会增量地将所有块复制到不包含离开磁盘的组，最终不会残留数据。

## 卷与子卷

快照和配额是 Btrfs 中的文件系统级实体，因此能够将文件树的部分定义为独立实体是有帮助的。Btrfs 将这些称为“子卷（subvolumes）”。子卷看起来非常像普通文件系统目录，事实上，它可以作为父卷的子目录被访问，如下：

```
$ btrfs subvolume create /mnt/demo/sub
创建子卷 '/mnt/demo/sub'
```

24. `btrfs` 命令可以缩写为任何前缀。

# 数据备份策略

即使受到勒索软件感染，尽管物理层保持完好无，你的数据也可能被更改或损坏。将受感染的数据自动复制到多个磁盘或站点只会加剧痛苦。你永远需要对关键数据进行不可变的时间点备份，以便在作为回退选项时还原。

在过去的几十年里，磁带等媒体是离线备份的流行方法。然而，这些媒体的容量证明无法赶硬盘和 SSD 呈指数增长的容量。除了运输和存储磁带的物理挑战以及维护娇贵的机械磁带驱动器的挑战外，容量问题最终使磁带媒体沦落到 35mm 胶卷的地位：它在技术上仍在市场上，但你不得不怀疑到底是谁在买这些东西。

今天，大多数云平台都允许你按照自动计划以快照的形式捕捉时间点备份。你需要为每个快照占用的存储空间支付月费，并设置保留策略。

无论你使用什么具体技术来实现备份，你都需要一个回答以下所有问题的计划。

## 总体策略：

- 需要备份的数据是什么？
- 将由什么系统或技术执行备份？
- 备份数据将存储在何处？
- 备份是否加密？如果是，加密密钥将存储在哪里？
- 随着时间的推移，存储的成本是多少？

## 时间线：
