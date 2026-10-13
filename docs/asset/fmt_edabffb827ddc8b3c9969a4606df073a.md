
使用 LVM 有若干种重要的方式可以提高生产服务器的可靠性，包括：

使用 LVM 允许你定制分配给文件系统或其他数据对象的空间量，使得分配的空间与实际空间紧密匹配。这导致了磁盘空间预算的一种从根本上不同的方式。因为 LVM 可以动态分配存储，因此没有必要预测未来需要多少存储空间。相反，你可以为文件系统分配足够的存储以满足其当前需求，然后随着文件系统的需要动态增加。你会倾向于将任何未真正需要的空间保留在未分配池中，以便在需要时在需要的地方将其重定向。如果未分配空间不足，可以动态地向池中添加更多存储。因此，你不太可能遇到这种情况：由于文件系统已满，且需要为耗时且风险较高的磁盘重新分区和数据调整工作而安排停机时间（这在固定空间分配系统中是常见的）。

使用 LVM 消除了管理员采用从一个文件系统指向另一个文件系统的符号链接作为临时解决方案的诱惑。使用链接从一个文件系统指向另一个是有效扩展目录结构可用存储的一种简单但粗浅的方法。它消除了涉及重构固定空间分配磁盘系统时的开销，这使其具有吸引力。然而，它也会导致数据结构复杂化，并且仍然受到连续分区所隐含的限制。所有这些导致了额外的管理复杂性，而没有提高可靠性。

LVM 使用的数据结构使得 PV 和 VG 成为包含的数据实体，携带了 VG 内部正常运行所需的所有元数据。这使得 VG 成为一个完全可移植的数据实体，其功能不依赖于存储在主机服务器操作系统上的任何数据。这意味着整个应用程序及其数据很容易地从一台服务器移动到另一台服务器。如果服务器故障，这将是一个明显的优势，并为第 10 节讨论的高可用性服务器集群中在主服务器和备份服务器之间共享磁盘奠定了必要的基础。

# 逻辑卷管理 309

Linux LVM 提供了一个名为 LV 快照（snapshots）非常有用的功能。快照允许 LV 中的数据在某一时刻被冻结，并以只读模式供备份，而生产 LV 仍保持可读写的生产活动状态。你将在本章稍后的部分看到它是如何工作的。

Linux LVM 代码与软件 RAID 驱动完全兼容。创建一个作为 `/dev/md0` 的 RAID 设备并将其作为 LVM VG 中的 PV 是完全可能的——甚至是理想的。因此，LVM 的灵活存储管理优势可以与 RAID 的可靠性相结合，产生一个可靠、灵活、可管理且可扩展的存储管理系统。

LVM 在磁盘管理方面极大地提高了灵活性，使管理员能够更容易做好存储管理工作，这不可避免地在服务器的稳定性和可靠性上获得了回报。我有荣幸在一个一直青睐 LVM 的商业 UNIX 环境中工作，在引入 LVM 之前，一直觉得它的缺失是成为实用且有效的生产系统的主要障碍之一。一旦你习惯了它，就再也回不去了！

# 与 Linux LVM 一工作

接下来的几页提供了 LVM 命令的一些实际示例。请注意，这些示例是使用 v0.9 beta（LVM 的一个预发布版本）完成的。你的版本可能更新且有所不同，某些命令的外观或行为可能与这些示例不同。请务必检查你的发行版提供的信息以及 LVM 命令的相应帮助页（man pages）。通过查看 `/proc/lvm` 是否存在来测试你的内核。如果该目录存在，说明你具有基本的 LVM 支持。你可以通过检查文件 `/proc/lvm/global` 来确定 LVM 版本以及任何 LVM 对象的当前状态。注意，Red Hat 7 发行版不包含 LVM 支持，也不包含必要的工具。你需要编译一个支持 LVM 的内核。

### 构建逻辑结构

本节将介绍构建示例中所示结构所需的命令。记住创建 LV 本身是该过程的最后阶段这一理论，我们必须做的第一件事是创建一些 PV。

### 创建物理卷

