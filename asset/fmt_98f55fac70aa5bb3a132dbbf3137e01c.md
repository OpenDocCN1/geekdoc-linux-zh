
![](img/f703ab958723c29086b17397273fad3b_58_0.png)

图 2-15 用于信息区域字段输入的信息对象主数据/文本

## 42 SAP 业务信息仓库报告

![](img/f703ab958723c29086b17397273fad3b_59_0.png)

2-16 查询设计器视图中作为信息提供者使用的信息对象需求。例如，我们希望您创建一个使用时间来与总账账户集成的报告，并为应收/应付账款（AR/AP）账龄流程生成报告。我们无法对特定的信息对象进行此类报告，因此我们需要组织一个信息集（InfoSet）来实现此。我们将在本章稍后部分讨论业务用户感兴趣的信息对象所需字段。

作为数据存储对象和信息立方体功能的总结，请参考表 2-4。

### 非数据目标（Non-Data Targets）

非数据目标是使用其他数据创建的信息提供者。因此，正如命名约定所示，信息提供者本身不持有数据，而是创建一个视图。如前所述，数据目标信息提供者仅显示已发生的事件，但通过非数据目标，您可以创建组合以满足额外的报告请求。非数据目标的类型包括多提供者、查询、虚拟信息提供者和信息集。我们处理这些内容时讨论它们的每一个优点。

## 第 2 章：存储数据——SAP/业务仓库

| 对象/属性 | 数据存储对象 | 信息立方体 |
| :--- | :--- | :--- |
| 方法/目的 | 协调、整合和大量存储（作为 EDW 架构的数据仓库层） | 聚合/优化查询性能 |
| 数据存储 | 事务数据和少量主数据的存储：永久，一到十年 | 事务数据的存储：永久，五到十年 |
| 数据源 | 清洗的数据（独立于源系统） | 清洗的数据（独立于源系统） |
| 操作 | 修改/添加/删除 | 添加 |
| 架构 | 关系数据库表，规范化，记录具有业务意义的键 | BW 扩展星型结构：去规范化 |
| 报告 | 高数据粒度（扁平报告） | 低数据粒度（多维报告） |

表 2-4 数据存储对象与信息立方体的比较

### 多提供者（MultiProviders）

多提供者是一种从多个信息提供者组合数据并用于分析目的的信息提供者类型。多提供者本身不包含任何数据。它的数据完全来自其基础信息提供者。这些信息提供者通过并集操作连接。多提供者可以由以下信息提供者的不同组合组成：信息立方体、数据存储对象、信息对象、信息集、虚拟提供和聚合层。图 2-17 显示了可能的组合示例。并集操作用于合并多提供者中这些对象的数据。在这里，系统构建所涉及数据集的并集；所有这些图 2-17

多提供者图形模型

## 44 SAP 业务信息仓库报告

数据集被组合在一起。作为对比，InfoSets 是通过连接（joins）创建的。这些连接合并了出现在两个表中的值。与并集（unions）不同，连接形成的是表的交集。在多提供者（MultiProvider）中，每个信息提供者（InfoProviders）的每个特征必须对应于一个特征或导航属性（如果可用）。如果这一点不明确，你需要定义想要分配给 MultiProvider 的特征信息对象（InfoObject）。在创建 MultiProvider 的过程中，确保在两个表中至少有一个特征是十分重要的，这样就可以生成成功的组合集。例如，如果你有一个数据存储对象（DataStore objects）——一个包含销售数据，一个包含交付数据——并且在 MultiProvider 中使用它们，那么生成的生成信息中的某个特征具有一个可以链接的唯一值是非常重要的。例如，假设你必须对数据/对比进行报告。在一个 InfoCube 中有实际数据，在另一个 InfoCube 中有模式，并构建一个 MultiProvider 来提供来自两个独立 InfoCube 的信息。这里的底层概念是，查询只能基于一个 InfoProvider，但如果使用 MultiProvider 尝试将信息组织到查询中，而没有两个 InfoCube 中相同的特征，将非常困难，尽管并非不可能。在图 2-18 中，你可以看到在过程中

![](img/f703ab958723c29086b17397273fad3b_61_0.png)

