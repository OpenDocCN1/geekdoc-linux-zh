
```sql
CREATE SEQUENCE CUSTOMER_NO AS INTEGER
```

图 7–74 客户序列

默认情况下，该序列从 1 开始，每次递增 1，数据类型为整数。应用程序需要使用 `NEXTVAL` 函数获取序列中的下一个值。该函数生成序列的下一个值，然后可以用于后续的 SQL 语句（图 7–75）：

```sql
VALUES NEXTVAL FOR CUSTOMER_NO
```

图 7–75 客户序列

与其在 `VALUES` 函数中生成下一个数字，程序员可以在 `INSERT` 语句中使用该函数。例如，如果客户表的第一列包含客户号，则可以这样编写 `INSERT` 语句（图 7–76）：

```sql
INSERT INTO CUSTOMERS VALUE
(NEXTVAL FOR CUSTOM_NO, 'Berts House of Moving', ...)
```

图 7–76 插入值

多年来一直在开发这些功能。以下 SQL 计算凸显了小数数学运算的问题（图 7–78）：

```sql
VALUES 1234567890.000000 * 1234567890.000000
SQL0802N Arithmetic overflow or other arithmetic exception occurred. SQLSTATE=22003
```

**图 7–78** 大数相法

如果计算中不包含小数部分，DB2 将返回一个有效结果（图 7–79）：

```sql
VALUES 1234567890.0 * 1234567890.0
---------------------------------
1
1524157875019052100.00
```

**图 7–79** 成功相法

这种异常行为由于小数数学的规则导致。使用小数数学的计算采用以下规则来确定有效数字和小位数，其中 $p$ 是数字的位置，$s$ 是标度：

- 精度 = min(31, p¹⁺+p²)
- 标度 = min(31, s¹⁺+s²)

在我们第一个示例中，两个数字的精度都是 17.7（17 位有效数字，带有 7 位小数）。该规则告诉我们，最终结果应该包含 (31, 17+17) = 31 位精度，以及至少 (3, 7+7) = 14 位标度（小数点后的数字）。如果我们将标度设为 14 位，将只给有效部分留下了 17 位数字。该图（图 7–79）包含 19 位有效数字，因此该数字无法放入数值字段中。解决此问题的唯一方法是将值强制转换为浮点数，但这可能导致精度丢失。

小数相乘的替代方法是在 DB2 UDB 7.2 版本中引入的。不再使用标准的乘法运算符，而是可以使用 `MULTIPLY_ALT` 函数来保持有效数字精度并限制小数部分的数字位数。图 7–78 中的原始计算现在可以使用此新函数完成（图 7–80）：

```sql
VALUES MULTIPLY_ALT(1234567890.0000000,1234567890.0000000)
1
---------------------------------------------
1524157875019052100.0000000000
```

**图 7–80** 使用 Multiply_Alt 成功相法

数字的小数部分被截断，标度被减小以容纳更多的有效数字。对于任何标度可能导致算术溢出的小数相法，都应该考虑此函数。

## SNAPSHOT 表函数

DB2 拥有许多表函数，可以返回内部对象的数据，而这些对象通常只能通过 API 调用访问。使用 SQL 获取这些信息的优势在于，编写脚本来提取这些信息，而不是编写 C++ 程序来完成相同的功能。此外，Java 开发者也可以利用这些 SQL 调用，而不是将 C 程链接到他们的应用程序中。

这些快照函数返回 DB2 内部各种对象的信息（表 7–1）：

**表 7–1** 快照函数

| 函数 | 目的 |
| --- | --- |
| `SNAPSHOT_AGENT` | `SNAPSHOT_AGENT` 函数返回来自应用程序快照的代理信息。 |
| `SNAPSHOT_APPL` | `SNAPSHOT_APPL` 函数返回来自应用程序快照的通用信息。 |
| `SNAPSHOT_APPL_INFO` | `SNAPSHOT_APPL_INFO` 函数返回来自应用程序快照的通用信息。 |
| `SNAPSHOT_BP` | `SNAPSHOT_BP` 函数返回来自缓冲池快照的信息。 |
| `SNAPSHOT_CONTAINER` | `SNAPSHOT_CONTAINER` 函数返回表空间快照的容器配置信息。 |
| `SNAPSHOT_DATABASE` | `SNAPSHOT_DATABASE` 函数返回数据库快照的信息。 |

## 第 7 章 高级 SQL

| 函数 | 目的 |
| --- | --- |
| `SNAPSHOT_DBM` | `SNAPSHOT_DBM` 函数返回 DB2 数据库管理器快照的信息。 |
| `SNAPSHOT_DYN_SQL` | `SNAPSHOT_DYN_SQL` 函数返回动态 SQL 快照的信息。它取代了 `SQLCACHE_SNAPSHOT` 函数，后者出于兼容性考虑仍然可用。 |
| `SNAP_FCM` | `SNAPSHOT_FCM` 函数返回关于数据库管理器级的快速通信管理器 (FCM) 信息。 |
| `SNAPSHOT_FCMPARTITION` | `SNAPSHOT_FCMPARTITION` 函数返回数据库管理器中快速通信管理器快照的信息。 |
| `SNAPSHOT_LOCK` | `SNAPSHOT_LOCK` 函数返回锁快照的信息。 |
| `SNAPSHOT_LOCKWAIT` | `SNAPSHOT_LOCKWAIT` 函数返回应用程序快照中的锁等待信息。 |
| `SNAPSHOT_QUIESCERS` | `SNAPSHOT_QUIESCERS` 函数返回试图静止数据库的代理信息。 |
| `SNAPSHOT_RANGES` | `SNAPSHOT_RANGES` 函数返回范围快照的信息。 |
| `SNAPSHOT_STATEMENT` | `SNAPSHOT_STATEMENT` 函数返回语句快照的信息。 |
| `SNAPSHOT_SUBSET` | `SNAPSHOT_SUBSET` 函数返回子集快照的信息。 |
| `SNAPSHOT_SWITCHES` | `SNAPSHOT_SWITCHES` 函数返回切换快照的信息。 |
| `SNAPSHOT_TABLE` | `SNAPSHOT_TABLE` 函数返回表快照的信息。 |
| `SNAPSHOT_TBS` | `SNAPSHOT_TBS` 函数返回 TBS 快照的信息。 |
| `SNAPSHOT_TBS_CFG` | `SNAPSHOT_TBS_CFG` 函数返回配置快照的信息。 |
| `SQLCACHE_SNAPSHOT` | `SQLCACHE_SNAPSHOT` 函数返回缓存快照的信息。 |

# XML 函数

DB2 在多个版本中都已支持 XML 结构。这些函数允许开发者从 DB2 数据库中存储和检索 XML 信息。

在 SQL 语言中，支持多种 XML 函数，允许以 XML 格式对数据进行格式化。这些函数在表（7–3）中进行了描述：

| 函数 | 用途 |
|---|---|
| `XML2CLOB` | `XML2CLOB` 函数将参数作为 CLOB 值返回。参数必须是数据类型为 XML 的表达式。结果为 CLOB 类型。 |
| `XMLLAGG` | `XMLAGG` 函数返回一组 XML 数据的拼接。如果将 `XMLAGG` 函数应用于空集，则结果为空值。否则，结果是集合中值的拼接。 |
| `XMLELEMENT` | 根据参数构造 XML 元素。此函数接受一个元素名称、一个可选的属性集合，以及零或多个构成元素内容的参数：结果数据类型为 XML。 |
