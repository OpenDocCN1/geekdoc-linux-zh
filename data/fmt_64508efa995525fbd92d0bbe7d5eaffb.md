
现在我们有了图 6-8 所示的计划，它也有正确的估计，但这次使用的是合并连接。

扩展事件 `interleaved_exec_status` 和 `interleaved_exec_status_update` 分别用于跟踪交叉执行的发生以及跟踪其更新的基数估计。此外，执行计划可以显示属性 `ContainsInterleavedExecutionCandidates` 和 `IsInterleavedExecuted`，以检测查询中是否存在交叉执行候选对象以及查询是否成功执行，如下 XML 示例所示：

```xml
<QueryPlan ContainsInterleavedExecutionCandidates="true">
```

```xml
<RuntimeInformation>
<RuntimeCountersPerThread IsInterleavedExecuted="true" />
</RuntimeInformation>
```

最后，在当前版本中，多语句表值函数必须是只读的且不能是数据修改操作的一部分才能成为交叉执行的候选对象。此外，它们不能位于 `CROSS` 运算符内部。

## 第 6 章：新的查询处理功能

## 自动调优

自动 SQL 是一项新功能，根据 SQL Server 2017 文档，其目的是“为潜在的查询性能问题提供洞察、建议解决方案并自动修复识别出的问题”。尽管听起来非常广泛且乐观，但它在 SQL Server 社区中引起了巨大轰动。目前唯一发布的功能是帮助处理原本运行最优的查询的计划回退。目前还没有公告表明它在未来的发布版本中是否会涵盖任何额外功能，或者这些额外功能可能是什么。虽然自动调优目前的优势非常有限，但我们希望在不久的将来可以将其扩展，以涵盖更多的查询性能问题。

自动调优还有第二个功能：自动索引管理，该功能仅适用于 Azure SQL Database。此功能旨在自动创建建议的索引，或删除不再被任何查询使用的索引。我在本书中没有介绍 SQL Database，但你可以通过查看在线文档 `https://docs.microsoft.com/en-us/sql/relational-databases/automatic-tuning/automatic-tuning` 获取有关此功能的更多细节。

自动计划回退包括在检测到查询回退时，自动切换到该查询的上一个良好计划。只有当预估的 CPU 收益大于 10 秒，或者强制计划优于当前计划且新计划中的错误数量高于建议计划中的错误数量时，数据库引擎才会强制执行建议。这些阈值无法更改。

此外，自动计划回退过程在最后已知良好计划之后并没有结束，因为数据库引擎会继续监控变化，如果新计划没有优于被替换的计划，它可以回滚。注意，你也可以手动实现此过程：在查询存储（`query store`）上识别查询和计划，并运行 `sp_query_store_force_plan` 过程。此过程要求你手动监控查询存储信息以找到计划回退，定位最后已知良好计划，应用所需的脚本强制计划，并继续监控更改的性能。所有这些功能都可以通过查询存储来实现，因此从 SQL Server 2016 开始即可实施。正如暗示的，这种手动过程的缺点是，你必须持续监控变化，以查看它们是否继续带来性能收益，否则将决定撤销执行计划。

最后，请注意，强制计划应仅作为寻找永久解决方案期间的临时修复。因为计划就像一组提示（`hints`），这在第 4 章中讨论过，它基本上禁用了查询优化器的工作。寻找永久解决方案可能需要应用标准的查询优化技术。

# Linux 上的 Microsoft SQL Server 2017

让我们通过观察自动计划修正的示例来看看该技术是如何工作的。（这里将不会涵盖自动索引管理，因为它实现在 Azure SQL Database 上。）

有时，尝试用 AdventureWorks 创建真实的性能问题可能是一个挑战，因为是一个非常小的数据库。虽然一种方法是可以创建包含数百万行的表，但我可以使用第 5 章中用于演示参数嗅探（`parameter sniffing`）的相同脚本展示这一概念。因此，让我们从恢复 AdventureWorks 数据库的最新副本开始。

在这种情况下，假设理想的计划是使用索引的那个，如果我们突然出现性能下降，我们可以将其视为一次回退。如果我们还没有这样做，请运行以下语句在 AdventureWorks 上启用查询存储：

```sql
ALTER DATABASE AdventureWorks2014 SET QUERY_STORE = ON
GO
ALTER DATABASE AdventureWorks2014 SET QUERY_STORE (OPERATION_MODE = READ_WRITE, MAX_STORAGE_SIZE_MB = 1024)
```

如果你已经启用了查询存储，只需运行以下语句即可清除其数据并从头开始：

```sql
ALTER DATABASE AdventureWorks2014 SET QUERY_STORE CLEAR ALL
```

创建以下过程：

```sql
CREATE PROCEDURE test (@pid int)
AS
SELECT * FROM Sales.SalesOrderDetail
WHERE ProductID = @pid
```

## 第 6 章：新的查询处理功能

