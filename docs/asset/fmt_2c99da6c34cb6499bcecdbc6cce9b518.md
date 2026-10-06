
如果你使用图 7.3 所示的 SQL 存储过程，你可以简单地将 `LASTNAME = 'BROWN'` 作为 `p_where_cond` 传递。

## 使用 PREPARE 和 EXECUTE 重用动态 SQL 语句

如上一节所述，有一个只需要执行一次的 SQL 语句，`EXECUTE IMMEDIATE` 是理想的。如果你有需要执行多次的 SQL 语句，更好的解决方案是使用 `PREPARE` 和 `EXECUTE`。

如果你有某些值会变化的相似 SQL 语句，参数标记非常有用。考虑以下两个语句：

```sql
UPDATE EMPLOYEE SET BONUS=500 WHERE EMPNO='0030';
UPDATE EMPLOYEE SET BONUS=1000 WHERE EMPNO='0034';
```

从 DB2 的角度来看，问号是以后替换的占位符。因此，查询可以简化为以下通用形式：

```sql
UPDATE EMPLOYEE SET BONUS=? WHERE EMPNO=?
```

`PREPARE` 语句有两个参数。`statement-name` 是准备形式查询的标识符。`host-variable` 是要准备的 SQL 语句的 `VARCHAR`。

**图 7.4** `PREPARE` 的语法图。

`EXECUTE` 语句接受一个或多个参数。至少必须指定 `statement-name`，它必须引用之前准备过的语句对象。如果 SQL 语句有一个或多个参数标记，可以在 `USING` 子句中指定逗号分隔的主变量列表。

`INTO` 子句仅用于本章节后面讨论的动态 `CALL` 语句。考虑以下示例，公司增加了所有部门经理的奖金。为了实现这一点，定义了一个所有经理的游标来获取当前奖金，然后根据 `p_bonus_increase` 参数指定的金额进行增加（见图 7.6）。

```sql
CREATE PROCEDURE change_mgr_bonus ( IN p_bonus_increase DECIMAL , OUT p_num_changes INT )
LANGUAGE SQL
SPECIFIC change_mgr_bonus -- 适用于 LUW 和 iSeries
-- WLM ENVIRONMENT <env> -- 适用于 zSeries
```

```sql
cmb: BEGIN

DECLARE v_dynSQL VARCHAR(200);
DECLARE v_new_bonus DECIMAL;
DECLARE v_no_data SMALLINT DEFAULT 0;

DECLARE v_mgrno CHAR(6);
DECLARE v_bonus DECIMAL;

所有是经理的员工的游标
DECLARE c_managers CURSOR FOR
SELECT e.empno
  ,e.bonus
FROM EMPLOYEE e
  ,DEPARTMENT d
WHERE e.empno=d.mgrno;

DECLARE CONTINUE HANDLER FOR NOT FOUND
SET v_no_data=1;

SET v_dynSQL = 'UPDATE EMPLOYEE SET BONUS=? WHERE EMPNO=?';
SET p_num_changes=0;

END
```

图 7.6 (此处未提供图片)

### 使用 PREPARE EXECUTE 重用动态 SQL 语句

```sql
PREPARE v_stmt1 FROM :dynSQL; -- (1)
OPEN c_managers;
FETCH c_managers INTO v_mgrno, v_bonus;
WHILE (v_no_data=0) DO
  SET p_num_changes = p_num_changes + 1;
  SET v_bonus = v_bonus + p_bonus_increase;
  EXECUTE v_stmt1 USING v_bonus, v_mgrno; -- (2)
  fetch the next row to be processed
  FETCH c_managers INTO v_mgrno, v_bonus;
END WHILE;
CLOSE c_managers;
END cmb
```

**图 7.6** 使用 `PREPARE` 和 `EXECUTE USING ...` 语句的动态 SQL 示例。

在上示例中，有几个需要强调的概念。SQL 过程从变量声明开始。存储在 `v_dynSQL` 中的语句文本在第 (1) 行被准备，并使用 `v_stmt1` 作为语句名称标识符。

在 `WHILE` 循环中，语句名称 `v_stmt1` 在第 (2) 行被重复执行。因为准备好的语句有两个参数标记符，因此 `EXECUTE` 的 `USING` 子句用于替换参数值。

> 提示 如果动态 SQL 语句没有参数标记符，可以不带 `USING` 子句执行 `EXECUTE`。

在运行 SQL 过程之前，查看部门经理的当前的奖金值并记录这些值。

```sql
SELECT e.empno, e.bonus FROM EMPLOYEE e, DEPARTMENT d WHERE e.empno=d.mgrno
```

| EMPNO | BONUS |
| :--- | :--- |
| 000010 | 1000.00 |
| 000020 | 800.00 |
| 000030 | 800.00 |
| 000050 | 800.00 |
| 000060 | 500.00 |
| 000070 | 700.00 |
| 000090 | 600.00 |
| 000100 | 500.00 |

