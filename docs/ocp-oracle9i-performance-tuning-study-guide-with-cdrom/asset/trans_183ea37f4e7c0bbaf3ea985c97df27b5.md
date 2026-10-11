

## 将片段分配给缓存池

现在，既然合适的缓冲区池（Buffer Pool）已经创建完成，你必须使用 `ALTER` 命令将每个片段（segment）分配给指定的缓冲区池。以下示例展示了如何将我们在上一节中识别出的各个片段分配到相应的缓冲区池：

```sql
SQL> ALTER TABLE apps.employee
2  STORAGE (BUFFER_POOL KEEP);

SQL> ALTER TABLE apps.region
2  STORAGE (BUFFER_POOL KEEP);

SQL> ALTER TABLE apps.division
2  STORAGE (BUFFER_POOL RECYCLE);

SQL> ALTER INDEX apps.employee_first_name_idx
2  STORAGE (BUFFER_POOL KEEP);

SQL> ALTER INDEX apps.employee_id_pk
2  STORAGE (BUFFER_POOL KEEP);

SQL> ALTER TABLE apps.sales_history
2  STORAGE (BUFFER_POOL RECYCLE);
```

你可以使用以下针对 `DBA_SEGMENTS` 的查询来查看哪些片段被分配了非默认的缓冲区池：

```sql
SQL> SELECT owner, segment_type,
2  segment_name, buffer_pool
3  FROM dba_segments
4  WHERE buffer_pool != 'DEFAULT';
```

| 拥有者 | 片段类型 | 片段名称 | 缓冲区池 |
| :--- | :--- | :--- | :--- |
| APPS | 表 | EMPLOYEE | KEEP |
| APPS | 表 | REGION | KEEP |
| APPS | 表 | DIVISION | RECYCLE |
| APPS | 索引 | EMPLOYEE_FIRST_NAME_IDX | KEEP |
| APPS | 索引 | EMPLOYEE_ID_PK | KEEP |
| APPS | 表 | SALES_HISTORY | RECYCLE |

> 在 `ALTER` 命令之前已缓存的任何片段缓冲区仍会保留在其当前的池中。这些缓冲区不会移动到新指定的缓冲区池，直到它们下次从磁盘重新读取时。

## 监控多个缓冲区池的性能

在对 `init.ora` 进行适当更改并指定将哪些片段缓存在哪些缓冲区池之后，你可以使用 `V$BUFFER_POOL` 和 `V$BUFFER_POOL_STATISTICS` 动态性能视图来监控缓冲区池的性能。

| **Oracle 目标** | 监控缓冲区缓存的使用情况，以及缓冲区缓存内不同的池 |
| :--- | :--- |

### 使用 V$BUFFER_POOL

`V$BUFFER_POOL` 动态性能视图包含关于多个缓冲区池自身配置的信息。表 5.11 描述了用于获取各个缓冲区池信息的有用列。

**表 5.11** V$BUFFER_POOL 列的部分描述

| **列名** | **描述** |
| :--- | :--- |
| NAME | 缓冲区池的名称 |
| BLOCK_SIZE | 此缓冲区池中缓冲区的块大小，以字节为单位 |
| CURRENT_SIZE | 缓冲区池的当前大小，以兆字节（MB）为单位 |

你可以使用这些列来查询此视图，并检查每个单独缓冲区池的大小：

```sql
SQL> SELECT name, block_size, current_size
 2   FROM v$buffer_pool;
```

| 名称   | 块大小 | 当前大小 |
|------------|------------|----------------|
| KEEP       | 8192       | 150            |
| RECYCLE    | 8192       | 50             |
| DEFAULT    | 8192       | 300            |

### 使用 V$BUFFER_POOL_STATISTICS

`V$BUFFER_POOL_STATISTICS` 动态性能视图包含多个列，其中包含用于计算各个单独缓冲区池命中率的信息。表 5.12 描述了用于计算命中率的列。

**表 5.12** V$BUFFER_POOL_STATISTICS 列的部分描述

| 列名 | 描述 |
| :--- | :--- |
| NAME | 缓冲区池的名称 |
| DB_BLOCK_GETS | 通过使用缓存的片段缓冲区来满足的数据片段请求数量 |
| CONSISTENT_GETS | 通过使用缓存的回滚块（用于读取一致性）来满足的数据片段请求数量 |
| PHYSICAL_READS | 需要从磁盘将数据读入缓冲区缓存的数据片段请求数量 |

