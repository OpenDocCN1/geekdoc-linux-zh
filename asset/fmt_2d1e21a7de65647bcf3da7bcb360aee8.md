
该示例中使用的每个参数都在表 3.9 中进行了描述。

## 表 3.9 `DBMS_UTILITY.ANALYZE_SCHEMA` 的参数

| 示例中使用的参数 | 描述 |
| :---------------------- | :---------------------------------------------------------- |
| SCOTT | 要分析的模式。 |
| ESTIMATE | 要执行的分析类型。如果使用 `COMPUTE`，则下两个参数无效。 |
| 0 | 在估计中使用的行数。如果估计将以行百分比表示，请在此处输入零。 |
| 40 | 估计中使用的总行数的百分比。如果前一个参数不为零，则此参数无效。 |
| FOR ALL INDEXED COLUMNS SIZE 40 | 如表 3.8 中所示的额外选项。 |

`DBMS_UTILITY` 包也可用于分析整个数据库。数据库级别分析可以使用表 3.9 中讨论过的相同参数，除了模式参数外。以下是一个使用与前面示例相同样本大小的完整数据库分析示例：

```sql
SQL> EXECUTE SYS.DBMS_UTILITY.ANALYZE_DATABASE
( 'ESTIMATE', 0,40,'FOR ALL INDEXED COLUMNS SIZE 40');
```

> **注意：** 由于递归数据字典查询严重依赖于特定的访问路径才能高效运行，您永远不应分析 `SYS` 模式中的段。使用 `ANALYZE_DATABASE` 过程会导致为 `SYS` 模式收集统计信息。您应该使用 `DBMS_UTILITY.ANALYZE_SCHEMA('SYS', 'DELETE');` 命令来删除它们。

### Oracle 目标

解释 `DBMS_STATS` 过程的用途

### DBMS_STATS

`DBMS_STATS` 包提供了一些在 `DBMS_UTILITY` 包中不可用的额外分析选项。其中一些选项包括：

- 在新统计信息收集之前备份旧的统计信息。这个非常有用的功能允许您在更新后的统计信息收集后，如果 CBO 表现不佳，恢复部分或全部原始统计信息。
- 在估算统计信息时，对*数据块*而不仅仅是行进行随机抽样。
- 通过并行执行分析来更快地收集表统计信息。
- 自动收集高波动表的统计信息，并跳过静态表的统计信息收集。

以下示例展示了如何使用 `DBMS_STATS` 包在 Joe 的模式中收集 `EMPLOYEE` 表的统计信息：

```sql
SQL> EXECUTE DBMS_STATS.GATHER_TABLE_STATS ('JOE', 'EMPLOYEE');
```

与 `DBMS_UTILITY` 包一样，`DBMS_STATS` 包也可以用于分析索引、整个模式或整个数据库，使用表 3.10 中显示的过程。

## 表 3.10 DBMS_STATS 包中的过程

| 过程名称 | 描述 |
| :--- | :--- |
| GATHER_INDEX_STATS | 用于收集指定索引的统计信息 |
| GATHER_SCHEMA_STATS | 用于收集指定模式的统计信息 |
| GATHER_DATABASE_STATS | 用于收集整个数据库的统计信息 |
| GATHER_SYSTEM_STATS | 用于收集服务器的 I/O 和 CPU 性能统计信息 |

表 3.10 中显示的两个过程，`GATHER_SCHEMA_STATS` 和 `GATHER_SYSTEM_STATS`，在使用 CBO 时特别有用。

### 使用 GATHER_SCHEMA_STATS 过程

表 3.10 中列出的 `GATHER_SCHEMA_STATS` 过程对于为 CBO 维护准确的统计信息特别有用。使用 `GATHER` 选项，您可以指定以下三个选项之一来收集模式统计信息：

- `GATHER STALE` 选项：使用 `ALTER TABLE ... MONITORING` 命令指定为“已监视”的模式中任何表都会收集其统计信息。

### GATHER EMPTY 选项

模式中任何先前未分析过的表都将收集其统计信息。

### GATHER AUTO 选项

根据应用程序用户的活动，Oracle 会自动确定哪些表需要进行分析，并仅针对这些表使用最合适的分析方法收集统计信息。

