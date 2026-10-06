
图 9.24 触发器调用函数和过程的示例（适用于 LUW 和 iSeries）。

`9.24` 显示了一个 `BEFORE INSERT` 触发器对输入数据进行数据验证。如果员工号为空字符串，它将创建一个新员工。它会验证部门号，如果部门号无效，则抛出 SQL 错误并停止 `INSERT` 语句。已经做了一项业务决策，通过函数实现生成新员工号的逻辑，以便该函数可以被其他触发器和需要的地方使用。触发器仅调用了第 `(1)` 行的 `UDF`。

另一项业务决策是使用游标来实现部门号验证逻辑。该示例仅说明了如何通过触发器中调用过程作为间接使用游标的方法。游标用在一个简单的示例中。在现实生活中，必要时你应该使用游标，因为部门表很大，且业务逻辑太复杂，查询无法处理。更多信息，请参考第 5 章“理解和使用游标和结果集”。触发器仅调用了第 `(2)` 行的 SQL 过程。触发器中实现的唯一逻辑是在部门号无效时在第 `(3)` 行抛出 SQL 错误。

图 9.25 图 9.24 触发器的支持性 UDF。

图 9.25 中的 `UDF` 通过在当前最大的员工号上加 10 来生成一个新的员工号。员工号在 `employee` 表定义为 `CHAR(6)`。然而，内容是数字字符串。由于 `DB2 SQL PL` 是一种强类型语言，因此需要显式转换。第 `(1)` 行的员工号需要转换为整数以计算下一个员工号。结果在第 `(2)` 行转换回字符。在第 `(2)` 行使用 `RTRIM` 函数删除从整数转换为字符字符串后的末尾空格。在第 `(2)` 行拼接前导零并在第 `(3)` 行取右侧六位字符，以正确的格式格式化员工号。

`UDF` 的体可以在一行 `RETURN` 语句中实现。为了更好的可读性，它按照图 9.25 所示的方式进行实现。在你的项目中，建议使用数值列作为 ID，并使用 `DB2 SEQUENCE` 对象或 `DB2 IDENTITY` 列用于自增 ID。图 9.25 中的实现展示了在触发器中使用 `UDF` 的方法。在现实应用中，使用最大值计算下一个 ID 可能会导致并发问题。关于 `SEQUENCE` 对象或 `IDENTITY` 列的更多信息，请参考第 3 章“SQL PL 语言元素概述”。

图 9.26 触发器调用函数和过程的示例（适用于 LUW 和 iSeries）。

`9.24` 显示了一个 `BEFORE INSERT` 触发器对输入数据进行数据验证。如果员工号为空字符串，它将创建一个新员工。它会验证部门号，如果部门号无效，则抛出 SQL 错误并停止 `INSERT` 语句。已经做了一项业务决策，通过函数实现生成新员工号的逻辑，以便该函数可以被其他触发器和需要的地方使用。触发器仅调用了第 `(1)` 行的 `UDF`。

另一项业务决策是使用游标来实现部门号验证逻辑。该示例仅说明了如何通过触发器中调用过程作为间接使用游标的方法。游标用在一个简单的示例中。在现实生活中，必要时你应该使用游标，因为部门表很大，且业务逻辑太复杂，查询无法处理。更多信息，请参考第 5 章“理解和使用游标和结果集”。触发器仅调用了第 `(2)` 行的 SQL 过程。触发器中实现的唯一逻辑是在部门号无效时在第 `(3)` 行抛出 SQL 错误。

# 从 UDF 和触发器调用 SQL 过程的考虑因素

为了保护数据库中的数据完整性，对于 `UDF` 和触发器调用的 SQL 过程实施了某些规则。当在 `LUW` 的 `DB2` 独立代码中调用 SQL 过程时，适用于相同的规则，见附录 B“适用于 Linux、Unix 和 Windows 的 DB2 内联 SQL PL”。

## 数据访问限制

`UDF` 和 SQL 过程都有三种数据访问选项：`CONTAINS SQL`、`READ SQL DATA` 和 `MODIFIES SQL DATA`，如第 2 章“基本 SQL 结构”以及本章后续章节所示。`AFTER` 和 `INSTEAD OF` 触发器可以修改数据。`BEFORE` 触发器不能 `UPDATE`、`INSERT` 或 `DELETE`。出于实际考虑，你可以将这些类型的触发器视为 `MODIFIES SQL` 访问级别，并将 `BEFORE` 触发器视为 `READ DATA` 访问级别。

`DB2` 不允许低数据访问级别的 `UDF` 或 SQL 过程调用高数据访问级别的 `UDF` 或 SQL 过程。

- 具有 `MODIFIES SQL DATA` 选项的 `UDF` 和 SQL 过程可以调用任何其他有效的 `UDF` 和 SQL 过程。
- 具有 `READ SQL DATA` 选项的 `UDF` 和 SQL 过程只能调用具有 `READ SQL DATA` 或 `CONTAINS SQL` 选项的 `UDF` 和 SQL 过程。
- 具有 `CONTAINS SQL` 选项的 `UDF` 和 SQL 过程只能调用具有 `CONTAINS SQL` 选项的 `UDF` 和 SQL 过程。

