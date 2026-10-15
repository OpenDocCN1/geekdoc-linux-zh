
**图 10.17** 返回临时表内容的存储过程。

为了总结此示例，表 10.1 列出了调用序列：

### 表 10.1 共享临时表的调用序列

| 步骤 | 命令 | 描述 |
|---|---|---|
| 步骤 1: | `CALL init_temp` | 这将重新初始化 `SESSION.temp` 表。 |
| 步骤 2: | `CALL insert_to_temp` | 这向 `SESSION.temp` 插入三行。 |
| 步骤 3: | `CALL show_rows` | 返回的结果将是包含 `insert_to_temp` 填充的临时表中的三个行数据。 |
| 步骤 4: | `CALL close_temp` | 删除临时表。 |

## 注意事项

在 `iSeries` 上，用户定义函数和触发器都支持临时表。在 `zSeries` 上，用户定义函数支持临时表但触发器不支持。在 `LUW` 上，用户定义函数或触发器不支持临时表。然而，函数和触发器可以调用使用临时表的存储过程。

## 创建全局临时表

在 `zSeries` 上，有两种临时表：

- 使用 `DECLARE GLOBAL TEMPORARY TABLE` 语句创建的临时表（声明）。
- 使用 `CREATE GLOBAL TEMPORARY TABLE` 语句创建的临时表（创建）。

本章讨论了第一种临时表。为了与其他平台的可移植性，应该使用这种类型的临时表。然而，如果您仅在 `zSeries` 上开发应用程序，则可能想要考虑第二种类型的临时表。

创建的临时表在目录中存储了表的描述。此描述是持久的，因此可以跨应用程序过程共享。尽管描述是共享的，但此表的实例对于每个应用程序过程都是独特的，并且它不会超出应用程序过程的生命周期。

此表的名称遵循任何标准表的规则，模式名称不需要是 `SESSION`。

创建的临时表不支持索引、`UPDATE` 操作和 `DELETE`（仅定位）操作。锁定、恢复、表空间和数据库操作也不适用于此类表。

创建的全局临时表存储在工作文件数据库的表空间中。它不像声明的全局临时表那样存储在名为 `TEMP` 的数据库中。

有关创建的全局临时表的更多细节，请参考《DB2 for zSeries SQL Reference》。

## 使用保存点 (Save Points)

保存点是一种服务器端机制，可以让你对事务有更强的控制。保存点允许您启动事务并保留部分内容同时回滚其他内容。在后续章节中，您将看到如何使用它们。

### 应用程序保存点介绍

应用程序保存点是应用程序（如 SQL 过程）内部控制事务的机制。保存点有三种：

- 语句保存点
- 复合 SQL 保存点
- 外部保存点

默认情况下，在执行每个 SQL 语句之前内部会创建一个保存点。如果 SQL 语句发生错误，DB2 将回滚到内部保存点。保存点由 DB2 内部使用。

如果您使用复合语句，DB2 将一组 SQL 语句视为一个语句执行。如果任何子语句失败，复合块中的所有操作都将回滚。原子复合实际上使用内部复合点。参见第 4 章“使用控制流语句”以讨论原子复合。第三种保存点——外部保存点是本节的重点。从这里开始，对“保存点”一词的任何引用均指外部保存点。

外部保存点类似于原子复合，具有更细粒度的事务控制。在事务中建立保存点后，您可以选择回滚事务中的语句，而不影响事务中的其他操作。

`ON ROLLBACK RETAIN CURSORS` 是强制性子句，描述保存点内的游标行为。如果在保存点中打开或引用了游标，回滚到保存点将保持游标打开并定位在结果集中的下一逻辑行。

回滚到保存点时的默认行为。使用 `ON ROLLBACK RETAIN LOCKS` 选项，DB2 将不会释放在保存点内获取的锁。

```
--TO---
>>RELEASE--+-------+SAVEPOINT--savepoint-name----------------<
```

# 图 10.19 释放保存点的语法图。

```
--WORK---
>>ROLLBACK--+-----------+----------------+----->

             '-TO SAVEPOINT--+-

                             '-savepoint-name-'
```

# 图 10.20 回滚到保存点的语法图。

块的最后一个子语句之后，你可以选择回滚到该保存点或保存点。一旦释放了保存点，将无法再次回滚到该保存点。
当事务完成时，保存点会被释放。回滚到保存点不被视为事务的结束，因此保存点不会被释放。

## 在 SQL 过程中使用保存点

