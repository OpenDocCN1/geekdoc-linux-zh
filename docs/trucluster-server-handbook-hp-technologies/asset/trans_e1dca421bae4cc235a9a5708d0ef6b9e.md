

```
`disklabel -r dsk5 | grep -p "8 part" | awk '{ printf("%2s %10s %10s %10s\n", $1,$2,$3,$4) }' | tail -10`
```

![](img/a0df85c2e542a8d6c913113908553aa4_357_0.png)

LSMpub
LSM 公共数据
磁盘的剩余部分
这是“g”分区

LSMpriv
LSM 私有数据
4096 块
这是“h”分区

LSMsimp
同一分区上的 LSM 公共和私有数据
私有数据位于分区的开头

LSMnoprv
仅 LSM 公共数据
无私有数据
这是一个分区或磁盘，其中已有数据

图 14-4：LSM 磁盘类型

![](img/a0df85c2e542a8d6c913113908553aa4_357_1.png)

concatvol
（1024 块）

stripevol
（1024 块）

concatvol-01
（1024 块）
块 0-499 dsk1-01
块 500-1023 dsk2-01

stripevol-01
（1024 块 – 条带宽度 64K）
块 0-127、256-383、512-639、… dsk1-01
块 128-255、384-511、640-767、… dsk2-01

图 14-5：LSM 串联和条带化 Plex

日志 plex 可以是：
- 脏区域日志（DRL）plex。
- RAID5 日志 plex。

日志 plex 用于跟踪镜像或 RAID5 卷上的写入活动，并在系统故障后用于恢复卷的完整性。有关更多信息，请参阅《Logical Storage Manager Guide》。

## NOTE：

截至本文撰写时，集群中不支持 RAID5 plex。

## 14.1.1.4 Volume

卷由一个或多个 plex 组成。如果卷内有多个数据 plex，则为镜像卷（即写入卷的数据会在每个数据 plex 上重复）。由两个或多个串联数据 plex 组成的镜像卷是 RAID1 风格的卷，而由两个或多个条带化数据 plex 组成的镜像卷是 RAID0+1 风格的卷。卷是操作系统使用的逻辑设备，就像物理磁盘或分区一样。卷可通过位于 /dev/rvol 子目录中的卷字符设备特殊文件用作原始设备。您也可以在卷上创建文件系统，该文件系统将使用位于 /dev/vol 子目录中的卷块设备特殊文件。

## 14.2 Why Do I Need LSM?

由于 LSM 是软件 RAID 实现，因此它是基于硬件的 RAID 的低成本替代方案。虽然 LSM 有一些限制，阻止您实现完整的无单点故障（NSPOF）解决方案，如我们在下一节中将讨论的那样，但它仍然可以在最重要的地方为您提供所需的冗余：您的数据和集群公共文件系统。此外，如果您从之前的 TruCluster 配置（V1.5 或 V1.6）迁移而来，并且它是一个 NSPOF 集群，那么您正在使用 LSM（这是实现 NSPOF 解决方案的唯一方法，因为直到 Tru64 UNIX 版本 5.0 才支持到存储设备的多路径）。

LSM 继续得到支持这一事实为您提供了实现冗余的另一种选择。结合基于 LAN 的集群互连，您可以组建一个低成本、冗余且功能强大的集群。从 TruCluster Server 版本 5.1A 开始，您可以使用 LSM 镜像 cluster_root、cluster_usr、cluster_var、swap 分区，当然还有您的数据。这意味着您现在拥有了一种低成本的集群解决方案。在 V5.1A 之前，cluster_root 和 swap 不能纳入 LSM。

法定磁盘的目的是为了提供额外的冗余，它本身并不是单点故障（SPOF）。并且一个成员的引导磁盘丢失也不会导致集群范围内的故障，因此它也不是 SPOF。此外，更换法定磁盘或成员的引导磁盘并不是一个非常困难或耗时的过程（我们将在第 22 章中介绍该过程）。

如果您已在当前 V5.0A 之前的集群上使用 LSM，那么迁移您在 LSM 卷上的任何数据都可以用最少的停机时间完成。

## NOTE：

为了启用许多高级 LSM 功能（镜像、条带化等），您需要安装 LSM-OA 许可证产品授权密钥（PAK）。这是一个额外付费的许可证，因此除非您已拥有它，否则您需要联系 Compaq 或经销商获取它。

## 14.3 CLSM Rules of the Road

现在您对 LSM 有了一些了解，让我们讨论在 TruCluster Server 环境中您可以使用 LSM 做什么以及不能做什么。我们将本节分为三个部分：

|  | Section |
|---|---:|
| 常见 CLSM 注释、规则和限制 | 14.3.1 |
| 集群公共文件系统规则和限制 | 14.3.2 |
| 成员引导磁盘规则和限制 | 14.3.3 |

## 14.3.1 Common CLSM Notes, Rules, and Restrictions

以下规则和限制适用于 CLSM：
- 集群中不支持 RAID5 LSM 卷。
- `volstat(8)` 命令返回的统计信息仅适用于运行该命令的成员。截至本文撰写时，没有集群范围的 `volstat` 命令。
- 使用“list”开关的 `voldisk(8)` 命令返回的输出在与 LSM 控制无关的设备方面可能在成员之间不一致。

```
                  [local]
# voldisk list

DEVICE      TYPE      DISK      GROUP       STATUS
dsk0        sliced    -         -           unknown
dsk1        sliced    -         -           unknown
dsk2        sliced    -         -           unknown
dsk3        sliced    -         -           unknown
dsk4        sliced    -         -           unknown
dsk5h       simple    dsk5h     rootdg      online
dsk6        sliced    -         -           unknown
```

