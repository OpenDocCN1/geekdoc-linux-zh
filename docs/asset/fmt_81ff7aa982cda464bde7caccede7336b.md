
`getBigDecimal` 使用包含在 `ResultSet` 中的元数据（关于数据）来确定要在检索到的 `BigDecimal` 对象中设置的小位数。如果你运行示例 JDBC 应用程序，将获得图 8.2 所示的简单列表，显示客户名称、编号和余额。

| | 名称 | 余额 |
|---|---|---|
| 846283 | Allison | 10.00 |
| 475938 | Doe | 250.00 |
| 938472 | Henning | 37.00 |
| 938465 | Johnson | 398.70 |
| 839283 | Jones | 100.00 |
| 192837 | Lee | 489.50 |
| 389572 | Stevens | 58.75 |
| 692829 | Thomas | 0.00 |
| 397267 | Tyron | 0.00 |
| 392859 | Vine | 439.00 |
| 593029 | Williams | 25.00 |

图 8.2：运行图 8.1 中的应用程序提供了来自 QUSTCDT 文件记录的客户编号、名称和余额列表。

# 数据修改

如前所述，RDB 修改是通过 SQL 的 `UPDATE` 语句完成的。`UPDATE`、`INSERT` 和 `DELETE` 语句必须使用 JDBC `Statement` 类的 `executeUpdate` 方法执行。以下 Java 代码执行了之前显示的 `UPDATE` 语句：

```java
stmt.executeUpdate(
  "UPDATE invoice set cust = 'Agway' WHERE invno = 101");
```

# 意外

事情并不总是进展如意，因此你的代码必须准备好处理潜在问题。当出现问题时，大多数 JDBC 方法会生成名为 SQL 异常的对象。所有的 JDBC 方法调用都必须封装在 Java `try` 块中。`init` 方法的 `try` 块使用 `System.out.println` 列出错误，而 `doGet` 方法的 `try` 块通过 `out.println` 将错误列到动态构建的 HTML 中。

## JSP 版本

图 8.3 显示了 JDBC servlet 的 JSP 版本。

```jsp
<@ page import="java.sql.*" %>

<%@ page import="java.math.*" %>

<%! Connection con = null; %>

<%! public Connection getConnection() {

    if (con != null) {

        return con;

    }

    try {

        Class.forName("com.ibm.as400.access.AS400JDBCDriver");

    } catch (ClassNotFoundException e) {

        System.out.println("JDBCBasics driver load error: "+e);

        return null;

    }

    try {

        con = DriverManager.getConnection(

            "jdbc:as400://207.212.90.55",

            "denoncourt","jiujitsu");

    } catch (SQLException e) {

        System.out.println("JDBCBasics SQL Connection error: "+ e);

        return null;

    }

    return con;

} %>

<html><body>

<%

    con = getConnection();

    Statement stmt = con.createStatement();

    ResultSet rs = stmt.executeQuery(

        "SELECT CUSNUM, LSTNAM, INIT, STREET, " + 

        "CITY, STATE, ZIPCOD, CDLTMT, " + 

        "CHCGOD, BALDUE, CDTOUE " + 

        "FROM WIQS.CUSTUM");

    while (rs.next()) {

        String cusnum = rs.getString(1);

        String cusnam = rs.getString("LSTNAM");

        BigDecimal baldeue = rs.getBigDecimal(10, 2);

        <%= cusnum %> &nbsp; <%= cusnam %> &nbsp; <%= baldeue %> <br>

    }

} catch (SQLException e) {

    SQL error: &nbsp; <%= e %>

} %>

</body></html>
```
