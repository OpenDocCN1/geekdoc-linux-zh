
```php
<?php
$database_link = mysql_connect("mysql.clearink.com");
$query = "DELETE FROM customer";
$result = mysql_db_query("store", $query, $database_link);
mysql_close($database_link);
?>
```

## 相关函数

`mysql_query`

## `boolean mysql_drop_db(string database, integer link)`

`mysql_drop_db` 函数删除整个数据库。`link` 参数是可选的，如果省略，将使用最后一个打开的连接。

## 示例

```php
<?php
$database_link = mysql_connect("mysql.clearink.com");
mysql_drop_db("store", $database_link);
mysql_close($database_link);
?>
```

## 相关函数

`mysql_create_db`

# 第 13 章 数据库函数

## `string mysql_error()`

使用 `mysql_error()` 获取 mysql 函数返回的上一个错误消息。

## 示例

```php
<?php
$database_link = mysql_connect("mysql.clearink.com");
mysql_select_db("store", $database_link);
$query = "DELETE FROM store";
if(!mysql_query($query, $database_link)) {
    print("ERROR: " . mysql_error());
}
mysql_close($database_link);
?>
```

## 相关函数

无

## `array mysql_fetch_array(integer result)`

`mysql_fetch_array` 函数返回当前行数据的数组。`result` 参数由 `mysql_query` 返回。结果列以两个元素的形式返回：一个通过数字索引引用，另一个通过字段名引用。

## 示例

```php
<?php
$database_link = mysql_connect("mysql.clearink.com");
mysql_select_db("store", $database_link);
$query = "SELECT * FROM customer";
$result = mysql_query($query, $database_link);
while($row_data = mysql_fetch_array($result)) {
    print($row_data["FirstName"] . "<BR>\n");
}
mysql_close($database_link);
?>
```

## 相关函数

`msql_fetch_object`, `msql_fetch_row`

## `object msql_fetch_field(integer result, integer field)`

`msql_fetch_field` 函数返回一个对象，其属性描述了指定的字段。`field` 参数可以省略，并将返回下一个未获取的字段。对象的属性列于图 13–7。

## 示例

```php
$database_link = msql_connect("msql.clearink.com");
msql_select_db("store"
```

**图 13-7** `msql_fetch_field` 的属性

| 属性 | 描述 |
| :--- | :--- |
| name | 列名 |
| not_null | 如果列不能为空 |
| primary_key | 如果该列是主键 |
| table | 列所属的表 |
| type | 列的类型 |

## 相关函数

无

## `object msql_fetch_object(integer result)`

`msql_fetch_object` 函数返回当前行的对象。对象的属性为字段名。

## 示例

```php
$database_link = msql_connect("msql.clearink.com");
msql_select_db("store", $database_link);
$query = "SELECT * FROM customer";
$result = msql_query($query, $database_link);
while($row_data = msql_fetch_object($result)) {
    print($row_data->FirstName . "<BR>\n");
}
```

## 相关函数

`msql_fetch_array`, `msql_fetch_row`

## `array mysql_fetch_row(integer result)`

`mysql_fetch_row` 函数返回当前行数据的数组。`result` 参数由 `mysql_query` 返回。

## 示例

```php
<?php
$database_link = mysql_connect("mysql.clearink.com");
mysql_select_db("store", $database_link);
$query = "SELECT * FROM customer";
$result = mysql_query($query, $database_link);
while($row_data = mysql_fetch_row($result)) {
    print($row_data[0] . "<BR>\n");
}
mysql_close($database_link);
?>
```

## 相关函数

`msql_fetch_array`, `msql_fetch_object`

## `integer msql_data_seek(integer result, integer row)`

使用 `msql_data_seek` 将内部行指针移动到指定的行。`result` 参数由 `msql_query` 返回。

## 示例

```php
<?php
$database_link = mysql_connect("msql.clearink.com");
msql_select_db("store", $database_link);
$result = msql_query('SELECT * FROM customer', $database_link);
// 跳到第十个客户
msql_data_seek($result, 10);
$row_data = msql_fetch_row($result);
msql_close($database_link);
?>
```

## 相关函数

`msql_fetch_array`, `msql_fetch_object`, `msql_fetch_row`

## `integer mysql_db_query(string database, string query, integer link)`

`mysql_db_query` 函数与 `mysql_query` 相同，不同在于它指定了一个数据库，而不是使用通过 `mysql_select_db` 选择的数据库。查询在指定的数据库中执行并返回结果标识符。

## 示例

```php
<?php
$database_link = mysql_connect("mysql.clearink.com");
$query = "DELETE FROM customer";
$result = mysql_db_query("store", $query, $database_link);
mysql_close($database_link);
?>
```

## 相关函数

`mysql_query`

## `boolean mysql_drop_db(string database, integer link)`

`mysql_drop_db` 函数删除整个数据库。`link` 参数是可选的，如果省略，将使用最后一个打开的连接。

## 示例

```php
<?php
$database_link = mysql_connect("mysql.clearink.com");
mysql_drop_db("store", $database_link);
mysql_close($database_link);
?>
```

## 相关函数

`mysql_create_db`

# 第 13 章 数据库函数

## `string mysql_error()`

使用 `mysql_error()` 获取 mysql 函数返回的上一个错误消息。

## 示例

