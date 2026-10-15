
示例中使用的每个参数都描述在表 3.9 中。

## 表 3.9 DBMS_UTILITY.ANALYZE_SCHEMA 的参数

| 示例中使用的参数 | 描述 |
| --- | --- |
| SCOTT | 要分析的模式。 |
| ESTIMATE | 要执行的分析类型。如果使用 COMPUTE，则后两个参数不起作用。 |
| 0 | 用于估计的行数。估计将以行数的百分比指定，在此输入 0。 |

## 表 3.9 DBMS_UTILITY.ANALYZE_SCHEMA 的参数（续）

| 示例中使用的参数 | 描述 |
|---|--|
| 40 | 用于估计的总行数的百分比。如果上一个参数非零，则此参数不起作用。 |
| FOR ALL INDEXED COLUMNS SIZE 40 | 如表 3.8 所示的附加选项。 |

`DBMS_UTILITY` 包也可以用于分析整个数据库。数据库级分析可以使用与示例相同的参数，模式参数除外。

```sql
SQL> EXECUTE DBMS_UTILITY.ANALYZE_DATABASE ('ESTIMATE',0,40,'FOR ALL INDEXED COLUMNS');
```

> 因为字典查询高度依赖访问路径来高效运行，你不应分析 SYS 模式。使用 `ANALYZE_SCHEMA('SYS','DELETE')` 命令删除它们。

![](img/c36db8fbb4893c30ad42a99bf63e3_155.png)

# 说明 DBMS_STATS

`DBMS_STATS` 包提供了许多 `DBMS_UTILITY` 包不具备的附加选项。这些选项包括：

- 在收集新统计信息之前备份统计信息。此实用功能允许在更新统计信息后 CBO 性能不佳时恢复或更新原始统计信息。
- 随机采样块，或仅估计统计信息。

# 了解 Oracle 优化器 117

- 比并行分析更快地收集统计信息。
- 自动对易变表收集统计信息并跳过静态表。

以下示例了如何使用 `DBMS_STATS` 包收集 Joe 模式下 `EMPLOYEE` 表的统计信息：

```sql
SQL> EXECUTE DBMS_STATS.GATHER_TABLE_STATS ('JOE', 'EMPLOYEE');
```

与 `DBMS_UTILITY` 包一样，`DBMS_STATS` 包也可以通过表 3.10 分析索引、整个模式或整个数据库。

## 表 3.10 DBMS_STATS 包中的过程

| 过程名称 | 描述 |
| --- | --- |
| GATHER_INDEX_STATS | 用于收集指定索引的统计信息 |
| GATHER_SCHEMA_STATS | 用于收集指定模式的统计信息 |
| GATHER_DATABASE_STATS | 用于收集整个数据库的统计信息 |
| GATHER_SYSTEM_STATS | 用于收集服务器的 I/O 和 CPU 性能统计信息 |

表 3.10 中的 `GATHER_SCHEMA_STATS` 过程对于维护 CBO 的准确统计信息特别有用。在 `GATHER` 选项中，你可以指定收集模式统计信息的三个选项之一：

`GATHER STALE` 选项任何使用 `ALTER TABLE MONITORING` 命令标记为“监控”的表都将被收集统计信息。

`GATHER EMPTY` 选项：模式中之前未进行分析过的任何表都将被收集统计信息。

`GATHER AUTO` 选项：根据应用程序的用户活动，Oracle 会自动确定哪些表需要分析，并使用适当的分析方法收集这些表的统计信息。

如果需要直方图统计信息，Oracle9 引入了一个名为 `AUTO_SAMPLE_SIZE` 的新 `DBMS_STATS` 常量，进一步简化了直方图统计信息的管理。当与 `DBMS_STATS.GATHER_STATS` 程序配合使用时，`AUTO_SAMPLE_SIZE` 将自动确定用于模式中每个段的采样百分比，以及是否有必要对段收集直方图统计信息。以下示例显示了如何使用 `AUTO_SAMPLE_SIZE` 收集 Joe 模式的统计信息：

```sql
SQL> execute DBMS_STATS.GATHER_SCHEMA(owname => 'JOE', estimate_percent => DBMS_STATS.AUTO_SAMPLE_SIZE, method_opt => 'for all columns size AUTO'
);
```

上述上述命令将导致 Oracle 对 Joe 模式中的每个表、列收集统计信息，并使用 Oracle 确定的采样大小。由于在 `METHOD_OPT` 中指定了 `AUTO` 选项，如果 Oracle 根据应用程序访问列数据的频率和方式判断需要直方图，则也会对这些段收集直方图统计信息。`METHOD_OPT` 参数的另外两个选项是 `REPEAT` 和 `SKEWONLY`。`REPEAT` 选项将导致 `DBMS_STATS` 包使用与原始直方图相同数量的桶（buckets）重新填充任何现直方图统计信息。`SKEWONLY` 选项将在列数据倾斜时随时生成直方图统计信息——无论应用程序访问数据的方式是否能直方图的存在受益。

## 使用 GATHER_SYSTEM_STATS 程序

为了让 CBO（成本优化器）对可能的执行计划做出良好的选择，让 CBO 了解 Oracle 数据库所在服务器的整体 CPU 和 I/O 利用模式非常重要。例如，如果系统统计表明服务器是 I/O 密集型而非 CPU 密集型，则当存在类似的 I/O 密集型和 CPU 密集型执行时，CBO 将选择 I/O 密集程度较低的执行计划。以下示例显示了如何使用 `GATHER_SYSTEM_STATS` 程序收集系统统计信息：

```sql
SQL> EXECUTE DBMS_STATS.CREATE_STAT_TABLE (
  ('SYSTEM', 'SYSTEM_STATISTICS', 'TOOLS');
```

PL/SQL 程序成功完成。

```sql
SQL> EXECUTE DBMS_STATS.GATHER_SYSTEM_STATS (
  interval => 180, 
  stattab => 'SYSTEM_STATISTICS', 
  statid => '05-MAR-02'
);
```

PL/SQL 程序成功完成。

上述命令将创建一个表（即 `SYSTEM_STATISTICS`）来存储系统统计信息，用三个小时（180 分钟）内收集的统计信息填充该表，并为这些统计信息分配标识 `05-MAR-02`。

![](img/c36db8fbb4893c630ad429a99bfd63e3_158_0.png)

> 在使用 `GATHER_SYSTEM_STATS` 程序的 `INTERVAL` 选项之前，必须将 `init.ora` 参数 `JOB_QUEUE_PROCESSES` 设置为非零值。

或者，您也可以通过交互式输入以下命令来手动确定系统统计信息的收集：

```sql
SQL> EXECUTE DBMS_STATS.GATHER_SYSTEM_STATS (
  gathering_mode => 'START', 
  stattab => 'SYSTEM_STATISTICS'
);
```

PL/SQL 程序成功完成。

```sql
SQL> EXECUTE DBMS_STATS.GATHER_SYSTEM_STATS (
  gathering_mode => 'STOP'
);
```
