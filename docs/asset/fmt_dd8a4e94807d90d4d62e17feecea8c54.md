
  `D. INSERT INTO products (prodid, category, description, quantity, sellprice, buyprice) VALUES (2, '615', 'dark blue socks', 3, 20.00, 25.65)`

## 问题 69

给出 `CREATE TABLE` 语句：

```
CREATE TABLE employee
  (empid INTEGER NOT NULL,
  lname VARCHAR(20),
  gender CHAR(1) NOT NULL,
  CONSTRAINT gender_ok CHECK (gender IN ('M', 'F')) ENFORCED
  ENABLE QUERY OPTIMIZATION)
```

以及以下 `INSERT` 语句：

```
INSERT INTO employee VALUES (1, 'Smith', 'M'), (2, 'Doe', 'F'), (3, 'Jones', 'U')
```

以下哪个查询将返回空结果集？

- A. `SELECT COUNT(gender) FROM employee`
- B. `SELECT * FROM employee WHERE gender = 'M'`
- C. `SELECT * FROM employee WHERE gender = 'F'`
- D. `SELECT * FROM employee WHERE gender = 'U'`

## 问题 70

以下对象中哪个不能通过控制中心（Control Center）创建？

- A. 缓冲池（Buffer pool）
- B. 事件监控器（Event monitor）
- C. 触发器（Trigger）
- D. 用户定义函数（User-defined function）

## 问题 71

使用工具设置（Tools Settings）笔记本无法执行以下哪项操作？

- A. 定义复制环境。
- B. 修改用于显示文本和菜单选项的 C1 字体。
- C. 设置默认调度方案。
- D. 配置健康状态信标（Health Status Beacons）。

## 问题 72

以下哪两项是 DB2 支持的有效索引？

- A. 空间网格索引（Spatial grid indexes）
- B. 静态位图索引（Static bitmap indexes）
- C. 动态位图索引（Dynamic bitmap indexes）
- D. 基于页的索引（Page-based indexes）
- E. 多维范围聚集索引（Multidimensional range-clustered indexes）

## 问题 73

给出 `CREATE TABLE` 语句：

```
CREATE TABLE tab1
  c1 SMALLINT,
  c2 CHAR(4))
```

`TAB1` 被两个应用程序频繁访问；一个应用程序按升序返回 `C1` 列的数据，另一个应用程序按降序返回 `C1` 列的数据。为了提高性能，数据库管理员执行了以下命令：

```
CREATE INDEX idx1 ON tab1(c1 ASC);
CREATE INDEX idx2 ON tab1(c1 DESC);
```

### 附录 B：示例测试

以下会发生哪种情况？

- A. 将创建索引 `INDEX1`，第一个应用程序在检索数据时将使用它；将创建索引 `INDEX2`，第二个应用程序在检索数据时将使用它。
- B. 将创建索引 `INDEX1`。当尝试创建索引 `INDEX2` 时，`DB2` 将修改索引 `INDEX1` 以允许反向扫描，两个应用程序在检索数据时将使用索引 `INDEX1`。
- C. 将创建索引 `INDEX1`。当尝试创建索引 `INDEX2` 时，`DB2` 将修改索引 `INDEX1` 以允许反向扫描并删除索引 `INDEX1`；两个应用程序在检索数据时将使用索引 `INDEX2`。
- D. 将创建索引 `INDEX1` 并默认允许反向扫描。当尝试创建索引 `INDEX2` 时，`DB2` 将发布重复消息。两个应用程序在检索数据时将使用索引 `INDEX1`。

## 问题 74

以下哪项最能描述 `dbls` 的功能？

- A. 它检索服务器信息。
- B. 它限制访问用户。
- C. 它返回已安装的服务器列表。
- D. 它返回数据库的位置。

## 分析 DB2 活动

## 问题 75

用户执行了以下命令：

```
UPDATE DBG USING SORT ON;
UPDATE SWITCHES USING UOW ON;
UPDATE DBG USING TIMESTAMP ON;
UPDATE BUFFERPOOL ON;
```

假设没有设置其他开关，如果数据库重启，以下哪项将？

