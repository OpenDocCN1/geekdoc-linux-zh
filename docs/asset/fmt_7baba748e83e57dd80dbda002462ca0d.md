
| :--- | :--- |

| PRSCNT | 语句被解析的次数 |

| PRSCPU | 解析语句所消耗的 CPU 时间 |

| PRSELA | 解析语句所消耗的实际时间（Elapsed time） |

| PRSDSK | 语句解析期间发生的磁盘读取次数 |

| PRSMIS | 语句解析期间库缓存未命中的次数 |

| PRSCU | 语句解析期间从 SGA 读取的数据或索引缓冲区数量 |

| PRSQRY | 语句解析期间从 SGA 读取的回滚缓冲区数量 |

SQL 语句处理的第二步是 *执行*，当 SQL 语句执行该语句指定的操作时发生。执行的示例可能包括从段中选择、插入、更新或删除数据，或者创建用户、表空间或数据文件。表 3.3 显示了与 SQL 语句处理执行阶段相关的 `TKPROF` 排序选项。

### 表 3.3 语句处理执行阶段的排序选项

| 选项 | 排序顺序 |

| :--- | :--- |

| EXECNT | 语句被执行次数 |

| EXECPU | 执行语句所消耗的 CPU 时间 |

| EXEELA | 执行语句所消耗的实际时间 |

| EXEDSK | 语句执行期间发生的磁盘读取次数 |

| EXECQRY | 语句执行期间从 SGA 读取的回滚缓冲区数量 |

| EXECU | 语句执行期间从 SGA 读取的数据缓冲区数量 |

| EXEROW | 语句执行期间处理的行数 |

| EXEMIS | 语句执行期间发生的库缓存未命中次数 |

如果发出的 SQL 语句是 `SELECT` 语句，它还将执行 SQL 语句处理的最后一步——获取（Fetch）操作。获取阶段发生在 SQL 语句返回的结果集发回给用户时。与 SQL 语句处理获取阶段相关的 `TKPROF` 排序选项如表 3.4 所示。

### 表 3.4 语句处理获取阶段的排序选项

| 选项 | 排序顺序 |

| :--- | :--- |

| FCHCNT | 发生的行获取次数 |

| FCHCPU | 获取行所消耗的 CPU 时间 |

| FCHELA | 获取行所消耗的实际时间 |

| FCHDSK | 获取行期间发生的磁盘读取次数 |

| FCHQRY | 获取行期间从 SGA 读取的回滚块数量 |

| FCHCU | 获取行期间从 SGA 读取的数据块数量 |

| FCHROW | 语句获取的行数 |

> 除了表 3.2、3.3 和 3.4 中显示的排序参数外，`TKPROF` 输出还可以使用 `USERID` 排序参数，按解析该语句的用户 ID 进行排序。

## 解释使用 TKPROF 格式化的跟踪文件

一旦使用 `TKPROF` 工具对用户跟踪文件进行格式化，结果文件的内容可以作为衡量 SQL 性能的绝佳指标。图 3.1 展示了一个使用 `TKPROF` 格式化的示例跟踪文件。

### 图 3.1 TKPROF 格式化跟踪文件的示例输出

