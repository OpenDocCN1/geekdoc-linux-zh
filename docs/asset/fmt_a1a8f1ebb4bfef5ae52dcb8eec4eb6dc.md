
`fprintf(stderr,"CLI error %d in SQLFreeHandle\n", clIRC); exit(clIRC);`

}

```c
/* disconnect from the database */

if((clIRC = SQLDisconnect(hdbc)) != SQL_SUCCESS) {

    fprintf(stderr,"CLI error %d in SQLConnect\n", clIRC); exit(clIRC);

}
```

```c
/* Free database handle */

if((clIRC = SQLFreeHandle(SQL_HANDLE_DBC, hdbc)) != SQL_SUCCESS) {

    fprintf(stderr,"CLI error %d in SQLFreeHandle\n", clIRC); exit(clIRC);

}
```

```c
/* Free environment handle */

if((clIRC = SQLFreeHandle(SQL_HANDLE_ENV, henv)) != SQL_SUCCESS) {

    fprintf(stderr,"CLI error %d in SQLFreeHandle\n", clIRC); exit(clIRC);

}
```

## 示例 8-10 运行 CLI

```bash
db2inst1@puget:~$ export LD_LIBRARY_PATH=/home/db2inst1/sqlib/lib
db2inst1@puget:~$ cc -I /home/db2inst1/sqlib/include cli_test.c
db2inst1@puget:~$ cc -o cli_test -L/home/db2inst1/sqlib/lib -ldb2 cli_test.o
db2inst1@puget:~$ ./cli_test
000290
00310
200310
200330
200340
```

注意：你可以在 Information Center 中选择 Database application development -> Database Applications -> CLI 来阅读 CLI 函数的详细介绍。你可以通过选择 Reference -> APIs -> CLI 获取详细的参考信息。可用手册包括《Call Level Interface Guide and Reference, Volume 1, SC23-5844》以及《Call Level Interface Guide and Reference, Volume 2, SC23-5845》。

# 嵌入式 SQL

嵌入式 SQL 允许将 SQL 语句直接放入 C/C++ 代码中。在用 C/C++ 编译之前，嵌入式 SQL 需要经过预编译。预编译步骤生成一个绑定文件（包）和一个程序文件。包具有后缀 `.bind`。程序文件可以使用 C/C++ 编译器编译。包包含了嵌入式 SQL 语句的执行计划。该包专门用于此文件。如果你再次编译程序文件，将获得一个新的绑定文件。在运行之前，你需要将相关的包绑定到数据库。使用包的优势是 SQL 语句的执行计划在预编译期间已经生成，运行时不再需要生成。对于复杂的 SQL 语句，此功能可以节省大量时间。包允许你向用户或应用程序授予权限，而无需授予表权限。为了运行嵌入式 SQL 程序，系统需要安装 DB2 客户端。示例 8-11 显示了使用嵌入式 SQL 的程序。它从 EMPLOYEE 表读取记录并使用游遍历结果集。在运行示例之前，你需要替换 `<password>`。