你可以使用 `V$BUFFER_POOL_STATISTICS` 中的统计信息，通过以下查询来计算每个单独缓冲区池的命中率：

```sql
SQL> SELECT name 'Buffer Pool',
2 1-
3 (physical_reads / (db_block_gets + consistent_gets))
4 'Buffer Pool Hit Ratio'
5 FROM v$buffer_pool_statistics
6 ORDER BY name;
```

缓冲区池          缓冲区池命中率
-------------------  --------------------
DEFAULT                          .713179916
KEEP                             .9721
RECYCLE                          .238907

正如你所料，如果你正确地调整了多个缓冲区池，Keep 池的命中率应该非常高，而 Recycle 池的命中率应该很低。Default 池的命中率应该介于这两个值之间，但通常在 70–80 百分比的范围内。

## 实际场景

### 100% 的命中率并不总是意味着最佳性能

你的用户一直抱怨应用程序性能较差，但你在 `V$SYSSTAT` 上执行的查询显示缓冲区缓存命中率为 99.97 百分比。由于这个命中率表明改进空间很小，你考虑转向其他领域以寻找可能的调优改进。

在这种情况下，应该仔细检查缓冲区缓存的内容。特别是，你应该确定有多少个索引缓冲区被缓存在缓冲区缓存中，以及它们属于哪些索引。假设使用 `V$CACHE` 和 `DBA_USERS`，你确定非常大的 `ORDERS` 表中 `ORDER_STATUS` 列上的索引使用了缓冲区缓存中的许多缓冲区。进一步检查后，你还确定 `ORDER_STATUS` 只有三个可能的值：Open（开启）、Closed（关闭）和 Hold（保持）。此外，你发现 `ORDERS` 表中 90 百分比的记录状态为 Closed。

`ORDERS` 表中 `ORDER_STATUS` 列上的低选择性索引可能是导致你的应用程序性能差但缓冲区缓存命中率高的主要原因。当扫描此类索引时，其许多块会被引入缓冲区缓存。如果索引位于“热门”应用程序表——如 `ORDERS`——上，那么由于缓冲区缓存中缓存了大量索引块以及应用程序频繁请求这些块，缓冲区缓存命中率会被人为地抬高。这导致高命中率，但应用程序的整体性能低下。

> 可以采取几个步骤来修复这种情况。第一步是确保在数据字典中维护当前统计信息，以便基于成本的优化器能够确定索引的选择性，并在全表扫描更有效时放弃使用该索引。减少此问题的第二种方法是在 `ORDERS` 表上创建直方图，以便基于成本的优化器能更好地掌握 `ORDER_STATUS` 列中值的分布情况。最后，你可能希望指定将来自该索引的缓冲区缓存在 Recycle 池而不是缓冲区缓存中。所有这些步骤不仅有助于保持高的缓冲区缓存命中率，而且确保为你的应用程序用户提供真正的性能好处。

## 在内存中缓存表

无论决定使用多少个缓冲区池，每个池仍由一个最近最少使用（LRU）列表进行管理。通常，应用程序用户访问的块会被放置在 LRU 列表的最近使用端。然而，正如本章前面提到的，通过全表扫描（FTS）访问的表会将其块立即放置在 LRU 列表的最久未使用端。

这种行为可能会带来一个有趣的调优困境。如果基于成本的优化器看到经常使用的表（如验证表或查找表）很小，它很可能会通过全表扫描访问该表。但这种全表扫描会将该表的缓冲区放置在 LRU 列表的最久未使用端，在那里它们很快会从缓冲区缓存中移除，仅仅因为随后的应用程序用户再次需要它们时，它们会被重新读入内存。

管理此问题的一种方法，特别是对于小表，是利用缓存表。被指定为*缓存表*的表，在通过全表扫描访问时，其缓冲区不会被放置在 LRU 列表的最久未使用端。相反，这些缓冲区会被放置在 LRU 列表的最近使用端，就好像它们没有经过全表扫描一样。这具有在内存中保留这些缓冲区更长时间的效果，同时仍以最高效的方式访问它们。缓存表可以通过三种方式实现：在表创建时、在表创建后通过修改表、或使用提示（hint）。

