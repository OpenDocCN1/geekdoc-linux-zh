
| Health Center | System health monitor configuration | 6 |

| Development Center | Integrated tool for stored procedure, UDF development | 8 |

在本章中，我们挑选了几个工具和向导进行详细讨论。有关完整的 DB2 UDB 工具和向导集合，请参阅 IBM DB2 UDB Guide to GUI Tools for Administration and Development，SC09-4851。该书侧重于介绍 GUI 工具，并涵盖了许多工具。此外，您还可以阅读 IBM DB2 UDB Command Reference V8，SC09-4828，以获取有关系统和 DB2 CLP 命令提供的工具和实用程序的更多信息。

通常，要在 Linux 平台的 DB2 UDB 中调用 GUI 工具，您可以从 DB2 控制中心启动它们。要启动 DB2 控制中心，请单击 Linux 桌面上可用的控制中心图标，或从命令行输入命令 `db2cc`，然后按回车。大多数 GUI 工具可以从控制中心调用，如图 7-1 所示；有一个工具菜单可供您选择所需的工具。此外，如果您单击工具菜单中的 `Wizards...` 项目，将会弹出另一个包含向导选择的窗口

menu. 你可以选择 Create Table Space Wizard 在 DB2 的指导下逐步创建表空间，或选择 Load Wizard 将数据加载到单个或多个分区环境中。大多数情况下，这些工具或向导在导航树中右键单击特定对象时出现的弹出菜单中也可用；例如，如果你选择 Databases 并右键单击它，则 Create Database Wizard 将显示在弹出菜单中。

![](img/d95c931f4f3da4a6bd0ee55148fefad7_270_0.png)

Figure 7-1 Tools and Wizards menu in Control Center

> Tip: 如果在 Linux 桌面上未显示 DB2 UDB 的图标，你可以使用 DB2 Icon Generation Tool for Linux 为 Linux 添加这些图标。要调用 Icon Generation Tool，请从命令行输入 "`db2icons <instance_owner>`"，或仅输入 "`db2icons`" 以获取使用帮助。在为指定用户添加图标后，如果你使用该用户登录系统，DB2 Icons 将出现在该用户的桌面上。

本章将讨论以下工具和向导：

- **Design Advisor:** 也可通过命令行形式 `db2advis` 使用，它可以根据给定的工作负载为你的表推荐合适的索引，或验证虚拟索引是否对给定的工作负载有帮助。

- **Visual Explain:** 它可用于以图形形式获取指定 SQL 语句的访问计划，并帮助你调整 SQL 语句和数据库管理器配置参数以提高性能。命令行工具也可用于获取 SQL 语句的访问计划信息，例如 `db2expln`（用于静态 SQL）、`dynexpln`（用于动态 SQL）等。

- **Memory Visualizer:** 也可通过命令行形式 `db2mtrk`（Memory Tracker）使用，它可用于监控 DB2 实例的内存使用情况。

## 7.1 Design Advisor

Design Advisor 可帮助你根据现有的工作负载为表设计和定义合适的索引，或帮助你验证虚拟索引是否适用于数据库系统。对于设计非常大的表的索引尤其有益，因为有时你无法确定要创建的索引是否真的对应用程序有帮助，并且需要先创建它来测试是否有效。但对于数据量大的表，创建索引通常需要很长时间，并且也需要相当大的磁盘空间。此外，有时你会发现刚创建的索引什么帮助也没有。在这种情况下，Design Advisor 将是最好的工具，因为 Design Advisor 依赖于虚拟索引，无需创建真实索引即可工作。

在使用 Design Advisor 之前，你需要了解两个术语。

### Workload

工作负载是一组具有指定执行频率的 SQL 语句，数据库管理器需要在给定时间内处理的语句。SQL 语句可以包括 SELECT、INSERT、UPDATE 和 DELETE 语句。例如，在一个月内，你的数据库管理器可能需要处理 1,000 条 INSERT、10,000 条 UPDATE、10,000 条 SELECT 和 1,000 条 DELETE。建议引擎使用此工作负载信息结合数据库信息（如统计信息）来推荐索引。建议引擎的目标是最小化总工作负载成本。

