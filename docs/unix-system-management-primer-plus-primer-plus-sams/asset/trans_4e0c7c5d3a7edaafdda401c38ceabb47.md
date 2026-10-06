

# 图 10.10
RAID-5 通过在多个磁盘上跨盘分列校验数据来提高更好的性能。

| 1011 | 1001 | 0010 |
|---|---|---|
| 0001 | 1110 | 1111 |
| 0000 | 0101 | 0101 |
| 1110 | 0011 | 1101 |
| 磁盘 1 (数据与校验) | 磁盘 2 (数据与校验) | 磁盘 3 (数据与校验) |

# 选择 RAID 级别

RAID 0、1、4 和 5 是目前领域中最常见的 RAID 形式。起初，决定哪种级别适用于你的应用可能会令人困惑。表 10.2 总结了每个 RAID 种级的优缺点，可以帮助你做出正确的决定。

| RAID 级别 | 优点 | 缺点 |
|---|---|---|
| 0 | I/O 快速 | 无冗余 |
| 1 | 易于增加冗余，可以在磁盘间进行轮询读取 | 容量/成本率最高 |
| 4 | 容量/成本低，读取性能高 | 写入性能极差 |
| 5 | 容量/成本低，读取性能高 | 写入性能差，重建时间慢 |

# 硬件 RAID 与 软件 RAID

RAID 既可以通过硬件也可以通过软件实现。硬件 RAID 设备是内置 RAID 功能的磁盘阵列；除了配置阵列本身外，不需要其他任何设备。软件 RAID 通常通过操作系统设备驱动实现，可以使用不具备任何原生 RAID 功能的普通驱动器。

硬件 RAID 是一种优化配置，因为所有的计算和磁盘操作都在专用硬件中调解，因此非常快。你可以通过移动阵列轻松地将 RAID 功能转移到新主机。RAID 阵列可能非常贵，但在 CPU 可能成为瓶颈的大型部署中是物值的。这对于 RAID-5 特别重要，因为校验计算的开销会对服务器 CPU 带来巨大负载。某些服务器甚至自带内部硬件控制器，尽管你主要在 Dell 和 Compaq 等供应商的 Intel 软件包中看到它。

软件 RAID 天生比硬件 RAID 慢，因为主机 CPU 必须执行所有计算。然而，软件 RAID 极其灵活；它可以使用内部硬盘、外部磁盘阵列和任何其他 RAID 设备来形成自己的 RAID 分区。软件 RAID 也是一种极具成本效益的解决方案，因为它不需要购买或安装额外的驱动器。大多数 Unix 操作系统都带有某种形式的软件 RAID 功能，使其成为一种方便的替代方案。表 10.3 总结了几种 Unix 操作系统上的软件解决方案。

# 表 10.3 各种 Unix 操作系统上的软件 RAID 选项

| 操作系统 | 可用的软件 RAID 解决方案 |
|---|---|
| Solaris | Sun Solstice DiskSuite (在 Solaris 9 中称为 Solaris Logical Volume Manager), Veritas Volume Manager |
| AIX | AIX Logical Volume Manager (LVM) |
| Linux | Linux Software RAID, Linux Veritas Volume Manager (Red Hat) |

# 代表性的 RAID 解决方案：Solstice DiskSuite

Solstice DiskSuite 是一个用于 Solaris 的软件包，提供了你在本章中学习到的大部分 RAID 功能。它同时提供命令行界面和图形界面，GUI 的功能与命令行一样强大，因此你可以使用任何你更熟悉的界面。

DiskSuite 使用元磁盘（metadrives），元磁盘是像像物理磁盘一样使用的虚拟磁盘。DiskSuite 使用这些元磁盘来抽象实际物理存储配置：元磁盘可以代表整个物理磁盘、单个切片（Sun 对分区的命名）以及由这些磁盘和切片构建的 RAID 设备。许多软件实现都使用虚拟磁盘。

DiskSuite 的独特之处在于它可以与切片或分区一起工作，而不是额外的磁盘。这意味着你可以镜像磁盘上的一个文件系统，但不镜像其他系统。例如，你可以使用两个物理磁盘上的两个切片，通过创建两个元磁盘（每个切片一个）来创建一个镜像设备，如下所示：

```
# maintain d11 1 1 c0t00s0
d11: Concat/Stripe is setup
# maintain d12 1 1 c0tid0s0
d12: Concat/Stripe is setup
```

这段代码产生两个子镜像元磁盘 d11 和 d12，它们可被用于创建一个镜像 d10。首先使用 d11 创建镜像，然后附加 d12，触发镜像的初始同步：

# 第 10 章 • 在你的 UNIX 系统中提供高可用性

```
# maintainit d10 -m d11
d10: Mirror is setup
# metattach d10 d12
d10: Submirror d12 is attached
```

同步完成后，你可以使用 `metat` 命令检查镜像状态：

```
# metastat d10
d10: Mirror
Submirror 0: d11
State: Okay
Submirror 1: d12
State: Okay
Pass: 1
Read option: roundrobin (default)
Write option: parallel (default)
Size: 1027216 blocks
```

```
d11: Submirror of d10
State: Okay
Size: 1027216 blocks
Stripe 0:
| Device | Start Block | Dbase State | Hot Spare |
| c0tid0s0 | 0 | | |
```

```
d12: Submirror of d10
State: Okay
Size: 1027216 blocks
Stripe 0:
| Device | Start Block | Dbase State | Hot Spare |
| c0tid0s0 | 0 | | |
```

