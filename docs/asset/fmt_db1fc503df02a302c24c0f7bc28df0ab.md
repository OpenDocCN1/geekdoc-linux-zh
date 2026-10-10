
```php
$sql = "SELECT c_id, c_email FROM customer WHERE c_name = :name";
try {
    $sth = $dbh->prepare($sql, array(PDO::ATTR_CURSOR, PDO::CURSOR_SCROLL));
    $sth->execute(array(':name' => 'Daniel'));
    while ($row = $sth->fetch(PDO::FETCH_NUM, PDO::FETCH_ORI_NEXT)) {
        $data = $row[0] . "\t" . $row[1] . "\t" . $row[2] . "\n";
        echo $data;
    }
    $sth->closeCursor();
} catch (PDOException $exp) {
    echo 'Exception: ' . $exp->getMessage();
}
```

### 示例 8.21 – 使用可滚动游标

#### 8.3.3.3.2 在 PDO 中捕获错误

`PDO` 具有`异常处理程序`来捕获异常并显示其详细信息。这些处理程序具有与其他编程语言类似的`try`和`catch`结构。

当 `PDO` 程序引发异常时，会创建一个 `PDOException` 实例。`PDOException` 类是 `Exception` 类的扩展，具有三种操作模式。通过设置 `PDO` 属性 `PDO::ATTR_ERRMODE` 来强制应用错误处理模式。*表 8.2* 描述了其可取的值。

| 值 | 描述 |
| :--- | :--- |
| PDO::ERRMODE_SILENT | 这是 `PDO` 中默认的错误处理模式。相应的错误代码和 |

### PDO 中的错误处理模式

当发生错误时，错误代码和消息会在语句对象（`PDOStatement`）和数据库对象（`PDO`）中同时被设置。对于使用此模式的语句，错误不会被捕获，而在函数失败后，下一条语句将被执行。

| 模式 | 描述 |
| :--- | :--- |
| `PDO::ERRMODE_SILENT` | 这是默认模式。当您希望自行处理错误时，该模式非常有用。当错误发生时，不会报告任何错误。 |
| `PDO::ERRMODE_WARNING` | 当您在开发或测试 `PDO` 应用程序时，此模式非常有用。除了设置错误代码和消息外，它还会引发一个 `E_WARNING`。<br><br>您可以在函数名前面加上“@”来抑制此行为。 |
| `PDO::ERRMODE_EXCEPTION` | 这是在 `PDO` 程序中处理错误的最佳方式。一旦发生错误，就会抛出一个异常，从而阻止 `try` 块中后续函数的执行。控制将转移到 `catch` 块，在那里处理异常。会提供错误信息和堆栈跟踪。 |

### 表 8.2 - 通过参数 `PDO::ATTR_ERRMODE` 设置的错误处理模式

*Listing 8.18* 给出了一个示例，展示如何将错误处理模式设置为 `PDO::ERRMODE_EXCEPTION`，以及如何使用 `try` 和 `catch` 块来处理异常。该程序故意发出一个错误的 SQL 语句，该语句使用了表中不存在的列。当错误发生时，会抛出 `PDOException`，并使用 `getMessage()` 方法打印异常对象的详细信息。

```php
<?php
/* Use one of the following connection string */
/* The connection below is for pdo_ibm */
$constring = 'ibm:sample';
/* The connection below is for pdo_odbc */
$constring = 'odbc:sample';
$dbh = new PDO($constring, 'db2inst1', '123');
$dbh->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
$sql = "SELECT c_id FROM customer WHERE notexistingcol = :name ";
$sth = $dbh->prepare($sql);
try {
    $sth->execute(array(':name' => 'ABC'));
    $row = $sth->fetchAll();
    print_r($row);
    $sth->closeCursor();
} catch (PDOException $exp) {
    echo 'Exception: ' . $exp->getMessage();
}
?>
```

**Listing 8.18—使用 `PDO::ERRMODE_EXCEPTION` 处理异常**

当生成异常时，`getMessage()` 方法产生的输出看起来像这样：

```
Exception : SQLSTATE[42S22]: Column not found: -206 [IBM][CLI Driver][DB2/LINUX] SQL0206N "NONEXISTINGCOL" is not valid in the context where it is used. SQLSTATE=42703 (SQLExecute[-206] at /root/Desktop/php-5.1.2/ext/pdo_odbc/odbc_stmt.c:133)
```

可以调用 `errorCode()` 和 `errorInfo()` 方法来获取有关错误的更多信息：

- `PDO::errorCode()` 提供关于错误 SQLSTATE 的信息。
- `PDO::errorInfo()` 提供关于错误的所有信息，例如来自数据库服务器的 SQLSTATE、SQLCODE 和错误消息。

#### 8.3.3.3 使用哪种隔离级别

在 PHP 中使用 `PDO_IBM`/`PDO_ODBC` 时考虑使用哪种隔离级别，与之前描述的 `ibm_db2` 扩展的考虑因素相同。

#### 8.3.3.4 准备和执行 SQL 语句

`PDO` 提供了机制，允许您在一步中准备和执行 SQL 语句，也可以分步进行。

### 一步准备和执行 SQL 语句

通常，我们使用这种方法执行那些在同一程序中不会重复执行的 SQL 语句。我们有两种类型的 SQL 语句：

- **返回结果集的 SQL 语句**

函数 `PDO::query` 用于准备和执行返回结果集的 SQL 语句，该结果集既可以通过列位置索引，也可以通过列名索引。Listing 8.19 是 `query` 函数的一个示例。您会看到，查询返回的结果集中的每一行都被获取到一个名为 `$row` 的数组中，并且值被打印出来。

```php
<?php
/* Use one of the following connection string */
/* The connection below is for pdo_ibm */
$connectString = 'ibm:sample';
/* The connection below is for pdo_odbc */
$connectString = 'odbc:sample';
$dbh = new PDO($connectString, 'db2inst1', '123');
$sql = 'SELECT c_id, c_name FROM customer';
try {
    foreach ($dbh->query($sql) as $row) {
        echo $row[0] . ' ' . $row['C_NAME'];
    }
} catch (PDOException $exp) {
    print_r($sth->errorInfo());
    echo 'Exception: ' . $exp->getMessage();
}
?>
```

**Listing 8.19 – 准备并执行返回结果集的 SQL**

- **不返回结果集的 SQL 语句**

`PDO` 采用不同的方式来准备和执行不返回结果集的 SQL 查询。`PDO::exec` 用于这种类型的 SQL 语句。`PDO::exec` 返回受该函数影响的行数。诸如 `DELETE`、`INSERT` 和 `UPDATE` 等 SQL 语句使用 `PDO::exec` 执行，并且它返回受此函数影响的行数。
