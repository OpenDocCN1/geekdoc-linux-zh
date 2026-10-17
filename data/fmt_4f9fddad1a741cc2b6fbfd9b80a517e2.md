
如果你修改程序，使传入的语句是一个 `UPDATE` 操作，你可以再次测试编译和运行该程序，并会得到以下结果：

```
Number of rows updated: 1
```

### 4.3.2.3 PreparedStatement 接口

实现 `PreparedStatement` 接口的类可用于运行可以包含 `参数标记` 的查询。参数标记是一个出现在动态语句字符串中的问号 (`?`)，它可以出现在变量可能出现的地方。`PreparedStatement` 扩展了 `Statement` 接口。

如前所述，`Connection` 对象的 `prepareStatement` 方法用于创建 `PreparedStatement` 对象。

如果 SQL 语句包含参数标记，在执行语句之前需要使用 setter 方法设置这些参数标记的值。`PreparedStatement` 对象的 setter 方法看起来像 "`setXXX`" ，其中 `XXX` 表示参数标记的数据类型。例如，`setInt`、`setString`、`setDouble`、`setBytes`、`setClob`、`setBlob`。

在设置参数值后，根据 SQL 类型使用 `executeQuery`、`executeUpdate` 或 `execute` 方法。

*列表 4.9* 提供了一个使用 `PreparedStatement` 和 SELECT 的示例代码片段。

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

#### 4.3.2.4 CallableStatement 接口

实现 `CallableStatement` 接口的类可用于调用存储过程。`CallableStatement` 继承自 `PreparedStatement` 接口。使用 `Connection` 对象的 `prepareCall` 方法来创建 `CallableStatement` 对象。

`CallableStatement` 可以拥有三种类型的参数：IN、OUT、INOUT。在执行 `CallableStatement` 之前，必须使用 setter 方法（`setXXX`）为 IN 和 INOUT 参数设置值。同样地，在执行语句之前，OUT 和 INOUT 参数应注册（使用 `registerOutParameter` 方法）到数据库。

`CallableStatement` 可以使用 `executeUpdate`、`executeQuery` 和 `execute` 方法执行。这三种方法的使用说明如下：

- `executeUpdate`：当期望调用的输出不包含结果集时使用。
- `executeQuery`：当期望调用的输出包含单个结果集时使用。
- `execute`：当期望调用的输出包含多个结果集时使用。

让我们查看一下 *Listing 4.12* 中的示例代码片段，该代码使用了 `CallableStatement` 对象和 `executeUpdate` 方法。假设 `view_salary_increase` 存储过程定义如下：

```java
view_salary_increase (IN p_empno varchar(6),
                       INOUT p_increase int,
                       OUT p_firstname)
```

其中，该存储过程根据给定的员工编号，通过 `OUT` 参数返回员工的名字。

```java
(1) CallableStatement cstmt;
(2) cstmt = con.prepareCall("Call view_salary_increase(?,?,?)");
(3) cstmt.setString(1, "000010");
(4) cstmt.setInt(2, 10000000);
(5) cstmt.registerOutParameter(3, Types.VARCHAR);
(6) cstmt.executeUpdate();
(7) System.out.println(cstmt.getString(3) +
                       " would receive an increase of " +
                       cstmt.getInt(2));
(8) cstmt.close();
```

### Listing 4.12 - 使用 executeUpdate 的 CallableStatement：不返回结果集

在上述代码片段中：

- (1) 声明了 `CallableStatement` 对象 `cstmt`。
- (2) 通过连接的方法 `prepareCall` 创建 `CallableStatement` 对象，并将其赋值给 `cstmt`。
- (3) 存储过程的输入参数（`IN` 或 `INOUT`）必须在执行调用之前设置。
- (4) 同上，此参数为 `INOUT` 参数。
- (5) 存储过程的输出参数必须注册以指示其类型。对于 `INOUT` 参数，如果先使用 `setXXX` 设置值，则注册它是可选的。
- (6) 在此情况下，由于存储过程未返回结果集，因此使用 `executeUpdate` 方法。
- (7) 使用 `getXXX` 方法从存储过程参数（`OUT` 和 `INOUT`）中检索信息。
- (8) 关闭 `CallableStatement` 对象 `cstmt`。

在下一个由 *Listing 4.13* 中代码片段展示的例子中，使用了一个 `CallableStatement` 对象来调用定义如下 `high_paid_employees` 存储过程：

```java
high_paid_employees(IN p_salary INT)
```

其中，该存储过程返回一个包含两列的结果集：工资大于 `p_salary` 的员工的姓和名。

```java
CallableStatement cstmt;
(1) cstmt = con.prepareCall("call high_paid_employees(?)");
(2) cstmt.setInt(1,80000);
(3) ResultSet rs = cstmt.executeQuery();
    System.out.println("High-paid employees list\n" +
        "--------------------------------");
(4) while (rs.next()) {
        System.out.println( rs.getString(1) + " " +
            rs.getString(2) );
    }
rs.close();
cstmt.close();
```

### Listing 4.13 - 返回单个结果集的 CallableStatement 对象

在上述代码片段中：

- 1. 通过连接的方法 `prepareCall` 创建 `CallableStatement` 对象 `cstmt`，以调用 `high_paid_employees` 存储过程。
- 2. 在执行调用之前设置存储过程的输入参数。没有输出参数需要注册。
- 3. 由于存储过程返回单个结果集，因此发出 `executeQuery` 方法。
- 4. 我们遍历结果集，并使用 getter 方法（`getXxx`）获取结果集中返回的列。

### 4.3.3 接收结果

本节描述了使用 JDBC 程序时的第三个步骤。它描述了如何接收结果，主要是 `ResultSet` 对象。

#### 4.3.3.1 ResultSet
