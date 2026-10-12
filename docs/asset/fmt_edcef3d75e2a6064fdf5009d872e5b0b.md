
```sql
dbms_stats.gather_table_stats (ownername=>'PROD',
tabname=>'ORDERS',
estimate_percent=>10,
method_opt=>FOR ALL COLUMNS,
deg=>10,
cascade=>TRUE);
*** Schema 名称
*** 采样大小 (%)
*** 列
*** 并行度
*** 级联索引
```

你还可以使用 `DBMS_STATS.gather_schema_stats` 过程在模式级别上并行收集统计信息。`gather_schema_stats` 过程也接受并行度。下面的示例说明了如何使用 `gather_schema_stats` 并指定并行度。

```sql
dbms_stats.gather_schema_stats (ownername=>'PROD',
estimate_percent=>10,
method_opt=>FOR ALL COLUMNS,
degree=>10,
cascade=>TRUE);
*** Schema 名称
*** 采样大小 (%)
*** 列
*** 并行度
*** 级联索引
```

并行生成统计信息的能力显著减少了刷新统计信息所需的时间。维护对象统计信息有助于提高优化器选择最优执行计划的能力。在创建索引期间也可以通过在 `CREATE INDEX` 或 `ALTER INDEX` 命令中计算 `STATISTICS` 子句生成索引统计信息。`DBMS_STATS` 包还允许通过 `DBMS_STATS.export_table_stats` 过程导出统计信息。然后可以使用 `DBMS_STATS.import_table_stats` 过程导入统计信息。这非常有用，因为它允许对象统计信息复制到分布相同（例如备用数据库）或非常相似的其他数据库。导出和导入统计信息的能力对于计划分析很有用。例如，你可以将生产统计信息导入开发数据库，并使用这些统计信息来审查执行计划。

`DBMS_STATS` 包提供了以下过程：

- `CREATE_STAT_TABLE`
- `DELETE_COLUMN_STATS`
- `DELETE_DATABASE_STATS`
- `DELETE_INDEX_STATS`
- `DELETE_SCHEMA_STATS`
- `DELETE_TABLE_STATS`
- `DROP_STAT_TABLE`
- `EXPORT_COLUMN_STATS`
- `EXPORT_DATABASE_STATS`
- `EXPORT_INDEX_STATS`
- `EXPORT_SCHEMA_STATS`
- `EXPORT_TABLE_STATS`
- `GATHER_DATABASE_STATS`
- `GATHER_INDEX_STATS`
- `GATHER_SCHEMA_STATS`
- `GATHER_TABLE_STATS`
- `GET_COLUMN_STATS`
- `GET_INDEX_STATS`
- `GET_TABLE_STATS`
- `IMPORT_COLUMN_STATS`
- `IMPORT_DATABASE_STATS`
- `IMPORT_INDEX_STATS`
- `IMPORT_SCHEMA_STATS`
- `IMPORT_TABLE_STATS`

有关 `DBMS_STATS` 包的更多信息，请参考《Oracle8i Supplied PL/SQL Packages Reference》手册。

## 4.6.2 Oracle8i/优化器增强

Oracle8i 通过许多改进执行计划的新功能极大增强了基于成本的优化器，从而缩短了执行时间。`init.ora` 参数 `optimizer_features_enable` 控制 CBO 使用哪个版本和哪些功能。设置 `optimizer_features_enable=8.1.6` 可以启用新的 Oracle 版本 2 CBO 特性，例如扩展视图合并以及将连接谓词推入 `UNION ALL` 视图内部。

在 8.1.6 中，CBO 通过考虑更多表作为起始表来启用计划生成。为了启用新的多起始表优化，请将 `init.ora` 参数 `optimizer_max_permutations` 设置为小于默认值 80,000 的值。例如，设置 `optimizer_max_permutations=79000` 可启用新的多起始表优化。

在 Oracle8 中，复杂视图合并默认被禁用。在 Oracle8 中，如果 `optimizer_features_enable=8.0.4` 则启用复杂视图合并，可以通过设置 `init.ora` 参数 `complex_view_merging=FALSE` 禁用复杂视图合并。在 Oracle8 中，可以通过设置 `init.ora` 参数 `complex_view_merging=TRUE` 启用复杂视图合并。该参数启用复杂视图合并功能，允许某些类型的复杂视图（如带有聚合或列连接的视图）合并。此参数默认禁用，因此必须显式设置。有关视图合并的更多细节，请参阅第 4.5 节。

另一个在 Oracle8.0.4 中引入并在 Oracle8 中进一步扩展的优化器特性称为谓词推入（push predicate）。谓词推入特性允许优化器将谓词推入不可合并的视图内部。这有助于消除对表的全表扫描。在 Oracle8 中，谓词推入特性默认禁用，因此必须显式设置。以下是谓词推入的示例：

```sql
select ai.invoice_num
from ai, ahv
where ai.invoice_id = ahv.invoice_id
```

## 4.6 优化器

199

在此示例中，由于分别存在表达式 `+0` 和 `||`，GBAL.code_combination 和 GBAL.translated_flag 的字典列统计信息没有被应用。因此，CBO 使用内部默认统计信息，并估计 GL_BALANCES 表的基数为 4,213。CBO 在 GL_BALANCES 和 GL_CODE_COMBINATIONS 两张表之间选择了哈希连接（hash join）方法，并在 GL_CODE_COMBINATIONS 表进行全表扫描，该表包含 128,228 行。如果启用了 `use_column_statistics_for_function` 功能，则生成的执行计划在效率上更高，在基数方面也更加准确。

```sql
SQL> alter session set "use_column_stats_for_function"=TRUE;
```

### 执行计划

```sql
SELECT Cost-27287,1089 bytes=344124 ,
NESTED LOOPS Cost=27287,1089 bytes=344124 ,
TABLE ACCESS BY INDEX ROW GL_BALANCES Cost=26198,1089 bytes=99099 ,
INDEX RANGE SCAN GL_BALANCES_N1 Cost=497,1089 bytes=,
TABLE ACCESS BY INDEX ROW GL_CODE_COMBINATIONS Cost=1,128238
bytes=2885350 ,
INDEX UNIQUE SCAN GL_CODE_COMBINATIONS_U1 Cost=128238 bytes=,
```

执行计划显示 GL_BALANCES 表的估计值为 1,089，几乎是之前基数估计的四分之一。CBO 随后在 GL_BALANCES 和 GL_CODE_COMBINATIONS 表之间选择了嵌套循环（nested loops join），而不是使用 GL_CODE_COMBINATIONS 表上 CODE_COMBINATION 的唯一索引作为访问方法。该功能对于以前使用 RBO 且迁移到 CBO 的应用程序非常有用。在 RBO 中，许多开发者通常会使用 `+0` 或 `||` 来禁用非选择性索引或强制执行特定的连接顺序。如果应用程序以前完全基于 RBO，可能存在大量的 SQL 语句，通过这种经典的 RBO 技术，不需要从所有 SQL 语句中手动删除 `+0` 和 `||` 即可减少 CBO 的影响。

另一个在 8.1.6 中添加的 CBO 功能允许优化器将连接谓词推入 UNION 视图内部。由于包含 UNION 或 UNION ALL 等集合操作符的视图是不可合并的，此功能允许优化器将连接谓词推入包含 UNION ALL 操作符的不可合并视图。这提高了连接到包含 UNION ALL 操作符的视图的查询执行性能。可以通过设置 `init.ora` 参数 `_push_join_union_view=TRUE` 来启用推连接视图功能。接接示例说明了推连接视图功能的使用。