## 示例 8-11 嵌入式 SQL 程序：test_emb.sqc

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
int main(int argc, char *argv[])
{
    EXEC SQL DECLARE
    char empno[7];
    char database[20];
    char user[20];
    char password[20];
    strcpy(database, "SAMPLE");
    strcpy(user, "db2inst1");
    strcpy(password, "<password>");
    EXEC SQL CONNECT TO :database USING :password;
    if(sqlca.sqlcode != 0) {
      fprintf(stderr,"Error connect %d\n", sqlca.sqlcode);
      exit(sqlca.sqlcode);
    }
    EXEC SQL DECLARE EMP_CUR CURSOR FOR
SELECT EMPNO FROM EMPLOYEE WHERE SALARY < 36000;
    EXEC SQL OPEN EMP_CUR;
    if(sqlca.sqlcode != 0) {
      fprintf(stderr,"Error open %d\n", sqlca.sqlcode);
      exit(sqlca.sqlcode);
    }
    EXEC SQL FETCH EMP_CUR INTO :empno;
    if(sqlca.sqlcode != 0) {
      fprintf(stderr,"Error fetch %d\n", sqlca.sqlcode);
      exit(sqlca.sqlcode);
    }
    while (sqlca.sqlcode != 100) {
      printf("%s\n", empno);
      EXEC SQL FETCH EMP_CUR INTO :empno;
      if(sqlca.sqlcode != 0) {
        fprintf(stderr,"Error fetch %d\n", sqlca.sqlcode);
        exit(sqlca.sqlcode);
      }
    }
    EXEC SQL CLOSE EMP_CUR;
    if(sqlca.sqlcode != 0) {
      fprintf(stderr,"Error close %d\n", sqlca.sqlcode);
      exit(sqlca.sqlcode);
    }
}
```

在示例 8-12 中，我们编译并运行程序。预编译步骤生成 `.c` 和 `.bnd` 文件。第一个 `cc` 步骤编译 C 程序，第二个 `cc` 步骤将其链接起来。

## 示例 8-12 运行嵌入式 SQL 程序

```bash
db2inst1@puget> db2 connect to SAMPLE
```

### 数据库连接信息

| 数据库服务器 | = DB2/LINUX 9.5.0 |
| SQL 授权 ID | = DB2INST1 |
| 本地数据库别名 | = SAMPLE |

```bash
db2inst1@puget> db2 precompile test_emb.sqc bindfile
```

```
LINE MESSAGES FOR test_emb.sqc
SQL0006W "C" 预编译器正在运行。
SQL0091W 预编译或绑定结束时有“0”个错误和“0”警告。
db2inst1@puget> cc -c -L/home/db2inst1/sqlib/include test_emb.c
db2inst1@puget> cc -o test_emb -L/home/db2inst1/sqlib/lib -ldb2 test_emb.o
db2inst1@puget> ./test_emb
00290
000310
200310
200330
200340
```

如果你想在另一个数据库上运行此程序，必须通过以下命令绑定包文件：
`db2 bind test_emb.bnd`

否则，你将收到 `-805` SQL 错误。

> 注意：你可以在《Developing Embedded SQL Applications, SC23-5852》中获取更多文档。

# 管理 API

管理 API 为不同的编程语言提供了应用程序接口。它允许你从应用程序对数据库执行各种管理命令。例如，你可以启动数据库，或创建表空间。

你可以在 Information Center 中选择 Database administration -> Administrative interfaces -> Administrative APIs 以及在 Administrative API Reference, SC23-5842 获取有关该 API 的更多信息。

# C 语言 UDF

C 是支持的用户定义函数（UDF）语言之一。如果你希望在多个应用程序中访问相同的业务逻辑，并且难以共享通用 API，UDF 是一个很好的选择。在程序代码编译后，使用 `CREATE FUNCTION` 命令将函数注册到数据库管理器。

示例 8-13 显示了用 C 编写的 UDF。它将字符串转换为小写。

## 示例 8-13 C 语言编写的 UDF 示例：tolower.c

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sqludf.h>
void SQL_API_FN
to_lower(SQLUDDF_VARCHAR *value,
SQLUDDF_VARCHAR *result,
SQLUDDF_NULLIND *value_ind,
SQLUDDF_NULLIND *result_ind,
SQLUDDF_TRAIL_ARGS)
{
    int i, len;
    if(*value_ind == -1) {
    *result_ind = -1;
    return;
    }
    len = strlen(value);
    for(i = 0; i < len; i++) {
        result[i] = tolower(value[i]);
    }
    result[i] = '\0';
}
```

在第 448 页的示例 8-14 中，我们编译这个 UDF。第一个 `cc` 步骤编译程序，第二个 `cc` 步骤创建动态对象。在 64 位机器上，请使用选项 `-m64` 和 `lib64` 代替。

## 示例 8-14 编译 UDF

```bash
db2inst@puget:> SQL=~/home/db2inst/sqlib tolower.c -D_REENTRANT
db2inst@puget:> cc -m32 -fpic -i$SQL/include -c tolower.c
db2inst@puget:> cc -m32 -fpic -shared -o tolower tolower.o -W1,-rpart,RLL -L$SQL/lib32 -idb2 -lpthread
db2inst@puget:> cp tolower $SQL/function
```

生成的可执行文件 `tolower` 被拷贝到目录 `<instancehome>/lib/function`。从那里开始，数据库管理器将在通过 `CREATE FUNCTION` 命令注册函数后（如示例 8-15 所示）访问该 UDF。

