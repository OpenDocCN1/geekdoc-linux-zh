
## 3. 执行语句

**PDOStatement::execute** 用于执行预编译语句。可以使用绑定函数将变量绑定到语句中，或者在调用此函数时传入一个数组作为参数，从而在绑定参数的同时执行语句。列表 8.23 展示了如何在 execute 函数中使用命名参数标记。

```php
<?php
/* Use one of the following connection string */
/* The connection below is for pdo_ibm */
$constring = 'ibm:sample';
/* The connection below is for pdo_odbc */
$constring = 'odbc:sample';
$dbh = new PDO($constring, '', '');
$id = 10;
$sql = "select c_name from customer where c_id > :id";
$dbh->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
try {
  $sth = $dbh->prepare($sql);
  $rc = $sth->execute(array(':id' => $id));
  $result = $sth->fetchAll();
  print_r($result);
} catch (PDOException $exp) {
  print_r($sth->errorInfo());
  echo 'Exception: ' . $exp->getMessage();
}
?>
```

**列表 8.23 – 使用命名参数标记调用 PDOStatement::execute**

### 8.3.3.3.5 创建和调用存储过程

你可以像执行其他任何 SQL 语句一样，使用 PHP 的 PDO 来创建 SQL 存储过程。但如果需要从客户端调用存储过程，你需要根据参数的类型仔细处理参数绑定。存储过程中有三种类型的参数，分别是 **IN**、**OUT** 和 **INOUT**。在绑定参数时，数据类型常量和参数通过按位或运算符（|）关联。参数类型 `PDO::PARAM_INPUT_OUTPUT` 用于 **OUT** 和 **INOUT** 参数。IN 参数不需要参数类型。*列表 8.24* 展示了一个包含所有三种类型参数并返回结果集的存储过程。一旦存储过程执行完毕，与存储过程参数标记绑定的变量将被填充存储过程执行后的值。

```php
<?php
/* Use one of the following connection string */
/* The connection below is for pdo_ibm */
$constring = 'ibm;sample';
/* The connection below is for pdo_odbc */
$constring = 'odbc;sample';
$dbh = new PDO($constring, 'db2inst1', '123');
$id = 10;
$sql = 'CALL getdetails(?, ?, ?)';
$dbh->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
$amount = 0;
$c_id = 140;
$quantity = 100;
try {
    $sth = $dbh->prepare($sql);
    // Input parameter
    $sth->bindParam(1, $c_id, PDO::PARAM_INT);
    // Output parameter
    $sth->bindParam(2, $amount, PDO::PARAM_INT|PDO::PARAM_INPUT_OUTPUT);
    // Input output parameter
    $sth->bindParam(3, $quant, PDO::PARAM_INT|PDO::PARAM_INPUT_OUTPUT);
    $sth->execute();
    echo 'The INOUT parameter is: ' . $quant . ' and the OUT parameter is: ' . $amount;
    $rowset = $sth->fetchAll(PDO::FETCH_NUM);
    print_r($rowset);
} catch (PDOException $exp) {
    print_r($sth->errorInfo());
    echo 'Exception: ' . $exp->getMessage();
}
?>
```

**列表 8.24 – 使用 PHP 的 PDO\_IBM/PDO\_ODBC 调用存储过程**

### 8.3.3.3.6 处理事务

PDO 默认运行在 **自动提交** 模式下。这意味着所有查询要么被提交（如果成功），要么被回滚（如果不成功）。你可以使用 **PDO::beginTransaction** 等方法使多个 SQL 查询成为单个事务的一部分。此功能会关闭 PDO 应用的自动提交模式。一旦事务完成，可以使用 **PDO::commit** 函数提交，或使用 **PDO::rollback** 函数回滚。

*列表 8.25* 展示了 PHP 使用 DB2 的 PDO\_IBM 或 PDO\_ODBC 处理事务的过程。可以看到，当发生错误时，由于错误处理模式被设置为 **PDO::ERRMODE\_EXCEPTION**，异常会被抛出。在 catch 块中，事务被回滚并打印错误。如果没有发生错误，事务将被提交并完成。

