
将此文件放在你的 Web 服务器上，并通过浏览器访问其 URL `http://www.yourserver.com/show_createtable1.html`。在你的浏览器窗口中，你现在应该看到图 4.1 所示的内容。

在下一步中，你将根据第 1 步通过表单发送的值，在第 2 步中动态创建表单的各个。

![](img/f8bb5053a1d20d75df488da4d4dbfceb_131_0.png)

## 第二步：字段定义

在第 1 步中，你创建了变量来存储表名 (`$table_name`) 和你想放在表中的字段数量 (`$num_fields`)。在这一步中，你将创建一个 PHP 脚本来显示进一步定义字段所需的额外表单元素。开始，打开你喜欢的文本编辑器并创建一个名为 `do_showfielddef.php` 的文件。

在脚本执行其他操作之前，你可能想要检查第 1 步表单中是否真的输入了值。设置一个查找这些值的语句，如果它们不存在，则将用户重定向到第 1 步的表单：

```php
<?php
if (!$table_name) || (!($num_fields)) {
    header("Location: http://www.yourserver.com/show_creatable1.html");
    exit;
}
?>
```

接下来，在 if 语句之后添加 HTML “外壳”：

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 3.2//EN">
<HTML>
<HEAD>
<TITLE>创建数据库表：第 2 </TITLE>
</HEAD>
<BODY>
<!-- HTML form将放在这里 -->
</BODY>
</HTML>
```

```php
<?php
if (!$table_name) || (!$num_fields)) {
    header("Location: http://www.yourserver.com/show_createtable.html");
    exit;
}
?>
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 3.2//EN">
<HTML>
<HEAD>
<TITLE>创建数据库表：第 2 步</TITLE>
</HEAD>
<BODY>
<h1>为 <?php echo $table_name; ?> 定义字段</h1>
<FORM method="POST" action="do_createtable.php">
<INPUT type="hidden" name="table_name" value="<?php echo $table_name; ?>">
<table cellspacing="5">
<tr
<th>字段名称</th><th>字段类型</th><th>字段长度</th>
</tr>
<?php
for ($i = 0; $i < $num_fields; $i++) {
    echo "
<tr>
<td align="center">
<input type="text" name="field_name[]" size="30">
</td>
<td align="center">
<select name="field_type[]">
<option value="float">float</option>
<option value="int">int</option>
<option value="text">text</option>
<option value="varchar">varchar</option>
</select>
</td>
<td align="center"></td>
</tr>
";
}
?>
</table>
</FORM>
</BODY>
</HTML>
```

### 创建数据库表

```html
<input type="text" name="field_length[]" size="5">
</td>
</tr>
?>
<tr>
<td align="center" colspan=3">
<INPUT type="submit" value="创建表">
</td>
</tr>
</table>
</FORM>
</BODY>
</HTML
```

将此文件放置在你的 Web 服务器上，返回访问第 1 步表单的 URL：`http://www.yourserver.com/show_createtable1.html`。为表名输入 `MY_PRODUCTS`，字段数量输入 `4`。在你的浏览器窗口中，你现在将看到图 4.2 所示的内容。

![](img/f8bb5053a1d20d75df488da4d4dbfceb_136_0.png)

### 为 MY_PRODUCTS 定义字段

| 字段名称 | 字段类型 | 字段长度 |
|---|---|---|
| Real | | |
| Real | | |
| Real | | |
| Real | | |

图 4.2 第 2 步：字段定义表

## 第 3 步：连接 MySQL 并创建表

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 3.2//EN">
<HTML>
<HEAD>
<TITLE>创建数据库表：第 3 步</TITLE>
</HEAD>
<BODY>
<!--你的 HTML 表单将在这里 -->
</BODY>
</HTML>
```

为页面添加一个标题，以便知道你正在操作什么：

```html
<h1>正在添加表 <?php echo $table_name; ?></h1>
```

下部分 PHP 代码将构建发送到 MySQL 的 SQL 语句。记住，CREATE 的语法是：

```sql
CREATE TABLE [table name] ([field_name field_data_type,...]) [options])
```

将 SQL 语句存储在名为 `$sql` 的变量中，并初始为该变量填充 CREATE 语句的第一部分加上 `$table_name` 的值：

```php
$sql = "CREATE TABLE $table_name ("
```

现在创建一个循环来填充 SQL 语句的剩余部分。该循环的的次数取决于你想向表中添加的字段数量，或者你在第 2 步中定义的字段数量。由于每个字段定义都存放在一个数组中，因此你可以通过计算 `$field_name` 数组中的元素数量来获取循环运行次数：

```php
for ($i = 0; $i < count($field_name); $i++) {
// 此处编写更多代码
}
```

对于每个新字段，你需要使用以下语法向 SQL 语句中添加字段名、类型和长度：

```text
field_name_field_type (field_length)
```

| 必须用逗号分隔多个字段定义。

![](img/f8bb5053a1d20d75df488da4d4dbfceb_137_0.png)

在循环内部，添加此语句以开始向 `$sql` 变量添加值：

```php
$sql .= "$field_name[$i] $field_type[$i];";
```

在添加字段长度之前，检查是否指定了长度，将其添加到 `$sql` 变量，然后结束循环：

```php
if ($field_length[$i] != "*") {
  $sql .= "($field_length[$i]);";
} else {
  $sql .= ",";
}
```

此 `if_else` 语句会查找 `$field_length` 的值，如果找到则将其打印在括号内。它添加一个逗号将该值与下一个等待添加的字段隔开。如果没有找到值，则在 SQL 语句中添加逗号。

整个循环看起来应该是这样：

```php
for ($i = 0; $i < count($field_name); $i++) {
  $sql .= "$field_name[$i] $field_type[$i];";
  if ($field_length[$i] != "*") {
    $sql .= "($field_length[$i]);";
  } else {
    $sql .= ",";
  }
}
```

然而，SQL 语句还有一些工作需要完成：它末尾有一个多余的逗号，且括号尚未关闭。为了去掉末尾的多余逗号，使用 `substr()` 函数只返回字符串的一部分。在这种情况下，你将返回整个字符串但排除最后一个字符：

```php
$sql = substr($sql, 0, -1);
```