```text
select /*+ rule */ bucket_cnt, row_cnt, cache_cnt, null_cnt, timestamp,
     sample_size, minimum, maximum, distcnt, lowval, hival, density, col,
     spare2, spare3, maxnum, where obj#=:1 and intcol#=:2
from hist_head

 call count cpu elapsed disk query current rows
------ ------ ------ ------ ------ ------ ------ ------
Parse 2 0.07 0.10 2 2 1 0
Execute 11 0.00 0.00 0 0 0 0
Fetch 11 0.00 0.00 2 22 0 11
total 24 0.07 0.11 4 58 1 11

Misses in library cache during parse: 1
Optimizer goal: RULE
Parsing user id: SYS (recursive depth: 1)
**********************************************************************
select employee_id, last_name, hire_date, job_id
from hr.employees
where salary > 15000

 call count cpu elapsed disk query current rows
------ ------ ------ ------ ------ ------ ------ ------
Parse 1 0.06 0.18 0 149 0 0
Execute 1 0.00 0.00 0 0 0 0
Fetch 2 0.00 0.03 3 3 2 3
total 4 0.06 0.22 3 152 2 3

Misses in library cache during parse: 1
Optimizer goal: CHOOSE
Parsing user id: 3
**********************************************************************
insert into hr.employees
(employee_id, last_name, email, hire_date, job_id)
values
(500, 'johnson', 'jjohnson@r.com', sysdate, 'AD_VP')

 call count cpu elapsed disk query current rows
------ ------ ------ ------ ------ ------ ------ ------
Parse 1 0.01 0.00 0 0 0 0
Execute 1 0.01 0.10 5 5 1 1
Fetch 0 0.00 0.00 0 0 0 0
total 2 0.02 0.11 5 1 1 1
```

![](img/832fbc6aca8b6075843ca6f2356c0a8d_133_0.png)

上述示例中显示的 CPU 和 Elapsed 计时仅当 `init.ora` 参数为 `TIMED_STATISTICS=TRUE` 时才为非零值。

查看上述跟踪文件时，您会注意到以下元素：

- 第一个列表是针对一个递归语句，该语句针对数据字典发出，以支持随后的 `SELECT` 语句。由于这种详细程度很少有用，可以在格式化期间使用 `SYS=NO` 选项，以从输出文件中消除这些类型的条目。
- 第二个列表是一个 `SELECT` 语句，包含解析、执行和获取阶段的信息。
- 第三个列表是一个 `INSERT` 语句，它不返回任何行（例如，Fetch），因此仅包含解析和执行阶段的信息。

表 3.5 显示了格式化 `TKPROF` 输出文件中每一列的描述。

### 表 3.5 TKPROF 输出描述

| 统计名称 | 统计描述 |

| :--- | :--- |

| Count | 解析、执行或获取阶段发生的次数 |

| CPU | CPU 处理该语句中所有解析、执行或获取调用所消耗的总秒数 |

| Elapsed | 处理该语句中所有解析、执行或获取调用所消耗的总秒数 |

| Disk | 该语句中解析、执行和获取调用期间从磁盘读取的数据块总数 |

| Query | 该语句中解析、执行和获取调用期间从 SGA 读取的回滚块（一致模式下的块）总数 |

| Current | 该语句中解析、执行和获取调用期间从 SGA 读取的数据块（当前模式下的块）总数 |

| Rows | 受执行阶段影响的行数（对于 `INSERT`、`UPDATE` 和 `DELETE` 语句），或受获取阶段影响的行数（对于 `SELECT` 语句） |

使用这些统计信息，您可以看到第二条语句被解析了一次，执行了一次，并执行了两次获取。此处理共消耗了 `.06` 秒的 CPU 时间，并且语句处理期间过去了 `.22` 秒。该语句需要从磁盘读取 3 个数据块，从 SGA 读取 152+2=154 个块，并返回了 3 行。

## 识别可能需要调优的语句

`TKPROF` 工具还会在输出文件的末尾以汇总形式显示这些统计信息。这些统计信息将提供递归和非递归语句的总体总计。

使用 `TKPROF` 的格式化输出，相对容易定位可能需要进一步调优的 SQL 语句。通常，你会寻找包含以下一个或多个缺点的语句：

- 消耗过多的 CPU 资源
- 解析、执行或获取花费时间过长
- 从磁盘读取过多的数据块，而从 SGA 读取的数据块过少
- 访问了大量数据块，但只返回了少量行

作为 `TKPROF` 工具的替代方案，OEM 诊断包中的 Top SQL 组件也可以用来识别表现出上述缺点的 SQL 语句。图 3.2 展示了 Top SQL GUI 工具输出示例。

### 图 3.2 Top SQL 的输出示例