```php
<?php
/* Use one of the following connection string */
/* The connection below is for pdo_ibm */
$constring = 'ibm:sample';
/* The connection below is for pdo_odbc */
$constring = 'odbc:sample';
$dbh = new PDO($constring, 'db2inst1', '123');
$dbh->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
try {
    $dbh->beginTransaction();

    $dbh->exec("
        INSERT INTO customer (c_name, c_email) VALUES ('ABC', 'a123@123.com')
    ");
    
    $dbh->exec("
        INSERT INTO customer (c_name, c_email) VALUES ('DEF', '1a23@123.com')
    ");
    
    $dbh->exec("
        INSERT INTO customer (c_name, c_email) VALUES ('GHI', '1n23@123.com')
    ");

    $dbh->commit();
} catch (PDOException $exp) {
    print 'Rolling back transaction';
    $dbh->rollback();
}
print_r($dbh->errorInfo());
echo 'Exception: ' . $exp->getMessage();
?>
```

**列表 8.25 – PHP 与 IBM_PDO/PDO_ODBC 的事务处理**

## 8.3.3.4 处理结果

PDO 提供两种获取数据的方式：

1.  **缓冲获取**
    缓冲获取允许将 SQL 查询返回的结果集中的所有行获取到一个数组中。如果查询返回巨大的结果集，我们不建议使用此方法，因为它会消耗大量系统资源。

2.  **非缓冲获取**
    使用 PDOStatement::fetch，你可以每次获取一行并对结果集进行操作。PDOStatement::fetch 有不同的选项用于获取不同数据的列。以下各节将描述这些选项。

### 使用 FETCH_BOUND 和 bindColumn

此方法允许将结果集返回的每一列分配给一个变量。在执行 PDOStatement::fetch 之后，绑定的变量对应的值将被更新为结果集中的值。常量 PDO::FETCH_BOUND 是 fetch 的一个参数，使得绑定的列变量由 fetch 函数填充。列表 8.26 展示了绑定列获取的示例。

```php
<?php
/* Use one of the following connection string */
/* The connection below is for pdo_ibm */
$constring = 'ibm:sample';
/* The connection below is for pdo_odbc */
$constring = 'odbc:sample';
$dbh = new PDO($constring, '', '');
$id = 10;
$sql = "select c_id, c_name from customer where c_id > :id";
$dbh->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
try {
    $sth = $dbh->prepare($sql);
    $sth->execute(array(':id' => $id));
    $sth->bindColumn(1, $id);
    $sth->bindColumn(2, $name);

    while ($row = $sth->fetch(PDO::FETCH_BOUND)) {
        echo "id is: " . $id . " and name is: " . $name;
    }

} catch (PDOException $exp) {
    print_r($sth->errorInfo());
    echo "Exception: " . $exp->getMessage();
}
?>
```

**列表 8.26 – 使用 FETCH_BOUND 获取数据**

### 使用无参数传递的 Fetch 函数

这是默认选项。fetch 函数返回结果集中的每一行，列通过其位置索引。列表 8.27 提供了一个示例。

```php
while ($row = $sth->fetch()) {
    echo "id is: " . $row[0] . " and name is: " . $row[1];
}
```

**列表 8.27 – 使用 Fetch 函数的示例**

### 使用 FETCH_ASSOC

我们可以将结果集中的行获取到一个数组中，该数组通过查询返回的结果集列名进行索引。列表 8.28 提供了一个示例。

```php
while ($row = $sth->fetch(PDO::FETCH_ASSOC)) {
    echo "id is: " . $row['C_ID'] . " and name is: " . $row['C_NAME'];
}
```

**列表 8.28 – 使用 Fetch_Assoc 函数的示例**

### 使用 FETCH_BOTH

将参数 PDO::FETCH_BOTH 传递给 PDOStatement::fetch 进行获取时，将返回一个数组，该数组对每一行同时使用列名和位置作为索引。列表 8.29 提供了一个示例。

```php
while ( $row = $sth->fetch(PDO::FETCH_BOTH)) {
    echo "id is: " . $row[0] . " and name is: " . $row['C_NAME'];
}
```

**列表 8.29 – 使用 Fetch_Both 的示例**

### 使用可滚动游标

