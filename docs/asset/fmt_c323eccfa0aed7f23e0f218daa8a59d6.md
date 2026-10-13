
本节结束。

# 管理分存储

## 目标

分析构成存储栈的多个存储组件。

# 存储栈

RHEL 中的存储由多个层驱动程序、管理器和工具组成，这些工具成熟且功能丰富。管理存储需要熟悉栈组件，并意识到配置会影响引导过程、应用程序性能以及为特定应用提供所需存储的能力。

| | | | | File System |
|---|---|---|---|---|
| Virtual Device | Multipath | Partitions | RAID | LVM |
| SAS | | | | Database |
| FC | | | | Ceph OSD |
| iSCSI | | | | LVM VDO |
| NVMe | | | | |

图 6.2：存储栈

系统管理之前的章节涵盖了 XFS 文件系统、网络存储共享、分区和卷管理器。本节概述了从底部到部的 RHEL 存储栈并引入了每一层。

本节还涵盖了 Stratis，这是一个统一、配置和监控底层 RHEL 存储组件并从 CLI 或 RHEL Web 控制台提供自动化存储管理的守护进程。

# 块设备

块设备是存储栈的基础，提供稳定一致的设备协议，允许几乎任何设备透明地包含在 RHEL 配置中。大多数块设备通过 RHEL SCSI 驱动程序作为 SCSI 设备访问，包括 ATA 硬盘、固态设备和常用的总线适配器 (HBA)。RHEL 还包括 iSCSI、以太网光纤 (FCoE)、虚拟机驱动 `virtio`、串行存储 (SAS) 以及非易性内存 (NVMe)。

iSCSI 目标可以是网络中的物理设备或 iSCSI 配置逻辑卷。目标是 SCSI 协议总线通信中的终端，用于作为逻辑单元（LUN）访问存储。

以太网光纤（FCoE）通过以太网传输光纤帧。通常，数据中心具有针对其流量单独配置的 LAN 和存储区域网络（SAN）线路。通过 FCoE，两种流量可以合并到更大的融合以太网架构中。FCoE 的优势包括更低的硬件和能量成本。

# 多路径

路径是服务器与底层存储之间的连接。设备多路径（`dm-multipath`）是一个 RHEL 多路径工具，用于将冗余 I/O 路径配置为单一路径聚合逻辑卷。通过设备映射（dm）为连接到系统的每个 LUN 创建 `/dev/mapper/` 唯一块设备映射器而生成的设备。

当 iSCSI 和 FCoE 等存储使用网络线路时，通过网络绑定（bonding）可以增强存储多路径冗余。

## 分区

块设备可以进一步划分为分区。分区可能会消耗整个设备的大小或划分块设备以创建多个分区。这些分区可以创建文件系统、LVM 或直接用于原始存储。

## RAID

冗余磁盘阵列（RAID）是一种存储虚拟化技术，从多个物理或虚拟设备组件创建大型逻辑卷。不同形式的 RAID 提供数据冗余、性能改进，或通过实现镜像或条分来实现。

LVM 支持 RAID 0、1、4、5、6 和 10。由 LVM 创建和管理的 RAID 卷使用 `dmadm` 内核驱动程序。在不使用 LVM 的情况下，设备映射 RAID（`dm-raid`）为 dmadm 内核驱动程序提供设备映射接口。

## 第 6 章 | 管理存储栈

## 文件系统或其他用例

栈的顶层通常是文件系统，但也可以作为数据库或自定义数据需求的原始空间。RHEL 支持多种文件系统类型，但建议在大多数用例下使用 XFS。当实现 LVM 的工具是 Red Hat Ceph 或 Stratis 工具时，则需要 XFS。

数据库服务器根据其架构和大小以不同的方式消耗存储。某些较小的数据库将其结构存储在文件系统中的普通文件中，但受限于文件系统访问的开销或限制，这种架构具有扩展性局限性。较大的数据库则跳过文件系统，使用它们自己的缓存机制，在原始存储上创建其数据库结构。逻辑卷适用于数据库和原始存储用例。

Red Hat Ceph 也倾向于在原始设备上创建其自己的存储管理结构，用于创建 Ceph 节点存储设备 (OSD)。在最新版本的 Red Hat Ceph 中，它使用 LVM 初始化设备以用作 OSD。更多信息请参阅《Red Hat Ceph 的云存储 (CL260)》课程。

## Stratis 存储管理

Stratis 是由 Red Hat 和上游 Fedora 社区开发的一种本地管理工具。它使得执行初始存储配置、更改存储配置以及使用高级存储功能变得更加简单。

> > 重要：Stratis 目前作为技术预览（Technology Preview）提供，但预计将在后续的 RHEL 9 版本中获得支持。有关 Red Hat 技术预览功能的支持范围的信息，请参阅[技术功能支持范围](https://access.redhat.com/support/offerings/techpreview) 文档。

Red Hat 鼓励客户在部署 Stratis 时提供反馈。

Stratis 作为服务运行，管理存储设备池，并透明地为新创建的文件系统创建并管理卷。

Stratis 通过一种名为*置备*（provisioning）的概念，从共享设备池构建文件系统。Stratis 不会在当您使用数据时立即为文件系统分配物理空间，而是从池中为文件系统分配更多空间。因此，文件系统的看起来可能为 1 TB，但实际分配给它的真实空间可能多于 100 GiB。

你可以从不同的存储设备创建多个池。从每个池中，你可以创建一个或多个文件系统。目前，每个池最多可以创建 `$2^{24}$` 个文件系统。

Stratis 使用 Linux 内部组件构建 Stratis 管理的文件系统的组件。Stratis 使用 LVM 同样使用的 Device Mapper 基础设施。Stratis 使用 XFS 格式化文件系统。

6.3 展示了 Stratis 如何组装其存储管理解决方案的元素。Stratis 将存储设备作为硬盘或 SSD 分配给池，每个设备为池贡献一些物理存储，然后从池创建文件系统，并根据需要将存储映射到每个文件系统。

IH134-RHEL9.0-en-2-20220609

![](img/2eff90170b8c94cce3a908ab927e38c2_203_0.png)

## Stratatis 管理方法

要使用 Stratatis 存储管理解决方案管理文件系统，请安装 `stratis-cli` 和 `stratis` 包。`stratis-cli` 包提供了 `stratis` 命令，该命令向 stratis 守护进程发送重配置请求。Stratatis 提供 `stratis` 服务，该服务处理重配置请求并监控 Stratatis 的块设备、池和文件系统。

Stratatis 管理包含在 RHEL Web 控制台中。

> > 警告
使用 Stratatis 工具和命令重配置由 Stratatis 创建的文件系统。
Stratatis 使用存储的元数据来识别受管理的池、卷和文件系统。使用非 Stratatis 命令手动配置 Stratatis 文件系统可能会覆盖这些元数据，并防止 Stratatis 识别其之前创建的文件系统卷。

## 安装并启用 Stratatis

要使用 Stratatis，请确保您的系统已安装所需的软件且 stratis 服务正在运行。安装 `stratis-cli` 和 `stratis` 包，并启动且启用 stratis 服务。

```
[root]# dnf install stratis-cli stratis

...output omitted...

Is this ok [Y/n]: y

...output omitted...

Complete!

[root]# systemctl enable --now stratis
```

## 创建 Stratatis 池

使用 `stratis pool create` 命令创建一个或多个块设备的池。使用 `stratis pool list` 命令查看可用池的列表。

186 RH14-RHEL9.0-en-20220609

```
[root@host ~]# stratis create pool pool1 /dev/vdb

[root@host ~]# stratis create pool list
```
