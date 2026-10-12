
## 12.6.3 字符串函数

PHP 拥有大量的字符串函数。这里是其中几个。细节太多，无法详尽介绍，但请记住这个观点：如果你想处理文本，可能有一个内置函数可以实现你想要的功能。

### `printf()`

PHP 的 `printf()` 输出一个最终在浏览器显示的字符串。它的工作原理与 C 语言（以及 Perl）的 `printf()` 函数非常相似：

```php
printf "Integer: %d, Float: %6.2f", $i, $f;
```

PHP 还有 `sprintf()` 函数，它可以返回一个指定格式的字符串。

### `join()`

`join()` 函数将数组元素合并成一个字符串：

```php
$array = array(2, 4, 6, 8);
$string = join(":", $array);
// $string 现在是 "2:4:6:8"
```

### `substr()`

该函数返回从字符索引（从 0 开始）开始指定长度的字符串部分：

```php
$string = "hello, world!";
$substring = substr($string, 2, 6);
// $substring 是 "llo, w"
```

## 第 12 章 PHP

### `trim()`

`trim()` 函数移除字符串两尾的空白字符并返回结果：

```php
$string = " hello, world!\n\n";
$string2 = trim($string);
// $string2 是 "hello, world!"
```

## 12.6.4 其他函数

PHP 拥有大量的内置函数。本章没有足够的空间讨论它们。更多信息请参阅文档（`www.php.net/manual/en/funref.php`）。另一个学习所有函数的有用起点处是 `www.php.net/quickref.php`。

## 12.7 PHP 与 MySQL

现在我们已经涵盖了 PHP 的基础知识，可以进入核心内容了。PHP 提供了内置函数来连接和查询 MySQL 数据库。这是使用 PHP 的主要优势之一。许多 Web 程序员转向 PHP，是为了在网页和 MySQL 之间建立无缝的接口。

### 12.7.1 MySQL 函数，部分 1

我们将从连接 MySQL 服务器、执行简单的数据库查询并显示结果所需的常用 PHP 函数开始。

这些函数的大部分对其参数都有默认值。其中一个默认参数是密码的空字符串。这简直太愚蠢了！我们不会详细讨论这些参数——如果你对所有细节感兴趣，请查看 `www.php.net/manual/en/ref.mysql.php`。

#### `mysql_connect()`—连接到 MySQL 服务器

该函数在成功时返回一个 MySQL 链接标识符，在失败时返回错误：

```php
<?php
  $mysql = mysql_connect("localhost", "apache", "LampIsCool")
  or die("could not connect to mysql");
?>
```

#### `mysql_close()`—关闭 MySQL 服务器连接

该函数关闭与 MySQL 服务器的连接：

```php
<?php mysql_close($mysql); ?>
```

#### `mysql_db_query()`—执行查询

该函数为指定的数据库执行查询。成功时返回一个结果标识符，错误时则失败。该结果标识符用于获取查询结果：

```php
$result = mysql_db_query($db, $query)
```

#### `mysql_num_rows()`—返回选定的行数

该函数返回查询选定的行数：

```php
<?php echo mysql_num_rows($result); ?>
```

#### `mysql_fetch_row()`—作为枚举数组获取行

该函数将下一行作为枚举数组返回。每一列都存储在数组元素中，索引从 0 开始：

```php
<?php
$array = mysql_fetch_row($result);
echo "First column: $array[0];"
echo "First column: $array[1];"; ?>
```

#### `mysql_errno()` 和 `mysql_error()`—返回 MySQL 错误

`mysql_errno()` 返回最近一次调用的错误代码，如果没有错误则返回 0。`mysql_error()` 函数返回最近一次调用的错误文本，如果没有错误则返回空字符串：

```php
<?php $result = mysql_db_query($db, $query)
or die("query failed - " . mysql_errno() . ": " . mysql_error());
?>
```

## 汇总

让我们将这些函数整合在一起创建一个简单的示例。为了演示连接数据库和执行基础查询，我们使用第 8 章中有的“books”数据库。

## 第 12 章 PHP 413

此示例连接到 MySQL 服务器 (`mysql_connect()`) 查询数据库、报告任何错误、显示返回的行数并获取每一行。查询完成后，程序关闭连接。

```php
<?php
  $mysql = mysql_connect("localhost", "apache", "LampIsCool")
  or die("could not connect to mysql");
?>
```

```html
<!DOCTYPE html>
<html>
<head>
<title>PHP and MySQL</title>
</head>
<body>
  <table border="1">
    <tr>
      <th>ISBN</th>
      <th>Author</th>
      <th>Title</th>
    </tr>
    <?php
    while ($array = mysql_fetch_row($result)) {
    ?>
    <tr>
      <td><?php echo $array[0]; ?></td>
      <td><?php echo $array[1]; ?></td>
      <td><?php echo $array[2]; ?></td>
    </tr>
    <?php
    }
    ?>
  </table>
</body>
</html>
```

# 第 12 章 PHP

`mysql_free_result()`—释放内存
此函数释放结果所使用的内存。如果你不调用此函数，当脚本运行结束时，结果占用的所有内存将被删除。只有当你担心脚本运行时的内存时，才需要此函数：

```php
<?php mysql_free_result($result);
?>
```

## 整合在一起，V2.0
作为 MySQL 函数的第三个示例，我们再次查询书籍数据库。此示例仅选择了三个字段：`isbn`、`title` 和 `price`。通过调用 `mysql_fetch_array()` 获取查询结果，该函数返回一个数据的关联数组。通过键索引访问数组中的元素，例如 `$array("isbn")`。

代码可以位于 `/var/www/html/php/mysql13.php` 文件，或者在线通过 `http://localhost/php/mysql13.php` 或 `www.opensourcewebapp.com/php/mysql13.php` 查看。由于代码较长，我们将分段进行讲解。先是代码，然后是解释。

```php
<?php
// 连接到本地 上的 mysql 服务器
$mysql = mysql_connect("localhost", "apache", "LampIsCool")
or die("not connect to mysql");
// 选择 "books" 数据库
mysql_select_db("books") - $mysql_error($mysql) . ": " . $mysql_error($mysql);
or die("select failed - " . $mysql_error($mysql));
// 执行 MySQL 查询，并将结果存入 $result
$result = mysql_query("SELECT isbn,title,price FROM book_information")
or die("query failed - " . $mysql_error($mysql) . ": " . $mysql_error($mysql));
?>
```

在文件顶部，PHP 代码连接到数据库，选择正确的数据库并执行我们的查询（以 // execute . . . 开始）。

```html
<html>
<head>
```
