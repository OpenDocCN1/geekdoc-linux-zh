
图 4.10 展示了在 Java 程序中使用 XQuery 的示例。同样，在 Java 程序中使用 SQL/XML 或 XQuery 并没有什么特别之处。

```java
try {
    // get a database connection
    Connection conn = Conn.getconn();
    // define, prepare, and execute an XQuery (without SQL).
    // note that we must hard-code query predicate values.
    String query = "xquery for $y in dd2-fn:xmlicolumn"
            + "(\"CLIENTS.CONTACTINFO\")/$client = "
            + "where $y/Address/city='San Jose' and $y/Address/state=\"CA\" "
            + "return <emailList> { $y/email } </emailList>";
    PreparedStatement selectStmt = conn.prepareStatement(query);
    ResultSet rs = selectStmt.executeQuery();
    // iterate over all items in the sequence and print results.
    while (rs.next()) {
        System.out.println(rs.getString(1));
    }
    // release all resources
} catch (Exception e) {
    // catch and handle any exceptions
}
```

**图 4.10 - 在 Java 程序中使用 XQuery**

> **注意：**
> 有关 JDBC 的更完整说明，包括关于数据库元数据、批量更新、事务、保存点、处理大型对象等主题，可以在 IBM 红皮书 *DB2 Express-C: The Developer Handbook for XML, PHP, C/C++, Java, and .NET (SG24-7301-00)* 中找到。有关更多信息，请参见本书的资源部分。

## 4.4 SQLJ 编程

SQLJ 编程是将 SQL 语句嵌入到 Java 程序中的标准。所有 SQL 语句都是使用*上下文*静态执行的。上下文提供有助于解释 SQL 语句执行位置的信息。有不同类型的上下文：

- **连接上下文。** 这相当于 JDBC 中的**Connection** 对象。当未指定连接上下文时，会使用默认连接上下文。
- **执行上下文。** 这是获取执行 SQL 语句前后相关信息的必要条件。

### 4.4.1 SQLJ 语法

在使用 SQLJ 时，可以使用不同的语法来帮助预编译器识别需要从嵌入 SQL 的 Java 程序中的其他语句中转换的语句。虽然语法的类型不同，但它们都以**“#sql”开头，并使用花括号作为定界符，如下所示：**

- `#sql [connection-context] { sql statement }`
- `#sql [connection-context, execution context] { sql statement }`
- `#sql { sql statement }`
- `#sql [execution context] { sql statement }`

主机变量可以通过冒号来识别，如下例所示：

```java
#sql {SELECT EMPNO FROM EMP WHERE WORKDEPT = :dept};
```

### 4.4.2 连接上下文

要在 SQLJ 程序中处理 SQL，首先需要建立数据库连接。连接上下文即用于此目的。在下面的*清单 4.17*和*清单 4.18*中，展示了处理连接上下文的不同方法。

```java
(1) #sql context ctx; // This should be outside the class
(2) Class.forName("com.ibm.db2.jcc.DB2Driver").newInstance();
(3) ctx ctx1 = new ctx("jdbc:db2:sample", false);
(4) #sql [ctx1] { DELETE FROM dept };
```

**清单 4.17 - 处理连接上下文**

在上述清单中：

1. 使用以下语法声明连接上下文类：
   ```
   #sql context <context-class-name>
   ```
2. 加载 JDBC 驱动程序；类似于 JDBC 程序。
3. 调用*context*类的构造函数。
4. 在连接上下文**"ctx1"**下执行 SQL 语句（**DELETE**）。

*清单 4.18*中的这个其他示例与此类似，但它将 JDBC 连接对象与 SQLJ 结合使用。

```java
#sql context ctx; // This should be outside the class
Class.forName("com.ibm.db2.jcc.DB2Driver").newInstance();
(1) Connection con = DriverManager.getConnection();
(2) ctx ctx1 = new ctx(con);
#sql [ctx1] { DELETE FROM dept };
```

**清单 4.18 - 从 Connection 对象创建连接上下文的示例：**

在上述清单中：

1. 使用一个 **Connection** 对象。
2. 调用 *context* 类的构造函数。

此外，您还可以为连接创建一个默认上下文。这意味着以后在执行 SQL 操作时无需指定上下文，因为将使用指定为默认的上下文。语法形式如下：

```java
#sql ( sql statement )
```

*清单 4.19* 提供了一个示例。

```java
Class.forName("com.ibm.db2.jcc.DB2Driver").newInstance();
Connection con = DriverManager.getConnection();
(1) DefaultContext ctx1 = new DefaultContext(con);
(2) DefaultContext.setDefaultContext(ctx1);
(3) #sql ( DELETE FROM dept );
```

**清单 4.19 - 具有默认上下文的连接示例**

在上述清单中：

1. 创建一个 DefaultContext。
2. 将默认上下文设置为 *ctx1*。
3. 指定要执行的 SQL，在此情况下是一条 **DELETE** 语句。请注意，语法中不需要指定上下文名称。将使用默认上下文 *ctx1*。

