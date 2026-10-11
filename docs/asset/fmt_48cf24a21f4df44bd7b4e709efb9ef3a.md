
如果此时任何必填字段均为空，则在页头中打印特殊消息，并使用用户之前输入的字段变量调用 `register` 函数，包括任何仍然为空的字段。

PHP 函数 `echo <string>` 会将整个字符串发送到浏览器，包括字符串中可能任何 HTML 元素。

```php
echo "All the required fields must be filled in to
continue:\n";
```

这次，调用 `register()` 时带了所有可能的参数。`register()` 在之前已经定义过。

```php
register($userid,$password
.$reusername
.$firstname,$middleinit
.$lastname,$address_1
.$address_2,$city
.$state,$zip
.$phonumber);
}
```

另一个需要测试的可能性是用户以一种方式输入密码，然后在密码确认字段中以另一种方式重新输入（无意的？）。如果它们不匹配，再次调用 `registration()`。

```php
else if ($userpassword != $reusepassword)
{
}
```

`<P>` HTML 元素会在消息之前在 Web 页面插入一个新的段落。

```php
echo "<P> Password confirmation password did not match password.\n";
echo "Please try again. Thank you.";
```

重新显示注册页面，所有字段都保留用户最初填入的内容，但密码和密码确认字段外，这两个字段将留白（不是空引号！）。

```php
register($userid,$userpassword="",
$reusepassword=""
$firstname,$middleinit
$lastname,$address_1
$address_2,$city
$state,$zip
$phonenumber);
```

测试登录名（存储为 `$userid`）的值，确保它没有被其他客户占用。如果是，则条件（`result=check_user($userid)`）将求值为 TRUE（真）。

```php
elseif(!$result=check_user($userid))
{
```

因此，如果登录名（存储为 `$userid`）未使用的事实是真的，我们可以将此客户添加到管理数据库中。我们将管理数据库作为我们的服务；我们添加用户对登录名和密码的选择。但是，我们必须以 DBA 的身份连接服务器以添加此用户。

```php
$link = mysql_connect("localhost","dba","dba2pass") or die
("Could not connect");
```

连接到 Admin 数据库并添加新用户。以下 SQL 查询允许此用户对此服务器上的数据库拥有受限访问。在我们的案例中只有一个 Order Entry 数据库。

```php
$query = "GRANT usage on *.* to $userid@localhost identified by
$userpassword";
```

# 第16章 Web应用程序

如果此操作失败，我们必须退出，因为这是一个致命错误！

```php
$result = mysql_query($query)
or die("Unable to add user\n");
```

在我们连接到 Order 数据库并将客户的全名和地址添加（SQL insert）到 Customer 表之前，我们需要选择 Order Entry 数据库，我们已将其命名为 `order_entry`（区分大小写）。如果此操作失败，我们必须退出，因为这是一个致命错误。在发生致命错误的情况下，在用户的浏览器上显示 `die()` 函数中的消息字符串，如果发生致命错误则完全退出。

```php
mysql_select_db("order_entry") or die("Web page unavailable");
```

接下来（假设上述查询成功），我们需要将客户的全名和地址添加到 Customer 表中。我们使用用户在注册页面上填入的值。

```php
$query = "insert into Customer values\n('$userid','$firstname','$middleinit','$lastname','$address_1',
'$address_2','$ci','$state','$zip','$phonumber','N')";
```

为该客户执行查询（SQL insert）。将查询的返回值保存起来以测试是否有错误（但不是致命错误）。如果查询失败，则被视为致命错误，因此在用户的浏览器上显示 `die()` 函数中的消息字符串并完全退出。

```php
$result=mysql_query($query) or die("Unable to update\n");
if($result) {
```

如果成功添加到 Customer 表，我们给客户有机会编辑这些信息（使用 `updatecustomer.php` 表单），或者进入订单表单。

```php
echo "If the following information is correct";
echo "<input type='hidden' name='userid' value=$userid>";
echo $userid<br>";
```

以下文本显示为链接，“here”是指向订单表单的链接。`<a></a>` HTML 元素封装了该链接。三个 `<br>` 元素在 Web 页面上插入换行符，使用之前定义的 `customer_pretty_print()` 函数显示客户的名字和地址。

```php
echo "<a href=/orderform.php>here</a> to
continue.<br><br><br>";
customer_pretty_print($userid);
```

以下文本显示为链接，“here”是指向更新客户表单的链接。`<a></a>` HTML 元素封装了该链接。两个 `<br>` 元素在 Web 页面上插入换行符以显示链接文本。链接文字是“here”。

```php
echo "<br>If the preceding information is not correct
click";
echo "<a href=updatecustomer.php> here</a><br>";
}
```

我们要检查的最后一个可能性是否存在相同登录名的客户，例如已经有一个 `johnsmith`。`check_user()` 函数在之前已定义。如果存在 `$userid` 值相同的客户，我们通知用户并要求用户选择不同的登录名。

```php
elseif($result=check_user($userid))
{
echo "<b> Sorry, username $userid is already in use. Please select another
username </body>";
```

重新注册页面，除 `$userid` 之外的所有字段均按照用户之前的输入设置。注意密码和确认密码被保留了，因为我们的 Order Entry 数据库的 Customer 表中登录名必须是唯一的。

```php
register($userid="",$userpassword
.$reuserpassword
$firstname,$middleinit
$lastname,$address_1
$address_2,$city
$state,$zip
$phonenumber);
}
```

此 `?>` 元素结束了 PHP 的处理。它之后出现的任何内容都由 PHP 直接传递给浏览器。

```php
?>
</html>
```

## 新成员注册

* 表示必填字段

| 用户 ID | * |
| --- | --- |
| 密码 | * |
| 再次确认密码 | * |
| 名字 | * |
| 中间字母首字母 | |
| 姓 | * |
| 地址行 1 | * |
| 地址行 2 | |
| 城市 | * |
| 州 | [选择州] |
| 邮政编码 | * |
| 电话号码 | * |

图 16-3：新注册表

## 列表 16-3： 生成的 HTML

```html
<html
<!-- 演示包含文件的使用-->
<!-- 一个名为 header.inc 的文件
(实际上是一个名为 header.inc 的文件，但我认为不应该是这样)
现在包含[sic: 应该包含]我们所有网页的共用内容。 -->
<<html>
<head>
  <title> 注册页面 </title>
</head>
<BODY
```
