
$ tkprof ora_1253.txt trace.txt

```
此示例将格式化名为 `ora_1253.txt` 的跟踪文件，并将格式化后的版本存储在名为 `trace.txt` 的文件中。如示例所示，`TKPROF` 命令后的前两个参数分别是跟踪文件和输出文件。`TKPROF` 工具具有

## 第 3 章 • SQL 应用程序调优与设计

在格式化跟踪文件时，还可以使用几个额外的命令行参数，取决于所需的信息。这些选项紧跟在要求的跟踪文件名和输出文件名参数之后在命令行上指定。表 3.1 显示了这些选项。

### 表 3.1 TKPROF 命令行选项

| 选项 | 定义与用法 |
| --- | --- |
| EXPLAIN | 使用此命令指定的模式下的 `PLAN_TABLE` 为跟踪文件中的每个语句生成执行计划。此选项必须包含有效的 Oracle 用户名和密码。 |
| TABLE | 使用 `EXPLAIN` 执行计划指定的模式，将结果存储在指定的表中而不是默认表 `PLAN_TABLE`。 |
| SYS | 指明格式化后的跟踪文件应包含递归 SQL 语句（即为了支持主 SQL 语句而隐式向数据字典发布的语句）。 |
| SORT | 确定格式化跟踪文件中语句的排序顺序。22 种排序选项列在表 3.2、3.3 和 3.4 中。 |
| RECORD | 指定跟踪文件中的 SQL 语句应写入的文件名。允许你在不带任何相关资源使用信息的情况下隔离 SQL 语句。将省略递归 SQL。 |
| PRINT | 将生成的格式化跟踪文件中所包含的 SQL 语句数量限制为指定值。 |
| INSERT | 创建一个 SQL 脚本，执行该脚本时将创建一个名为 `TKPROF_TABLE` 的表，然后用此跟踪文件中包含的原始统计数据填充该表。 |

### 表 3.1 TKPROF 命令行选项（续）

| 选项 | 定义与用法 |
|---|---|
| AGGREGATE | 决定来自同一 SQL 语句的多个发布者的统计信息是合并计数还是独立计数。 |
| WAITS | 计算跟踪过程中发生的等待事件的摘要统计信息。等待事件在第 9 章“调优争用”中进行了讨论。 |

下面显示了使用这些选项配合 `TKPROF` 的几个示例。
以下演示了在 Unix 系统上使用 `SYS` 和 `EXPLAIN` 参数使用 `TKPROF`：

```
$ tkprof ora_1234.trc trace.txt=no explain=joe/sidney@PROD
```

此 `TKPROF` 的使用方法将：

- 格式化跟踪文件 `ora_1234.trc` 并将结果存储在名为 `trace.txt` 的输出文件中。
- 导致原始跟踪文件中的递归 SQL 从格式化后的跟踪文件 `trace.txt` 中省略。
- 在格式化后的跟踪文件 `trace.txt` 中，发布每个 SQL 语句的执行计划。`PROD` 数据库中用户 `Joe` 模式下的 `PLAN_TABLE` 将用于生成执行计划。

以下演示了在 Windows 系统上使用 `RECORD` 和 `PRINT` 参数使用 `TKPROF`：

```
C:\ tkprof ora0740.trc trace.txt print=10 record=sql.txt
```

此 `TKPROF` 工具的使用将：

- 格式化跟踪文件 `ora0740.trc` 并将前 10 条 SQL 语句存储在输出文件 `trace.txt` 中。
- 创建 `sql.txt` 文件，其中包含原始跟踪文件的前十条 SQL 语句。

以下演示了在 Unix 系统上使用 `INSERT` 和 `SORT` 参数使用 `TKPROF`：

```
$ tkprof ora1702.trc trace.txt insert=trace.sql sort=(fchrow)
```

### 第 3 章 · SQL 应用程序调优与设计

此 `TKPROF` 工具的使用将：

- 格式化 `.trc` 文件并将结果存储在 `trace.txt` 中。其他 `TKPROF` 排序选项的讨论将在下一节出现。
- 创建第二个文件 `trace.sql`，其中包含创建 `TKPROF_TABLE` 表并填充其统计数据的 SQL 命令。

如果没有像 `FCHROW` 这样的排序参数，`TKPROF` 工具将按照执行顺序在格式化输出列出 SQL 语句。当不需要这种默认顺序时，`TKPROF` 有额外的排序参数。格式化后的输出将根据你指定的选项进行降序排序。可以同时使用多个排序参数。在这种情况下，排序后的输出将根据指定的顺序进行排序，但基于排序选项值的总和。

#### TKPROF 排序参数

每个参数都与 SQL 语句处理的三个阶段之一：解析（Parse）、执行（Execute）或提取（Fetch）。解析是指让 SQL 语句准备好执行的过程。该过程包括检查语句的语法正确性并确定用户对引用的对象的权限。与 SQL 语句解析阶段相关的 `TKPROF` 排序选项如表 3.2 所示。

| 选项 | 排序顺序 |
| --- | --- |
| PRSCNT | 语句解析的次数 |
| PRCPU | 解析语句消耗的 CPU 时间 |
| PRSELA | 解析语句消耗的流逝时间 |
| PRDSK | 解析语句期间发生的磁盘读取次数 |
| PRMSIS | 解析语句期间的库缓存缺失次数 |

### 表 3.2 语句处理解析阶段的排序选项（续）

| 选项 | 排序依据 |
| --- | --- |
| PRSCU | 语句解析期间从 SGA 读取的数据缓冲区或索引缓冲区数量 |
| PRSQRY | 语句解析期间从 SGA 读取的回滚缓冲区（rollback buffers）数量 |

SQL 语句处理的第二步——*执行（Execute）*——发生在 SQL 语句执行其在语句中所指定的操作时。执行的示例可能包括从段（segment）中选择、插入、更新或删除数据，或者创建用户、表空间或数据文件。表 3.3 显示了与 SQL 语句处理执行阶段相关的 `TKPROF` 排序选项。

### 表 3.3 语句处理执行阶段的排序选项

| 选项 | 排序依据 |
| --- | --- |
| EXCNT | 语句执行的次数 |
| EXECCPU | 执行语句消耗的 CPU 时间 |
| EXEELA | 执行语句消耗的经过（时间 |
| EXEDSK | 语句执行期间发生的磁盘读取次数 |
| EXECQRY | 语句执行期间从 SGA 读取的回滚缓冲区数量 |
| EXECU | 语句执行期间从 SGA 读取的数据缓冲区数量 |
| EXEROW | 语句执行期间处理的行数 |
| EXEMIS | 语句执行期间发生库缓存缺失（Library cache misses）次数 |

### 第 3 章 • SQL 应用程序调优与设计

如果发布的 SQL 语句是 `SELECT` 语句，它还将执行 SQL 语句处理的最后一步——取回（Fetch）操作。取回阶段发生在 SQL 语句返回的结果发送回用户时。表 3.4 显示了与 SQL 语句处理取回阶段相关的 `TKPROF` 排序选项。

### 表 3.4 语句处理取回阶段的排序选项

| 选项 | 排序依据 |
| --- | --- |
| FCHCNT | 发生的取次数 |
| FCPU | 取行消耗的 CPU 时间 |
| FCHELA | 取行消耗的经过时间 |
| FCHDSK | 行取回期间发生的磁盘读取次数 |
| FQRY | 行取回期间从 SGA 读取的回滚块数量 |
| FCHCU | 行取回期间从 SGA 读取的数据块数量 |
| FCHROW | 语句取回的行数 |

除了表 3.2、3.3 和 3.4 中所示排序参数外，还可以使用 `USERID` 排序参数根据解析该语句的用户 ID 对 `TKPROF` 输出进行排序。

### 解析使用 TKPROF 格式化的跟踪文件

一旦使用 `TKPROF` 工具对跟踪文件进行了格式化处理，生成的文件内容就可以作为衡量 SQL 性能的极佳标准。图 3.1 显示了一个用 `TKPROF` 格式化的示例跟踪文件。

#### 3.1 使用 TKPROF 格式化跟踪文件的示例输出

```
select* rule / bucket_cnt, row_cnt, cache_cnt, null_cnt, timestamp;

sample_size, minimum, maximum, distcnt, lowwal, hival, density, col;

sphere, sparea, agcvnl

from hist_heads where objid!=1 and intype=2
```