查询返回了之前讨论的一些信息，外字段：`scripts`，即在手动强制执行计划时执行的脚本；`query_id`，退化查询的 `query_id`；`regressed_plan_id`，退化计划的 `plan_id`；`recommended_plan_id`，推荐计划的 `plan_id`。对于此示例，我创建的脚本如下，它基本上将为 ID 为 1 的查询强制使用计划 1。

```sql
exec sp_query_store_force_plan @query_id = 1, @plan_id = 1
```

因此，我已经介绍了如何手动强制执行计划。这要求我手动监控查询存储（`query store`）的信息以找到性能退化，找到最后一个已良好计划，应用所需的脚本强制执行计划，并继续监控更改后的性能。所有这些功能都可以通过查询存储来实现，因此它们从 SQL Server 2016 开始就可以实现。SQL Server 2017 的新之处在于能够让数据库引擎自动实现这些更改。`sys.db_tuning_recommendations` DMV 也是 SQL Server 2017 中的新功能。

此外，新的 `sys_database_automatic_tuning_options` DMV 可以帮助你跟踪特定数据库的自动调优选项。运行以下语句检查当前配置：

```sql
SELECT * FROM sys.database_automatic_tuning_options
```

你将得到以下输出：

| Name | desired state | desired state desc | actual_state | actual_state desc | reason | reason_desc |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| FORCE_LAST_GOOD_PLAN | 0 | OFF | 0 | OFF | NULL | NULL |

要启用自动计划退化功能，使用新的 `AUTOMATIC_TUNING` 选项和 `FORCE_LAST_GOOD_PLAN` 选择运行以下语句：

```sql
ALTER DATABASE AdventureWorks2014
SET AUTOMATIC_TUNING (FORCE_LAST_GOOD_PLAN = ON)
```

这将 `sys_database_automatic_tuning_options` DMV 的输出如下：

| Name | desired state | desired state desc | actual_state | actual_state desc | reason | reason_desc |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| FORCE_LAST_GOOD_PLAN | 1 | ON | 1 | ON | NULL | NULL |

## Linux 版 Microsoft SQL Server 2017

注意，此自动调优选项需要查询存储。尝试在没有查询存储的情况下启用它将生成以下错误消息：

```
Msg 15705, Level 16, State 1, Line 3
Tuning option FORCE_LAST_GOOD_PLAN cannot be enabled, because Query
Store is not turned on.
Msg 5069, Level 16, State 1, Line 3
ALTER DATABASE statement failed.
```

最后，重要的是记住，SQL Server 仅在估计的 CPU 收益大于 10 秒，或者强制执行计划优于当前计划且新计划中的错误数量高于推荐计划中的错误数量时，才会自动强制建议。早些时候我展示了如何使用 `sys.dm_db_recommendations` DMV 的 `reason` 列查看 CPU 性能信息的差异。错误数量可以通过同一 DMV 中 `details` 列的以下字段获取：

- `regressedPlanColumnCount`：执行退化计划期间检测到的错误
- `recommendedPlanCount`：执行推荐计划期间检测到的错误

## SQL Server 2016 Service Pack 1

如前所述，SQL Server 2016 Service Pack 1 为所有 SQL Server 版本的开发者提供了一致的编程界面。从此发行版开始，列存储索引、内存内存 OLTP（`In-Memory OLTP`）、始终加密（`always encrypted`）、压缩、分区、数据库快照、行级安全和动态数据掩码等功能现在已适用于所有 SQL Server 版本，如 Express、Web、Standard 和 Enterprise。

SQL Server 2016 Service Pack 1 还带来了一系列新的查询相关功能，包括：

- `CREATE OR ALTER` 语句：新的 `CREATE OR ALTER` 语句可以应用于存储过程、触发器、用户定义函数和视图。
- `USE HINT` 查询选项：新的查询选项提供了在不使用 `QUERYTRACEON` 不需要系统凭据的情况下，在查询级别启用某些跟踪标志的行为的能力。
- 以程序方式识别 SQL 服务启动时“内存锁页”（`Lock Pages in Memory`）权限和“即时文件初始化”（`Instant File initialization`）是否生效：这些信息分别可用 `sys.dm_os_sys_info` 和 `sys.dm_server_DMVs` 查看。
- 执行计划上的额外诊断信息：执行计划上提供了如顶级等待、启用的跟踪标志和额外的性能信息。
- `EstimatedRowsRead` 属性：该属性可对具有下推谓词（`pushdown predicates`）的查询计划进行故障排除和诊断。

有关 SQL Server 2016 Service Pack 1 的更多信息，请参考在线文章 `https://blogs.microsoft.com/sqlreuseservices/sql-server-2016-service-pack-1-sp1-released/`

## USE HINT 查询选项

在 SQL Server 2016 Service Pack 1 中首次提供的新的 `USE HINT` 查询选项仍然是一个非常不为人知的特性。可以使用 `USE HINT` 配合 `QUERYTRACE` 提示在查询级别获取某些跟踪标志的行为。如你所知，`QUERYTRACE` 提示允许你启用影响计划的跟踪标志。

`QUERYTRACE` 某些功能的一个问题是它需要系统管理员（`sysadmin`）权限。通过 `USE HINT`，你可以使用表 6-1 中列出的任何支持的标志来更改查询优化器。

