
如果你想在一条语句中同时获取旧工资和新工资怎么办？这个主题将在接下来的关于 `INCLUDE` 列的子节中讨论。

如果你想知道正在插入的值，且该值无法立即获取，那么 `SELECT FROM INSERT` 就很有用。一个很好的例子是向带有标识列（identity column）的表中插入数据。通常情况下，你会调用 `IDENTITY_VAL_LOCAL` 函数来获取最近插入的标识值。

当使用单个 SQL 语句插入多行时，`IDENTITY_VAL_LOCAL` 无法返回所有生成的标识值。换句话说，如果表 `identity_tab` 定义如下：

```sql
CREATE TABLE identity_tab
(id INT NULL GENERATED ALWAYS AS IDENTITY, data VARCHAR(100))
```

那么在语句之后无法使用 `IDENTITY_VAL_LOCAL`，例如：

```sql
INSERT INTO identity_tab (data) VALUES ('A'), ('B'), ('C');
```

或者（`t2` 包含多行）

```sql
INSERT INTO identity_tab (data) SELECT data FROM t2
```

图 10.3 中的过程演示了如何使用 `NEW TABLE` 在多行插入后获取所有生成的标识值。

### 利用高级 SQL

```sql
CREATE PROCEDURE insert_identities()
LANGUAGE SQL
SPECIFIC insert_identities
ii: BEGIN
  -- 此过程需要如下定义的表：
  -- CREATE TABLE identity_tab (id INT NOT NULL GENERATED ALWAYS AS IDENTITY, data VARCHAR(100));
  DECLARE c1 CURSOR WITH RETURN TO CALLER FOR
  SELECT id FROM NEW TABLE (INSERT INTO identity_tab (data) SELECT
  deptname FROM department);
  OPEN c1;
END ii
```

图 10.3 使用 `NEW TABLE` 获取 `identity_tab` 表的标识值，LU。

当您调用此过程时，部门名称被插入到 `identity_tab` 表，并为每行生成标识值。光标将所有用于多行插入的标识列返回给客户端。

> 注意
> 在 ZSeries 上，`FINAL TABLE` 仅支持 `INSERT` 语句。

## INCLUDE

上一节讨论了 `UPDATE` 语句如何访问 `NEW TABLE` 和 `OLD TABLE` 值。示例演示了在工资增加 10% 后如何获取员工的旧工资或新工资。这里重复了这些 SQL 语句是为了引入 `INCLUDE` 列。

```sql
SELECT salary FROM OLD TABLE (UPDATE EMPLOYEE SET salary = salary * 1.1 WHERE
EMPNO='000340')
```

```sql
SELECT salary FROM NEW TABLE (UPDATE EMPLOYEE salary = salary * 1.1 WHERE
EMPNO='000340')
```

然而，仅用 `NEW TABLE` 和 `OLD TABLE` 无法获取旧的和新工资值。`INCLUDE` 列可以用来填补这一空白。

```sql
SELECT salary as new_salary, old_salary
FROM NEW TABLE ( UPDATE employee INCLUDE (old_salary DECIMAL(9,2)) 
SET salary = salary * 1.10,
old_salary = salary
WHERE empno='000340')
```

## 第 10 章 利用 DB2 应用开发特性

嵌套 `UPDATE` 语句中的 `INCLUDE` 子句创建了一个新列，可以从外部 `SELECT` 语句中选择。你可以看到 `old_salary` 获取了旧工资值，而表列 `salary` 增加了 10%。如果 `p_empno` 是 000340，输出将是：

```
NEW_SALARY OLD_SALARY
26224.00 23840.00
```

## FINAL TABLE

除了 `OLD TABLE` 和 `NEW TABLE` 之外，还有被称为 `FINAL TABLE` 的东西。在插入、更新或删除时，可能仍存在 `AFTER` 触发器或引用约束，这些因素会导致数据的进一步修改。`FINAL TABLE` 可用于确保此类更改能够发生。

> 注意
> 在 ZSeries 上，`FINAL TABLE` 仅支持 `INSERT` 语句。

考虑以下示例，使用在本节之前定义的 `identity_tab`，创建了一个 `AFTER` 触发器，将所有值设置为 `NULL`。这意味着在 `INSERT` 到 `identity_tab` 时提供的任何数据值始终会被擦除。虽然这并不特别，但它清楚地演示了 `NEW TABLE` 和 `FINAL TABLE` 之间的区别。

```sql
CREATE TRIGGER trig1
AFTER INSERT ON identity_tab REFERENCING NEW AS n
FOR EACH ROW MODE DB2SQL
UPDATE identity_tab SET data=null
```

如果您在执行 `INSERT` 后使用 `NEW TABLE`，即使 `AFTER` 触发器最终将其设置为 NULL，`SELECT` 也会获取插入的值。

```sql
SELECT data FROM NEW TABLE (INSERT INTO identity_tab VALUES (default,'x'))
DATA
-----------------------
x
1 record(s) selected.
```