`pvcreate` 命令从磁盘分区创建一个 PV。参考图 8.3，创建必要的 PV 的命令为：

```
# pvcreate /dev/sda1 /dev/sda2 /dev/sdb1 /dev/sdb2 /dev/sdc1 /dev/sdd1
pvcreate -- physical volume "/sda1" successfully created
pvcreate -- physical volume "/sda2" successfully created
pvcreate -- physical volume "/sdb1" successfully created
pvcreate -- physical volume "/sdb2" successfully created
pvcreate -- physical volume "/sdc1" successfully created
pvcreate -- physical volume "/sdd1" successfully created
```

此命令在 PV 的开头创建了一个名为卷描述符区域（VGDA）的数据结构。这是 LVM 的核心数据实体。它是每个 VG 的每个 PV 上持有的 VGDA 的冗余副本。VGDA 完全描述了整个 VG 结构。可以使用 `pvdata` 命令从 PV 读取 VGDA：

```
# pvdata -a /dev/sda
--- NEW Physical volume
PV Name /dev/sda
VG Name
PV Size 104.03 MB
PV# 0
PV Status NOT available
Allocable NO
Cur LV 0
PE Size (KByte) 0
Total PE 0
Free PE 0
Allocated PE 0
PV UUID VGq-nkGs-YW3F-vvTq-QC0H-DBS1-dIO0M
```

--- Volume group

VG Name

VG read

VG Status NOT available/NOT resizable

VG # 0

# 逻辑卷管理 311

| 字段 | 值 |

| :--- | :--- |

| MAX LV | 0 |

| Cur LV | 0 |

| Open LV | 0 |

| MAX LV Size | 0 |

| Max PV | 0 |

| Cur PV | 0 |

| Act PV | 0 |

| VG Size | 0 |

| PE Size | 0 |

| Total PE | 0 |

| Alloc PE / Size | 0 / 0 |

| Free PE / Size | 0 / 0 |

| VG UUID | HM |

- 逻辑卷列表

- 物理区列表

- 物理卷 UUID 列表

注意，尽管这个 VGDA 是从一个 PV 读取的，但它不仅包含了 PV 本身的信息（输出的第一部分），还包含了该 PV 所属的整个 VG 的信息。VG 中的每个 PV 都是如此。这对于可靠性是有好处的，因为如果 VG 丢失 PV，LVM 仍然拥有使用 VG 所需的信息（至少是故障 PV 丢失后幸存的 VG 部分）。这意味着 PV 本身携带了使用整个 VG 所需的所有数据。这使得 VG 成为一个可移植的数据结构。从泰坦尼克原则（如第 4 节“为了可靠性进行安装和配置”所述）来看，这是很好的，因为这意味着你可以从故障服务器上移除 VG 并将其插入到备份机器中，从 VG 中的任何 PV 读取 VGDA 信息，并能够在新家中使用整个 VG。注意，每个 PV 都分配了一个全局唯一标识符（UUID）；你可以在 VGDA 输出中看到它。这是一个通过算法生成的数字，旨在不重复标识符，并用于与其他任何其他 PV 区分开来。如果要在服务器之间迁移 VG，这将是必要的，因为在一台服务器上是 `/dev/sdb` 的磁盘在另一台服务器上可能是 `/dev/sdg`，取决于磁盘在第二台服务器上配置 SCSI 地址和控制器。像 `/dev/sda1` 这样的标识符在机器间传输 VG 时是不可靠的，但 UUID 是的。这种数据可移植性可以成为高可用服务器数据集群的关键组件。

由于 VGDA 是 LVM 的关键数据结构，任何操作它的的命令都会自动对 VGDA 进行备份。

位于 `/etc/vgconf` 目录下的 VGDA 数据文件。可以使用 `vgcf-restore` 命令将这些任何 VGDA 备份恢复到损坏的磁盘上。务必将这些 VGDA 备份包含在你的备份轮中。

## 创建卷组 (Volume Groups)

现在我们有了一些 PV，下一步工作是将它们合并为 VG。请记住，在定义 LV 之前，你必须先定义它将所属的 VG。我们需要使用 `vgcreate` 命令为示例创建两个 VG：
