
还有设计顾问向导的 GUI 版本（称为设计顾问向导）。可以通过在控制 Center 的数据库菜单项中选择适当的操作来激活设计顾问向导。图 6–20 显示了为了激活设计顾问向导必须选择的 Control Center 菜单项；图 6–21 显示了设计顾问向导在激活后典型的第一页界面。

# 其他工具

![](img/7bc9d5f6e46add86bfa073e2146c4fd4_546_0.png)

图 6-20：从 Control Center 启动设计顾问向导。

# 第 6 章：DB2工具

![](img/7bc9d5f6e46add86bfa073e2146c4fd4_547_0.png)

图 6-21：设计顾问向导的第一页。

## 练习题

# 题 1

下列哪项不是调用 `Export` 工具的方法？

- A. `Control Center`
- B. 命令行处理器
- C. `ADMIN_CMD` 存储过程
- D. 复制中心

# 题 2

下列哪个 `IMPORT` 命令选项会导致 Import 工具在每次提交后获取表级锁锁？

- A. `ALLOW NO ACCESS`
- B. `ALLOW READ ACCESS`
- C. `ALLOW WRITE ACCESS`
- D. `ALLOW FULL ACCESS`

# 题 3

对于包含被另一个表的外键引用的主键的表，执行哪些操作是不允许的？

- A. `IMPORT ... INSERT`
- B. `IMPORT ... REPLACE`
- C. `IMPORT ... INSERT_UPDATE`
- D. `IMPORT ... CREATE`

# 题 4

下列哪个 `IMPORT` 命令选项可以防止导入操作填满数据库事务日志文件并失败？

- A. `ALLOW NO ACCESS`
- B. `TIMEOUT`
- C. `COMMITCOUNT AUTOMATIC`
- D. `ALLOW WRITE ACCESS`

# 第 6 章：DB2工具

# 题 5

在处理标识列数据时，可以使用下列哪个 `LOAD` 命令修符？

- A. `IDENTITYRESET`
- B. `IDENTITYOVERRIDE`
- C. `IDENTITYSUPRESS`
- D. `IDENTITYRETAIN`

# 题 6

一个数据库管理员想要删除名为 `DEPARTMENT` 的表中的所有记录，该表位于一个数据库中。下列哪个命令可以实现此目标？

- A. `LOAD FROM NULL INTO department`
- B. `LOAD FROM NULL REPLACE INTO department`
- C. `LOAD FROM NULL INTO department`
- D. `LOAD FROM NULL REPLACE INTO department`

# 题 7

给定以下命令：

```
LOAD FROM sales.del INTO sales
ALLOW READ ACCESS
STATISTICS PROFILE
```

下列哪项是错误的？

- A. 在加载期间，将收集统计信息并更新相关索引。
- B. 加载之前的 `SALES` 表数据可以被读取。
- C. 加载优先级是字符分隔符。
- D. 如果加载中止，表将是可用的。

# 题 8

使用哪个命令可以显示加载状态？

- A. `STATUS`
- B. `MESSAGES`
- C. `QUERY`
- D. `STATISTICS`

# 题 9

表 `EMPLOYEES` 是通过以下命令创建的：

```sql
CREATE TABLE employees (empid INTEGER NOT NULL PRIMARY KEY, name VARCHAR(25))
```

假设 `EMPDATA.DEL` 包含以下数据：

100, "Kim Moutsos"

200, "Dwane Snow"

300, "Rebecca Bond"

400, "Paul Gunning"

执行以下命令：

```sql
CREATE TABLE emp_exp LIKE EMPLOYEES;
LOAD FROM empdata.del INTO emp_exp;
```

下列哪种说法是正确的？

- A. `EMPLOYEES` 将包含四行；`emp_exp` 将为空。
- B. `EMPLOYEES` 将包含五行。
- C. 表将包含四行；`emp_exp` 将包含一行。
- D. `EMPLOYEES` 将包含五行；`emp_exp` 将包含一行。

