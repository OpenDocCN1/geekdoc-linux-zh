
| 02 | SKY | 2 |

| 03 | SCHOOL BUS | 3 |

| 04 | COAL | 4 |

图 4-12：引用约束的 ON DELETE SET NULL 删除规则的执行方式。

```sql
CREATE TABLE color
(c_id INTEGER
NOT NULL PRIMARY KEY,
c_desc CHAR(20))
```

```sql
CREATE TABLE object
(o_id CHAR(2),
  o_desc CHAR(20),
  c_id INTEGER
REFERENCES COLOR (c_id)
ON DELETE RESTRICT)
```

### COLOR 表

| C_ID | C_DESC |

|---|---|

| 1 | RED/ROJO |

| 2 | BLUE/AZUL |

| 3 | YELLOW/AMARILLO |

| 4 | BLACK/NEGRO |

| 5 | WHITE/BLANCO |

### OBJECT 表

| O_ID | O_DESC | C_ID |

|---|---|---|

| 01 | STOP SIGN | 1 |

| 02 | SKY | 2 |

| 03 | SCHOOL BUS | 3 |

| 04 | COAL | 4 |

主键

外键

### 删除操作（父表）

```sql
DELETE FROM color WHERE c_id = 2
```

违反 ON DELETE RESTRICT 规则，删除操作失败

### COLOR 表

| C_ID | C_DESC |

|---|---|

| 1 | RED/ROJO |

| 2 | BLUE/AZUL |

| 3 | YELLOW/AMARILLO |

| 4 | BLACK/NEGRO |

| 5 | WHITE/BLANCO |

### OBJECT 表

| O_ID | O_DESC | C_ID |

|---|---|---|

| 01 | STOP SIGN | 1 |

| 02 | SKY | 2 |

| 03 | SCHOOL BUS | 3 |

| 04 | COAL | 4 |

图 4-13：引用约束的 ON DELETE RESTRICT 删除规则的执行方式。

```sql
CREATE TABLE color
(c_id INTEGER
NOT NULL PRIMARY KEY,
c_desc CHAR(20))
```

```sql
CREATE TABLE object
(o_id CHAR(2),
  o_desc CHAR(20),
  c_id INTEGER
REFERENCES COLOR (c_id)
ON NO ACTION)
```

### COLOR 表

| C_ID | C_DESC |

|---|---|

| 1 | RED/ROJO |

| 2 | BLUE/AZUL |

| 3 | YELLOW/AMARILLO |

| 4 | BLACK/NEGRO |

| 5 | WHITE/BLANCO |

### OBJECT 表

| O_ID | O_DESC | C_ID |

|---|---|---|

| 01 | STOP SIGN | 1 |

| 02 | SKY | 2 |

| 03 | SCHOOL BUS | 3 |

| 04 | COAL | 4 |

主键

外键

### 删除操作（父表）

```sql
DELETE FROM color WHERE c_id = 2
```

删除操作成功

### COLOR 表

| C_ID | C_DESC |

|---|---|

| 1 | RED/ROJO |

| 2 | BLUE/AZUL |

| 3 | YELLOW/AMARILLO |

| 4 | BLACK/NEGRO |

| 5 | WHITE/BLANCO |

### OBJECT 表

| O_ID | O_DESC | C_ID |

|---|---|---|

| 01 | STOP SIGN | 1 |

| 02 | SKY | 2 |

| 03 | SCHOOL BUS | 3 |

| 04 | COAL | 4 |

图 4-14：引用约束的 ON NO ACTION 删除规则的执行方式。

## 告知约束 (Informational Constraints)

每当向表中添加新的数据值或对现有数据值进行修改或删除时，DB2 数据库管理器会自动执行我们迄为止看过的所有约束。正如你想象的，如果定义了大量的约束，那么执行这些约束可能需要大量的系统开销——特别是在向表中加载大量数据时。