然后，带有奖金增加值调用 SQL 过程。例如，在 LUW 中，你可以使用命令行进程 (CLP)：

```sql
CALL CHANGE_MGR_BONUS (100,?)
```

输出应该类似于下面：

输出参数的值

参数名称 : P_NUM_CHANGES

参数值 : 8

返回状态 = 0

在此示例中，如 `p_NUM_CHANGES` 所示，更新了八行。为了进一步验证结果正确，再次查询数据。

```sql
SELECT e.empno, e.bonus FROM EMPLOYEE e, DEPARTMENT d WHERE e.empno=d.dmgrno
```

| EMPNO | BONUS |
| :--- | :--- |
| 000010 | 1100.00 |
| 000020 | 900.00 |
| 000030 | 900.00 |
| 000050 | 900.00 |
| 000060 | 600.00 |
| 000070 | 800.00 |
| 000090 | 700.00 |
| 000100 | 600.00 |

图 7.6 被用于说明使用一个 `PREPARE` 语句重复执行 `EXECUTE` 语句。这种“准备一次，执行多次”的设计与反复对同一语句运行 `PREPARE` 或 `EXECUTE IMMEDIATE` 相比，将提供许多更好的性能。

## 在游标中使用动态 SQL

有时，可能需要迭代结果集的一组行，并确定结果集是使用动态 SQL 创建的。在本节中，将介绍游标中动态 SQL 的示例。

### 使用动态 SQL 游标

考虑使用与上一节相同的示例，只是 `c_managers` 游标是动态定义的。图 7.7 展示了这些代码。

```sql
CREATE PROCEDURE change_mgr_bonus2 ( IN p_bonus_increase DECIMAL
                                            OUT p_num_changes INT)

LANGUAGE SQL
SPECIFIC change_mgr_bonus2               -- 适用于 LUW 和 iSeries
WLM ENVIRONMENT <env>                                     -- 适用于 zSeries

cmb2: BEGIN
  DECLARE v_dynMgrSQL    VARCHAR(200);               -- (1)
  DECLARE v_dynSQL       VARCHAR(200);

  DECLARE v_new_bonus    DECIMAL;
  DECLARE v_no_data      SMALLINT DEFAULT 0;

  DECLARE v_mgrno        CHAR(6);
  DECLARE v_bonus        DECIMAL;

  -- 所有也是经理的员工游标
  DECLARE c_managers CURSOR FOR v_cur_stmt;          -- (2)

  DECLARE CONTINUE HANDLER FOR NOT FOUND
    SET v_no_data=1;

  -- c_managers 游标的 SQL
  SET v_dynMgrSQL = 'SELECT e.empno,e.bonus FROM EMPLOYEE d ||
                     'WHERE e.empno=d.mgrno';

  SET v_dynSQL = 'UPDATE EMPLOYEE SET BONUS = ? WHERE EMPNO=?';
  SET p_num_changes=0;

  PREPARE v_stmt1 FROM v_dynSQL;

  PREPARE v_cur_stmt FROM v_dynMgrSQL;               -- (3)
  OPEN c_managers;                                   -- (4)
  FETCH c_managers INTO v_mgrno, v_bonus;

WHILE (v_no_data=0) DO
SET p_num_changes = p_num_changes + 1;
SET v_new_bonus = v_bonus + p_bonus_increase;
EXECUTE v_stmt1 USING v_new_bonus, v_mgrno;
-- 处理下一行
FETCH c_managers INTO v_mgrno, v_bonus;
END WHILE;

CLOSE c_managers;
END cmb2
```

# 第 7 章 使用动态 SQL

### 7.7 动态 SQL 游标

首先，必须为第 (2) 行的游标声明一个足够包含 SQL 语句的 `VARCHAR` 变量，注意第 (1) 行所示。在游标声明中，`v_cur_stmt` 名称将最终标识为 `v_dynsql` 持有的准备语句。最后在第 (3) 行使用 `v_dynsql` 准备 `c_managers` 语句。当打开第 (4) 行的 `c_managers` 游标时，DB2 期望 `v_cur_stmt` 名称引用一个准备语句。

注意在此示例中，`p_bonus` 和 `p_mgrno` 的参数标记未指定类型。根据情况，可能会遇到参数标记提供了错误类型的问题。可以使用 `CAST` 确保正确的类型来保护应用程序。例如，以下 SQL 语句：

```sql
SET v_dynsql = 'UPDATE EMPLOYEE SET BONUS = CAST(? AS DECIMAL) WHERE EMPNO= CAST(? AS CHAR(6))';
```

使用 `CAST` 确保正确的类型并不总是必要的。只有在类型不匹配时不才使用，因为 `CAST` 会增加执行开销。在运行 SQL 过程之前，查看部门经理的当前奖金值：

```sql
SELECT e.empno, e.bonus FROM EMPLOYEE e, DEPARTMENT d WHERE e.empno=d.mgrno
```