图 2-18 MultiProvider 数据模型：特征到 InfoProvider 的分配

## 第 2 章：存储数据——SAP/业务信息提供者 45

创建 MultiProvider 时，我们通过检查不同 InfoProvider 特征之间的链接来识别连接。在这种情况下，特征 T_SOLD_TO（销售方）被分配给 InfoCube Billing 以及信息对象 InfoObject Sold Party（销售方）。因此，它将是来自 InfoObject 的主数据和来自 Billing InfoCube 的事务数据的组合。特征和键值（key figures）都被分配给特定的组合或单个 InfoProvider。键值的分配比特征分配更重要（甚至更重要），因为如果你将一个键值分配给两个不同的 InfoProvider，你需要确保在查询设计器（Query Designer）过程中识别出特定的数据源。否则，由于信息的组合，你将获得双倍的数据。

MultiProviders 仅作为逻辑定义存在。数据继续存储在 MultiProvider 所在的 InfoProviders 中。基于 MultiProvider 的查询在内部被分为多个子查询。MultiProvider 中包含的每个 InfoProvider 都有一个查询。这些子查询通常并行处理。从技术上讲，MultiProvider 中可以包含的 InfoProvider 数量没有限制。然而，我建议在单个 MultiProvider 中使用的 InfoProvider 不要超过十个，因为拆分 MultiProvider 并为单个 InfoProvider 重建结果会花费大量时间，而且通常是适得其反的。建模超过 10 个 InfoProvider 的 MultiProvider 也是极其复杂的。在图 2-19 中，你可以看到查询设计器中 MultiProvider 的格式。注意，在特征列表（绿色三角形）中，增加了一个特征

![](img/f703ab958723c29086b17397273fad3b_62_0.png)

图 2-19 查询设计器视图中的 MultiProvider

该特征是该 MultiProvider 特有的（即特征信息提供者 InfoProvider (INFPROV)）。该特征允许从 MultiProvider 创建查询的高级用户选择特定的 InfoProvider 来限制正在读取的数据。因此，如果你有一个从不同 InfoProvider 读取键值的 MultiProvider，你可以将其限制为仅将信息提供者 (IINFPROV) 特征与你正在读取的键值进行组合。

> 注意 这种过程被称为创建受限键值（restricted key figure），我们将在第 5 章讨论并创建此对象。

### InfoSets

InfoSets 是通过连接数据源的 DataStore、InfoCubes 和 InfoObject 构建的逻辑视图。InfoSets 允许通过连接多个 InfoProvider 的数据来分析数据。由于 InfoSet 是时间依赖的，你可以设置 InfoSet 以回答查询问题。例如，在 InfoSets 的创建过程中，如果你有一个名为 Region（地区）的 InfoObject，且该属性具有一个名为 Country（国家）的属性，你可以设置 InfoSet 以包含这些数据。如果连接中的一个对象是时间依赖的，那么该连接就是时间依赖（或时间）连接。对于所有其他类型，键值都被考虑在内。

否则，在 MultiProvider 中，由于信息的组合，数据量就会翻倍。因为如果你在 MultiProvider 中分配了从不同 InfoProvider 读取键值，你需要确保在查询设计器过程中识别出特定的数据源。

键值的分配比特征分配更重要（甚至更重要），因为如果你将一个键值分配给两个不同的 InfoProvider，你需要确保在查询设计器过程中识别出特定的数据源。

MultiProviders 仅作为逻辑定义存在。数据继续存储在 MultiProvider 所在的 InfoProviders 中。基于 MultiProvider 的查询在内部被分为多个子查询。MultiProvider 中包含的每个 InfoProvider 都有一个查询。这些子查询通常并行处理。从技术上讲，MultiProvider 中可以包含的 InfoProvider 数量没有限制。然而，我建议在单个 MultiProvider 中使用的 InfoProvider 不要超过十个，因为拆分 MultiProvider 并为单个 InfoProvider 重建结果会花费大量时间，而且通常是适得其反的。建模超过 10 个 InfoProvider 的 MultiProvider 也是极其复杂的。

*(注：由于原文文本中存在部分段落重复，翻译已根据您的要求确保逻辑连贯性)*

# 48 SAP 业务数据仓库报表