# 从 UDF 和触发器调用 SQL 存储过程的注意事项

由于 `READ SQL DATA` 是 `UDF` 的默认选项，而 `MODIFIES SQL DATA` 是 SQL 过程的默认选项，如果你需要在 `UDF` 中调用 SQL 存储过程，则需要使用显式的数据访问选项。这在图 9.14 和 9.15 中得到了演示。

行函数不支持 `MODIFIES SQL DATA` 选项。修改表的 SQL 过程无法在行函数中调用。然而，它可以在表函数和触发器中调用。

> 提示
> 为了可读性，请在 `UDF` 和 SQL 过程中都使用显式的数据访问选项。这样更容易找到数据访问级别不兼容的 `UDF` 和过程。

# SQL 存储过程中的事务控制

如果过程被 `UDF` 或触发器调用，则过程体内不允许使用 `ROLLBACK` 和 `COMMIT` 语句，除非它回滚到在同一过程中定义的保存点（save point）。

> 注意
> 在 `iSeries` 上，除了 `ROLLBACK` 和 `COMMIT` 之外，由 `UDF` 或触发器调用的过程也不能包含 `CONNECT`、`SET CONNECTION`、`DISCONNECT` 或 `SET TRANSACTION` 语句。
> 在 `zSeries` 上，图 9.27、9.28 和 9.29 中的示例仅存储存储和触发器，不适用于表 `UDF`。`zSeries` 不支持表 `UDF`。要演示 `zSeries` 上的事务控制，请将表 `UDF` 替换为标量 `UDF`。

在图 9.27 中，`show_trans_sp` 过程在末尾有一个 `COMMIT` 语句。创建了一个表 `UDF` 和一个触发器来调用该过程。

```sql
CREATE PROCEDURE show_trans_sp()
LANGUAGE SQL
SPECIFIC show_trans_sp    -- 适用于 LUW 和 iSeries
-- WLM ENVIRONMENT <env>    -- 适用于 zSeries
MODIFIES SQL DATA
st: BEGIN
INSERT INTO cl_sched (class_code) VALUES ('AAA');
INSERT INTO cl_sched (class_code) VALUES ('BBB');
INSERT INTO cl_sched (class_code) VALUES ('CCC');
                                                              -- (1)
COMMIT;
END sts
```

# 第 9 章 用户定义函数和触发器

```sql
CREATE FUNCTION show_trans_func()
RETURNS TABLE (subject CHAR(64))
LANGUAGE SQL
SPECIFIC show_trans_func
MODIFIES SQL DATA
-- DISALLOW PARALLEL -- 适用于 iSeries
```

```sql
stf: BEGIN ATOMIC
CALL show_trans_sp();
RETURN
  SELECT subject FROM in_tray;
END stf
```

```sql
CREATE TRIGGER show_trans_trig
AFTER INSERT ON in_tray
FOR EACH ROW MODE DB2SQL
BEGIN ATOMIC
  CALL show_trans_sp();
END
```

**图 9.27** 由 `UDF` 和触发器调用的过程中的事务控制示例。

执行时，由于第 `(1)` 行 `COMMIT` 语句的顺序无效，函数和触发器会产生以下错误信息：

```sql
SELECT * FROM TABLE(show_trans_func()) AS t
```

`SQL0751N` 程序 `"DB2ADMIN.SHOW_TRANS_SP"`（特定名称 `"SQL040220311219103"`）尝试执行不受允许的语句。

```sql
INSERT INTO in_tray (subject) VALUES ('ABCD');
```

`DB21034E` 该命令不是有效的行处理器命令，因此被作为 SQL 语句处理。在 SQL 处理期间，它返回：`SQL0723N` 触发器 `"DB2ADMIN.SHOW_TRANS_TRIG"` 中的触发 SQL 语句发生错误。错误信息包括 `SQLCODE "-751"`，`SQLSTATE " "` 和消息标记 `"DB2ADMIN.SHOW_TRANS_SP|SQL040220311219103"`。`SQLSTATE=09000`

如果移除 `COMMIT` 语句，`UDF` 和触发器均可工作。将第 `(1)` 行的 `COMMIT` 语句替换为 `ROLLBACK` 语句会产生相同的错误信息。

# 从 UDF 和触发器调用 SQL 存储过程的注意事项

正如你可能注意到的，产生的错误是运行时错误。只要不执行 `COMMIT` 或 `ROLLBACK` 语句，`UDF` 和触发器均可工作。图 9.28 显示了图 9.27 的修改版本，其中 `COMMIT` 语句永远不会被执行。

