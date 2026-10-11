
具体来说，那里的讨论使用了三个逻辑等价的 WHERE 子句作为例子，其中只有第三个子句能够启用索引：

```sql
WHERE TO_DAYS(date_col) - TO_DAYS(CURDATE()) < cutoff
WHERE TO_DAYS(date_col) < cutoff + TO_DAYS(CURDATE())
WHERE date_col < DATE_ADD(CURDATE(), INTERVAL cutoff DAY)
```

`EXPLAIN` 可以帮你检查一种表达式写法是否比另一种更好。为了说明这一点，让我们尝试使用上述每个 WHERE 子句来查找 member 表中 expiration 列的过期值，截止值设为 30 天。不过，按创建时的状态，member 表的 expiration 列上没有索引。为了看出索引使用与表达式写法之间的关系，首先给 expiration 列添加索引：

```sql
mysql> ALTER TABLE member ADD INDEX (expiration);
```

然后针对表达式的每种形式尝试使用 `EXPLAIN`，看看优化器生成了什么执行计划：

```sql
mysql> EXPLAIN SELECT * FROM MEMBER
-> WHERE TO_DAYS(expiration) - TO_DAYS(CURDATE()) < 30\G
*************************** 1. ROW ***************************
           id: 1
      select_type: SIMPLE
          table: MEMBER
         type: ALL
   possible_keys: NULL
            key: NULL
      key_len: NULL
          ref: NULL
         rows: 102
        Extra: Using where
```

```sql
mysql> EXPLAIN SELECT * FROM MEMBER
-> WHERE TO_DAYS(expiration) < 30 + TO_DAYS(CURDATE())\G
*************************** 1. ROW ***************************
           id: 1
      select_type: SIMPLE
          table: MEMBER
         type: ALL
   possible_keys: NULL
            key: NULL
      key_len: NULL
          ref: NULL
         rows: 102
        Extra: Using where
```

```sql
mysql> EXPLAIN SELECT * FROM MEMBER
-> WHERE expiration < DATE_ADD(CURDATE(), INTERVAL 30 DAY)\G
*************************** 1. ROW ***************************
           id: 1
      select_type: SIMPLE
          table: MEMBER
         type: range
   possible_keys: expiration
            key: expiration
      key_len: 4
          ref: NULL
         rows: 6
        Extra: Using where
```

前两个语句的结果显示索引未被使用。`type` 的值指示了从表中读取数据的方式。`ALL` 意味着“将检查所有行”。也就是说，将执行全表扫描，而无法利用索引。`key` 相关各列中的 `NULL` 也表明不会使用任何索引。

相比之下，第三个语句的结果显示该 WHERE 子句的写法使得优化器可以使用 expiration 列上的索引：

- `type` 值表明可以使用索引来查找特定范围的值（即小于表达式右侧给定日期的值）。
- `possible_keys` 和 `key` 值表明 expiration 上的索引被视为候选索引，并且实际上也是会被使用的索引。
- `rows` 值显示优化器估计处理该查询需要检查 6 行。这比前两个执行计划中的值 102 要好。

`EXPLAIN` 的另一个用途是确定添加索引是否能帮助优化器更高效地执行语句。对于这个示例，我将使用两个最初没有索引的表。这足以展示创建索引的效果。同样的原则也适用于涉及许多表的更复杂的连接。

假设有两个表 t1 和 t2，每个表都有 1,000 行，包含从 1 到 1000 的值。我们要检查的查询是查找两个表中对应值相同的行：

```sql
mysql> SELECT t1.i1, t2.i2 FROM t1 INNER JOIN t2
         -> WHERE t1.i1 = t2.i2;
+-------+-------+
| i1    | i2    |
+-------+-------+
| 1 | 1 |
| 2 | 2 |
| 3 | 3 |
| 4 | 4 |
| 5 | 5 |
...
```

当两个表都没有索引时，`EXPLAIN` 产生如下结果：

```sql
mysql> EXPLAIN SELECT t1.i1, t2.i2 FROM t1 INNER JOIN t2
    -> WHERE t1.i1 = t2.i2\G
*************************** 1. row ***************************
     id: 1
 select_type: SIMPLE
    table: t1
      type: ALL
possible_keys: NULL
        key: NULL
    key_len: NULL
        ref: NULL
       rows: 1000
      Extra:
*************************** 2. row ***************************
     id: 1
 select_type: SIMPLE
    table: t2
      type: ALL
possible_keys: NULL
        key: NULL
    key_len: NULL
        ref: NULL
       rows: 1000
      Extra: Using where
```

这里，`type` 列中的 `ALL` 表示检查所有行的全表扫描。`possible_keys` 列中的 `NULL` 表示未找到任何可用于加速查询的候选索引。（由于缺乏合适的索引，`key`、`key_len` 和 `ref` 列也全都是 `NULL`。）`Using where` 表示使用了 `WHERE` 子句中的信息来识别符合条件的行。

