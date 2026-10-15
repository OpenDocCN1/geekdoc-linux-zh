
包 `javax.sql.rowset` 包含 RowSet 的两个子集——`JdbcRowSet` 和 `CachedRowSet`。`JdbcRowSet` 是一种已连接的 RowSet，它作为 `ResultSet` 对象的包装器，允许你滚动和更新 `ResultSet` 对象中的行。请记住，默认情况下，`ResultSet` 对象是不可滚动且只读的——你必须显式将结果集类型设置为 `TYPE_SCROLL_INSENSITIVE`，并将结果集并发常量设置为 `CONCUR_UPDABLE`，才能使 `ResultSet` 可滚动且可更新。`JDBCRowSet` 默认是可滚动和可更新的。`CachedRowSet` 是一种断开连接的 RowSet，它缓存 `ResultSet` 的数据并与数据库断开连接。与 `CachedRowSet` 类似，`CachedRowSet` 对象也是可滚动和可更新的。`CachedRowSet` 还是序列化的，因此可以通过网络（如互联网）在 Java 之间传递。然而，`CachedRowSet` 有局限性——内存中可以存储的数据量是的。`java.sql` 包包含其他 RowSet 接口。有关这些接口的详情，请访问 `java.sun.com/javase/6/docs/techniques/guides/jdbc/rowsetImpl1.html`。

## 25.10 Java DB/Apache Derby

从 JDK 6 开始，Sun Microsystems 现在将开源 Java DB（Apache Derby 的 Sun 版本）与 JDK 绑定在一起。在 25.11 节中，我们将使用 Java DB 演示新的 JDBC 4.0 功能。在执行下一节的应用程序之前，你必须在 Java DB 中设置 AddressBook 数据库。在 25.11 节中，我们将嵌入式 Java DB。还有一个网络版本，其执行方式与本章早期介绍的 MySQL DBMS 类似。对于后续步骤，我们假设你在安装了 Java 的 Microsoft Windows 上运行。

1. Java DB 带有几个用于配置和运行的批处理文件。在命令行提示符中执行这些批处理文件之前，你必须设置环境变量 `JAVA_HOME` 指向 JDK 的 `C:\Program Files\Java\jdk1.6.0` 安装目录。有关设置环境变量值的信息，请参阅本书的“准备工作”部分。

2. 用文本编辑器（如记事本）打开批处理文件 `setEmbeddedCP.bat`（位于 `C:\Program Files\Java\jdk1.6.0\frameworks\embedded\bin`）。找到行

```
set DERBY_INSTALL=
```

将其更改为

```
set DERBY_INSTALL=C:\Program Files\Java\jdk1.6.0.db
```

此外，通过在前面加上 REM 来注释掉该行

```
@FOR %%X in ("%DERBY_HOME%") DO SET DERBY_HOME=%%X~s
```

```
REM @FOR %%XX in ("%%DERBY_HOME%") DO SET DERBY_HOME=%%XX-s
```

保存你的更改并关闭此窗口。

3. 打开命令提示符并切换目录到 `C:\Program Files\Java\jdk1.6.0\db\frameworks\embedded\bin`，然后运行 `setEmbeddedCP.bat` 并回车以设置 Java DB 所需的环境变量。

4. 嵌入式 Java 数据库必须与维护数据库的应用程序位于同一位置。因此，切换到包含 `address.sql` 脚本的目录，该脚本用于构建 AddressBook 数据库。

5. 执行命令

```
"C:\Program Files\Java\jdk1.6.0\db\embedded\bin\ij"
```

启动与 Java DB 交互的命令行工具。双引号是必要的，因为路径中包含空格。这将显示 ij 提示符。

6. 在 `ij>` 提示符下输入

```
connect:jdbc:derby:AddressBook;create=true;user=jhtp7;password=jhtp7;
```

在当前目录创建 AddressBook 数据库。该命令还会创建一个用户 `jhtp7`，密码为 `jhtp7` 用于访问数据库。

8. 要终止 Java DB 命令行工具，输入

```
exit;
```

你现在已准备好执行第 25.12 节中的 AddressBook 应用程序。

## 25.11 PreparedStatements

`PreparedStatement` 允许你创建比 `Statement` 对象执行效率更高的 SQL 语句。`PreparedStatements` 还可以指定参数，使其比 `Statements` 具具灵活性。程序可以带有不同的参数值重复执行相同的查询。例如，在 books 数据库中，你可能想要查找具有特定姓氏和名字的作者的所有书名，并且可能想对多个作者执行该查询。使用 `PreparedStatement`，你的查询定义如下：

```java
PreparedStatement authorBooks = connection.prepareStatement(
"SELECT lastName, firstName, title " +
"FROM authors INNER JOIN authorISBN " +
"ON authors.authorID=authorISBN.authorID " +
"INNER JOIN titles " +
"ON authorISBN.isbn=titles.isbn " +
"WHERE lastName = ? AND firstName = ?"
);
```

上述 SQL 语句最后一行中的两个问号 (?) 是值的占位符，这些值将作为查询的一部分传递给数据库。在执行 `PreparedStatement` 之前，程序必须使用 `PreparedStatement` 接口的方法来指定参数值。

对于前面的查询，两个参数都是字符串，可以使用 `PreparedStatement` 方法 `setString` 如下设置：

```java
authorBooks.setString(1, "Deitel");
authorBooks.setString(2, "Paul");
```

`setString()` 方法的第一个参数代表参数值的编号。参数编号从 1 开始计数，从第一个问号 (?) 开始。当程序带有所示的参数值在数据库中执行前面的 `PreparedStatement` 时：

```sql
SELECT lastName, firstName, title
FROM authors INNER JOIN authorISBN
ON authors.authorID=authorISBN.authorID
INNER JOIN titles
ON authorISBN.isbn=titles.isbn
WHERE lastName = 'Deitel' AND firstName = 'Paul'
```

`setString()` 方法会自动对 O'Brien 参数值进行转义。例如，如果姓氏是 O'Brien，则语句

```java
authorBooks.setString(1, "O'Brien");
```

通过用两个单引号替换 O'Brien 中的 ' 字符来对该字符进行转义。

### 性能提示 25.2

在多次执行带有不同参数值的 SQL 语句时，`PreparedStatements` 比 `Statements` 更高效。

### 错误预防提示 25.1

对于接收 String 值作为参数的查询，使用 `PreparedStatement` 参数以确保这些字符串在 SQL 语句中被正确引用。
