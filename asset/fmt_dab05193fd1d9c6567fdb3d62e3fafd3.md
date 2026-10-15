
D. FORCE ALL

E. FORCE ALL

### 问题 25

- 数据库管理员想要临时禁用任务中心。可以使用以下哪个来实现这一目标？

A. 为 `SHED_ENABLE` 变量赋值 `OFF`

B. 在数据库配置中将 `SHED_ENABLE` 设置为 `OFF`

C. 在 `TOOLSDB` 数据库配置中将 `SHED_ENABLE` 设置为 `OFF`

D. 在 `DAS` 配置中将 `SHED_ENABLE` 设置为 `OFF`

# 附录 B：示例测试

### 问题 26

- 以下活动无法通过自动维护执行？

A. 数据库备份

B. 快照

C. 统计收集和统计分析

D. 表索引重组

### 问题 27

- 数据库管理员需要创建一个 DB2 数据库，并在数据碎片化时自动执行离线表重组。实现此目标的最小步骤是？

A. 使用 `CREATE DATABASE` 创建数据库

B. 使用 `CREATE DATABASE` 创建数据库并将 `AUTO_MAINT` 配置参数设置为 `ON`

C. 使用 `CREATE DATABASE` 创建数据库并将 `AUTO_REORG` 配置参数设置为 `ON`

D. 使用 `CREATE DATABASE` 创建数据库，将 `AUTO_MAINT` 配置参数设置为 `ON`，并将 `AUTO_REORG` 配置参数设置为 `ON`

### 问题 28

`LIST UTILITIES` 命令返回了以下输出：

| ID = 1 |
| 类型 = BACKUP |
| 数据库名称 = SAMPLE |
| 分区号 = 0 |
| 说明 =离线 db |
| 开始时间 = 06/02/2007 10:35:31.442019 |
| 状态 = 执行中 |
| 调用类型 = 用户 |
| 节流: |
| 优先级 = 20 |
| 进度监控: = 46 |
| 预计百分比完成 = 49310404 字节 |
| 总工作 = 22696620 字节 |
| 完成工作 = 06/02/2007 10:35:31.466054 |

以下哪个命令允许备份操作在不受节流的情况下继续运行？

A. `SET UTIL_IMPACT_PRIORITY TO 0`

B. `SET UTIL_IMPACT_LIMIT TO 0`

C. `SET UTIL_IMPACT_PRIORITY TO 100`

D. `SET UTIL_IMPACT_LIMIT TO 100`

### 问题 29

随着数据库工作负载的变化，以下哪些内存消耗不能被自调内存管理器（Self-Tuning Memory Manager）自动调整？

A. 缓冲池 (`Buffer pools`)

B. 锁内存 (`Locking memory`)

C. 工具内存 (`Utility memory`)

D. 数据库共享内存 (`Database shared memory`)

### 问题 30

通知日志条目显示由名为 `sqlsize` 的函数生成的错误。函数名中的第四个字母表示什么？

A. 错误发生在缓冲区池管理/处理操作期间

B. 错误发生在数据管理操作期间

C. 错误发生在数据保护操作期间

D. 错误发生在排序操作期间

## 数据放置

Data Placement

# 问题 31

创建新的 DB2 9 数据库时，以下哪个功能不会自动启用？

A. 自动维护 (`Automatic maintenance`)

B. 自调优内存管理器 (`Self tuning memory manager`)

C. 数据行压缩 (`Data row compression`)

D. 工具节流 (`Utility throttling`)

# 722 附录 B：示例测试

# 问题 32

以下哪个不是有效的表空间状态？

- A. 待处理加载 (`Load pending`)
- B. 在线且不可访问 (`Online and not accessible`)
- C. 加载中 (`Load in progress`)
- D. 离线且不可访问 (`Offline and not accessible`)

# 问题 33

关于全局临时表（Global Temporary Tables），以下哪些说法是不正确的？

- A. 可以在全局临时表上创建索引
- B. 全局临时表位于用户临时表空间
- C. 可以在全局临时表上收集统计信息
- D. 全局临时表对所有连接到数据库的用户可见

