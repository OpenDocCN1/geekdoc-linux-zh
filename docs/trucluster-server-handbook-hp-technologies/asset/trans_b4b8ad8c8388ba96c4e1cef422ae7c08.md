

从我们的示例中可以看到，我们的两块局域网卡（设备 alt0 和 alt1）以 1000 Mb/sec 的速率运行，并且为全双工。

使用局域网互连的集群需要以下信息：

- 每个集群成员的虚拟集群互连设备的 IP 名称和 IP 地址。
- `clu_create` 和 `clu_add_member` 程序默认提供 `10.0.0.0` 子网上的 IP 地址用于虚拟集群互连。IP 地址的主机部分设置为正在配置的集群成员的 memberid，IP 名称为成员主机名的简写后跟“-ics0”。同样，与 Memory Channel 配置一样，虚拟集群互连的 IP 地址和 IP 名称不应在 DNS 中。
- 对于每个集群成员的物理局域网接口，需要在与虚拟集群互连不同的子网上提供 IP 名称和地址。
- 集群创建程序也为物理局域网接口提供了默认值。默认情况下，提供 `10.1.0.0` 子网上的 IP 地址，IP 地址的主机部分设置为正在配置的集群成员的 memberid，并附加“member”加上成员 ID 和“-icstcp0”。物理局域网接口的 IP 地址和 IP 名称不应在 DNS 中。

以下示例提供了在局域网互连上运行的 clue 集群的两个成员 mustard 和 plum 的集群互连 IP 名称和地址。此信息也包含在集群的 `/etc/hosts` 文件中。

```
##
# member1's cluster interconnect
#

10.0.0.1 mustard-ics0       # virtual interface IP name and address
10.1.0.1 member1-icstcp0     # physical interface IP name and address

#
# member2's cluster interconnect
#

10.0.0.2 plum-ics0           # virtual interface IP name and address
10.1.0.2 member2-icstcp0     # physical interface IP name and address
```

正如我们在 Memory Channel 互连部分所述，您应提前确定不仅是集群的名称和集群的 IP 地址，而且还应确定每个集群互连的 IP 名称和 IP 地址——虚拟和物理。参见第 4.8 节中的 Tru64 UNIX/TruCluster Server 规划工作表。

## 4.4.3 为什么使用一种互连而不是另一种？

我们有机会研究了 Memory Channel 互连和以太网局域网互连。我们讨论了每种互连的硬件要求、配置以及创建集群所需获取的互连信息。

为什么使用一种互连而不是另一种？遗憾的是，我们无法令人满意地回答这个问题，因为，嗯，这取决于。它取决于将在集群上运行哪些应用程序，集群上有多少用户，存储将如何使用，以及集群的用途是什么。它取决于许多变量，但归结为一点——用于部署集群规划的用户需求。

为了帮助您选择使用哪种互连，我们提供了以下表格 - 表 4-8。该表格比较了 Memory Channel 与 LAN 互连。

| Memory Channel | LAN Interconnect |
|---|---|
| 成本较高
- 高带宽（100MB/s）。
- 低延迟（~3µs）。 | 通常成本较低
- 中等带宽，100 Mb/s 时延迟中等至高。
- 高带宽，1000 Mb/s 时延迟中等至高。 |
| 最多支持八个成员，这受限于 Memory Channel 集线器的容量。 | 初始版本最多支持八个成员；不过，未来可能支持更多成员。 |
| 使用铜缆时成员之间支持的距离最长为 20 米（65.6 英尺），使用光纤电缆在虚拟集线器模式下最长可达 2000 米（1.2 英里），使用物理集线器的光纤电缆最长可达 6000 米（3.7 英里）。 | 成员之间使用 LAN 互连硬件支持的距离由网络段的长度以及
- 最大快速以太网距离为 ~4Km。
- 最大千兆以太网距离为 ~1.6Km（SPOF）或 ~1Km（NetRAIN）。 的能力和允许的选项决定。 |
| 支持使用 Memory Channel 应用程序编程接口（API）库。 | 不支持 Memory Channel API 库。 |
| 双轨冗余 Memory Channel 配置可提供互模通信冗余。 | 通过将多个网络适配器配置为独立网络适配器冗余阵列（NetRAIN）来实现互模通信冗余。每个成员上的虚拟接口通过在多个交换机之间分配其连接来实现。* |
| * - 如需更具体的信息，请查阅有关 NetRAIN 的章节以及 TruCluster Server 集群 LAN 互连指南。 |

## 表 4-8：Memory Channel 与 LAN 互连