在图 10.21 中，展示了 SQL 过程 `bonus_incr`。它用于自动增加公司员工的奖金。ABC 公司正在实施一项让每位员工都获得 10% 奖金增长的计划。由于某些部门的奖金总额较高，管理层决定，如果某个部门的奖金总额超过 $3,000，其员工将不会立即增长，而是将进行单独评估。

```
CREATE PROCEDURE bonus_incr (
LANGUAGE SQL
SPECIFIC bonus_incr -- applies to LUW and iSeries
  -- WLM ENVIRONMENT <env> -- applies to zSeries
bi: BEGIN
  DECLARE VARIABLES
  DECLARE v_dept, v_actdept CHAR(3);
  DECLARE v_bonus, v_deptbonus, v_newbonus DECIMAL(9,2);
  DECLARE v_empno CHAR(6);
  DECLARE v_attend SMALLINT DEFAULT 0;
  DECLARE CURSORS
  DECLARE c_sales CURSOR WITH HOLD FOR -- (1)
```

## 使用保存点操作

```
SELECT workdept, bonus, empno FROM employee
ORDER BY workdept;
```

```
-- DECLARE HANDLERS
DECLARE CONTINUE HANDLER FOR NOT FOUND
SET v_attend=1;
DECLARE EXIT HANDLER FOR SQLLEXCEPTION
SET v_attend=1;
```

```
-- Procedure body
OPEN c_sales;
FETCH c_sales INTO v_dept, v_bonus, v_empno;
```

```
WHILE (v_attend = 0) DO
  SAVEPOINT svpt_bonus_incr ON ROLLBACK RETAIN CURSORS;
  SET v_actdept = 0;
  SET v_deptbonus = 0;
  WHILE (v_actdept = v_dept) AND (v_attend = 0 ) DO
    SET v_newbonus = v_bonus * 1.1;
    UPDATE employee
      SET bonus = v_newbonus
      WHERE empno = v_empno;
    SET v_deptbonus = v_deptbonus + v_newbonus;
    FETCH c_sales INTO v_dept, v_bonus, v_empno;
  END WHILE;
```

```
IF v_deptbonus <= 3000.00 THEN
  COMMIT;
ELSE
  ROLLBACK TO SAVEPOINT svpt_bonus_incr;
  RELEASE SAVEPOINT svpt_bonus_incr;
END IF;
END WHILE;
```

END bi

**图 10.21** SQL 过程 *BONUS_INCR.*

## 第 10 章 利用 DB2 应用开发功能

第 (1) 行的语句显示了一个游标，用于检索按部门编号排序的员工集合。第 (3) 行的语句定义了一个保存点 `svpt_bonus_incr`。这是应用程序可以回滚到的点。WHILE 循环遍历给定部门的员工并执行奖金计算。如果一个部门的奖金总额为 3000 或以下，自保存点以来所的更改将在第 (4) 行提交。为了保持游标打开以便处理其他部门，游标在第 (1) 行中带有 `HOLD` 选项进行声明。另一方面，如果一个部门的奖金总额超过 3000，则自上次保存点以来对数据库的更新将在第 (5) 行回滚。保存点也会在第 (6) 行被释放，以便在处理下一个部门之前在第 (4) 行重新创建。

如果用于保存点的语句执行失败，会发生什么？DB2 是只回滚该语句、保存点块，还是整个 SQL 过程？答案取决于是否为错误定义了 `HANDLER`。如果没有定义，保存点中的任何语句失败都会导致 SQL 过程中的所有更改回滚，无论这些更改是在保存点内部还是外部。相反，如果为错误定义了 `HANDLER`，则只回滚该语句。这是使用保存点时的预期行为。为了使图 10.21 中的示例更完整，在第 (2) 行定义了一个 `EXIT HANDLER`。这确保了保存点被回滚并退出存储过程调用。

还支持嵌套保存点以实现更细粒度的事务控制。图 10.22 展示了嵌套保存点的用法。

```
CREATE PROCEDURE nested_savepoint (  )
  LANGUAGE SQL
  SPECIFIC nested_savepoint -- applies to LUW and iSeries
  -- WLM ENVIRONMENT <env> -- applies to zSeries
  nsp: BEGIN
  CREATE TABLE SP_TABLE (INT);
  COMMIT;
  SAVEPOINT sp1 ON ROLLBACK RETAIN CURSORS;
  INSERT INTO SP_TABLE (1);
  SAVEPOINT sp2 ON ROLLBACK RETAIN CURSORS;
  INSERT INTO SP_TABLE (2);
  SAVEPOINT sp3 ON ROLLBACK RETAIN CURSORS;
  INSERT INTO SP_TABLE (3);
  ROLLBACK TO SAVEPOINT sp2;
  COMMIT;
  DROP TABLE SP_TABLE;
  COMMIT;
END nsp;
```

