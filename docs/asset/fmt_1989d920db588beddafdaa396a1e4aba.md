
现在既然已经创建了合适的缓冲区池（`Buffer Pools`），你必须使用 `ALTER` 命令将每个段分配到其指定的缓冲区池。以下示例将我们在上一节中识别的每个段分配到相应的缓冲区池：

```sql
SQL> ALTER TABLE apps.employee
STORAGE (BUFFER_POOL KEEP);
```

```sql
SQL> ALTER TABLE apps.region
STORAGE (BUFFER_POOL KEEP);
```

```sql
SQL> ALTER TABLE apps.division
STORAGE (BUFFER_POOL RECYCLE);
```

```sql
SQL> ALTER INDEX apps.employee_first_name_idx
STORAGE (BUFFER_POOL KEEP);
```

```sql
SQL> ALTER INDEX apps.employee_id_pk
STORAGE (BUFFER_POOL KEEP);
```

```sql
SQL> ALTER TABLE apps.sales_history
STORAGE (BUFFER_POOL RECYCLE);
```

你可以通过对 `DBA_SEGMENTS` 执行以下查询，查看哪些段已分配了非默认（`Default`）缓冲区池：

```sql
SQL> SELECT owner, segment_type,
segment_name, buffer_pool
FROM dba_segments
WHERE buffer_pool != 'DEFAULT';
```

| OWNER | SEGMENT_TYPE | SEGMENT_NAME | BUFFER_POOL |
| :--- | :--- | :--- | :--- |
| APPS | TABLE | EMPLOYEE | KEEP |
| APPS | TABLE | REGION | KEEP |
| APPS | TABLE | DIVISION | RECYCLE |
| APPS | INDEX | EMPLOYEE_FIRST_NAME_IDX | KEEP |
| APPS | INDEX | EMPLOYEE_ID_PK | KEEP |
| APPS | TABLE | SALES_HISTORY | RECYCLE |

# 监控多个缓冲区池的性能

在执行 `ALTER` 命令之前缓存的段缓冲区将留在当前的池中。在下一次从磁盘重新读取之前，这些缓冲区不会移动到新指定的缓冲区池。

在对 `init.ora` 进行适当更改并指定要在哪些缓冲区池中缓存段后，你可以使用 `V$BUFFER_POOL` 和 `V$BUFFER_POOL_STATISTICS` 动态性能视图来监控缓冲区池的性能。

> Oracle 目标：监控缓冲区缓存（`Buffer Cache`）的使用，以及缓冲区缓存内不同的池

`V$BUFFER_POOL` 动态性能视图包含关于多个缓冲区池本身配置的信息。表 5.11 描述了用于获取单个缓冲区池信息的列。

## 表 5.11 V$BUFFER_POOL 列部分描述

| 列 | 描述 |
| :--- | :--- |
| NAME | 缓冲区池的名称 |
| BLOCK_SIZE | 此缓冲区池中缓冲区的块大小，以字节为单位 |
| CURRENT_SIZE | 缓冲区池的当前大小，以兆字节为单位 |

你可以使用这些列查询此视图并检查每个单独缓冲区池的大小：

```sql
SQL> SELECT name, block_size, current_size
FROM v$buffer_pool;
```

### 缓冲区缓存性能 275

| NAME | BLOCK_SIZE | CURRENT_SIZE |
| :--- | :--- | :--- |
| KEEP | 8192 | 150 |
| RECYCLE | 8192 | 50 |
| DEFAULT | 8192 | 300 |

使用 `V$BUFFER_POOL_STATISTICS`

`V$BUFFER_POOL_STATISTICS` 动态性能视图包含若干列，这些列包含有助于计算每个单独缓冲区池命中率的信息。表 5.12 描述了用于计算命中率的列。

## 表 5.12 V$BUFFER_POOL_STATISTICS 列部分描述

