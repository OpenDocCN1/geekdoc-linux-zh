
# START（见下文注释）

禁用 `SQL*Plus` `SET` 命令将也将禁用 `SQL SET ROLE` 和 `SET TRANSACTION` 命令。

禁用 `SQL*Plus` `START` 命令也将禁用 `SQL*Plus` `e` 和 `ee` 命令。

可以禁用以下 `SQL` 命令：

- `ALTER`
- `ANALYZE`
- `AUDIT`
- `CONNECT`
- `CREATE`
- `DELETE`
- `DROP`
- `GRANT`
- `INSERT`
- `LOCK`
- `NOAUDIT`

## 在 SQL*PLUS 中限制用户特权

- `RENAME`
- `REVOKE`
- `SELECT`
- `SET TRANSACTION`
- `TRUNCATE`
- `UPDATE`

您还可以禁用以下 `PL/SQL` 命令：

- `BEGIN`
- `DECLARE`

> 禁用 `BEGIN` 和 `DECLARE` 不会阻止使用 `SQL*Plus` `EXECUTE` 命令。`EXECUTE` 必须单独禁用。

## 禁用 SET ROLE

`SQL` 命令 `SET ROLE` 允许应用程序用户访问通过应用程序角色授予的权限，这会导致安全问题。为了防止应用程序用户在 `SQL*Plus` 中访问应用程序角色，`DBA` 可以使用 `PRODUCT_USER_PROFILE` 表禁用 `SET ROLE` 命令。这限制了 `SQL*Plus` 用户可以使用其启动 `SQL*Plus` 时启用的角色的权限。

## 禁用角色

要为特定用户禁用某个角色，请在 `PRODUCT_USER_PROFILE` 中插入一行，在 `UserID` 列中包含用户的用户名，在 `Attribute` 列中包含 `ROLES`，在 `Char_Value` 列中包含该角色。

> 如果在禁用角色时在 `UserID` 列输入 `PUBLIC %`，则将为所有用户禁用该角色。`%` 或 `PUBLIC` 应适用于授予给 `PUBLIC` 的角色。

`Oracle` 用户系统拥有 `PRODUCT_USER_PROFILE` 表。当系统用户登录时，`SQL*Plus` 不读取 `PRODUCT_USER_PROFILE` 表。因此，没有 `SQL*Plus` 限制适用于用户系统。

> 由 `PRODUCT_USER_PROFILE` 提供的产品级安全仅由 `SQL*Plus` 强制，而不是由 `Oracle RDBMS` 执行。

## 跟踪 SQL 语句

在 `SQL*Plus 3.3` 之前，获取 `SQL*Plus` 中 `SQL` 语句执行的统计信息非常有限。此目的唯一可用命令是 `SET TIME` 和 `SET TIMING`。

`SET TIME` 命令控制 `SQL*Plus` 如何显示当前时间。`ON` 参数在 `SQL*Plus` 提示符之前显示当前时间，`OFF` 参数抑制当前时间的显示。`SET TIME` 命令的语法为

```
SET TI[ME] { OFF | ON }
```

列表 26.14 显示了使用 `SET TIME` 命令的示例。

### 列表 26.14 估算运行时间

```
SQL> SHOW TIME
time OFF
SQL> SET TIME ON
01:17:57 SQL> SELECT t1.name, t2.name, t2.sal, t2.job
01:18:11     FROM t1, emp t2
01:18:23     WHERE t1.deptno = t2.deptno;
```

| NAME | ENAME | SAL | JOB |
| --- | --- | --- | --- |
| RESEARCH | SMITH | 800 | CLARK |
| SALES | ALLEN | 1600 | SALESMAN |
| SALES | WARD | 1250 | SALESMAN |
| RESEARCH | JONES | 2975 | MANAGER |
| SALES | MARTIN | 1250 | SALESMAN |
| SALES | BLAKE | 2850 | MANAGER |
| ACCOUNTING | CLARK | 2450 | MANAGER |
| RESEARCH | SCOTT | 3000 | ANALYST |
| ACCOUNTING | KING | 5000 | PRESIDENT |
| SALES | TURNER | 1500 | SALESMAN |
| RESEARCH | ADAMS | 1100 | CLARK |
| RESEARCH | FORD | 950 | CLARK |
| ACCOUNTING | MILLER | 1300 | CLARK |

