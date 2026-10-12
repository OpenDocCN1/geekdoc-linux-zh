
`$sql_result = sybase_query($sql,$connection) or die ("Couldn't execute query.");`

要格式化当前存储在 `$sql_result` 中的结果，首先使用 `sybase_fetch_array()` 函数按行分离结果：

```
while ($row = sybase_fetch_array($sql_result)) {

  // 在此处编写代码。

}
```

`while` 循环为结果集中的每条记录创建一个名为 `$row` 的数组。要获取记录的单独元素（`FULL_NAME`、`BIRTH_DATE`、`FAVE_COLOR`），请创建特定的变量：

```
$full_name = $row["FULL_NAME"];

$birth_date = $row["BIRTH_DATE"];

$fave_color = $row["FAVE_COLOR"];
```

你可能想在一个简单的 HTML 表格中打印结果。退一步在 `while` 循环开始之前放置此语句，以打开标签并创建行头：

```
echo "<TABLE ORDER=1>";
echo "<tr><th>Full Name</th><th>Birthday</th><th>Fave Color</th></tr>";
```

在 `while` 循环内定义变量后，按你的表格格式打印它们：

```
echo "<tr><td>$full_name</td><td>$birth_date</td><td>$fave_color</td></tr>";
```

新的 `while` 循环看起来像这样：

```
while ($row = sybase_fetch_array($sql_result)) {

$full_name = $row["FULL_NAME"];
```

# 第 3 章：与数据库交互

```
$birth_date = $row["BIRTH_DATE"];

$fave_color = $row["FAVE_COLOR"];

echo "<TR><TD>$full_name</TD><TD>$birth_date</TD><TD>$fave_color</TD></TR>;
```

`while` 循环，关闭 HTML 表格：

```
echo "</TABLE>";
```

最后，你想要释放执行查询所需的资源并关闭数据库连接。不这样做可能会导致内存泄漏和其他糟糕的资源占用问题。

```
sybase_free_result($sql_result);

sybase_close($connection);
```

从 Sybase 数据库执行简单连接和数据选择的完整脚本可能如下：

```
<?php

// 创建连接

// 替换为你自己的主机名、用户名和密码

$connection = sybase_connect("localhost","sandman","34Nhjjp") or die("Couldn't
connect to the server.");

// 选择数据库

$db = sybase_select_db("secretDB", $connection) or die("Couldn't
database.");

// 创建 SQL 语句

$sql = "SELECT FULL_NAME, BIRTH_DATE, FAVE_COLOR
FROM FRIEND_INFO
ORDER BY BIRTH_DATE ASC";

// 执行 SQL 查询并获取结果

$sql_result = sybase_query($sql,$connection) or die("Couldn't execute query.");

// 开始格式化结果

echo "<TABLE BORDER=1>";
echo "<TR><TH>Full Name</TH><TH>Birthday</TH><TH>Favorite Color</TH></TR>";

// 按行格式化结果

while($row = sybase_fetch_array($sql_result)) {
$full_name = $row["FULL_NAME"];
$birth_date = $row["BIRTH_DATE"];
$fave_color = $row["FAVE_COLOR"];
echo "<TR><TD>$full_name</TD><TD>$birth_date</TD><TD>$fave_color</TD></TR>";
}

echo "</TABLE>";

// 释放资源并关闭连接

sybase_free_result($sql_result);

sybase_close($connection);

?>
```

# 第 4 章：创建和填充数据库表

希望上一章节已经让你对使用 PHP 连接数据库有了基本的了解。现在，我们将超越基础连接，使用 PHP 和 HTML 表单来创建数据库表并向这些表填充数据。

以下代码示例使用了 MySQL 数据库；然而，每个操作都可以在任何支持的数据库类型上执行。请检查 http://www.php.net/manual/ 上的 PHP 手以获取适用于你数据库的精确函数名称——它们不会差异。

## 创建数据库表

本质上，要创建一个简单的数据库表，你只需要给它一个名称。但这会让表变得很无趣，因为它不包含任何列（字段），也无法存储任何数据。因此，除了名称之外，你应该知道你想要在表中包含的字段数量以及字段类型。

假设你开了一家商店，想要创建一个表来存储所有的产品。考虑一下你可能需要的字段类型：产品识别码、标题、描述以及物品价格。现在，为该表想一个名称，例如 MY_PRODUCTS。

接下来，你将创建一系列表单，获取你的表信息并将其发送到 MySQL 数据库中。在第一步中，你将提交表名和你想包含的字段数量。第二步将显示额外的表单字段，以便你定义表列的属性。最后，第三步将请求发送到 MySQL，验证表是否已创建，并显示“成功！”消息。

### 第一步：基础表定义

开始，打开你喜欢的文本编辑器，创建一个名为 `show_creatatable1.html` 的文件，并设置一个 HTML “外壳”：

```html
<!DOCTYPE HTML PUBLIC "//W3C//DTD HTML 3.2//EN">
<HTML>
<HEAD>
<TITLE>创建数据库表：第 1 </TITLE>
</HEAD>
<BODY>
  <!-- HTML form将放在这里 -->
</BODY>
</HTML>
```

为了创建表单代码，假设序列中的第二步是一个名为 `do_showfielddef.php` 的 PHP 脚本，并且你的表单将使用 POST 方法：

```html
<FORM method="POST" action="do_showfielddef.php">
```

接下来，创建两个文本字段来获取 `$table_name` 和 `$num_fields` 的值——即新表的名称和它包含的字段数量：

```html
<P>Table Name:<br><INPUT type="text" name="table_name" size=30></P>
<P>Number of Fields:<br><INPUT type="text" name="num_fields" size=5></P>
```

最后，添加“前往第 2 步”按钮：

```html
<INPUT type="submit" value="Go to Step 2">
```

不要忘记闭合 `</FORM>` 标签：

你的 HTML 源代码应该如下：

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 3.2//EN">
<HTML>
<HEAD>
<TITLE>创建数据库表：第 1  </TITLE>
</HEAD>
<BODY>
<FORM method="POST" action="do_showfielddef.php">
<P>Table Name:<br><INPUT type="text" name="table_name" size=30></p>
<P>Number of Fields:<br><INPUT type="text" name="num_fields" size=5></p>
<INPUT type="submit" value="Go to Step 2">
</FORM>
</BODY>
</HTML>
```