```php
<?php
$database_link = mysql_connect("mysql.clearink.com");
mysql_select_db("store", $database_link);
$query = "DELETE FROM store";
if(!mysql_query($query, $database_link)) {
    print("ERROR: " . mysql_error());
}
mysql_close($database_link);
?>
```

## 相关函数

无

## `array mysql_fetch_array(integer result)`

`mysql_fetch_array` 函数返回当前行数据的数组。`result` 参数由 `mysql_query` 返回。结果列以两个元素的形式返回：一个通过数字索引引用，另一个通过字段名引用。

## 示例

```php
<?php
$database_link = mysql_connect("mysql.clearink.com");
mysql_select_db("store", $database_link);
$query = "SELECT * FROM customer";
$result = mysql_query($query, $database_link);
while($row_data = mysql_fetch_array($result)) {
    print($row_data["FirstName"] . "<BR>\n");
}
mysql_close($database_link);
?>
```

## 相关函数

`msql_fetch_object`, `msql_fetch_row`

## `object msql_fetch_field(integer result, integer field)`

`msql_fetch_field` 函数返回一个对象，其属性描述了指定的字段。`field` 参数可以省略，并将返回下一个未获取的字段。对象的属性列于图 13–7。

## 示例

```php
$database_link = msql_connect("msql.clearink.com");
msql_select_db("store"
```

**图 13-7** `msql_fetch_field` 的属性

| 属性 | 描述 |
| :--- | :--- |
| name | 列名 |
| not_null | 如果列不能为空 |
| primary_key | 如果该列是主键 |
| table | 列所属的表 |
| type | 列的类型 |

```php
<?php
print("Field 0 is " . msql_fieldname($result, 0));
msql_close($database_link);
?>
```

## 相关函数

- `msql_fetch_field`

### `string msql_fieldtable(integer result, integer field)`

`msql_fieldtable` 函数返回指定字段的表名。

## 示例

```php
<?php
$database_link = msql_connect("msql.clearink.com");
msql_select_db("store", $database_link);
$query = "SELECT * FROM item";
$result = msql_query($query, $database_link);
print("Field 0 is from " . msql_fieldtable($result, 0));
msql_close($database_link);
?>
```

## 相关函数

- `msql_fetch_field`

### `string msql_fieldtype(integer result, integer field)`

`msql_fieldtype` 函数返回指定字段的类型。

## 示例

```php
<?php
$database_link = mysql_connect("mysql.clearink.com");
mysql_select_db("store", $database_link);
$query = "SELECT * FROM item";
$result = mysql_query($query, $database_link);
print("Field 0 is " . mysql_fieldtype($result, 0));
mysql_close($database_link);
?>
```

## 相关函数

- `mysql_fetch_field`

### `boolean mysql_free_result(integer result)`

当脚本结束时，所有结果都会释放。如果脚本运行期间内存内存问题，请使用 `mysql_free_result`。

## 示例

```php
<?php
$database_link = mysql_connect("mysql.clearink.com");
mysql_select_db("store", $database_link);
$query = "INSERT INTO store VALUES (0, 'Martinez')";
$result = mysql_query($query, $database_link);
mysql_free_result($result);
mysql_close($database_link);
?>
```

## 相关函数

- `mysql_query`

### `integer mysql_list_dbs(integer link)`

`mysql_list_dbs` 函数返回一个结果标识符，就好像使用 `mysql_query` 查询了数据库一样。可以使用任何获取行的函数来获取数据库的名称。`link` 参数是可选的。如果留空，将使用上一个打开的连接。

## 示例

```php
<?php
$database_link = mysql_connect("mysql.clearink.com");
mysql_select_db("store", $database_link);
$result = mysql_list_dbs($database_link);
while($row_array = mysql_fetch_row($result)) {
    print($row_array[0]) . "<br>";
}
mysql_close($database_link);
?>
```

## 相关函数

- `mysql_list_fields`, `mysql_list_tables`

### `integer mysql_list_fields(string database, string tablename, integer link)`

`mysql_list_fields` 函数返回一个结果标识符，就好像使用 `mysql_query` 查询了数据库一样。可以使用任何用于获取字段名称的函数。`link` 参数是可选的。如果留空，将使用最后一个打开的连接。

## 示例

```php
<?php
$database_link = mysql_connect("mysql.clearink.com");
mysql_select_db("store", $database_link);
$result = mysql_list_fields("store", "item");
while($row_array = mysql_fetch_row($result)) {
    print($row_array[0]) . "<br>";
}
mysql_close($database_link);
?>
```

## 相关函数

- `mysql_list_dbs`, `mysql_list_tables`

### `integer mysql_list_tables(string database, integer link)`

`mysql_list_tables` 函数返回一个结果标识符，就好像使用 `mysql_query` 查询了数据库一样。可以使用任何获取行或字段的函数来获取字段名称。`link` 参数是可选的。如果留空，将使用上一个打开的连接。

## 示例

```php
<?php
$database_link = mysql_connect("mysql.clearink.com");
mysql_select_db("store", $database_link);
$result = mysql_list_tables("store");
while($row_array = mysql_fetch_row($result)) {
    print($row_array[0]) . "<br>";
}
mysql_close($database_link);
?>
```

## 相关函数

- `mysql_list_dbs`, `mysql_list_fields`
