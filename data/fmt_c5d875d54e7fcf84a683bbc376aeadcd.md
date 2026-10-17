
`ConnStatus PQstatus(PGconn *conn);`

它返回枚举值之一：`CONNECTION_OK` 或 `CONNECTION_BAD`，它们的含义显而易见。一旦建立了良好的连接，它将一直保持“良好”，除非出现网络问题或远程数据库被关闭。

如果连接出现问题，可以通过以下命令获取有意义的错误信息：

```c
char *PQerrorMessage(PGconn *conn);
```

它返回一个字符串。

# 第 4 章

```c
#include <stdio.h>
#include <stdlib.h>
#include <libpq-fe.h>

int main() {
    PGconn *conn;
    const char *connstr = "host=localhost dbname=template";

    conn = PQconnectdb(connstr);
    if (PQstatus(conn) == CONNECTION_BAD) {
        fprintf(stderr, "连接数据库失败: %s\n", PQerrorMessage(conn));
    } else {
        printf("连接成功\n");
    }

    PQfinish(conn);
    return 0;
}
```

## 执行 SQL 语句

在服务器上执行查询异常地简单。只有一个函数可以调用。执行 SQL 语句时调用：

```c
PGresult *res = PQexec(conn, sql_string);
```

结果将是 `ExecStatus`，具有以下值之一：

```c
ExecStatusType status = PQresultStatus(result);
```

| status | 描述 |
| :--- | :--- |
| `PGRES_EMPTY_QUERY` | 无操作。 |
| `PGRES_COMMAND_OK` | 执行成功，但没有返回数据。 |
| `PGRES_TUPLES_OK` | 执行成功，并可能返回数据。 |
| `PGRES_COPY_OUT` | 正在向外部文件拷贝。 |
| `PGRES_COPY_IN` | 正在从外部文件拷贝。 |
| `PGRES_BAD_RESPONSE` | 发生了意外情况。 |
| `PGRES_NONFATAL_ERROR` | 发生了非致命错误。 |
| `PGRES_FATAL_ERROR` | 发生了致命错误。 |

注意 `PGRES_TUPLES_OK` 的仔细定义。接收此响应意味着 SQL 语句执行成功，但并不意味着返回了任何数据。

如果你想要文本消息，可以：

```c
const char *PQresultErrorMessage(PGresult *result);
```

注意，这与连接相关的错误不同，在那种情况下我们使用 `PQerrorMessage` 获取文本消息。

知道受 SQL 命令影响的行数通常很有用。对于 `DELETE` 命令尤其是如此，因为如果你执行了一个语法正确但实际上没有删除任何行的 `DELETE` 命令，PostgreSQL 认为该命令执行成功。

对于 `INSERT`、`UPDATE` 和 `DELETE` 命令，我们可以通过 `PQcmdTuples` 获取影响的行数。

```c
const char *PQcmdTuples(PGresult *result);
```

注意它返回的是一个 `char *result`，包含以 NULL 结尾的数字格式字符串，而不是你预期的整数。

## 调试与示例程序

本节中另一个对调试非常有用的函数是：

```c
const char *PQresStatus(ExecStatusType status); // 将状态枚举转换为描述性字符串。
```

现在我们已经掌握了足够的知识来编写执行 SQL 的 C 程序了。由于我们还不知道如何从查询中检索结果，我们将继续专注于执行一个 `DELETE` 操作。这里是我们的第一个具有实际用途的 C 程序 `dell.c`，它扩展了最初的 `conn.c`。这一次，我们连接到名为 `gwl` 的服务器上的数据库 `rick`。

在整个章节中，我们将对数据库中名为 `children` 的单表进行实验，该表是在上一章中创建的。如果你需要重新创建该表，在 `psql` 中输入的 SQL 如下：

```sql
CREATE TABLE children (
  childno SERIAL,
  fname VARCHAR,
  age INTEGER
);
```

`conn.c` 和 `dell.c` 之间变化的行已高亮：

```c
#include <stdlib.h>
#include <stdio.h>
#include <libpq-fe.h>
int main() {
  PGconn *conn;
  PGresult *result;
  const char *connection_str = "host=gwl dbname=rick";
  conn = PQconnectdb(connection_str);
  if (PQstatus(conn) == CONNECTION_BAD) {
    fprintf(stderr, "Connection to %s failed, %s", connection_str, PQerrorMessage(conn));
    PQfinish(conn);
  }
  printf("Connected OK\n");
  result = PQexec(conn, "DELETE FROM children WHERE fname = 'freda'");
  if (!result) {
    printf("PQexec command failed, no error code\n");
  }
  else {
    switch (PQresultStatus(result)) {
      case PGRES_COMMAND_OK:
        printf("Command executed OK. %s rows affected\n", PQcmdTuples(result));
        break;
      case PGRES_TUPLES_OK:
        printf("Query may have returned data\n");
        break;
      default:
        printf("Command failed with code %s, error message %s\n",
               PQresStatus(PQresultStatus(result)),
               PQresultErrorMessage(result));
        break;
    }
  }
  PQclear(result);
  PQfinish(conn);
  return EXIT_SUCCESS;
}
```

如果我们确保 `children` 表中有一行的 `fname` 列的值为 `freda`，那么当我们编译并执行此程序时：

```bash
[rick@gw1$] ./dell
Connected OK
Command executed OK. 1 rows affected
```

现在已经没有符合此标准的行被删除了。如果我们再次执行该程序，它仍然会执行成功，但这次没有行受到影响：

```bash
[rick@gw1$] ./dell
Connected OK
Command executed OK, 0 rows affected
```

你必须仔细区分“未影响任何行的语句”和“由于语法错误而失败的语句”。

## 从查询中获取结果

现在我们来到 `libpq` 中最常用、也最复杂的部分——检索数据。

当我们检索数据时，可能会遇到一些问题。通常情况下，我们无法预先知道将检索多少行。如果我们使用 `*` 列名来执行 `SELECT` 语句以检索所有列，我们可能甚至不知道所检索的行中有多少字段或什么类型的数据。应对这些情况正使得 API 的这部分变得更加复杂。别担心，这并不是什么火箭科学，只是多有几个 API 调用需要了解而已。

让我们把 `dell.c` 测试程序转换为一个返回数据的查询，并顺便对其进行重构，以便在执行 SQL 语句后更容易地添加新功能。这个新文件是 `self.c`：

```c
#include <stdlib.h>
#include <stdio.h>
```
