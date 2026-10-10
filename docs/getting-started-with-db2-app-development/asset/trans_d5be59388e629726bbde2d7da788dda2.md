
## 实现 Statement 接口的类
实现 Statement 接口的类用于执行不包含参数标记的 SQL 语句。Statement 对象通过 Connection 对象的 createStatement 方法创建。

表 4.4 展示了适用于 Statement 对象以执行查询的不同方法。

| 方法 | 描述 |
| --- | --- |
| executeQuery | 当期望获得结果集时使用，例如 SELECT 语句。它返回一个 ResultSet 对象。 |
| executeUpdate | 用于更新数据库内容，例如 INSERT、UPDATE 和 DELETE。它返回一个表示受影响行数整数。 |
| execute | 当在运行时之前不知道执行的语句是 SELECT 还是 UPDATE 语句时使用。如果 SQL 的结果是结果集，则返回 true；如果是更新计数，则返回 false。请结合 getResultSet 或 getUpdateCount 方法使用此方法。 |

### 表 4.4 - Statement 对象的方法

列表 4.4 提供了一个代码片段，说明了 Statement 对象和 executeQuery 方法的使用。

```java
// ...
(1) Statement stmt = con.createStatement();
(2) ResultSet rs = stmt.executeQuery
    ("SELECT EMPNO, FIRSTNAME, LASTNAME " +
     " FROM EMPLOYEE " +
     " WHERE SALARY > 80000" );
(3) while ( rs.next() ) {
       System.out.println("Empno = " + rs.getString(1) +
              " Full name = " + rs.getString(2) +
              " " + rs.getString(3));
   }
(4) rs.close();
(5) stmt.close();
(6) con.close();
} catch (Exception e) {
   e.printStackTrace();
}
} }
```

### 列表 4.4 - Statement 对象：使用 executeQuery 执行 SELECT

开头的三个点表示这是程序的一部分，并没有展示完整的列表。下面解释每个带有编号标记的行：

- (1) **Statement** 对象（或实现 **Statement** 接口的类）可用于执行不包含参数标记的 SQL 语句。可以通过 **Connection** 对象使用 **createStatement** 方法来创建 **Statement** 对象。
- (2) **ResultSet** 对象维护查询结果集当前行的游标。**executeQuery** 方法允许你执行查询（**SELECT**）。如果你想要更新、删除或插入，请使用稍后介绍的 **executeUpdate** 方法。
- (3) 使用 **ResultSet** 对象的 next 方法可以将游标前进到下一行。默认情况下，游标只能向前移动且是只读的。
- (4) 关闭结果集。
- (5) 关闭语句。
- (6) 关闭连接。

如果你想测试上面的代码片段，请适当编辑 *myprg.java* 程序（随书附带）。该程序包含 *列表 4.2* 中显示的连接语句。程序的编译和执行如下所示。

```bash
javac myprg.java
java myprg <userid> <password>
```

输出结果将如 *图 4.6* 所示，其中 *userid* 为 **arfczhong**，密码为 **mypasswd**。

![](img/5f6ba170efa3a607142589708531bef8_134_0.png)

图 4.6 - 执行 myprg.java 程序

下面 *列表 4.5* 中显示的下一个代码片段提供了使用 **Statement** 对象和 **executeUpdate** 方法的示例。

```java
Statement updStmt = con.createStatement();
(1) int numRows = updStmt.executeUpdate
    ("UPDATE EMPLOYEE " +
     "  SET FIRSTNAME = 'Raul', " +
     "      LASTNAME = 'Chong' " +
     "  WHERE EMPNO  = '000010' " );
System.out.println("Number of rows updated: " + numRows);
```

### **列表 4.5** - Statement 对象：使用 executeUpdate 执行 UPDATE

在上述列表中，在第 (1) 行：

**executeUpdate** 方法用于执行 SQL UPDATE 操作，它返回一个表示受影响行数整数。上面的代码片段是 *myprg.java* 程序的一部分。在注释掉程序中的相应部分后，你可以按以下方式运行它：

```bash
javac myprg.java
java myprg <userid> <password>
```

输出结果将如下：

```
Number of rows updated: 1
```

*列表 4.6* 和 *列表 4.7* 中的示例与之前的 *列表 4.5* 类似，但在这种情况下，查询首先被保存在一个名为 *query* 的字符串中，并且我们使用 **executeUpdate** 方法来分别执行 **INSERT** 和 **DELETE** 操作。