### Virtual index

虚拟索引是指当前数据库模式中不存在的索引。这些索引可能是建议设施所做的推荐，或者是你希望建议设施评估的索引。虚拟索引信息在 `ADVISE_INDEX` 表中定义和操作。

Design Advisor 既有图形形式也有命令行形式。可从 DB2 Control Center 启动的 GUI 形式是使用 Design Advisor 的推荐方法，因为它提供了广泛的帮助页面，可以回答你的问题，并且还可以帮助你通过查找最近执行的 SQL 语句，或查看最近使用的包，或让你手动添加 SQL 语句来构建工作负载。

下面提供了一个示例来演示 Design Advisor 在图形形式中的使用。你可以从 DB2 Control Center 启动它，如图 7-2 所示，或在 Control Center 中选择 Tools → Wizards 后从 Wizard 弹出窗口调用它。

![](img/d95c931f4f3da4a6bd0ee55148fefad7_272_0.png)

Design Advisor 的第一个窗口（图 7-3）是一个介绍性窗口。它告诉你顾问的用途以及你正在操作的数据库。你可以单击 Next 来定义工作负载。

![](img/d95c931f4f3da4a6bd0ee55148fefad7_272_1.png)

在工作负载定义窗口中，如图 7-4 所示，首先，你需要为工作负载指定一个名称，然后点击 Add 将一条 SQL 语句添加到工作负载中，并指定 SQL 语句名称和执行频率。此处也允许添加多条 SQL 语句，你只需再次选择 Add 即可添加额外的 SQL 语句。

![](img/d95c931f4f3da4a6bd0ee55148fefad7_273_0.png)

### 图 7-4 为 Design Advisor 定义工作负载

你也可以选择 Import，该选项位于窗口右侧，用于从已解释的 SQL 语句导入工作负载，如图 7-5 所示。

- 1. 选择 SQL 语句的来源。
- 2. 点击要导入的语句旁边的复选框。
- 3. 点击 OK。

SQL 语句来源：已解释的 SQL 语句

导入 SQL 语句：全选、取消全选、确定、取消、应用、帮助

### 图 7-5 导入已解释的 SQL 语句以定义工作负载

下一步是指定需要收集统计信息的表。如前所述，咨询引擎结合工作负载信息和数据库信息（如统计信息）来推荐索引。因此，如果涉及表的最新统计信息不存在，你需要先收集它们，以使推荐的索引可用。图 7-6 显示了一些表被选中进行统计信息更新。

正在更新目录统计信息...

为了提供最佳建议，你数据库目录中的表统计信息必须是最新的。如果要更新表统计信息，请选择指定工作负载所需的表。更新表统计信息会增加计算时间。

可用表 已选表 DB2INST1 EMPLOYEE SALES 返回 下一步 完成 取消

### 图 7-6 为 Design Advisor 更新目录统计信息

然后你可以在磁盘使用窗口中指定推荐对象的默认表空间和组合最大磁盘空间。你可以在计算窗口中指定顾问引擎何时计算建议。如果想立即开始计算，请在窗口中选择 Now，然后建议将在建议窗口中给出，如图 7-7 所示。

在此，如果你想更改推荐索引的名称而不是使用 DB2 提供的名称，可以点击名称字段中显示的原始名称，然后输入你想要的名称。你可以点击 Show SQL 以获取创建索引的详细 SQL 语句，并且你也可以切换 Create 字段中的复选框来指出是否希望由 DB2 创建该索引。

![](img/d95c931f4f3da4a6bd0ee55148fefad7_275_0.png)

### 图 7-7 Design Advisor 推荐的索引

如果为所选表已存在某些索引，Design Advisor 可以告诉你这些索引在指定工作负载中是否未被使用。然后你可以指定是否要删除这些未使用的索引——在选择这样做之前，请确保删除“未使用”的索引不会影响其他工作负载。

剩余的步骤是安排推荐的 SQL 语句的运行，包括创建索引和删除索引，然后相关索引将被创建或删除。