| EMPNO | BONUS |
| :--- | :--- |
| 000010 | 1100.00 |
| 000020 | 900.00 |
| 000030 | 900.00 |
| 000050 | 900.00 |
| 000060 | 600.00 |
| 000070 | 800.00 |
| 000090 | 700.00 |
| 000100 | 600.00 |

## 动态调用语句

然后，带有奖金增加值调用 SQL 过程。例如，在 LUW 中，你可以使用命令行进程 (CLP)：

```sql
CALL CHANGE_MGR_BONUS (100,?)
```

输出应该类似于：

输出参数的值

参数名称 : P_NUM_CHANGES

参数值 : 8

返回状态 = 0

在此示例中，如 `p_NUM_CHANGES` 所示，更新了八行。为了进一步验证结果正确，再次查询数据。

```sql
SELECT e.empno, e.bonus FROM EMPLOYEE e, DEPARTMENT d WHERE e.empno=d.dmgrno
```

| EMPNO | BONUS |
| :--- | :--- |
| 000010 | 1100.00 |
| 000020 | 900.00 |
| 000030 | 900.00 |
| 000050 | 900.00 |
| 000060 | 600.00 |
| 000070 | 800.00 |
| 000090 | 700.00 |
| 000100 | 600.00 |

图 7.6 被用于说明使用一个 `PREPARE` 语句重复执行 `EXECUTE` 语句。这种“准备一次，执行多次”的设计与反复对同一语句运行 `PREPARE` 或 `EXECUTE IMMEDIATE` 相比，将提供许多更好的性能。

## 在游标中使用动态 SQL

有时，可能需要迭代结果集的一组行，并确定结果集是使用动态 SQL 创建的。在本节中，将介绍游标中动态 SQL 的示例。

### 使用动态 SQL 游标

考虑使用与上一节相同的示例，只是 `c_managers` 游标是动态定义的。图 7.7 展示了这些代码。

```sql
CREATE PROCEDURE change_mgr_bonus2 ( IN p_bonus_increase DECIMAL
                                            OUT p_num_changes INT)

LANGUAGE SQL
SPECIFIC change_mgr_bonus2               -- 适用于 LUW 和 iSeries
WLM ENVIRONMENT <env>                                     -- 适用于 zSeries

cmb2: BEGIN
  DECLARE v_dynMgrSQL    VARCHAR(200);               -- (1)
  DECLARE v_dynSQL       VARCHAR(200);

  DECLARE v_new_bonus    DECIMAL;
  DECLARE v_no_data      SMALLINT DEFAULT 0;

  DECLARE v_mgrno        CHAR(6);
  DECLARE v_bonus        DECIMAL;

  -- 所有也是经理的员工游标
  DECLARE c_managers CURSOR FOR v_cur_stmt;          -- (2)

  DECLARE CONTINUE HANDLER FOR NOT FOUND
    SET v_no_data=1;

  -- c_managers 游标的 SQL
  SET v_dynMgrSQL = 'SELECT e.empno,e.bonus FROM EMPLOYEE d ||
                     'WHERE e.empno=d.mgrno';

  SET v_dynSQL = 'UPDATE EMPLOYEE SET BONUS = ? WHERE EMPNO=?';
  SET p_num_changes=0;

  PREPARE v_stmt1 FROM v_dynSQL;

  PREPARE v_cur_stmt FROM v_dynMgrSQL;               -- (3)
  OPEN c_managers;                                   -- (4)
  FETCH c_managers INTO v_mgrno, v_bonus;

WHILE (v_no_data=0) DO
SET p_num_changes = p_num_changes + 1;
SET v_new_bonus = v_bonus + p_bonus_increase;
EXECUTE v_stmt1 USING v_new_bonus, v_mgrno;
-- 处理下一行
FETCH c_managers INTO v_mgrno, v_bonus;
END WHILE;

CLOSE c_managers;
END cmb2
```

### 7.7 动态 SQL 游标

首先，必须为第 (2) 行的游标声明一个足够包含 SQL 语句的 `VARCHAR` 变量，注意第 (1) 行所示。在游标声明中，`v_cur_stmt` 名称将最终标识为 `v_dynsql` 持有的准备语句。最后在第 (3) 行使用 `v_dynsql` 准备 `c_managers` 语句。当打开第 (4) 行的 `c_managers` 游标时，DB2 期望 `v_cur_stmt` 名称引用一个准备语句。

注意在此示例中，`p_bonus` 和 `p_mgrno` 的参数标记未类型。根据情况，可能会遇到参数标记提供了错误类型的问题。可以使用 `CAST` 确保正确的类型来保护应用程序。例如，以下 SQL 语句：

```sql
SET v_dynsql = 'UPDATE EMPLOYEE SET BONUS = CAST(? AS DECIMAL) WHERE EMPNO= CAST(? AS CHAR(6))';
```
