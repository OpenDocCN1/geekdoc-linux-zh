
```java
import java.net.URL;
import java.sql.*;

class jex14_15 {
    public static void main(String argv[])
    {
        Connection con;
        Statement stmt;
        byte[] sql_text = new byte[1000];

        try {
            Class.forName("com.mysql.jdbc.jdbc.Driver");
            con = DriverManager.getConnection("jdbc:mysql://localhost:3306/baseball", "user", "password");
            stmt = con.createStatement();
            System.out.println("Type SQL statement, or 'quit' to exit");

            while (true) {
                System.out.print("ok> ");
                System.in.read(sql_text);
                String sql_string = new String(sql_text).trim();

                if (sql_string.equals("quit")) {
                    break;
                }

                if (stmt.execute(sql_string)) {
                    ResultSet rs = stmt.getResultSet();
                    ResultSetMetaData mr = rs.getMetaData();

                    for (int i = 1; i <= mr.getColumnCount(); i++) {
                        String colname = mr.getColumnName(i);
                        int colwidth = mr.getColumnWidth(i);
                        System.out.print(colname);
                        for (int j = 0; j < colwidth; j++) {
                                System.out.print(" ");
                        }
                        System.out.println("*");
                    }

                    while (rs.next()) {
                        for (int i = 1; i <= mr.getColumnCount(); i++) {
                            String colvalue;
                            int colwidth = mr.getColumnSize(i);
                            colvalue = rs.getString(i);
                            if (rs.wasNull()) {
                                colvalue = "NULL";
                            }
                            System.out.print(colvalue);
                            for (int j = 0; j < colwidth; j++) {
                                    System.out.print(" ");
                            }
                        }
                        System.out.println();
                    }
                } else {
                    int rows = stmt.getUpdateCount();
                    System.out.println("Database modified, rows: " + rows);
                }
            }
        } catch (Exception e) {
            e.printStackTrace();
        }

        try {
            stmt.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
        try {
            con.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
        System.out.println("\ngoodbye!");
    }
}
```

## 518 第四部分 + 编程应用 541

接下来，程序调用 `Statement.execute()` 方法来执行用户输入的语句。如果语句没有被正确解析或运行，该方法将抛出一个 `SQLException`，该异常会在循环底部被捕获。

如果语句执行正确且没有生成 `ResultSet`（即该语句执行了 INSERT、UPDATE 或 DELETE 操作），程序将打印一条简短的语句并继续 `while()` 循环：

```java
// 如果为真，说明执行的语句生成了 ResultSet
if (!stmt.execute(sql_string)) {
    // 如果语句没有返回 ResultSet
    // 它是一个 UPDATE、INSERT 或 DELETE 语句
    System.out.println("database modified");
    continue;
}
```

如果用户输入的 SQL 语句确实生成了 `ResultSet`，则必须对其进行获取并处理。首先，我们调用 `Statement.getResult()` 方法获取 `ResultSet`：

```java
// 如果到达这里，说明语句生成了
// ResultSet：获取它
ResultSet rs = stmt.getResult();
```

接下来，我们调用 `ResultSet.getMetaData()` 方法获取有关结果集的元数据。元数据将告诉我们有关结果集本身的信息，例如集合由多少列组成、每列的名称以及每列的宽度：

```java
// 获取描述此 ResultSet 的 MetaResult 对象
ResultSetMetaData mr = rs.getMetaData();
```

接着，程序构建一个由每列名称组成的表头。`ResultSetMetaData.getColumnName()` 方法获取列的名称，`ResultSetMetaData.getColumnDisplaySize()` 获取列的宽度。列根据它们在 SELECT 语句中出现的顺序进行标识，从左到右从 1 开始计数。程序利用这些信息显示列的宽度，然后用适当数量的空白填充每一列：

```java
for (int i = 1; i <= mr.getColumnCount(); i++) {
    int colwidth = mr.getColumnDisplaySize(i);
    String columnName = mr.getColumnName(i);
    int strwidth = columnName.length();
}

System.out.print(colname);
```

## 第 14 章 ❖ 编程 API—扩展示例 519

```java
// 用空格填充列
for (int j = 0; j < colwidth - strwidth; j++)
{
    System.out.print(" ");
}
System.out.println("");
```