```java
String query = null;
query = "INSERT INTO employee (EMPNO, " +
        "FIRSTNAME, LASTNAME, EDLEVEL, SALARY)" +
        "VALUES ('099999', 'Jin', 'Xie', 25, 90000)";
Statement stmt = con.createStatement();
int numRows    = stmt.executeUpdate( query );
System.out.println("Number of rows inserted: " + numRows);
stmt.close();
```

### **列表 4.6** - Statement 对象：使用 executeUpdate 执行 INSERT

```java
String query = null;
query = "DELETE FROM employee where empno = '000999'";
Statement stmt = con.createStatement();
int numRows = stmt.executeUpdate( query );
System.out.println("Number of rows deleted: " + numRows);
stmt.close();
```

### 列表 4.7 - Statement 对象：使用 executeUpdate 执行 DELETE

下面 *列表 4.8* 中显示的下一个代码片段是使用 **execute** 方法的示例。如前所述，当在运行时之前不知道执行的是 **SELECT** 还是更新操作时，会使用此方法，其中更新指的是 SQL **UPDATE**、**INSERT** 或 **DELETE**。

```java
String passedStmt = "SELECT firstname, lastname " +
                   "FROM employee  " +
                   "WHERE salary > 80000";
Statement  stmt       = con.createStatement();
ResultSet  rs         = null;
int        numRows    = 0;
(1) if (stmt.execute(passedStmt)) {
    rs = stmt.getResultSet();
    while (rs.next() ) {
        System.out.println("Full name = " + rs.getString(1) +
               " " + rs.getString(2));
    }
    rs.close();
}
else {
    numRows = stmt.getUpdateCount();
    System.out.println("Number of rows updated: " + numRows);
}
```

### 列表 4.8 - Statement 对象：使用 execute 执行 SELECT 或 UPDATE

在上述列表中，在第 (1) 行：

如果传入的语句（在本例中为 *passedStmt*）是 **SELECT**，execute 方法将返回 *true*。如果是 **UPDATE/INSERT/DELETE**，它将返回 *false*。在这个特定的示例中，我们硬编码了传入的语句；然而，它也可以实现为一个参数。

要使用 *myprg.java* 程序测试此功能，请注释掉程序中的相应部分，并运行这些命令：

```bash
javac myprg.java
java myprg <userid> <password>
```

输出结果将如下：

```
Full name = Raul Chong
Full name = MICHAEL THOMPSON
Full name = SALLY KWAN
Full name = JOHN GEYER
Full name = EVA PULASKI
Full name = EILEEN HENDERSON
Full name = THEODORE SPENSER
```

如果你修改程序，使传入的语句是一个 **UPDATE** 操作，你可以再次测试编译和运行该程序，并会得到以下结果：

```
Number of rows updated: 1
```

### 4.3.2.3 PreparedStatement 接口

实现 **PreparedStatement** 接口的类可用于运行可以包含 **参数标记** 的查询。参数标记是一个出现在动态语句字符串中的问号 (?)，它可以出现在变量可能出现的地方。**PreparedStatement** 扩展了 **Statement** 接口。

如前所述，**Connection** 对象的 **prepareStatement** 方法用于创建 **PreparedStatement** 对象。

如果 SQL 语句包含参数标记，在执行语句之前需要使用 setter 方法设置这些参数标记的值。**PreparedStatement** 对象的 setter 方法看起来像 "**setXXX**"，其中 **XXX** 表示参数标记的数据类型。例如，**setInt**、**setString**、**setDouble**、**setBytes**、**setClob**、**setBlob**。

在设置参数值后，根据 SQL 类型使用 **executeQuery**、**executeUpdate** 或 **execute** 方法。

*列表 4.9* 提供了一个使用 **PreparedStatement** 和 SELECT 的示例代码片段。

```java
(1) PreparedStatement pStmt = con.prepareStatement
("SELECT firstname, " +
"lastname " +
"FROM employee WHERE salary > ? ");
(2) pStmt.setInt(1,80000);
(3) ResultSet rs = pStmt.executeQuery();
(4) while ( rs.next() ) {
(5) System.out.println("Full name = " + rs.getString(1) +
(6) " " + rs.getString(2));
(7) }
(8) rs.close();
(9) pStmt.close();
```

### 列表 4.9 - PreparedStatement 对象：使用 executeQuery 执行 SELECT

在上述列表中：