然而，当使用 `FINAL TABLE` 时，SQL 语句是不允许执行的。

```
SELECT data FROM FINAL TABLE (INSERT INTO identity_tab VALUES (default,'x'))
```

## 利用高级 SQL

### 分批删除行

当您想要删除大量数据时，一个主要问题是日志空间。

> 注意
> 在 LUW 上，如果你想删除表而不是使用 `DELETE`，可以使用 `ALTER TABLE`

即使你有足够的日志空间，通常也不应该删除表。图 10.4 提供了一个如何通过这种方式的示例。该过程的核心特性是 `DELETE` 语句将其结果集限制在固定行数。在这个示例中，行按每 10 行进行删除并提交（然而，在您自己的情况下，删除数百或数千行将产生更好的性能）。这种操作一直持续，直到没有行可删除（由 `GETNOSTICS` 决定）。

```sql
CREATE PROCEDURE chunk_delete (OUT p_batches INT)
LANGUAGE SQL
SPECIFIC chunk_delete
cd: BEGIN
  -- 此示例当前支持 LU
  DECLARE SQLSTATE CHAR(5) DEFAULT '00000';
  DECLARE v_cnt INT DEFAULT 0;
  DECLARE rows_deleted INT DEFAULT 1;
  REPEAT
    SET v_cnt = v_cnt + 1;
    DELETE FROM EMP_ACT
    WHERE EXISTS (SELECT 1 FROM EMP_ACT
      WHERE YEAR(EMEND) < YEAR(current date)
      FETCH FIRST 10 ROWS ONLY);
    GET DIAGSTICS rows_deleted = ROW_COUNT;
    COMMIT;
  UNTIL rows_deleted = 0
  END REPEAT;
  SET p_batches = v_cnt;
END cd;
```

### MERGE 语句

`MERGE` SQL 语句用于将 `INSERT`、`UPDATE` 和 `DELETE` 语句合并为一条，可能会带来更好的性能。

> 注意
> `MERGE` 目前适用于 LUW。然而，实现数据合并 语句的方法（见图 10.6）适用于所有平台。

为了演示，请考虑这样一个示例：你有一个临时表，其中包含对现有数据的更新以及要插入主表的新数据。以下表和数据支持后续示例。

```sql
CREATE TABLE master_table (id INT NOT NULL, data VARCHAR(100));
CREATE UNIQUE INDEX ix1 ON master_table (id);
ALTER TABLE master_table ADD CONSTRAINT master_pk PRIMARY KEY (id);
CREATE TABLE stage_table LIKE master_table;
```

```sql
INSERT INTO master_table VALUES (1,'a');
INSERT INTO master_table VALUES (2,'b');
INSERT INTO master_table VALUES (3,'c');
INSERT INTO master_table VALUES (4,'d');
```

```sql
INSERT INTO stage_table VALUES (1,'A');
INSERT INTO stage_table VALUES (3,'C');
INSERT INTO stage_table VALUES (10,'j');
INSERT INTO stage_table VALUES (11,'k');
```

图 10.5 两个表合并数据的场景设置。

在本例中，`master_table` 表是主表，而 `stage_table` 是临时表。如果 `stage_table` 中的某行也存在于 `master_table` 中，则应该更新 `master_table` 中的现有行。如果 `stage_table` 中的某行不存在于 `master_table`，则应将其插入到 `master_table` 中。图 10.6 展示了如何实现此操作。

```sql
CREATE PROCEDURE old_merge (
LANGUAGE SQL
SPECIFIC old_merge -- applies to LUW and iSeries
--WLM ENVIRONMENT <env> -- applies to zSeries
AS BEGIN
  DECLARE v_id INT;
  DECLARE v_data VARCHAR(100);
  DECLARE SQLSTATE CHAR(5) DEFAULT '00000';
  DECLARE cur CURSOR FOR
    SELECT id, data FROM stage_table;
  DECLARE CONTINUE HANDLER FOR SQLSTATE '23505'
    -- 主键冲突。改为执行更新而非插入。
    UPDATE master_table SET data = v_data WHERE id = v_id; --
OPEN cur;
FETCH cur INTO v_id, v_data;
WHILE (SQLSTATE = '00000') DO
  INSERT INTO master_table VALUES (v_id, v_data); --
  FETCH cur INTO v_id, v_data;
END WHILE;
END cm
```

**图 10.6** 使用 `INSERT` 和 `UPDATE` 语句从两个表中合并数据。

该存储过程的工作原理是在第 (1) 行为表 `stage_table` 创建一个游标，并尝试在第 (3) 行将每行插入到 `master_table`。如果由于主键冲突导致插入失败，则该行必须已经存在于 `master_table` 中。此时，第 (2) 行的 `CONTINUE` 处理程序将执行 `UPDATE`，而不是直接使用待合并行的主键值。

使用行的 `MERGE` 语句可以极大地简化存储过程并以更高的效率执行。请对比图 10.6 和图 10.7。

