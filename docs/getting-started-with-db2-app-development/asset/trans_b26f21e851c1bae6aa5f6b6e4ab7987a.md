

### 3.3.10.1 条件处理

要处理条件，您可以创建一个条件处理程序，其中必须指定：

-   它处理哪些条件
-   在哪里恢复执行（基于处理程序类型：CONTINUE、EXIT 或 UNDO）
-   为处理该条件需要执行哪些操作。这些操作可以是任何语句，包括控制结构。

如果引发 `SQLEXCEPTION` 条件且没有处理程序，过程将终止并返回错误给客户端。

### 3.3.10.2 处理程序类型

有三种类型的处理程序：

-   **CONTINUE** – 此处理程序用于指示，在引发异常且处理程序处理完条件后，流程将**继续**执行引发条件的那个语句之后的下一条语句。
-   **EXIT** – 此处理程序用于指示，在引发异常且处理程序处理完条件后，流程将跳转到过程的结尾。
-   **UNDO** – 此处理程序用于指示，在引发异常且处理程序处理完条件后，流程将跳转到过程的结尾，并撤消或回滚已执行的任何语句。

*图 3.10 展示了不同的条件处理程序及其行为。*

![](img/5f6ba170efa3a607142589708531bef8_99_0.png)

## 3.3.11 调用存储过程

以下代码片段（在 *清单 3.5、3.6 和 3.7* 中展示）分别说明了如何从 CLI/ODBC、VB.NET 和 Java 程序中调用存储过程。

```c
SQLCHAR *stmt = (SQLCHAR *)
"CALL MEDIAN_RESULT_SET( ? )";
SQLDOUBLE  sal = 20000.0;  /* Bound to parameter marker in stmt */
SQLINTEGER salind = 0;     /* Indicator variable for sal */

sqlrc = SQLPrepare(hstmt, stmt, SQL_NTS);
sqlrc = SQLBindParameter(hstmt, 1, SQL_PARAM_OUTPUT,
    SQL_C_DOUBLE, SQL_DOUBLE, 0, 0, &sal, 0, &salind);
SQLExecute(hstmt);

if (salind == SQL_NULL_DATA)
    printf("Median Salary = NULL\n");
else
    printf("Median Salary = %.2f\n\n", sal);

/* Get first result set */
sqlrc = StmtResultPrint(hstmt);
/* Check for another result set */
sqlrc = SQLMoreResults(hstmt);
if (sqlrc == SQL_SUCCESS) {
    /* There is another result set */
    sqlrc = StmtResultPrint(hstmt);
}
```

**清单 3.5 - 从 CLI/ODBC 应用程序调用存储过程的示例**

有关更多详细信息，请参阅 DB2 示例文件：`sqllib/samples/sqlproc/resultset.c`

```vbnet
Try
    ' Create a DB2Command to run the stored procedure
    Dim procName As String = "TRUNC_DEMO"
    Dim cmd As DB2Command = conn.CreateCommand()
    Dim parm As DB2Parameter

    cmd.CommandType = CommandType.StoredProcedure
    cmd.CommandText = procName

    ' Register the output parameters for the DB2Command
    parm = cmd.Parameters.Add("v_lastname", DB2Type.Varchar)
    parm.Direction = ParameterDirection.Output
    parm = cmd.Parameters.Add("v_msg", DB2Type.VarChar)
    parm.Direction = ParameterDirection.Output

    ' Call the stored procedure
    Dim reader As DB2DataReader = cmd.ExecuteReader
Catch myException As DB2Exception
    DB2ExceptionHandler(myException)
Catch
    UnhandledExceptionHandler()
End Try
```

**清单 3.6 - 从 VB.NET 应用程序调用存储过程的示例**

```java
try
{
   // Connect to sample database
   String url = "jdbc:db2:sample";
   con = DriverManager.getConnection(url);

   CallableStatement cs = con.prepareCall("CALL trunc_demo(?, ?)");

   // register the output parameters
   cs.registerOutParameter(1, Types.VARCHAR);
   cs.registerOutParameter(2, Types.VARCHAR);

   cs.execute();
   con.close();
}
catch (Exception e)
{
   /* exception handling logic goes here */
}
```

**清单 3.7 - 从 Java 应用程序调用存储过程的示例**

## 3.3.12 动态 SQL

在动态 SQL 中，与静态 SQL 不同，在运行时并非整个 SQL 语句都是已知的。例如，如果此语句中的 *coll* 和 *tabname* 是变量，那么我们就在处理动态 SQL：

```sql
'SELECT ' || coll || ' FROM ' || tabname;
```

对于 DDL，建议使用动态 SQL以避免依赖问题和服务包失效。它也是实现递归所必需的。

动态 SQL 可以使用两种方法执行：

-   使用 EXECUTE IMMEDIATE 语句 – 这适用于单次执行的 SQL
-   使用 PREPARE 语句配合 EXECUTE 语句 - 这适用于多次执行的 SQL

