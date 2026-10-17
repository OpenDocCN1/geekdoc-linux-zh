
### `integer` `mysql_num_fields`(`integer` `result`)

使用 `mysql_num_fields` 获取结果集中的字段数量。

## 示例

```php
<?php
$database_link = mysql_connect("mysql.clearink.com");
mysql_select_db("store", $database_link);
$query = "SELECT * FROM item i, s";
$query .= "WHERE i.SKU = s.ID";
$result = mysql_query($query, $database_link);
print(mysql_num_fields($result));
mysql_close($database_link);
?>
```

## 相关函数

- `mysql_num_rows`

### `integer` `mysql_num_rows`(`integer` `result`)

`mysql_num_rows` 函数返回结果集中的行数。

## 示例

```php
<?php
$database_link = mysql_connect("mysql.clearink.com");
mysql_select_db("store", $database_link);
$query = "SELECT * FROM item i, s";
$query = "WHERE i.SKU = s.ID";
$result = mysql_query($query, $database_link);
print(mysql_num_rows($result));
mysql_close($database_link);
?>
```

## 相关函数

- `mysql_num_fields`

### `integer` `mysql_pconnect`(`string` `host`)

`mysql_pconnect` 函数与 `mysql_connect` 函数相同，不同之处脚本结束时不会关闭连接。这在 PHP 编译为 Apache 模块时才有意义。这些被称为持久连接；它们会随着服务器进程而存在。

## 示例

```php
<?php
$database_link = mysql_pconnect("localhost");
?>
```

## 相关函数

- `mysql_connect`

### `integer` `mysql_query`(`string` `query`, `integer` `link`)

使用 `mysql_query` 执行查询。使用的数据库将是调用 `mysql_select_db` 时指定的。`link` 参数是可选的。如果留空，将使用最后建立的连接。

## 示例

参见本节中的其他示例。

## 相关函数

- `mysql_db_query`

### `msql_regcase`

这是 `sql_regcase` 的别名。

### `string` `mysql_result`(`integer` `result`, `integer` `row`, `string` `field`)

`mysql_result` 函数返回给定行的单个字段值。`field` 参数可以有两种解释方式。如果它是一个数字，将被用作字段偏移量，从零开始。否则，它被视为列名。

`mysql_result` 函数相对较慢。应该避免使用它，而是使用更快的函数，如 `mysql_fetch_row`。

## 示例

```php
<?php
$database_link = mysql_connect("mysql.clearink.com");
mysql_select_db("store", $database_link);
$query = "SELECT * FROM item i, s";
$result = mysql_query($query, $database_link);
?>
```

## 第 13 章 数据库函数

### `boolean` `mysql_close`(`integer` `link`)

使用 `mysql_close` 关闭与数据库的连接。该连接必须已通过 `mysql_connect` 开启。使用此函数并非绝对必要，因为所有非持久性连接在脚本结束时会自动关闭。

## 示例

```php
<?php
// 打开连接
$mysql_link = mysql_connect("localhost", "httpd", "");

// 关闭连接
mysql_close($mysql_link);
?>
```

## 相关函数

- `mysql_connect`

### `integer` `mysql_connect`(`string` `host`, `string` `user`, `string` `password`)

`mysql_connect` 函数在指定的主机上开始与 MySQL 数据库建立连接。如果数据库在不同的端口，请在主机名后加上冒号和端口号。所有参数都是可选的，将默认为 `localhost`、执行脚本的用户名以及空字符串。执行脚本的用户通常是 `httpd`，即 Web 服务器。

连接在脚本执行完毕时会自动关闭，尽管也可以通过 `mysql_close` 提前关闭。如果你尝试打开一个已经打开的连接，则不会建立第二个连接。将返回之前打开的连接的标识符。

如果发生错误，则返回 False (0)。

## 示例

参见本节中的任何其他示例。

## 相关函数

- `mysql_close`, `mysql_pconnect`

### `boolean` `mysql_create_db`(`string` `database`, `integer` `link`)

使用 `mysql_create_db` 创建新数据库。请注意，你必须使用具有创建数据库权限的账户开启连接。如果你省略了 `link` 参数，将使用最后一个打开的连接。

## 示例