```sql
CREATE PROCEDURE new_merge()
LANGUAGE SQL
SPECIFIC new_merge
BEGIN
  -- MERGE 语句目前仅支持 LUW
MERGE INTO master_table AS M
USING (SELECT id, data FROM stage_table) AS S
ON M.id=S.id
WHEN NOT MATCHED THEN
    INSERT VALUES (S.id, S.data)
WHEN MATCHED THEN
    UPDATE SET M.data=S.data;
END
```

图 10.7 在 LUW 上使用 `MERGE` 语句从两个表中合并数据。

现在你已经看到了一个基础示例，可以介绍关于 `MERGE` 语句的更多细节。`MERGE` 语句可以拆解如下：

```
MERGE INTO <target> USING <source> ON <match-condition>
{WHEN [NOT] MATCHED [AND <predicate>]
THEN (UPDATE SET ...|DELETE|INSERT VALUES ...|SIGNAL ...)
[ELSE IGNORE]
```

`<target>` 是主表，`<source>` 是定义要合并到表中的行的 `SELECT` 语句。在图 10.7 中，源是简单的从 `stage_table` 中选择所有行的 `SELECT`。然而，源可以是任何有效的 `SELECT` 语句，并可能包含表连接。`<match-condition>` 是一个唯一的列值，定义了源表和目标表之间的关系。在之前的示例中，这是 `master_table` 和 `stage_table` 共享的主键。

一旦定义了源、目标及其关系，你就可以决定在匹配或未匹配时该做什么。`MERGE` 具有许多复杂的细节，最好通过 SQL 参考来获取。请参阅 SQL 参考以获取更多示例或在需要额外信息时。

#### 声明的临时表

声明的全局临时表类似于普通表，但提供了性能优势：
- 它们以极少的基础设施和资源需求存储数据。
- 它们可以调整到内存中以获得更好的性能。
- 因为它们只能从创建它们的连接进行访问，因此不需要锁定机制。
- 在某些平台上，它们可以在不记录事务日志的情况下进行操作。

在接下来的章节中，你将学习如何在应用程序中使用临时表。

#### 临时表简介

声明的全局临时表通常被称为 `DGTTs` 或简单称为临时表。正如名称所示，临时表不是持久化对象。它们与普通表相似，不同之处它们仅在连接持续期间存在，并且只能由声明它们的连接访问。如果两个连接创建了同名的临时表，每个临时表的实例都是唯一的。当连接关闭时，通过该连接声明的所有临时表都将被删除。临时表不属于特定用户；它们属于创建它们时的会话（`session`）。否则，DB2 将在当前模式中查找临时表（例如，`QTEMP`）。

#### 为临时表创建环境

在 DB2 LUW 和 zSeries 上，在使用临时表之前需要进行一些设置。在 iSeries 上，不需要设置（临时表将在库 `QTEMP` 中创建）。

在 DB2 LUW 上，必须存在表空间（这与 `SYSTEM` space 不同且经常被混淆）。与其他所有类型的表空间一样，临时表空间需要为其分配一个缓冲池（`buffer pool`）。当声明并填充临时表时，数据将使用分配给该表空间的缓冲池以保留在内存中。如果临时表的内存需求超过了分配给表空间的缓冲池大小，DB2 将自动将部分数据分页到磁盘。以下是在 LUW 上创建临时表空间的简单示例：

```sql
CREATE USER TEMPORARY TABLESPACE usempspace
MANAGED BY SYSTEM USING ('usempspace')
BUFFERPOOL IBMDEFAULTBP
```

#### 利用 DB2 特性

使用表池的临时表将保留在 `IBMDEFAULTBP` 中。如果你担心临时表会消耗过多的缓冲池，可能需要为临时表创建一个专用的缓冲池。在 zSeries 上，你需要：
- 创建数据库并使用 `AS TEMP` 子句以确保该数据库仅用于临时表。
- 在数据库中创建表空间。

例如，此语句将创建一个仅供临时表使用的 `tempdb`：

```sql
CREATE DATABASE AS TEMP
```

每个子系统或共享成员只能创建一个 `TEMP` 数据库。`TEMP` 数据库无法在子系统或共享成员之间共享。一旦创建了 `TEMP` 数据库，你必须在该数据库中创建表空间。例如，以下语句使用 8K 页缓冲池在 `tempdb` 中创建表空间 `temptbl`：

```sql
bufferpool BPK
```

#### 声明全局临时表

让我们看看声明临时表的多种方式。声明临时表的语法与创建普通表相似。声明全局临时表的语法和选项随平台有所不同。因此，图 10.8、10.9 和 10.10 为每个平台提供了语法图。关于 `DECLARE GLOBAL TEMPORARY TABLE` 的完整描述，请咨询对应平台的 SQL 参考。以下示例还将指出你应该注意的一些选项和语法上的细微差异。

```sql
DECLARE GLOBAL TEMPORARY TABLE table_name
      *
```

图 10.8 DB2 LUW 的 `DECLARE GLOBAL TEMPORARY TABLE` 语法。

```sql
```