**图 10.22** 嵌套保存点示例。

## 序列对象

图 10.22 显示的过程演示了嵌套保存点的用法。在第 3 章“SQL 语言元素概述”中，你学习了如何使用序列对象和标识列。通过将 `NEXTVAL` 封装在存储过程或序列对象中，可以提高可管理性。图 10.23 显示了一个示例。

```
CREATE PROCEDURE seqnextval ( IN p_seqname VARCHAR(50), OUT p_nextval INT )
LANGUAGE SQL
SPECIFIC seqnextval -- applies to LUW and iSeries
-- WLM ENVIRONMENT <env> -- applies to zSeries
env: BEGIN
  DECLARE v_dynstmt VARCHAR(100);
  -- DECLARE CONDITIONS
  -- SQLSTATE 42704, object not found
  DECLARE seq_notfound CONDITION FOR SQLSTATE '42704';
  -- SQLSTATE 42501, object privilege error
  DECLARE obj_access_error CONDITION FOR SQLSTATE '42501';
  -- DECLARE CURSORS
  DECLARE c_nextval CURSOR FOR v_prepstmt;
  -- DECLARE HANDERS
  DECLARE EXIT HANDLER FOR seq_notfound
  RESIGNAL SQLSTATE '70000'
  SET MESSAGE_TEXT = 'Sequence NOT FOUND';
  DECLARE EXIT HANDLER FOR obj_access_error
  RESIGNAL SQLSTATE '70001'
  SET MESSAGE_TEXT = 'User encounters privilege problems;
  -- Procedure body
  SET v_dynstmt = 'SELECT NEXTVAL FOR || p_seqname || ' FROM SYSIBM.SYSDUMMY1';
  PREPARE v_prepstmt FROM v_dynstmt;
  OPEN c_nextval;
  FETCH c_nextval INTO p_nextval;
  CLOSE c_nextval;
END env;
```

**图 10.23** 序列过程接收序列对象名称作为输入并返回下一个序列值。

## 序列对象

如果用户对序列没有 `USAGE` 权限，或者对存储过程包本身没有 `EXECUTE` 权限，可能会导致此错误。关于创建或执行存储过程所需的权限详细信息，请参考附录 E“SQL 过程中的安全考虑”。

可以使用 `ALTER SEQUENCE` 更改序列对象的行为。也可以定义另一个带有特定选项的修改序列对象的存储过程（参见图 10.24）。

```sql
CREATE PROCEDURE alterseq ( IN p_seqname VARCHAR(50)
                                                              IN p_options VARCHAR(100 )
  LANGUAGE SQL
  SPECIFIC alterseq -- 应用于 LUW 和 iSeries
  -- WLM ENVIRONMENT <env> -- 应用于 zSeries
aseq: BEGIN
  DECLARE VARIABLES
  DECLARE v_dynymnt VARCHAR(100);
  DECLARE v_retcode INTEGER DEFAULT 0;
  DECLARE CONDITIONS
  -- SQLSTATE 42704, 对象未找到
  DECLARE seq_notfound CONDITION FOR SQLSTATE '42704';
  -- SQLSTATE 42501, 对象权限错误
  DECLARE obj_access_error CONDITION FOR SQLSTATE '42501';
  DECLARE HANDLERS
  DECLARE EXIT HANDLER FOR seq_notfound
    RESIGNAL SQLSTATE '70000'
    SET MESSAGE_TEXT = 'Sequence Object NOT FOUND';
  DECLARE EXIT HANDLER FOR obj_access_error
    RESIGNAL SQLSTATE '70001'
    SET MESSAGE_TEXT = 'User encounters privilege problems';
  DECLARE EXIT HANDLER FOR SQLEXCEPTION
    RESIGNAL SQLSTATE '70002'
    SET MESSAGE_TEXT = 'SQL Exception raised';
  -- 过程体
  SET v_dynymnt = 'ALTER SEQUENCE ' || p_seqname || ' ' || p_options;
  PREPARE v_prepstmt FROM v_dynymnt;
  EXECUTE v_prepstmt;
```

图 10.24 封装在 SQL 过程中的序列对象修改。

要测试 `ALTERSEQ` 存储过程，可以执行：

```sql
CALL alterseq('staff_seq', 'restart with 500')
```
