
# 第 5 章：SQL Server 查询调优与优化

## 执行计划基础

```sql
SELECT DISTINCT (City) FROM Person.Address
```

然后在结果窗格中选择“执行计划”选项卡。这显示了如图 5-3 所示的计划。

![执行计划示例](img/0a5d3f27ca07081d5ee426b77bb624b8_149_0.png)

### 注意

本书包含大量的示例查询，所有示例都在 `SQL Server 2017 RTM` 上测试过。这些示例数据库未包含在 `SQL` 安装中，但可以单独下载。最新版本是 `AdventureWorks OLTP`，你可以从 `https://github.com/Microsoft/sql-server-samples/releases/tag/adventure` 下载。如何在 `Linux` 上拷贝备份文件并恢复数据库的更多细节，请参阅第 1 章。

树结构中的每个节点由一个图标表示，指定逻辑和物理算子，例如 `Index Scan` 和 `Hash Aggregate` 算子，如图 5-3 所示。第一个图标是一个语言元素，它代表 `SELECT` 语句，并且通常是计划的根元素。

### 注意

从 `SQL Server Management Studio 17.4` 开始，执行计划图标与之前的版本略有不同。在本书出版时它们可能会更新，参考 `SQL Server` 文档页面：`https://docs.microsoft.com/en-us/sql/relational-databases/showplan-logical-and-physical-operators`

算子实现了执行引擎的基本功能或操作；例如，逻辑连接操作由三个物理连接算子之一实现：嵌套循环、合并连接或哈希连接。显然，执行引擎中实现了许多算子，你可以在此处查看完整列表：`https://msdn.microsoft.com/en-us/library/ms19158(v=sql.110).aspx`。逻辑和物理算子图标以蓝色显示，光标算子为黄色，语言元素以绿色显示：

![算子图标说明](img/0a5d3f27ca07081d5ee426b77bb624b8_150_0.png)

- 蓝色逻辑/物理算子
- 绿色语言元素
- 黄色光标

查询优化器从这些算子中构建执行计划，这些算子可能会从数据库读取记录，如上一个计划中的 `Index Scan` 算子；或者它们可能会从另一个算子读取记录，例如从 `Index Scan` 算子读取记录的 `Hash Aggregate`。

每个节点与父节点相关，通过箭头连接，数据从子算子流向父算子，箭头宽度与行数成正比。在算子对其拥有的记录执行某些功能后，结果输出到其父节点。你可以将鼠标指针悬停在箭头上以获取有关该数据流的更多信息，这些信息以索引工具框的形式显示。例如，如果你将鼠标指针悬停在图 5-3 所示的 `Index Scan`（索引扫描）和 `Hash Aggregate`（哈希聚合）算子之间的箭头，你可以看到这些算子之间的数据流信息，如图 5-4 所示。

通过查看实际行数，可以看到 `Index Scan` 算子从数据库读取了 19,614 行并将其发送到 `Hash Aggregate` 算子。`Hash Aggregate` 算子对数据执行某些操作并向其父节点发送 575 行，你可以通过将鼠标指针放在 `Hash Aggregate` 和 `SELECT` 图标之间的箭头上看到这一点。

基本上，在执行计划中，`Index Scan` 算子从一个索引中读取了所有 19,614 行，而 `Hash Aggregate` 正在处理这些行以获取不同的城市列表（共 575 个），这些城市将在 `Management Studio` 的结果窗口中显示。请注意，你可以估算行数（即查询优化器对该算子的基数估计）以及实际行数。比较实际行数和估计行数有助于检测估计误差，这些误差可能会影响你执行计划的质量。

为了完成其工作，物理算子必须实现以下方法至少一种：

- `Open()` 导致算子初始化，并可能包括设置任何所需的数据结构
- `GetRow()` 从算子请求一行数据
- `Close()` 在算子完成其职责后执行某些清理操作并关闭算子

算子通过调用其他算子的 `GetRow()` 方法来请求行，这意味着执行计划中的执行操作是从左到右开始的。由于 `GetRow()` 每次只产生一行数据，因此执行计划中显示的实际行数也是该方法在特定算子上被调用的次数，算子会使用额外的 `GetRow()` 调用来指示结果集的结束。在上一个示例中，`Hash Aggregate` 算子调用了一次 `Open()`，在 `Index Scan` 算子上调用了 19,615 次 `GetRow()`，调用了一次 `Close()`。