如果需要直方图统计信息，Oracle 引入了一个新的 `DBMS_STATS` 参数常量，称为 `AUTO_SAMPLE_SIZE`，它进一步简化了直方图统计信息的 manage。当与 `DBMS_STATS.GATHER_SCHEMA_STATS` 过程一起使用时，`AUTO_SAMPLE_SIZE` 常量将自动确定模式中每个段应使用的适当采样百分比，以及是否需要在这些段上收集直方图统计信息。以下示例展示了如何使用 `AUTO_SAMPLE_SIZE` 来收集 Joe 模式的统计信息：

```sql
SQL> EXECUTE DBMS_STATS.GATHER_SCHEMA_STATS(
  ownname => 'JOE',
  estimate_percent => DBMS_STATS.AUTO_SAMPLE_SIZE,
  method_opt => 'for all columns size AUTO'
  );
```

上述命令将使 Oracle 收集 Joe 模式中所有表、列和索引的统计信息，使用由 Oracle 确定的样本大小。由于在 `METHOD_OPT` 中指定了 `AUTO` 选项，如果 Oracle 根据应用程序访问列数据的频率和方式确定需要直方图，则也会在这些段上收集直方图统计信息。`METHOD_OPT` 参数的另外两个选项是 `REPEAT` 和 `SKEWONLY`。`REPEAT` 选项将导致 `DBMS_STATS` 包使用与原始直方图相同数量的直方图桶来重新填充任何现有的直方图统计信息。无论应用程序访问列数据的方式是否受益于直方图的存在，只要列数据存在偏斜，`SKEWONLY` 选项都会生成直方图统计信息。

## 使用 GATHER_SYSTEM_STATS 过程

为了让 CBO（基于成本的优化器）就可能的执行计划做出良好的选择，重要的是让 CBO 了解 Oracle 数据库所在的服务器上的整体 CPU 和 I/O 利用模式。例如，如果系统统计信息显示服务器通常是 I/O 受限而非 CPU 受限，那么当可用 I/O 密集型和 CPU 密集型执行计划相当时，CBO 将选择 I/O 密集度较低的执行计划。以下示例展示了如何使用 `GATHER_SYSTEM_STATS` 过程来收集系统统计信息：

```sql
SQL> EXECUTE DBMS_STATS.CREATE_STAT_TABLE ( -
> ('SYSTEM','SYSTEM_STATISTICS','TOOLS'));
```

```sql
PL/SQL procedure successfully completed.
```

```sql
SQL> EXECUTE DBMS_STATS.GATHER_SYSTEM_STATS ( -
> interval => 180,
> stxttab => 'SYSTEM_STATISTICS', -
> statid => '05-MAR-02'
> );
```

```sql
PL/SQL procedure successfully completed.
```

上述命令将创建一个表（即 `SYSTEM_STATISTICS`）来保存系统统计信息，用在三个小时（180 分钟）期间收集的统计信息填充该表，并为这些统计信息分配标识符 `05-MAR-02`。

> 在使用 `GATHER_SYSTEM_STATS` 过程的 `INTERVAL` 选项之前，必须将 `init.ora` 参数 `JOB_QUEUE_PROCESSES` 设置为非零值。

或者，你也可以通过交互式输入以下命令手动确定系统统计信息收集间隔：

```sql
SQL> EXECUTE DBMS_STATS.GATHER_SYSTEM_STATS ( -
> gathering_mode => 'START', -
> sttxttab => 'SYSTEM_STATISTICS' -
> );
```

```sql
PL/SQL procedure successfully completed.
```

```sql
SQL> EXECUTE DBMS_STATS.GATHER_SYSTEM_STATS ( -
> gathering_mode => 'STOP' -
> );
```

```sql
PL/SQL procedure successfully completed.
```

**提示** 如果在 `STATTAB` 参数中未指定表名，则收集的系统统计信息将存储在数据字典中。希望将统计信息存储在数据字典中的用户必须具有 `SYSDBA` 权限。

**提示** Oracle 强烈建议收集系统统计信息，以改进 CBO 的性能。

**注意** 要查看 `DBMS_STATS` 包中可用众多选项的完整详情，请参阅《Oracle9i 提供的 PL/SQL 包和类型参考，Release 1 (9.0.1)》（部件号 A89852-02）第 63 章“DBMS_STATS”。