```php
<?
// 打开连接
$mysql_link = mysql_connect("localhost", "admin", "secret");
mysql_create_db("store", $mysql_link);
?>
```

## 相关函数

- `mysql_drop_db`

### `boolean` `mysql_data_seek`(`integer` `result`, `integer` `row`)

`mysql_data_seek` 函数将结果集的内部行指针移动到指定的行。将此函数与 `mysql_fetch_row` 配合使用，可以跳转到获取特定行的数据。`result` 参数必须由 `mysql_query` 或类似的函数返回。

## 示例

```php
<?
// 连接到服务器
$mysql_link = mysql_connect("localhost", "httpd", "");

// 选择 'store' 数据库
$mysql_select_db("store", $mysql_link);

// 获取 customer 表中的所有内容
$query = "SELECT * FROM customer";
$mysql_result = mysql_query($query, $mysql_link);

// 跳转到第五行
mysql_data_seek($mysql_result, 4);

// 获取行
$row = mysql_fetch_row($mysql_result);

// 打印第一个字段
print($row[0]);
```

## 相关函数

- `mysql_fetch_array`, `mysql_fetch_object`, `mysql_fetch_row`

### `integer` `mysql_db_query`(`string` `database`, `string` `query`, `integer` `link`)

`mysql_db_query` 函数在指定的数据库上执行查询并返回一个结果标识符。如果省略了 `link` 参数，将使用最后一个打开的连接，或者在必要时创建一个新连接。

## 示例

```php
<?
// 连接到服务器
$mysql_link = mysql_connect("localhost", "httpd", "*");

// 获取 customer 表中的所有内容
$query = "DELETE FROM customer";
$mysql_result = mysql_db_query("store", $query, $mysql_link);
?>
```

## 相关函数

- `mysql_query`

### `boolean` `mysql_drop_db`(`string` `database`, `integer` `link`)

使用 `mysql_drop_db` 删除数据库。如果省略了 `link` 参数，将使用最后一个打开的连接。

## 示例

```php
<?php
// 打开连接
$mysql_link = mysql_connect("localhost", "admin", "secret");
mysql_drop_db("store", $mysql_link);
?>
```

## 相关函数

- `mysql_create_db`

### `integer` `mysql_errno`(`integer` `link`)

`mysql_errno` 函数返回上一次数据库操作的错误代码。如果省略了可选的 `link` 标识符，则假设为最后一个连接。

## 示例

```php
<?php
// 使用错误的密码连接
$mysql_link = mysql_connect("localhost", "admin", "bad");

// 获取错误和错误代码
$errno = mysql_errno($mysql_link);
$error = mysql_error($mysql_link);

print("ERROR $errno: $error<BR>\n");
?>
```

## 相关函数

- `mysql_error`

### `string` `mysql_error`(`integer` `link`)

使用 `mysql_error` 获取上一次数据库操作错误的文本描述。如果省略了可选的 `link` 标识符，则假设为最后一个连接。

## 示例

参见 `mysql_errno` 示例。

## 相关函数

- `mysql_errno`

### `array` `mysql_fetch_array`(`integer` `result`)

`mysql_fetch_array` 函数返回一个表示结果集中某行所有字段的数组。每次调用都会产生下一行，直到没有剩余行，此时返回 false。每个字段值都存储两次：一次通过从零开始的偏移量索引，另一次通过字段名索引。

## 示例

```php
<?
// 连接到服务器
$mysql_link = mysql_connect("localhost", "httpd", "");

// 选择 'store' 数据库
$mysql_select_db("store", $mysql_link);

// 获取 customer 表中的所有内容
$query = "SELECT * FROM customer";
$mysql_result = mysql_query($query, $mysql_link);

// 获取每一行
while($row = mysql_fetch_array($mysql_result)) {
    // 名称
    print($row["name"]);
}
?>
```

### `string` `mysql_fetch_field`(`integer` `result`, `integer` `row`)

`mysql_fetch_field` 函数返回关于结果集中字段的对象。该对象具有以下属性：

| 属性 | 说明 |
| :--- | :--- |
| table | 表名 |
| name | 字段名 |
| null | 如果字段可以为空 |
| type | 字段类型 |
| primary_key | 如果字段为主键 |
| unique | 如果字段是唯一的 |
| unsigned | 如果字段是无符号 |

