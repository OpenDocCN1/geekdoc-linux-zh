
`mysql -user -p`

```
- 登录后，创建你的数据库：
```

```sql
CREATE DATABASE my_test;
```

如果数据库创建成功，你将看到：

```
Query OK, 1 row affected (0.02 sec)
```

- 输入以下命令切换到数据库：

```sql
USE my_test;
```

执行该命令后，系统会提示：
`Database Changed`

- 选中数据库后，执行以下操作：

```sql
CREATE TABLE my_table (
  my_table_id INT(11) NOT NULL AUTO_INCREMENT,
  my_value VARCHAR(30),
  my_date DATE,
  PRIMARY KEY(my_table_id)
);
```

结果是，你应该看到一个 `Query OK` 语句并返回 SQL 提示符。现在你已经创建了一个数据库和一个表。

- 现在你将为此数据库创建一个具有完全权限的唯一用户，以便你通过 PHP 进行连接。这可以防止任何获取你 PHP 脚本访问的人篡改整个 MySQL 服务器。运行此查询：

```sql
GRANT ALL PRIVILEGES ON my_test.* TO 'test_user'@'localhost'
IDENTIFIED BY 'test_pass';
```

现在，你已经为你的 PHP 脚本准备好了数据库、表和测试用户。

## 测试 Apache、PHP 和 MySQL

在本节中，你将运行几个测试，以确保 Apache 正在正确解析你的 PHP 文件，并且 PHP 和 MySQL 正在连接并协同工作。你将知道 Apache 和 PHP 是否工作正常，因为你会看到 PHP 的输出，我们将在本章的剩余部分中讨论它。

## 数据库连接脚本

首先，你将创建一个负责数据库连接的 PHP 脚本。该脚本命名为 `database-connection.php`，位于你的虚拟主机根目录 (`/home/mytest/public_html`)。此脚本将包含该脚本使用的 MySQL 主机、用户名、密码和数据库信息。假设你遵循了前一节“准备 MySQL 数据库和用户”中的示例，脚本将包含列表 11.1 中的信息。

### 列表 11.1 `database-connection.php` 脚本

```php
<?php
// Database Connection Script
$dbUser = 'test_user';
$dbPass = 'test_pass';
$dbName = 'my_test';
$dbHost = 'localhost';
$sql = mysqli_connect($dbHost, $dbUser, $dbPass)
or die (mysql_error());
mysql_select_db($dbName, $sql) or die (mysql_error());
?>
```

## 数据库插入脚本

现在你的数据库连接脚本已经准备就绪，让我们创建一个向数据库中插入一些信息的脚本。该脚本将包含列表 11.1 中创建的数据库连接文件 (`database-connection.php`)，这使得你的数据库连接对 `$sql` 资源标识符可用。接下来，此脚本将运行一个 `foreach` 循环，在你的数据库中创建 50 条数据。请查看列表 11.2 中的 `database-insert.php` 脚本。

### 列表 11.2 `database-insert.php` 脚本

```php
<?php
// Data insertion script
include('database-connection.php');
for($i = 0; $i <= 50; $i++){
  if($i % 2) {
    $data = $i.' - Odd Result';
  } else {
    $data = $i.' - Even Result';
  }
  mysql_query('INSERT INTO my_table (my_value, my_date)
VALUES ('$data', now())') or die (mysql_error());
  echo 'Inserting: $data<br />';
}
echo 'Done<br />';
?>
```

此时，你通过 浏览器使用 `http://yourtest.com/database-insert.php` 作为 URL 运行 `database-insert.php` 脚本。

如果你的 MySQL 工作正常，你将在 浏览器中看到一些输出结果，类似于下所示：

- Inserting: 0- Even Result
Inserting: 1- Odd Result
Inserting: 2- Even Result
Inserting: 3- Odd Result
Inserting: 4- Even Result
Inserting: 5- Odd Result
Inserting: 6- Even Result
Inserting: 7- Odd Result
Inserting: 8- Even Result
Inserting: 9- Odd Result
Inserting: 10- Even Result

> 为了本书，我们截断了此脚本的输出。

## 数据提取和格式化脚本

现在数据已经插入数据库，你将进行最后的测试，即使用 PHP 提取数据并将其格式化为 HTML 输出。请查看列表 11.3 中的脚本。

### 列表 11.3 `database-test.php` 脚本

```php
<?php
// Data test script
include('database-connection.php');
$sql = mysql_query('SELECT * FROM my_table');
while($row = mysql_fetch_array($sql)){
  echo "Database Entry: " . $row['my_table_id'] . " | Value: " . $row['my_value'] . " | Date: " . $row['my_date'] . "<br>";
}
?>
```