14 rows selected.

01:18:43 SQL>

通过从最后一行显示的时间 (01:18:43) 减去执行后第一个提示符显示的时间 (01:18:23)，用户可以获得执行查询所需的时间（包括输入 WHERE 子句的时间）。使用此方法计算的运行时间比 `SQL*Plus` 接口的实际运行时间短。

`SET TIMING` 命令控制执行统计信息的显示。`SET TIMING` 命令的语法为

```
SET TI[NG] { OFF | ON }
```

`SET TIMING ON` 显示 `SQL*Plus` 中执行的每个 `SQL` 或 `PL/SQL` 块的执行统计信息。`SET TIMING OFF` 抑制时间的显示。列表 26.15 显示了 `SET TIMING` 命令的示例。

### 列表 26.15 执行计时

```
SQL> SHOW TIMING
timing OFF
SQL> SET TIMING ON
SQL> SELECT t1.ename, t2.ename, t2.sal, t2.job
  FROM dept t1, emp t2
  WHERE t1.deptno = t2.deptno;
```

| NAME | ENAME | SAL | JOB |
| --- | --- | --- | --- |
| RESEARCH | SMITH | 800 | CLARK |
| SALES | ALLEN | 1600 | SALESMAN |
| SALES | WARD | 1250 | SALESMAN |
| RESEARCH | JONES | 2975 | MANAGER |
| SALES | MARTIN | 1250 | SALESMAN |
| SALES | BLAKE | 2850 | MANAGER |
| ACCOUNTING | CLARK | 2450 | MANAGER |
| RESEARCH | SCOTT | 3000 | ANALYST |
| ACCOUNTING | KING | 5000 | PRESIDENT |
| SALES | TURNER | 1500 | SALESMAN |
| RESEARCH | ADAMS | 1100 | CLARK |
| RESEARCH | FORD | 950 | CLARK |
| ACCOUNTING | MILLER | 1300 | CLARK |

14 rows selected.

real: 00:00:90

如列表 26.14 和 26.15 所示，`SET TIME` 和 `SET TIME` 命令为 `SQL*Plus` 中执行的 `SQL` 语句或 `PL/SQL` 块提供了非常基础但不精确的计时统计信息。在 `SQL*3.3` 之前，`SQL*Plus` 无法获取优化器的执行/访问路径信息。

从 `SQL*3.3` 开始了一个新功能 `autoTRACE`。它允许 `SQL*Plus` 用户在 `SQL*Plus` 中查看 `DML` 语句（`SELECT`、`INSERT`、`UPDATE` 和 `DELETE`）的执行情况，而无需使用 `Oracle` 用于跟踪 `SQL` 语句执行的常规设施（`SQL_TRACE`、`PLAN` 和 `TKPROF` 工具）。

要启用此功能，`DBA` 必须以 `SYS` 用户运行名为 `PLUSTRACE.SQL` 的 `SQL` 脚本。`PLUSTRACE.SQL` 文件的位置取决于操作系统。`PLUSTRACE` 脚本执行以下操作：

- 创建名为 `PLUSTRACE` 的角色
- 授予 `PLUSTRACE` 角色对 `VSTAT`、`VSTATNAME` 和 `VSESSION` 表的 `SELECT` 权限
- 以 `ADMIN OPTION` 将 `PLUSTRACE` 角色授予 `DBA` 角色

为用户启用 `AUTOTRACE` 功能必须满足三个条件：

- 用户必须由任何授予 `DBA` 角色的用户授予 `PLUSTRACE` 角色
- 用户必须在自己的模式中创建 `PLAN_TABLE`。用户运行 `utxplan.sql` 脚本来实现此操作。该脚本位于 `UNIX` 平台的 `ORACLE_HOME/rdbms/admin` 目录 `Windows 95/NT` 下的 `%ORACLE_HOME%\Rdbms8\Admin`
- 系统变量 `AUTOTRACE` 必须适当设置

执行这些步骤后，用户可以在成功运行任何 `DML` 语句（`SELECT`、`INSERT`、`DELETE`、`UPDATE`）后获取优化器使用的执行路径和执行统计报告。报告的输出由 `AUTOTRACE` 系统变量控制。

`AUTOTRACE` 系统变量的允许设置及其结果列于表 26.5。