支持以下提示：

- `DISABLE_OPTIMIZED_NESTED_LOOP`：禁用批排序。
- `FORCE_LEGACY_CARDINALITY_ESTIMATION`：启用新的基数估计，其中数据库配置为使用旧的基数估计。
- `ENABLE_QUERY_OPTIMIZER_HOTFIXES`：启用服务包和累积更新发布的查询修复。
- `DISABLE_PARAMETER_SNIFFING`：禁用参数嗅探。

让我们来看两个例子。首先，不要以系统管理员身份运行以下查询：

```sql
SELECT * FROM Sales.SalesOrderDetail Where ProductID = 898
OPTION (QUERYTRACEON 9481)
```

## 第 6 章：新的查询处理功能

在没有 `sysadmin` 权限的情况下运行查询将产生以下错误消息：

```
Msg 2571, Level 14, State 3, Line 1
User 'test' does not have permission to run DBCC TRACE.
```

然而，以下语句在不需要 `sysadmin` 凭据的情况下会产生完全相同的行为：

```sql
SELECT * FROM Sales.SalesOrderDetail WHERE ProductID = 898
OPTION (USE HINT ('FORCE_LEGACY_CARDINALITY_ESTIMATION'))
```

延续第 4 章和本章之前关于参数嗅探（`parameter sniffing`）的示例，创建测试存储过程：

```sql
CREATE PROCEDURE test (@pid int)
AS
SELECT * FROM Sales.SalesOrderDetail
WHERE ProductID = @pid
```

使用以下参数运行该过程将获得 9 行的估计值，以及一个使用索引查找（`index seek`）和键查找（`key lookup`）算子的执行计划。该执行使用参数嗅探来检查传递参数的值，并使用统计对象的直方图估计返回的行数（在第 5 章中介绍过）：

```sql
EXEC test @pid = 898
```

正如你在第 5 章中看到的，在少数情况下，我们可能想要禁用参数嗅探。可以通过不同的方式来实现，包括使用下所示跟踪标志（`trace flag`）4136。请记住，使用 `QUERYTRACEON` 提示需要再次具备 `sysadmin` 权限。

```sql
ALTER PROCEDURE test (@pid int)
AS
SELECT * FROM Sales.SalesOrderDetail
WHERE ProductID = @pid
OPTION (QUERYTRACEON 4136)
```

在这种情况下，像以前一样运行测试存储过程将获得 456.079 的估计值以及一个使用表扫描（`table scan`）的新计划。

> 第 5 章还涵盖了使用 `OPTIMIZE FOR UNKNOWN` 提示来获得完全相同的行为。

## Linux 上的 Microsoft SQL Server 2017

以下示例将在不需要提升权限的情况下，通过使用 `DISABLE_PARAMETER_SNIFFING` 提示名称产生完全相同的行为：

```sql
ALTER PROCEDURE test (@pid int)
AS
SELECT * FROM Sales.SalesOrderDetail
WHERE ProductID = @pid
OPTION (USE HINT ('DISABLE_PARAMETER_SNIFFING'))
```

还有一个 DMV `sys.dm_exec_valid_use_hints`，它返回支持的 `USE` 提示名称：

```sql
SELECT * FROM sys.dm_exec_valid_use_hints
```

SQL Server 2017 返回以下提示名称，这些名称也列在表 6-1 中：

- `DISABLE_OPTIMIZED_NESTED_LOOP`
- `FORCE_LEGACY_CARDINALITY_ESTIMATION`
- `ENABLE_QUERY_OPTIMIZER_HOTFIXES`
- `DISABLE_PARAMETER_SNIFFING`
- `ASSUME_MIN_SELECTIVITY_FOR_FILTER_ESTIMATES`
- `ASSUME_JOIN_PREDICATE_DEPENDS_ON_FILTERS`
- `ENABLE_HIST_AMENDMENT_FOR_ASC_KEYS`
- `ENABLE_OPTIMIZER_ROWGOAL`
- `FORCE_DEFAULT_CARDINALITY_ESTIMATION`

最后，表 6-1 还涵盖了三个数据库范围配置选项，你可以使用这些选项获得与跟踪标志或名称提示相同的行为，但是在数据库级别实现的。例如，要在数据库级别禁用参数嗅探，你可以运行以下语句：

```sql
ALTER DATABASE SCOPED CONFIGURATION SET parameter_SNIFFING = OFF
```

现在你可以运行我们测试过程的原始版本，并在无需任何提示的情况下获得禁用参数嗅探的行为：

```sql
ALTER PROCEDURE test (@pid int)
AS
SELECT * FROM Sales.SalesOrderDetail
WHERE ProductID = @pid
```

## 第 6 章：新的查询处理功能

运行该过程将获得 456.079 的估计值以及使用表扫描的计划。如果你尝试了之前的示例，请忘记启用参数嗅探：

```sql
ALTER DATABASE SCOPED CONFIGURATION SET PARAMETER_SNIFFING = ON
```