# 第 6 章：DB2工具

# 题 10

在下列哪些场景中应该使用 `load` 工具而不是 `import` 工具？

- A. 需要向表中添加数据并触发任何触发器。
- B. 需要向表中添加大量数据而不产生大量的日志。
- C. 需要将工作表（WSF）格式的文件的数据添加到表中。
- D. 需要向表中添加大量数据并在填充期间强制约束检查。

# 题 11

可以使用哪些步骤来构建一个与生产数据库结构和统计信息相同但数据较少的测试数据库？

- A. 1) 使用 `db2move` 工具（导出模式）提取生产数据库的数据。2) 使用 `db2move` 工具（导入模式）填充测试数据库。
- B. 1) 使用 `db2look` 工具生成生产数据库对象的 SQL。2) 创建测试数据库并运行 `db2look` 生成的脚本创建数据库对象。3) 使用 `db2move` 工具（导出模式）提取生产数据库的数据。4) 使用 `db2move` 工具（导入模式）填充测试数据库。
- C. 1) 在测试数据库的每个表上运行 `RUNSTATS` 工具。2) 使用 `db2look` 工具生成生产数据库对象的 SQL 并复制统计配置文件。3) 创建测试数据库并运行 `db2look` 生成的脚本创建数据库对象并复制统计信息。4) 插入、导入或加载测试数据到数据库中。
- D. 1) 使用 `db2look` 工具生成生产数据库对象的 SQL。2) 创建测试数据库并运行 `db2look` 生成的脚本创建数据库对象。3) 使用 `LOAD` 命令并指定 `STATISTICS PROFILE` 选项将测试数据加载到数据库，以便收集统计信息。

## 问题 12

- 以下哪项任务最适合使用 `db2batch` 实用？

- A. 对 SQL 和 XQuery 操作进行基准测试。
- B. 将单个架构下创建的50个表从一个数据库复制到另一个数据库。
- C. 重组表数据并对其进行聚集。
- D. 更新存储在包中的访问计划信息。

## 问题 13

- 为了提高查询性能，数据库管理员为名为 `EMPLOYEE` 的表创建了一个索引，该表包含 500,000 条记录。针对 `EMPLOYEE` 表运行的即时查询性能有所提高，但夜间运行的批处理应用程序的性能却没有提高。以下哪种操作可以解决这个问题？

- A. `REORGCHK`
- B. `REORG`
- C. `FLUSH PACKAGE CACHE`
- D. `REBIND`

## 问题 14

- 下列哪项图说明了可用的 DB2 数据管理工具的正确使用顺序？

- A. `RUNSTATS`, `REORG table`, `REORG indexes`, `REORGCHK`, `REBIND`
- B. `RUNSTATS`, `REORGCHK`, `REORG table`, `REORG indexes`, `RUNSTATS`, `REBIND`
- C. `REORGCHK`, `REORG indexes`, `REORG table`, `RUNSTATS`, `REBIND`
- D. `RUNSTATS`, `REBIND`, `REORGCHK`, `REORG table`, `REORG indexes`, `RUNSTATS`

## 问题 15

- 下列哪个命令调用了设计顾问（Design Advisor）并根据快照监控收集的信息为名为 `SAMPLE` 的数据库提供建议？

- A. `db2advis -d SAMPLE -k`
- B. `db2advis -d SAMPLE -qp`
- C. `db2advis -d SAMPLE -g`
- D. `db2advis -d SAMPLE -h`

## 问题 16

设计顾问（Design Advisor）可以分析来自以下哪内容的 SQL？

- A. `EXPLAIN_STATEMENT` 表
- B. 包含工作负载的文件
- C. `SYSIBM.SYSPLANS` 系统目录表
- D. `EXPLAIN_STREAM` 表
- E. `ADVISE_WORKLOAD` 表

## 答案

### 问题 1