## 示例

```php
<?php
// 连接到服务器
$mysql_link = mysql_connect("localhost", "httpd", "");

// 选择 'store' 数据库
$mysql_select_db("store", $mysql_link);

// 获取 customer 表中的所有内容
$query = "SELECT * FROM customer";
$mysql_result = mysql_query($query, $mysql_link);

// 获取每个字段
while($field = mysql_fetch_field($mysql_result)) {
    // 打印表名、名称和类型
    print($field->table . " - " . $field->name . " - " . $field->type . "<BR>\n");
}
?>
```

## 相关函数

- `mysql_fetch_array`, `mysql_fetch_row`

### `array` `mysql_fetch_lengths`(`integer` `result`)

`mysql_fetch_lengths` 函数返回结果集中每个字段的最大长度数组。

## 示例

```php
<?php
// 连接到服务器
$mysql_link = mysql_connect("localhost", "httpd", "");

// 选择 'store' 数据库
$mysql_select_db("store", $mysql_link);

// 获取 customer 表中的所有内容
$query = "SELECT * FROM customer";
$mysql_result = mysql_query($query, $mysql_link);

// 获取字段长度
$lengths = mysql_fetch_lengths($mysql_result);

// 打印第三列的长度
print($lengths[2]);
?>
```

## 相关函数

- `mysql_fetch_field`, `mysql_field_name`, `mysql_field_table`, `mysql_field_type`, `mysql_field_flags`

### `object` `mysql_fetch_object`(`integer` `result`)

`mysql_fetch_object` 函数与 `mysql_fetch_array` 和 `mysql_fetch_row` 类似。它不返回数组，而是返回一个对象。结果中的每个字段都是返回对象中的一个属性。每次调用 `mysql_fetch_object` 都会返回下一行，如果没有剩余行，则返回 false。

## 示例

```php
<?
// 连接到服务器
$mysql_link = mysql_connect("localhost", "httpd", "");

// 选择 'store' 数据库
$mysql_select_db("store", $mysql_link);

// 获取 customer 表中的所有内容
$query = "SELECT * FROM customer";
$mysql_result = mysql_query($query, $mysql_link);

// 获取每一行
while($row = mysql_fetch_object($mysql_result)) {
    // 打印名称
    print($row->name);
}
?>
```

## 相关函数

- `mysql_fetch_array`, `mysql_fetch_row`

## `array` `mysql_fetch_row`(`integer` `result`)

`mysql_fetch_row` 函数返回一个数组，用于表示结果集中某行的所有字段。每次调用都会产生下一行，直到没有剩余行，此时将返回 false。每个字段值都通过从零开始的偏移量索引。这是从查询中获取结果最快的方法。

## 示例

```php
<?
// 连接到服务器
$mysql_link = mysql_connect("localhost", "httpd", "");

// 选择 'store' 数据库
$mysql_select_db("store", $mysql_link);

// 从 customer 表中获取所有数据
$query = "SELECT * FROM customer ";
$mysql_result = mysql_query($query, $mysql_link);

// 获取每一行
while($row = mysql_fetch_row($mysql_result)) {
    // 打印名称（第二列）
    print($row[1]);
}
?>
```

## 相关函数

- `mysql_fetch_array`, `mysql_fetch_object`

## `string` `mysql_field_flags`(`integer` `result`, `integer` `field`)

使用 `mysql_field_flags` 获取指定字段标志的描述。

## 示例

```php
// 连接到服务器
$mysql_link = mysql_connect("localhost", "httpd", "");

// 选择 'store' 数据库
$mysql_select_db("store", $mysql_link);

// 从 customer 表中获取所有数据
$query = "SELECT * FROM customer";
$mysql_result = mysql_query($query, $mysql_link);

$fields = mysql_num_fields($mysql_result);
for($index = 0; $index < $fields; $index++) {
    print(mysql_field_flags($index)) . "<BR>\n";
}
```

## 相关函数

- `mysql_fetch_field`, `mysql_field_len`, `mysql_field_name`, `mysql_field_table`, `mysql_field_type`
