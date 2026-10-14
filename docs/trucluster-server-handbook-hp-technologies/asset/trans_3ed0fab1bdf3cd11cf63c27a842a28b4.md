

最佳性能。如果成本是问题，并且你希望有一个坚实的基础来构建你的集群，我们建议对系统磁盘使用 RAID 1，对所有用户文件系统使用 RAID 5。

结论：选择使用哪种 RAID 级别是因地制宜的。我们能在这里做的就是为集群系统磁盘在不同 RAID 级别下的各种实现提供思路。

## 4.2.4.2 规划未来集群扩展

在规划你的集群时，不仅要规划集群的即将实施，还要规划其未来的扩展。如果为集群的未来扩展做好规划，那么增加集群成员的数量就变得简单直接，并且每增加一个集群节点不应超过 45 分钟。

好吧，这与构建 RAID 套件有什么关系，还是作者有点“疯了”？正如他们所说，我们的疯狂是有方法的。接下来关于为集群系统磁盘构建 RAID 套件的部分将包括为六个月或一年后可能添加的集群节点构建额外的存储空间。提前构建所有存储单元是明智的。

## 4.2.4.3 为集群系统磁盘构建 RAID 5 套件

在本节中，我们将使用 RAID 5 套件构建支持集群系统磁盘所需的所有存储单元。RAID 5 以最佳的每字节存储成本提供最佳的可用性。

由于磁盘驱动器往往非常大，任何 RAID 套件通常都非常大。对于最小的 RAID 5 套件尤其如此。一般来说，除了交换空间的需求外，支持集群系统磁盘所需的空间相对较小。虽然一些系统管理员会说这是一个好问题，但其他人会为浪费宝贵的磁盘空间而皱眉。

在我们构建 RAID 5 套件用于集群系统磁盘的示例中，我们将使用 18 GB 驱动器——三个 18 GB 驱动器。

- 创建并初始化 RAID 5 套件。
  - 如你所见，构建一个三磁盘 RAID 5 套件是一个相对简单的操作。

```
HSG> add raidset r0 disk10000 disk20000 disk30000
```

```
HSG> initialize r0 save_configuration
```

在 RAID 套件创建并初始化后，RAID 配置实际上使用 save_configuration 标志保存到 RAID 套件中。将 RAID 配置信息保存到控制器上的 RAID 套件非常重要，这样如果遇到灾难性故障并且两个存储控制器同时丢失，我们可以轻松恢复所有 RAID 套件而不会丢失任何数据。这是如何完成的？在更换故障存储控制器后，必须从最初保存它的 RAID 套件中读取恢复的已保存 RAID 配置信息。

- **分区 RAID 5 套件。**

下一步对 RAID 5 套件进行分区需要规划。在这里，我们使用表 4-5 中的信息来确定每个分区将占 RAID 5 套件有效存储利用空间的百分比。由于三驱动器（每个为 18 GB 驱动器）RAID 5 套件的有效存储利用空间约为 36 GB，每个分区大小是该数字的百分比。

```
HSG> create_partition r0 size=14
HSG> create_partition r0 size=14
HSG> create_partition r0 size=14
HSG> create_partition r0 size=14
HSG> create_partition r0 size=14
HSG> create_partition r0 size=largest
```

在此示例中，第一个分区创建的分区大小为 36 GB 的 14%。size=largest 允许我们在不设置百分比的情况下利用驱动器上所有剩余空间。

- **创建分区存储单元。**

现在 RAID 5 套件已分区，每个新的存储单元从每个存储分区创建。这些存储单元呈现给主机——集群成员。

```
HSG> add unit d1 r0 partition=1 disable_access_path=all
HSG> add unit d2 r0 partition=2 disable_access_path=all
HSG> add unit d3 r0 partition=3 disable_access_path=all
HSG> add unit d4 r0 partition=4 disable_access_path=all
HSG> add unit d5 r0 partition=5 disable_access_path=all
HSG> add unit d6 r0 partition=6 disable_access_path=all
```

> **IMPORTANT:**
>
> 当每个新的存储单元创建时，我们禁用对所有主机的访问路径。这可以防止连接到存储子系统的主机意外访问。

- **配置分区存储单元。**

在此最后一步中，我们为每个新存储单元设置标识符，并有选择地启用访问路径以仅允许每个集群节点的主机连接。

```
HSG> set d1 identifier=1 enable_access_path=(MOLR1A1,MOLR1B2,SHER1A1,SHER1B2)
HSG> set d2 identifier=2 enable_access_path=(MOLR1A1,MOLR1B2,SHER1A1,SHER1B2)
HSG> set d3 identifier=3 enable_access_path=(MOLR1A1,MOLR1B2,SHER1A1,SHER1B2)
HSG> set d4 identifier=4 enable_access_path=(MOLR1A1,MOLR1B2,SHER1A1,SHER1B2)
HSG> set d5 identifier=5 enable_access_path=(MOLR1A1,MOLR1B2,SHER1A1,SHER1B2)
HSG> set d6 identifier=6 enable_access_path=(MOLR1A1,MOLR1B2,SHER1A1,SHER1B2)
```