# 问题 34

以下语句将创建一个名为 `PARTS` 的表，并进行分区，使得零件号在 0 到 33 范围内的行存储在一个位于一个表空间的分区中，零件号在 34 到 66 范围内的行存储在位于另一个表空间的分区中，零件号在 67 到 99 范围内的行存储在位于第三个表空间的第三分区中？

- A. `CREATE TABLE parts (partno INT, desc VARCHAR(25))`

`IN tsp0, tsp1, tsp2`

`PARTITION BY (partno NULLS FIRST)`

`(STARTING 0 ENDING 33,`

`STARTING 34 ENDING 66,`

`STARTING 67 ENDING 99)`

- B. `CREATE TABLE parts (partno INT, desc VARCHAR(25))`

`PARTITION BY (partno STARTING 0 ENDING 33,`

`(part part0 STARTING 0 ENDING 33,`

`part part1 STARTING 34 ENDING 66,`

`part part2 STARTING 67 ENDING 99)`

- C. `CREATE TABLE parts (partno INT, desc VARCHAR(25))`

`PARTITION BY (partno NULLS FIRST)`

`(STARTING 0 ENDING 33,`

`STARTING 34 ENDING 66,`

`STARTING 67 ENDING 99)`

`IN tbsp0, tbsp1, tbsp2`

- D. `CREATE TABLE parts (partno INT, desc VARCHAR(25))`

`PARTITION BY (partno NULLS FIRST)`

`(STARTING 0 ENDING 33 IN tbsp0,`

`STARTING 34 ENDING 66 IN tbsp1,`

`STARTING 67 ENDING 99 IN tbsp2)`

# 问题 35

以下两个工具可以用于创建压缩字典？

A. `reorg`

B. `db2pd`

C. `inspect`

D. `runstats`

E. `db2buildcd`

# 问题 36

服务器上存在一个名为 `DB2INST1` 的实例，该实例的 `DFTD8PATH` 数据库管理器配置参数包含值 `"home"`。

如果服务器上不存在任何数据库并且执行了以下命令：

`CREATE DATABASE my_db`

数据库的元数据文件将位于何处？

A. 在 `/home/NODE0000/SQL00001` 子目录下

B. 在 `/home/DB2INST1/NODE0000/SQL00001` 子目录下

C. 在 `/home/NODE0000/MY_DB` 子目录下

D. 在 `/home/DB2INST1/NODE0000/MY_DB` 子目录下

# 724 附录 B：示例测试

# 问题 37

如果执行以下 `CREATE TABLESPACE` ：

```sql
CREATE REGULAR TABLESPACE sales_ts
PAGESIZE 4096
MANAGED BY DATABASE USING
(FILE: 'D:\tblsp1.tsf' 10 G, FILE: 'D:\tblsp2.tsf' 6 G, FILE
'D:\tblsp3.tsf' 4 G)
EXTSIZE 32
PREFETCHSIZE 96
```

`SALES_TS` 表空间可以存储的最大数据量是多少？

A. 10 GB

B. 12 GB

C. 16 GB

D. 20 GB

# 问题 38

以下两个命令可以用于获取名为 `SALES` 的数据库创建的所有表空间的详细信息（包括状态）？

A. `SELECT * FROM syscat.tablespaces`

B. `LIST TABLESPACE SHOW DETAIL`

C. `LIST TABLESPACE CONTAINERS SHOW DETAIL`

D. `GET SNAPSHOT FOR TABLESPACE ON sales`

E. `GET SNAPSHOT FOR TABLESPACE`

# 问题 39

关于 `schema`，以下哪些说法是不正确的？

A. 连接到数据库后

B. 像表空间一样 `schemas` 会增长

C. 如果显式创建 `schema`

D. `schema` 的所有权可以授予

## 数据放置

Data Placement

75 # 问题 40

为了使用行压缩 `table`，以下哪个必须存在？

A. `index`

B. `dictionary`

C. `user-defined`

D. `columns`

# 问题 41
