

如果只有一个集群连接到存储子系统，则无需禁用然后重新启用到存储的访问路径。禁用访问路径然后有选择地为某些主机连接启用访问路径是选择性存储呈现的一个示例。创建任何存储单元时的默认标志设置是 enable_access_path=all 或为所有主机连接启用访问。

## 4.2.4.4 为集群系统盘构建 RAID 1 阵列

在上一节中，我们构建了支持集群系统盘所需的所有存储单元；在本节中，我们将只构建其中大部分存储单元。由于我们使用的是 eager swap 分配，我们建议您为交换分区分配三倍于内存大小的空间。我们假设每个集群成员的主交换分区将在其他驱动器上。⁸ 在配置这些存储单元时预留的交换空间与每个集群成员的内存大小相同，最终可能用作每个集群成员的次要交换分区。

使用 RAID 1 用于集群的系统盘为集群的可用性提供了坚实的基础。虽然在 RAID 1 中的磁盘驱动器发生故障时，其写入性能不是最佳的，但您可以合理地确信您的数据是安全的。

与我们构建 RAID 5 阵列的示例类似，我们将使用 18 GB 驱动器——两个 18 GB 驱动器——在此构建集群系统盘的 RAID 1 阵列的示例中。

- 创建并初始化 RAID 1 或镜像集。

```
MSG> add mirrorset m0 disk10100 disk20100
```

```
MSG> initialize m0 save_configuration
```

请务必使用 save_configuration 标志以在镜像集上保留 RAID 配置信息。

- 对 RAID 1 或镜像集进行分区。

分区的方式与之前使用 RAID 5 阵列的示例中完全相同。唯一的区别是分区大小不同。与 RAID 5 阵列的有效存储利用空间为 36 GB 不同，我们的有效存储利用空间只有 18 GB。由于大小是可用空间的百分比，因此在可用空间不同且尤其是我们没有考虑所有交换空间的情况下，百分比不同是有意义的。

> 8 请参阅第 21 章关于在本地磁盘上配置交换。

```
HSG> create_partition m0 size=12
HSG> create_partition m0 size=12
HSG> create_partition m0 size=12
HSG> create_partition m0 size=12
HSG> create_partition m0 size=1
HSG> create_partition m0 size=largest
```

- 创建分区存储单元。

```
HSG> add unit d11 m0 partition=1 disable_access_path=all
HSG> add unit d12 m0 partition=2 disable_access_path=all
HSG> add unit d13 m0 partition=3 disable_access_path=all
HSG> add unit d14 m0 partition=4 disable_access_path=all
HSG> add unit d15 m0 partition=5 disable_access_path=all
HSG> add unit d16 m0 partition=6 disable_access_path=all
```

- 配置分区存储单元。

```
HSG> set d11 identifier=11 enable_access_path=(MOLRIA1,MOLRI82,SHERIA1,SHERI82)
HSG> set d12 identifier=12 enable_access_path=(MOLRIA1,MOLRI82,SHERIA1,SHERI82)
HSG> set d13 identifier=13 enable_access_path=(MOLRIA1,MOLRI82,SHERIA1,SHERI82)
HSG> set d14 identifier=14 enable_access_path=(MOLRIA1,MOLRI82,SHERIA1,SHERI82)
HSG> set d15 identifier=15 enable_access_path=(MOLRIA1,MOLRI82,SHERIA1,SHERI82)
HSG> set d16 identifier=16 enable_access_path=(MOLRIA1,MOLRI82,SHERIA1,SHERI82)
```

前两个要点与 RAID 5 示例中的完全相同。

## 4.2.4.5 为集群系统盘构建 RAID 0+1 阵列

在本节中，我们将使用条带镜像集（又名 RAID 0+1 阵列）构建支持集群系统盘所需的所有存储单元。RAID 级别 0+1 提供了最高可用性和最大性能，但代价也高。

与我们的 RAID 5 示例一样，最小的 RAID 0+1 阵列实际上非常大。它足够大，可以支持我们集群系统盘的所有空间需求——包括我们的大型交换空间建议。

再次与我们构建 RAID 5 阵列的示例一样，我们将使用四个 18 GB 驱动器来构建我们的 RAID 0+1 阵列，以支持我们集群系统盘的存储需求。

- 创建并初始化 RAID 0+1（条带镜像）集。

- 首先，我们创建我们需要的全部镜像集。

```
HSG> add mirror m1 disk10200 disk20200
HSG> add mirror m2 disk10300 disk20300
```