| SELECT Cost: 0 | Hash Match (Aggregate) Cost: 40 | Index Scan (NonClustered) (Address): [ID_Address_AddressLine_ |
|---|---|---|
| Actual Number of Rows | 19614 | |
| Estimated Number of Rows | 19614 | |
| Estimated Row Size | 28 B | |
| Estimated Data Size | 536 KB | |

图 5-4 Index Scan 和 Hash Aggregate 算子之间的数据流

## 传统查询处理模式

现在，我将解释传统的查询处理模式，算子每次只处理一行。这种处理模式自 `SQL Server 7.0` 以来用于所有版本。在下一章中，我将介绍随 `SQL Server 2012` 引入的新批处理模式，该模式用于列存储索引相关的算子。

除了学习更多数据流之外，你还可以将鼠标指针悬停在算子上以获取有关它的更多信息。例如，图 5-5 显示了 `Index Scan` 算子。注意，它包含了算子的描述以及有关估计成本信息的数据，例如估计的 I/O、CPU、算子成本和子树成本。

| Index Scan (NonClustered) | Index Scan |
|---|---|
| Physical Operation | Index Scan |
| Logical Operation | Adaptive Row |
| Actual Join Type | Row |
| Actual Execution Mode | Row |
| Estimated Execution Mode | Row |
| Storage | Row/Store |
| Number of Rows | 19614 |
| Actual Number of Rows | 19614 |
| Actual Number of Batches | 0 |
| Estimated (I/O) Cost | 0.158681 |
| Estimated Operator Cost | 0.180413 (52) |
| Estimated CPU Cost | 0.0217324 |
| Estimated Subtree Cost | 0.180413 |
| Estimated Number of Executions | 1 |
| Number of Rows | 19614 |
| Estimated Number of Rows to Read | 19614 |
| Estimated Row Size | 28 B |
| Actual Rebounds | 0 |
| Actual Rewinds | 0 |
| Ordered | False |
| Node ID | 1 |

**图 5-5** Index Scan 算子的工具框

值得注意的是，成本只是内部成本单位，不应以秒或毫秒等单位进行解释。

你还可以从计划中看到每个算子的相对成本占整个计划的百分比，如图 5-3 所示。例如，`Index Scan` 的成本占整个计划成本的 52%。可以通过属性窗口获取算子或整个查询的附加信息。例如，从菜单视图选择 `SELECT` 图标和属性窗口（或按 `F4`）将显示整个查询的属性。

## XML 计划

一旦显示了图形计划，你就可以轻松切换到 XML。只需在图形计划的任何地方右键点击并选择 `Plan XML`。这将打开 XML 编辑器。如果需要，可以通过右键点击并选择 `Execution Plan As...` 来将图形计划保存到文件中。计划通常以 `.sqlplan` 扩展名保存，实际上是一个包含计划信息的、供 `Management Studio` 读取的 XML 文档。

表 5-1 显示了用于获取文本、图形或 XML 估计或实际执行计划的不同语句。请记住，使用 `ON` 子句运行表中的任何语句时，将适用于后续语句。

| 文本计划 | 估计执行计划 | 实际执行计划 |
|---|---|---|

要直接显示 XML 计划，可以使用以下命令：

```sql
SET SHOWPLAN_XML ON
GO
SELECT DISTINCT(City) FROM Person.Address
GO
SET SHOWPLAN_XML OFF
```

这将显示单行单列（标题为 "Microsoft SQL Server 2005 XML ShowPlan"）的结果，包含以 `<ShowPlan xmlns="http://schemas.microsoft.com/2004/showplan">` 开头的 XML 数据。点击链接将显示图形计划，可以使用之前的步骤显示 XML 计划。

可以通过以下练习浏览 XML 计划的基本结构。简单的查询将创建基本的 XML 结构，但在本示例中，我展示了一个包含两个额外部分的查询：缺失索引和参数列表。运行以下查询并按照以前的方法请求 XML 计划：

```sql
SELECT FROM WHERE OrderQty = 1
```

通过点击左侧的减号 (-) 折叠 `<MissingIndexes>`、`<RelOp>` 和 `<ParameterList>`，以便方便查看整个结构。你应该看到类似于图 5-6 的内容。

```xml
<?xml version="1.0" encoding="utf-16"?>
<BatchSequence>
<Batch>
<Statements>
<SimpleStatement StatementId="1" EstimateRows="68468" StatementId="1" StatementOpLevel="Full" Car
<StatementOptions ARITH="true" ANSI_NULLS="true" ANSI_PADDING="true" ANSI_WARNINGS="true" ARITHABORT="true" CONCAT
<QueryPlan DegreeOfParallelism="1" CachedPlanSize="32" CompileTime="4" CompileCPU="4" CompileMemory="1"
<MemoryGrantInfo SerialRequiredMemory="0" SerialDesiredMemory="0" />
<DataSetMemoryDependent EstimatedAvailableMemory="20627" EstimatedCachedPages="-"
<Query>
<RelAttr ...
</Query>
</SimpleStatement>
</Statements>
</Batch>
</BatchSequence>
<ShowPlanXML>
```

图 5-6 XML 执行计划

## XML 计划结构解析

如你所见，XML 计划的主要组件是 `<StmtSimple>`、`<StatementSetOptions>` 和 `<QueryPlan>` 元素。这些元素包含了几个属性，其中一些我们在讨论图形计划时提到过。此外，`<QueryPlan>` 元素还包含其他元素，例如 `<MissingIndexes>`、`<MemoryGrantInfo>`、`<OptimizerHardwareDependentProperties>`、`<WaitStats>`、`<QueryTimeStats>`、`<RelOp>`、`<PropertyList>` 等，图 5-6 中未显示的 `SQL Server 2017` 中的新元素 `<OptimizerStatsUsage>` 将在下一章中进行详细介绍。

## 文本计划

如表 5-1 所示，你可以使用两个命令来获取估计的文本计划：`SET SHOWPLAN_TEXT` 和 `SHOWPLAN_ALL`。这两个语句都显示估计的执行计划，但 `SHOWPLAN_ALL` 显示了额外信息，包括估计行数、估计的 CPU 成本、估计的 I/O 成本和算子成本。你可以使用以下代码显示文本执行计划：

```sql
SET SHOWPLAN_TEXT ON
GO
SELECT DISTINCT(City) FROM Person.Address
GO
SET SHOWPLAN_TEXT OFF
GO
```

这段代码实际上会显示两个结果集，第一个返回 T-SQL 语句的文本。在第二个结果集中，你会看到下面的文本计划（已为了适应页面进行了编辑），它显示了图 5-3 中所示哈希聚合（`Hash Aggregate`）和索引扫描（`Index Scan`）算子。

```
-- Hash Match (Aggregate, HASH: ([Person].[Address].[City]), RESIDUAL ...
-- Index Scan (OBJECT: [AdventureWorks]).[Person].[Address].IX_Address ...
```

`SET SHOWPLAN_ALL` 和 `SET STATISTICS PROFILE` 提供的信息比 `SET SHOWPLAN_TEXT` 更加详尽。此外，如表 5-1 所示，你可以使用 `SET SHOWPLAN_ALL` 仅获取估计计划，并使用 `SET STATISTICS PROFILE` 实际执行查询。

## 查询排错

在上一节中，我向你介绍了将执行计划作为我们与 `SQL Server` 查询处理器交互的主要工具。现在，我将向你展示基础的调优工具和技术，你可以通过这些工具找出查询消耗了多少资源，并找到系统中开销最大的查询。

动态管理视图（`DMVs`）和动态管理函数（`DMFs`）随 `SQL 2005` 引入，是诊断问题、调优性能和监控服务器实例健康的极佳工具。有很多 `DMV` 可用，在本节中，我将关注 `sys.dm_exec_requests`、`sys.dm_exec_sessions` 和 `sys.dm_exec_query_stats`，你可以通过系统中运行的查询来确定服务器资源（如 CPU 和 I/O）。它们还可以用于查找你的 `SQL Server` 实例中开销最大的查询。

此外，`SQL Server 2016` 的查询存储（`Query Store`）是一项惊人的性能功能，可以帮助你收集历史查询和计划信息以及运行时统计数据，你可以利用这些信息识别与查询性能相关的问题，甚至强制执行特定的计划。

我将用 `SET STATISTICS TIME` 和 `SET STATISTICS` 语句结束本节，它们可以为你的查询提供额外的性能信息。

## sys.dm_exec_requests 和 sys.dm_exec_sessions

`sys.dm_exec_requests` DMV 可用于当前在 `SQL Server` 上执行的请求，而 `sys.dm_exec_sessions` 显示实例上的已身份验证会话。虽然这些 DMV 包含许多列，在本节中，我们将关注与资源使用和查询性能相关的列。你可以在 `SQL Server` 文档中查看其他列的定义。这两个 DMV 共享几个列，定义如下：

- **cpu_time**: 此请求或该会话中其他请求所使用的 CPU 时间（毫秒）。
- **elapsed_time**: 自请求到达或会话建立以来的经过时间（毫秒）。
- **reads**: 此请求或该会话中其他请求执行的读取次数。
- **writes**: 此请求或该会话中其他请求执行的写入次数。
- **logical_reads**: 此请求或该会话中其他请求执行的逻辑读取次数。
- **row_count**: 此请求返回给客户端的行数。

基本上，`sys.dm_exec_requests` 将显示当前执行的特定请求的资源，而 `sys.dm_exec_sessions` 将显示会话完成的所有请求的累积资源。为了理解这两个 DMV 如何收集资源使用信息，我们可以运行以下练习，使用一个至少需要几秒的查询。在 `Management Studio` 中打开新查询并获取其会话 ID（例如使用 `SELECT @@SPID`），但确保不要运行任何内容，因为资源使用将累积在 `sys.dm_exec_sessions` DMV 中。在该窗口中复制并运行以下代码：

```sql
DBCC FREEPROCCACHE
DBCC DROPBUFFERS
GO
SELECT * FROM Production.Product p1 CROSS JOIN Production.Product p2
```

将以下代码复制到第二个窗口，并将 `@session_id` 替换为第一个窗口获得的值：

```sql
DECLARE @session_id tinyint = 56
SELECT cpu_time, reads, total_elapsed_time, logical_reads, row_count
FROM sys.dm_exec_requests
WHERE session_id = @session_id

SELECT cpu_time, reads, total_elapsed_time, logical_reads, row_count
FROM sys.dm_exec_requests
WHERE session_id = @session_id
```