这些信息告诉我们，优化器没有找到有助于更高效执行查询的信息，并将按如下步骤进行：

- 它将执行 t1 的全表扫描。
- 对于 t1 的每一行，它将执行 t2 的全表扫描，并使用 `WHERE` 子句中的信息来识别符合条件的行。

`rows` 值显示了优化器对在每个查询阶段需要检查多少行的估计。对于 `t1`，估计值是 1000，因为将执行全表扫描。同样，对于 `t2`，估计值也是 1000，但这是*针对 `t1` 中的每一行*。换句话说，优化器估计处理该查询需要检查的行组合数是 1,000 × 1,000，即一百万。这是非常浪费的，因为实际上只有 1,000 个组合满足 `WHERE` 子句中的条件。

为了使这个查询更高效，在其中一个连接列上添加索引，并再次尝试 `EXPLAIN` 语句：

```sql
mysql> ALTER TABLE t2 ADD INDEX (i2);
mysql> EXPLAIN SELECT t1.i1, t2.i2 FROM t1 INNER JOIN t2
    -> WHERE t1.i1 = t2.i2\G
*************************** 1. ROW ***************************
 id: 1
 select_type: SIMPLE
 table: t1
 type: ALL
 possible_keys: NULL
 key: NULL
 key_len: NULL
 ref: NULL
 rows: 1000
 Extra:
*************************** 2. ROW ***************************
 id: 1
 select_type: SIMPLE
 table: t2
 type: ref
 possible_keys: i2
 key: i2
 key_len: 5
 ref: sampdb.t1.i1
 rows: 10
 Extra: Using where; Using index
```

这是一个改进。t1 的输出没有变化（表示仍然会对该表执行全表扫描），但优化器可以以不同的方式处理 t2：

- `type` 从 `ALL` 变为了 `ref`，这意味着可以使用引用值（来自 t1 的值）执行索引查找以定位 t2 中符合条件的行。
- 引用值在 `ref` 字段中给出：`sampdb.t1.i1`。
- `rows` 值从 1000 降至 10，这表明优化器认为对于 t1 中的每一行，它只需要检查 t2 中的 10 行。（这是一个略显悲观的估计。实际上，t2 中只有 1 行会与 t1 中的每一行匹配。我们稍后会看到如何帮助优化器改进此估计。）总共估计的行组合数是 1,000 × 10 = 10,000。这比在没有索引的情况下之前的一百万估计要好得多。

对 t1 建立索引有价值吗？毕竟，对于这个特定的连接，必须扫描其中一个表，并且无需索引即可做到。为了看看是否有任何效果，对 t1.i1 建立索引并再次运行 `EXPLAIN`：

```sql
mysql> ALTER TABLE t1 ADD INDEX (i1);
mysql> EXPLAIN SELECT t1.i1, t2.i2 FROM t1 INNER JOIN t2
    -> WHERE t1.i1 = t2.i2\G
*************************** 1. row ***************************
  id: 1
select_type: SIMPLE
     table: t1
      type: index
possible_keys: i1
      key: i1
  key_len: 5
      ref: NULL
     rows: 1000
    Extra: Using index
*************************** 2. row ***************************
  id: 1
select_type: SIMPLE
     table: t2
      type: ref
possible_keys: i2
      key: i2
  key_len: 5
      ref: sampdb.t1.i1
     rows: 10
    Extra: Using where; Using index
```

这个输出与之前那个 `EXPLAIN` 的输出类似，但添加索引确实使 t1 的输出产生了一些变化：`type` 从 NULL 变为了 index，`Extra` 从空白变为了 Using index。这些变化表明，尽管仍然会对索引值进行全扫描，但优化器现在可以直接从索引中读取这些值，而完全不需要触及数据文件。当优化器知道仅通过咨询索引文件就能获取所需的所有信息时，你会在 MyISAM 表中看到这种结果。当优化器可以仅使用索引中的信息而无需另一次查找来获取数据行时，你也会在 InnoDB 表中看到这种结果。

我们可以采取的另一项帮助优化器做出更好成本估计的步骤是运行 `ANALYZE TABLE`。这会导致服务器生成关于键值分布的统计信息。分析这些表并再次运行 `EXPLAIN` 会得到更好的 rows 估计：

```sql
mysql> ANALYZE TABLE t1, t2;
mysql> EXPLAIN SELECT t1.i1, t2.i2 FROM t1 INNER JOIN t2
    -> WHERE t1.i1 = t2.i2\G
*************************** 1. row ***************************
  id: 1
select_type: SIMPLE
     table: t1
      type: index
possible_keys: i1
```