*清单 4.20* 下面提供了一个使用默认上下文的完整 SQLJ 程序示例。

```java
import java.sql.*;
(1) import sqlj.runtime.*;       // SQLJ runtime support
(2) import sqlj.runtime.ref.*;   // SQLJ runtime support

class myprg3 {
    public static void main(String argv[]) {
        try {
            Connection con = null;
            Class.forName("com.ibm.db2.jcc.DB2Driver");
            String url = "jdbc:db2://127.0.0.1:50000/SAMPLE";
            if (argv.length == 2) {
                String userID = argv[0];
                String passwd = argv[1];
                con = DriverManager.getConnection(url, userID, passwd);
            } else {
                throw new Exception("\n Usage: java myprg3 userID password\n");
            }
            (3) DefaultContext ctx = new DefaultContext(con);
            (4) DefaultContext.setDefaultContext(ctx);
            (5) if (ctx != null) {
                (6) ctx.close();
            }
        } catch (Exception e) {
        }
    }
}
```

**清单 4.20 - 一个完整的 SQLJ 程序**

在上述清单中：

1. 第 1 项和第 2 项：需要导入这些包以提供 SQLJ 运行时支持。
2. 第 3 项：创建默认上下文。
3. 第 4 项：设置要使用的默认上下文。
4. 第 5 项：如果上下文未关闭。
5. 第 6 项：关闭上下文/断开连接。

### 4.4.3 执行上下文

执行上下文在 SQL 语句执行期间对其进行监控和控制；它相当于 JDBC 中的 Statement 接口，并在连接上下文对象中创建。

要创建 ExecutionContext 对象，请使用连接上下文的 getExecutionContext 方法。一些 ExecutionContext 方法在 SQL 语句执行前有效，而其他方法仅在执行后有效。

清单 4.21 提供了一个示例。

```java
#sql context ctx; // this should be outside the class
String url = "jdbc:db2:sample";
Class.forName("com.ibm.db2.jcc.DB2Driver").newInstance();
Connection con = DriverManager.getConnection(url);
ctx ctx1 = new ctx(con);
(1) ExecutionContext execTx1 = ctx1.getExecutionContext();
(2) #sql [ctx1, execTx1] { DELETE FROM purchaseorder WHERE status='UnShipped' };
(3) int i = execTx1.getUpdateCount();
```

**清单 4.21 - 使用执行上下文的示例**

在上述清单中：

1. (1) 使用连接上下文对象的 getExecutionContext 方法创建执行上下文。
2. (2) 指定与连接上下文 *ctx1* 和执行上下文 *execTx1* 关联的 SQL。
3. (3) 调用执行上下文对象的 getUpdateCount 方法以获取被删除或更新的记录数。

### 4.4.4 迭代器

*迭代器*相当于 JDBC 结果集。迭代器有两种类型：

- **命名迭代器**：通过结果集中列的名称来识别行。在定义命名迭代器时，指定列名及其数据类型。
- **位置迭代器**：通过其在结果集中的位置来识别行。在定义位置迭代器时，仅指定列的数据类型。

*清单 4.22* 提供了一个命名迭代器的示例。

```java
(1) #sql iterator namediterator (int *poid*, String *status*);
(2) namediterator *iterator1*;
(3) #sql [*ctx1*] *iterator1* = { select *poid*, *status* from *purchaseorder* };
(4) while (*iterator1*.next()) {
(5)     System.out.println("poid: " + *iterator1*.poid() + "Status: " + *iterator1*.status());
}
(6) *iterator1*.close();
```

**清单 4.22 - 一个命名迭代器的示例**

在上述清单中：

1. (1) 声明了一个具有两列的命名迭代器。请注意，列名 *poid* 和 *status* 被明确提及。这就是为什么这是一个命名迭代器。
2. (2) 声明了一个名为 *iterator1* 的命名迭代器。
3. (3) 在连接上下文 *ctx1* 中，使用 "select *poid*, *status* from *purchaseorder*" 定义 *iterator1*。
4. (4) 循环遍历迭代器。
5. (5) 打印检索到的每一行的 *poid* 和 *status*。注意语法："*iterator1*.poid()"，以及 "*iterator1*.status()"。
6. (6) 关闭 *iterator1*。

*清单 4.23* 提供了一个位置迭代器的示例。

```java
(1) #sql iterator *positionedIterator* (int, String);
(2) String *status* = null;
(3) int *poid* = 0;
(4) *positionedIterator* *iterator1*;
(5) #sql [*ctx1*] *iterator1* = ( select *poid*, *status* from *purchaseorder* );
(6) #sql { fetch : *iterator1* into : *poid*, : *status* };
(7) while (*iterator1*.endFetch()) {
(8)     System.out.println("poid: " + *poid* + "Status: " + *status*);
}
```