- A. `UOW`
- B. `BUFFERPOOL`
- C. `SORT`
- D. `TIMESTAMP`

## 问题 76

以下哪项可以用于从命令行（CLP）捕快照数据？

- A. `EXPLAIN FOR ALL`
- B. `SET CURRENT EXPLAIN`
- C. `SET CURRENT EXPLAIN SNAPSHOT`
- D. `EXPLAIN`

## 问题 77

数据库管理员与 `SAMPLE` 交互时执行了以下操作，并收到以下输出：

| 数据库名称 | SAMPLE |
| :--- | :--- |
| 序列号 | 0001 |
| 连接 | DB2 |
| 授权 ID | DBUSER |
| 当前连接代理 | 1 |
| 持有的锁 | 0 |
| 总时间 | 未收集 |
| 时间戳 | 05/14 18:57 |

为什么总时间返回的值为“未收集”？

- A. 在快照之前执行了 `RESET` 命令。
- B. `LOCK` 开关关闭。
- C. 此时没有持有任何锁。
- D. `UOW` 开关关闭。

## 问题 78

关于事件监控器，以下哪项是不正确的？

- A. 可以定义无限数量的事件监控器。
- B. 事件监控器在收集数据之前必须激活。
- C. 同时可以激活 16 个事件监控器。
- D. 活动的在删除之前必须停止。

## 问题 79

如果 `OLTP` 环境中的查询根据主键连接两个表，Visual Explain 生成的访问计划中哪个操作符最可能表示这种连接？

- A. `HSJOIN`
- B. `MSJOIN`
- C. `NLJOIN`
- D. `SJOIN`

## 分析 DB2 活动

## 问题 80

以下哪项可以用于显示创建绑定文件时使用的编译选项？

- A. `db2advis`
- B. `db2bfd`
- C. `dbmtrk`
- D. `db2bind`

## 问题 81

关于 `DB2` 问题诊断工具 (`db2pd`)，以下哪种陈述是不不正确的？

- A. `db2pd` 用于从 `DB2` 系统集中获取快速直接的信息。
- B. `db2pd` 不需要连接活动数据库即可获取其信息。
- C. `db2pd` 可用于获取意外停止的实例信息。
- D. 由于 `db2pd` 直接与内存交互，因此可以检索在收集过程中发生的信息。

## 问题 82

`RESET MONITOR` 命令的作用是什么？

- A. 重置所有快照监控计数为零。
- B. 重置单个快照监控计数为零。
- C. 关闭所有快照监控开关。
- D. 关闭除 `TIMESTAMP` 以外所有快照监控开关。

## 问题 83

一个包含两个嵌入动态 `SQL` 语句的应用程序已绑定到数据库。以下哪项可以捕获应用程序中两个语句的解释信息，并可以使用 Visual Explain 进行检查？

- A. `EXANSNAP ALL AND SET CURRENT EXPLAIN MODE EXPLAIN`
- B. `EXPLAIN ALL AND SET CURRENT EXPLAIN SNAPSHOT ALL`
- C. `EXPLSNAP NO AND SET CURRENT EXPLAIN SNAPSHOT YES`
- D. `EXPLAIN NO AND SET CURRENT EXPLAIN MODE YES`

### 附录 B：示例测试

## 问题 84

名为 `SAMPLE` 的数据库包含一个跨越五个文件的 `DMS` 表空间。其中三个文件的大小为 4 GB，另外两个文件的大小为 3 GB。数据库管理员希望在 3 GB 文件填充 80% 且 4 GB 文件填充 85% 时都能收到警报。使用健康中心（Health Center）实现此用点的最佳方法是什么？

- A. 修改所有表空间容器的全局（Global）级设置；修改 3 GB 表空间容器的实例（Instance）级设置。
- B. 修改所有表空间容器的实例（Instance）级设置；修改 3 GB 表空间容器的全局（Global）级设置。
- C. 修改所有表空间容器的全局（Global）级设置；修改 4 GB 表空间容器的对象（Object）级设置。
- D. 修改所有表空间容器的实例（Instance）级设置；修改 4 GB 表空间容器的对象（Object）级设置。

## 问题 85
