
`ResultSet` 对象由 `Statement`、`PreparedStatement` 和 `CallableStatement` 对象的 `executeQuery` 方法返回。`ResultSet` 对象维护一个指向结果集当前行的游标。可以使用该对象的 `next()` 方法将此游标移动到下一行。游标默认只能向前移动且为只读；但是，您可以将游标定义为可滚动或可更新的。

### 4.3.4 处理 SQL 错误和警告

可以通过调用结果集（Result Set）对象的 getter 方法获取当前行的列值。当所有行都获取完毕后，`next` 方法将返回一个异常。

表 4.5 列出了在创建 `Statement` 对象时可以设置的三个 Result Set 属性。

### 表 4.5 - resultSet 的属性

| 属性 | 描述 |
|---|---|
| resultSetType | 定义游标的可滚动性 |
| resultSetConcurrency | 定义游标的可更新性 |
| resultSetHoldability | 指示即使 statement 关闭后结果集仍保持打开状态 |

支持所有这些属性的 `createStatement` 和 `prepareStatement` 具有如下语法：

```java
createStatement (int resultSetType,
                resultSetConcurrency,
                resultSetHoldability)

prepareStatement (int resultSetType,
                  resultSetConcurrency,
                  resultSetHoldability)
```

这三个属性均为可选的。下方的清单 4.14 提供了一个处理结果集的示例，该示例取自 4.3 节开头提到的 IBM rebook。

### 清单 4.14 - 使用 ResultSet 对象的示例

```java
(1) Statement stmt = con.createStatement (ResultSet.TYPE_SCROLL_SENSITIVE,
                                           ResultSet.CONCUR_UPDATABLE);
(2) ResultSet rs=stmt.executeQuery("Select POID,Status from
                                     purchaseorder");
(3) while(rs.next()) {
        int id = rs.getInt(1);
        String status = rs.getString(2);
        if(id==5003 && status.toUpperCase().compareTo("UNSHIPPED")==0) {
            System.out.println("updating status to shipped for id value "+
                               id+"....");
(4)     rs.updateString(2, "Shipped");
(5)     rs.updateRow();
    }
(6) rs.beforeFirst();
    System.out.println("Printing all the purchase order record status");
    while(rs.next()) {
        int id         = rs.getInt(1);
        String info = rs.getString(2);
        System.out.println("id="+id+" info="+ info );
    }
```

在上述清单中：

- (1) 此行用于创建带有游标属性的 `Statement` 对象，使其可滚动（且对他人所做的更改敏感）并可更新。
- (2) 创建 `ResultSet` 对象。
- (3) 遍历结果集。
- (4) 在 `id = 5003` 且状态为 UNSHIPPED 的条件下，将游标该行的 String（第 2 列）更新为状态“Shipped”。如果有更多列，可以使用 updater 方法 `updateXXX` 更新其他列。
- (5) 更新该行（如果使用了 `rs.insertRow()`，则在该位置插入新行）。
- (6) 将游标移回此 `ResultSet` 对象的开头，即第一行之前。

#### 4.3.4.1 SQLException

每当在访问数据库时发生错误，都会创建并抛出一个 `SQLException` 对象。`SQLException` 对象提供表 4.6 中列出的信息。

#### 表 4.6 - SQLException 信息

| SQLException 信息 | 描述 | 获取此信息的方法 |
| :--- | :--- | :--- |
| Message | 错误代码的文本表示 | `getMessage` 方法 |
| SQLState | SQLState 字符串 | `getSQLState` 方法 |
| ErrorCode | 一个整数值，指示导致抛出异常的错误 | `getErrorCode` 方法 |

除了上述信息外，DB2 JCC 驱动程序还提供了额外的接口 `com.ibm.db2.jcc.DB2Diagnosable`。此接口提供了有关访问 DB2 数据库时发生的错误的更多信息。

如果抛出多个 `SQLException`，它们会被链接在一起。可以通过调用当前 `SQLException` 对象的 `getNextException` 方法来获取下一个异常的信息。如果当前 `SQLException` 对象是链中的最后一个，此方法将返回 null。可以在程序的 catch 块中使用 while 循环逐个获取所有 `SQLException` 对象。清单 4.15 展示了如何在 try-catch 块中处理 `SQLException`。

### 清单 4.15 - 处理 SQLException

```java
try {
    // 可能抛出 SQLException 的代码放在这里
} catch (SQLException sqle)
{
    System.out.println("Rollback the transaction and quit the program");
    System.out.println();
    try { con.rollback(); }
    catch (Exception e) {}
    System.exit(1);
}
```

#### 4.3.4.2 SQLWarning

当调用以下类的方法时发生数据库警告，就会创建 `SQLWarning` 对象：

- `Connection`
- `Statement`
- `PreparedStatement`
- `CallableStatement`
- `ResultSet`

所有这些接口都包含 `getWarning` 方法以获取警告信息。请注意，创建 `SQLWarning` 对象不会抛出任何 `SQLException`。您需要调用上述接口的 `getWarning` 方法以检查是否存在任何警告。清单 4.16 提供了处理 `SQLWarning` 的示例。

### 清单 4.16 - 处理 SQLWarning

```java
Statement stmt=con.createStatement();
stmt.executeUpdate("delete from product where pid='101'");
SQLWarning sqlwarn=stmt.getWarnings();
while(sqlwarn!=null)
{
    System.out.println("Warning description: " + sqlwarn.getMessage());
    System.out.println("SQLSTATE: " + sqlwarn.getSQLState());
    System.out.println("Error code: " + sqlwarn.getErrorCode());
    sqlwarn=sqlwarn.getNextWarning();
}
```

## 4.3.5 关闭连接