如果应用程序的编码方式是在将数据插入 DB2 数据库之前对其进行验证，那么创建一个或多个告知约束可能比创建其他可用约束更高效。与其他约束不同，告知约束在插入处理过程中不会执行。然而，DB2 SQL 优化器在考虑解析查询的最佳访问计划时，会评估告知约束提供的信息。告知约束是由关键字 `NOT ENFORCED` 和 `ENABLE QUERY OPTIMIZATION` 会将其转换为普通的约束定义。因此，信息性约束可能会带来更好的查询性能，尽管该约束本身不会用于验证数据录入/修改。图 4–15 展示了简单信息性约束的行为。

### 新记录

![](img/7bc9d5f6e46add86bfa073e2146c4fd4_292_0.png)

| EMPID | NAME | TAX_ID |

|---|---|---|

| 001 | JAGGER, MICK | 591075 |

| 002 | RICHARDS, KETH | 234667 |

| 003 | WOOD, RONNIE |   |

| 004 | WATTS, CHARLIE | 1194894 |

| 005 | WYMAN, BILL | 691647 |

| 006 | JONES, BRIAN | 90 |

```sql
CREATE TABLE employee
  empid CHAR(3),
  name VARCHAR(25),
  tax_id INTEGER CHECK (tax_id > 1000)
    NOT ENFORCED
    ENABLE QUERY OPTIMIZATION
```

图 4-15：简单信息性约束的行为。

需要注意的是，由于 DB2 优化器在选择最佳数据访问计划来解析查询时会评估信息性约束，因此插入表中违反一个或多个信息性约束的记录可能不会被某些查询返回。例如，如果对图 4–15 所示的 `EMPLOYEE` 表执行查询 "`SELECT * FROM employee WHERE tax_id = 90`"，则将不会返回任何记录，因为所选的访问计划将假设表中不存在 `TAX_ID` 值小于 1,000 的记录。

> 要让 DB2 优化器在选择用于解析查询的最佳数据访问计划时忽略信息性约束，你只需禁用该约束的查询优化即可。你可以在创建约束时执行此操作，也可以以后通过执行 `ALTER TABLE` 语句、识别要修改的约束并指定 `DISABLE QUERY OPTIMIZATION` 选项来实现。

## 使用 SET INTEGRITY SQL 语句临时挂起约束检查

虽然约束提供了一种在基表内操作数据时维持某种程度完整性的手段，但它们的强制执行可能会阻止某些类型操作的成功执行。例如，假设你想使用 `Load` 实用程序向基表批量加载 10,000 行数据（我们将在第 6 节“DB2 实用程序”中更详细地介绍）。如果数据包含了违反为要加载数据的基表所定义的约束的值，则操作将失败。假设你希望向已经包含数百行数据的现有表添加一个新约束。如果表中有一行或多行数据包含违反你想要添加的约束的数据值，则任何添加约束的尝试都将失败。在这种情况下，临时挂起约束检查以执行所需的操作将是有益的。然而，当挂起约束检查后，必须在某个点恢复检查，届时必须定位并处理表中导致违反约束的表行。

可以通过执行 `SET INTEGRITY` SQL 语句临时挂起表的约束检查。当用此语句挂起约束检查时，该语句的最简单形式是：

```sql
SET INTEGRITY FOR [TableName ... ] OFF <AccessMode>
```

其中：

- `TableName`：指定要临时挂起约束检查的一个或多个基表的名称。

- `AccessMode`：标识在约束检查挂起期间，指定的表是否可以以只读模式访问。此参数的有效值为：`NO ACCESS` 和 `READ ACCESS`——如果未指定访问模式，则默认使用 `NO ACCESS`。

因此，如果你想临时挂起名为 `EMPLOYEE` 的表的约束检查，并在约束检查关闭期间对该表进行只读访问，可以执行类似下面的 `SET INTEGRITY` 语句：

```sql
SET INTEGRITY FOR employee OFF
```

## 约束 271