## 示例 8-15 激活 UDF

```sql
CREATE FUNCTION to_lower(VARCHAR(40)) RETURNS VARCHAR(40)
FENCED
EXTERNAL NAME 'tolowerito_lower'
NOT VARIANT NO SQL PARAMETER STYLE DB2SQL LANGUAGE C
NO EXTERNAL ACTION;
```

之后，该 UDF 可以像示例 8-16 所示那样使用。

## 示例 8-16 执行 `to_lower('AAA')`

```bash
db2inst@puget:> db2 "select to_lower('AAA') from sysbm.sysdummy1"
1
aaa
1 record(s) selected.
```

如果你想删除该函数，可以运行命令：
`db2 "DROP FUNCTION to_lower(VARCHAR(40))"`

UDF 可以在围栏（fenced）模式或非围栏（not fenced）模式下运行。围栏例程序作为独立的进程运行，它们涉及一些通信开销。非围栏例程序作为数据库服务器的一部分运行。它们比围栏例程序效率高一点。但是，如果非围栏例程序崩溃，它也会导致数据库服务器崩溃。

因此，我们建议你在围栏模式下开发例程序。如果性能非常重要，你可以考虑将经过良好测试的例程序在生产系统中作为非围栏程序运行。

围栏例程序可以在不同的用户 ID 下运行，这允许你保护它们免受其他实例文件的影响。

在开发 UDF 时，将数据库管理器参数 `KEEPFENCED` 设置为 `NO`，这样每次调用 UDF 都会重新加载该函数。

> 注意：你可以在 *Developing User-defined Routines (SQL and External)*，SC23-5855 中获取更多关于 UDF 的信息。

### 8.3.4 Java

Java 编写将运行在多个平台上的程序的理想语言。与 C 或 C++ 等语言不同，Java 有了完全的规范，每个支持 Java 的平台都支持一个核心库。这些库之一是 JDBC，你可以将其认为 Java 版本的 ODBC。将 Java 与 JDBC 结合允许你编写可移植的数据库应用程序。

> 注意：你可以在 *Developing Java Applications*，SC23-5853 中获取关于为 DB2 编写 Java 信息。

#### JDBC

由于可移植性，你可以在任何系统上开发 Java 应用程序。如果你想在 Linux 下开发 Java 程序，可以使用工具，例如 Data Studio、Eclipse、Rational Developer、Netbeans，或者直接使用 Sun 的纯 Java 开发工具包 (JDK)。

第 450 页的示例 8-17 展示了如何使用纯软件开发工具包 (SDK) 和 Type 4 驱动开发一个基于 JDBC 的小型 Java 程序。它从 SAMPLE 数据库中的 EMPLOYEE 表中选择数据。

首先，驱动由驱动管理器加载。然后，根据驱动 URL 建立连接：`jdbc:db2://<hostname>:<port>/<database>`

```
jdbc:db2://<hostname>:<port>/<database>
```

应用程序随后对表执行 SELECT 操作并遍历结果集。

在运行示例之前，你必须将 `<port>` 替换为实例的端口号，并且将 `<password>` 替换为实际密码。

## 示例 8-17 Sample JDBC Java 程序：test_java.java

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.ResultSet;
import java.sql.Statement;
public class test_java {
    public static void main(String[] args) {
        try {
            Class.forName("com.ibm.db2.jcc.DB2Driver");
            Connection con = DriverManager.getConnection(
                "jdbc:db2://localhost:<port>/SAMPLE",
                "db2inst1",
                "<password>");
            Statement stmt = con.createStatement();
            ResultSet rs = stmt.executeQuery("select empno, salary from employee" + 
                " where salary = 36000 order by lastname");
            while(rs.next()) {
                System.out.println(rs.getString("empno") + " "," + rs.getDouble("salary"));
            }
            con.close();
        } catch (SQLException e) {
            System.out.println(e.getMessage() + "\nSQLCode=" + e.getErrorCode() + 
                ", SQLState=" + e.getSQLState());
        } catch (ClassNotFoundException e) {
            System.out.println(e.getMessage());
        }
    }
}
```