| 列 | 描述 |
| :--- | :--- |
| NAME | 缓冲区池的名称 |
| DB_BLOCK_GETS | 通过使用缓存段缓冲区满足段数据的请求数 |
| CONSISTENT_GETS | 通过使用缓存的回滚块满足一致性所需的段数据请求数 |
| PHYSICAL_READS | 需要将数据从磁盘读取到缓冲区缓存的段数据请求数 |

你可以使用以下查询利用 `V$BUFFER_POOL_STATISTICS` 中的统计信息来计算每个单独缓冲区池的命中率：

```sql
SQL SELECT name "Buffer Pool",
1- (physical_reads / (db_block_gets + consistent_gets))
"Buffer Pool Hit Ratio"
FROM v$buffer_pool_statistics
ORDER BY name;
```

### 缓冲区池缓冲区池命中率

| NAME | VALUE |
| :--- | :--- |
| DEFAULT | .713179916 |
| KEEP | .9721 |
| RECYCLE | .238907 |

正如你预期的，如果你正确地调优了多个缓冲区池，`Keep Pool` 的命中率应该非常高，而 `Recycle Pool` 的命中率应该很低。`Default Pool` 的命中率应该在这两个值之间，通常在 70–80 的范围内。

![](img/c36db8fbb4893c630ad429a99bfd63e3_315_0.png)

你的用户一直在抱怨应用程序性能不佳，但你对 `V$STAT` 的查询显示缓冲区缓存命中率为 99.9%。由于这表明几乎没有改进空间，你考虑转向其他领域以寻找可能的调优改进方案。

在这种情况下，应该仔细检查缓冲区缓存的内容。特别是，你应该确定缓冲区缓存中缓存了多少个索引缓冲区，以及它们属于哪些索引。

## 创建表时缓存

在创建表时包含 `CACHE` 关键字，可以创建一个缓存表，如下：

```sql
SQL> CREATE TABLE phone_list
2 ( employee_id number,
3 phone_number varchar(21),
4 extension varchar(4))
5 TABLESPACE appl_tab
6 STORAGE (INITIAL 50K NEXT 50K PCTINCREASE 0)
7 CACHE;
```

默认情况下，除非指定 `CACHE` 选项，否则所有表都创建为 `NOCACH`（不缓存）。

## 使用 ALTER TABLE 创建缓存表

你可以使用 `ALTER TABLE` 命令配合 `CACHE` 关键字将现有表改为缓存表：

```sql
SQL> ALTER TABLE employee CACHE;
```

`NOCACH` 选项用于将表恢复到常规的 `FTS`（全表扫描）行为。

## 使用提示（Hints）进行缓存

你还可以使用适当的提示动态地表进行 `CACHE` 或 `NOCACH` 操作：

```sql
SQL> SELECT /*+ CACHE */ last_name, first_name
2 FROM employee;
```

该提示将仅影响本次查询；对 `EMPLOYEE` 表的所有其他访问将使用默认的缓存模式。

## 显示缓存表信息

你可以使用 `DBA_TABLES` 视图中的 `CACHE` 列来确定哪些表被缓存了，如下：

```sql
SQL> SELECT owner, table_name
2 FROM dba_tables
3 WHERE LTRIM(cache) = 'Y';
```

### 提高缓冲区缓存性能 279

| OWNER | TABLE_NAME |
|-------|-----------|
| APPS | EMPLOYEE |
| APPS | PHONE_LIST |

## 绕过缓冲区缓存

另一种提高数据库缓冲区缓存性能的技术是针对某些类型的缓冲区请求完全绕过。通过绕过缓冲区，已存储的缓冲区在处理过程中不会向下移动或移出 `LRU` 列表。这两种类型的事务可以配置为绕过数据库缓冲区缓存：

- 排序直接写（在第 8 章“调优磁盘 I/O”中介绍）
- 并行 `DML`

并行数据操纵语言（`DML`）通过启动多个进程来执行操作，涉及并行批量插入、更新和删除。在有效使用并行执行之前，必须正确设置几个 `init_ora` 参数。

![](img/c36db8fbb4893c630ad429a99bfd63e3_318_0.png)
