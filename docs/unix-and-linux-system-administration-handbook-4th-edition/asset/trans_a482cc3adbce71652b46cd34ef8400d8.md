

“广播域”是指接收发往硬件广播地址的数据包的主机集合。每个逻辑以太网段定义了恰好一个广播域。在早期的以太网标准和介质（例如，10Base5）下，物理段和逻辑段完全相同，因为所有数据包都在一根大电缆上传输，主机接口被连接到电缆的侧面。

随着交换机的出现，如今的逻辑段通常由许多（可能数十或数百个）物理段（或在某些情况下，无线段）组成，每个段上仅连接了两个设备：交换机端口和主机。交换机负责将多播和单播数据包护送到预期接收方所在的物理（或无线）段。广播流量会被转发到逻辑段中的所有端口。

单个逻辑段可以由以不同速度运行的物理（或无线）段组成（10 Mb/s、100 Mb/s、1 Gb/s 或 10 Gb/s）。因此，交换机必须具有缓冲和定时能力，使其能够平滑任何潜在的定时冲突。

## 非屏蔽双绞线布线

非屏蔽双绞线（UTP）是以太网的首选电缆介质。它基于星型拓扑，并具有相对于其他介质的若干优点：

- 它使用价格低廉、 readily available 的铜线。（有时，可以使用现有的建筑布线。）
- UTP 线比同轴电缆或光纤更容易安装和调试。定制长度很容易制作。
- UTP 使用 RJ-45 连接器，它们便宜、可靠且易于安装。
- 每个机器的链路是独立的（并且是私有的！），因此一条链路上的布线问题不太可能影响网络上的主机。

UTP 网络的总体“形状”在展品 A 中示出。

适用于现代局域网的 UTP 线通常被细分为八个等级。性能评级系统最初由大型电缆供应商 Anixter 引入。这些标准由电信工业协会（TIA）正式化，今天被称为 Category 1 至 Category 7，并加入了一些特殊变体，如 Category 5e 和 Category 6a 以锦上添花。

国际标准化组织（ISO）也加入了令人兴奋且利润丰厚的电缆分类世界。他们推广的标准与较高编号的

### Exhibit A A UTP installation

![](img/14d78e3cecac4581d37024baf1e94cca_583_0.png)

TIA 类别完全或近似等效。例如，TIA Category 5 电缆相当于 ISO Class D 电缆。对于听众中的极客们，Table 16.2 说明了各种现代分类之间的主要差异。这是一个值得记住的好信息，以便你在聚会上给朋友留下深刻印象。

### Table 16.2 UTP cable characteristics

| Parameter¹ | Units | Cat 5 Class Dᵇ | Cat 5e Class E | Cat 6 Class E | Cat 6a Class EA | Cat 7 Class F | Cat 7a Class FA |
|---|---|---|---|---|---|---|---|
| Frequency range | MHz | 100 | 100 | 250 | 500 | 600 | 1000 |
| Attenuation | dB | 24 | 24 | 21.7 | 18.4 | 20.8 | 60 |
| NEXT | dB | 27.1 | 30.1 | 39.9 | 59 | 62.1 | 60.4 |
| ELFEXT | dB | 17 | 17.4 | 23.2 | 43.1 | 46.0 | 35.1 |
| Return loss | dB | 8 | 10 | 12 | 32 | 14.1 | 61.93 |
| Propagation delay | ns | 548 | 548 | 548 | 548 | 504 | 534 |

a. NEXT = Near-end crosstalk, ELFEXT = Equal level far-end crosstalk
b. Includes additional TIA and ISO requirements TSB95 and FDAM 2, respectively

在实践中，Category 1 和 Category 2 电缆仅适用于语音应用（如果可以的话）。Category 3 电缆是局域网可用的最低等级；它是 10 Mb/s 10BaseT 的标准，但在今天应仅作为最后手段使用。Category 4 有点像弃儿，并不特别适合任何特定应用。

Category 5 电缆可支持 100 Mb/s。Category 5e、Category 6 和 Category 6a 布线支持 1 Gb/s，并且是目前数据布线最常用的标准。Category 6a 是新安装的首选电缆，因为它对来自旧以太网信号标准（例如，10BaseT）的干扰特别具有抵抗力，这是一个困扰了一些 Category 5/5e 安装的问题。Category 7 和 Category 7a 电缆用于 10 Gb/s。