```sql
CREATE PROCEDURE show_trans_sp2 ()
LANGUAGE SQL
SPECIFIC show_trans_sp2      -- 适用于 LUW 和 iSeries
-- WLM ENVIRONMENT <env>      -- 适用于 zSeries
MODIFIES SQL DATA
st2: BEGIN
  INSERT INTO cl_sched (class_code) VALUES ('AAA');
  INSERT INTO cl_sched (class_code) VALUES ('BBB');
  INSERT INTO cl_sched (class_code) VALUES ('CCC');
IF (1=0) THEN
  COMMIT;
END IF;
END sts2
```

```sql
CREATE TRIGGER show_trans_trig2
AFTER INSERT ON in_tray
FOR EACH ROW MODE DB2SQL
BEGIN ATOMIC
  CALL show_trans_sp2();
END
```

**图 9.28** 图 9.27 的修改版本。

在此示例中，`UDF` 和触发器均可工作。以下 `INSERT` 语句调用了触发器，触发器反过来调用了修改后的过程：

```sql
INSERT INTO in_tray (subject) VALUES ('ABCD')
```

产生以下结果：

```sql
SELECT * FROM cl_sched
AAA
BBB
CCC
```

```sql
SELECT * FROM in_tray
ABCD
```

```sql
SELECT * FROM in_tray
ABCD
```

如果移除 `COMMIT` 语句，`UDF` 和触发器均可工作。将第 `(1)` 行的 `COMMIT` 语句替换为 `ROLLBACK` 语句会产生相同的错误信息。

# 从 UDF 和触发器调用 SQL 存储过程的注意事项

```sql
INSERT INTO cl_sched (class_code) VALUES ('AAA'); -- (1)
INSERT INTO cl_sched (class_code) VALUES ('BBB');
INSERT INTO cl_sched (class_code) VALUES ('CCC'); -- (2)
END scs
```

```sql
CREATE TRIGGER show_conflict_trig
AFTER INSERT ON in_tray
FOR EACH ROW MODE DB2SQL
sct: BEGIN ATOMIC
INSERT INTO cl_sched (class_code) VALUES ('DDD'); -- (3)
CALL show_conflict_sp(); -- (4)
END sct
```

**图 9.30** 阐明读写冲突 `LUW`（逻辑工作）的示例。

在图 9.30 中，过程 `show_conflict_sp` 由触发器 `show_conflict_trig` 调用。该过程和触发器都包含写入 `cl_sched` 表的 SQL 语句。当在第 `(4)` 行调用 SQL 存储过程时，会创建一个表访问上下文——为了方便引用，将其命名为 `context1`。过程体内的 `INSERT` 语句将在 `context1` 中执行。当触发器在第 `(3)` 行发出 `INSERT` 语句时，会被另一个访问上下文——`context2`。第 `(3)` 行的 `INSERT` 语句将在 `context2` 中执行。

回 `DB2` 强制执行的三条规则；本例违反了第一条规则。`context1` 和 `context2` 都尝试写入同一张表 `cl_sched`。这是不允许的。

当执行触发器时，你将看到以下错误消息：

```
INSERT INTO in_tray (subject) VALUES ('ABCD')
```

`DB21034E` 命令被处理为 SQL 语句，因为它不是有效的命令行处理器命令。在处理 SQL 期间，它返回了：`SQL0723N` 在 `"DB2ADMIN.SHOW CONFL"` 中的触发 SQL 语句中发生错误。返回的错误信息包括 `SQLCODE "746"`、`SQLSTATE "57053"` 以及消息标记 `"DB2ADMIN.SHOW_CONFLICT_SP|SQL0402220302220703"`。`SQLSTATE=09000`

由于冲突仅在运行时报告，因此测试所有可能导致此类错误的条件至关重要。

# DB2 for iSeries 的注意事项

为了完整起见，`iSeries` `CREATE FUNCTION` 语句的语法图如图 9.31 所示，随后是与 `LUW` 版 `DB2` 差异说明。

```text
>>-CREATE FUNCTION---function-name
```

```text
-->(--+ .-, ------------------------------------------------+--)*---------------------
|                                                               |
| V                                                               |
|'--parameter-name--data-type+--'
```

```text
-->RETURNS--+data-type-----------------------------------------------------------*-----
|                                                               |
| V                                                               |
|'--TABLE---column-name--data-type2+--'
```

```text
-->LANGUAGE SQL-------------------------------------------------------+---
..NOT DETERMINISTIC-- ..MODIFIES SQL DATA--
```

```text
+----------------------------------------------------------------------
'--DETERMINISTIC--'+CONTAINS SQL-------
'--READS SQL DATA--'
```

```text
---CALLED NULL INPUT--------------------------------------------------+---
'--RETURNS NULL ON NULL INPUT-'  '-SPECIFIC--specific-name--'
```

```text
..EXTERNAL ACTION---- ..FENCED-----
+----------------------------------------------------------------------+---
'--NO EXTERNAL ACTION--'  '-NOT FENCED--'
```

```text
---STATIC DISPATCH----+------------------------------------------------+---
''-ALLOW PARALLEL-------
'--DISALLOW PARALLEL--'
```

```text
---INHERIT SPECIAL REGISTERS---
+------------------------------------------------------------------+---
'--CARDINALTY integer-----'
```