清单 3.8 中展示的代码片段提供了使用这两种方法实现动态 SQL 的示例。该示例假设已创建表 T2，其定义如下：

```sql
CREATE TABLE T2 (c1 INT, c2 INT)
```

```sql
CREATE PROCEDURE dyn1 (IN value1 INT, IN value2 INT)
SPECIFIC dyn1
BEGIN
    DECLARE stmt varchar(255);
    DECLARE st STATEMENT;

    SET stmt = 'INSERT INTO T2 VALUES (?, ?)';
    PREPARE st FROM stmt;

    EXECUTE st USING value1, value1;
    EXECUTE st USING value2, value2;

    SET stmt = 'INSERT INTO T2 VALUES (9, 9)';
    EXECUTE IMMEDIATE stmt;
END
```

**清单 3.8 - 使用动态 SQL 的存储过程示例**

## 3.4 Java 存储过程

DB2 中的 Java 存储过程是使用 CREATE PROCEDURE 语句创建的，该语句提供过程的定义，并指向外部 Java 应用程序。可以使用 IBM Data Studio 轻松创建 Java 存储过程。您可以遵循第 3.2 节中讨论的步骤，选择 Java 作为语言。IBM Data Studio 还允许您为过程选择 JDBC 或 SQLJ。如果在创建 Java 存储过程时接受所有默认设置，系统将为您生成相应的 Java 应用程序。图 3.11 展示了创建了 Java 存储过程的 IBM Data Studio。图 3.12 显示了相应的 Java 源代码。

![](img/5f6ba170efa3a607142589708531bef8_103_0.png)

**图 3.11 - Java 存储过程的 CREATE PROCEDURE 定义**

![](img/5f6ba170efa3a607142589708531bef8_104_0.png)

**图 3.12 – Java 存储过程的 Java 源代码**

## 3.5 用户定义函数：宏观视角

用户定义函数（UDF）是一种数据库应用程序对象，它将一组输入数据值映射为一组输出值。例如，一个函数可能接收以英寸为单位的测量值作为输入，并返回以厘米为单位的结果。

DB2 支持使用 SQL PL、PL/SQL、C/C++、Java、CLR（公共语言运行时）和 OLE（对象链接与嵌入）创建函数。在本书中，由于 SQL PL 函数的简单性、流行性和性能，我们重点关注 SQL PL 函数。

> **注意：**
> 在 DB2 9.7 之前，UDF 仅支持 SQL PL 语句的一个子集，称为内联 SQL PL。在 DB2 9.7 中，所有 SQL PL 语句都得到完全支持。

> **注意：**
> 要了解有关 UDF 的更多信息，请观看此视频：
> http://www.channeldb2.com/video/video/show?id=807741/Video:4362

函数有四种类型：标量、表、行和列函数。在本书中，我们仅关注标量函数和表函数。

### 3.5.1 标量函数

标量函数返回单个值。标量函数不能包含会更改数据库状态的 SQL 语句；即，不允许使用 INSERT、UPDATE 和 DELETE 语句。一些内置的标量函数包括 SUM()、AVG()、DIGITS()、COALESCE() 和 SUBSTR()。

DB2 允许您构建自定义用户定义函数，您可以其中封装经常使用的逻辑。清单 3.9 提供了标量函数的一个示例。

```sql
CREATE FUNCTION deptname (p_empid VARCHAR(6))
RETURNS VARCHAR(30)
SPECIFIC deptname
BEGIN ATOMIC
    DECLARE v_department_name VARCHAR(30);
    DECLARE v_err VARCHAR(70);
    SET v_department_name = (
        SELECT d.deptname FROM department d, employee e
        WHERE e.workdept = d.deptno AND e.empno = p_empid
    );
    SET v_err = 'Error: employee ' || p_empid || ' was not found';
    IF v_department_name IS NULL THEN
        SIGNAL SQLSTATE '80000' SET MESSAGE_TEXT = v_err;
    END IF;
    RETURN v_department_name;
END
```

**清单 3.9 - 标量函数的示例**

在上面的清单中，函数名为 *deptname*，它根据员工 ID 返回员工所属部门的名称。可以使用 VALUES 语句调用标量 UDF。也可以在 SQL 语句中期望标量值的地方调用它。例如，尝试从 DB2 命令窗口或从 Linux 或 UNIX 终端执行以下操作：

```bash
db2 "values (deptname ('000300'))"
```

或者

```bash
db2 "select (deptname ('000300')) from sysibm.sysdummy1"
```

注意在第二个示例中使用了 SYSIBM.SYSDUMMY1。这是一个特殊的虚拟表，包含一行和一列。它用于确保只返回一个值。如果您尝试用任何行数更多的其他表执行相同的 SELECT 语句，该函数将被调用与表中行数相同次数。

