
```php
$result=mysql_query($query) or die("无法显示第 2 页");
```

现在，检查此查询的结果集。其中可能包含零行或一行。由于我们将 `Customer_id` 属性设置为 `Customer` 表的主键，因此具有给定 `Customer_id` 值的记录**最多**只有一个。`mysql_fetch_object()` 函数返回一个结果行对象。使用对象指针访问原始语句 `select` 列表中的每个字段。注意 `mysql_fetch_object` 使用的是之前 `mysql_query()` 执行返回的值。

```php
$premium_customer=mysql_fetch_object($result);
```

使用客户输入的 ID 值创建一个查询，并在调用此函数时将查询传递。在此查询中，SQL 语句的 `select` 列表包含了 `Customer` 表中的姓名字段。收集所需的客户信息。

```php
$query="select Customer_id,
First_Name, Middle_initial,
Last_name
from Customer
where Customer.Customer_id='$userid";
```

使用 DBA 登录名和密码连接数据库服务器。保持 DBA 登录安全至关重要，因此不要让任何浏览器显示此页面的源代码。

首先，建立与数据库的连接。

```
$link = mysql_connect("localhost", "dba", "dba2pass") or die("Failure connecting to database");
```

一旦连接到数据库服务器，我们必须选择想要访问服务器上的哪一个数据库。对于此应用程序，我们要访问 Order Entry（订单输入）数据库。

```
$database=mysql_select_db(order_entry);
```

向订单头表（order header）中插入记录。使用当前订单号的最大值加 1 来为订单号创建一个唯一键。

之前的订单号通过使用返回列最大值的 SQL 函数来确定。为了防止出现两个几乎同时执行的此类此类查询（这在同时插入多个订单时可能会发生），我们在执行以下操作时锁定表供我们独占使用：

- 查询当前最大订单号，然后
- 使用 `1+max(Order_Number)` 作为 Order_Number 的下一个值向 Order Header 表插入一条记录。

完成后，我们必须解锁表以便处理其他订单。

创建 SQL 查询字符串以锁定 Order_Header 表供我们独占使用。注意，这是一个写锁，因为我们需要同时读和写。

```
$lock="lock tables Order_Header write";
```

现在，执行 SQL 语句锁定表。

```
$result=mysql_query($lock);
```

创建 SQL 查询字符串以检索 Order Entry 数据库中 Order_Header 表 Order_Number 字段的当前最大值。

```
$order_number=" select max(Order_Number) from Order_Header";
```

下一步要做的是获取最大订单号。执行此查询（在最近选择的数据库上执行）。如果在执行此查询期间发生严重错误，我们将终止会话。注意，在 Customer 表中未找到具有此 Customer_id 值的记录**并不是**失败。`$result` 返回值用于获取结果行。

```
$result=mysql_query($order_number,$link)
or die("Unable execute 1 \n");
```

查看此查询查询的结果集。它可能包含零行或一行。`mysql_fetch_object` 返回一个行对象。原始 select 语句列表中的每个字段都通过指针对象进行访问。注意 `mysql_fetch_object` 使用从之前的 `mysql_query()` 执行返回的值。

```
$order_number=mysql_fetch_row($result);
```

将 `$order_number[0]` 的值加 1，以获得 Order_Number 的下一个唯一值。

```
$order_number[0]++; // 给最大订单号加 1。
```

现在，我们需要生成 SQL 查询，向 Order_Header 表插入一条新记录，使用新的新的 Order_Number 值；该客户的 `$userid` 值；以及通过 MySQL 的 `CURDATE()` 函数获取订单日期。

```
$header="insert into Order_Header\n(Order_Number,Customer_id,Order_Date)
values ($order_number[0],'userid',CURDATE());";
```

在 `$link` 值所指向的数据库上执行此查询。如果在执行此查询期间发生严重错误，我们将终止会话。`$result` 返回值用于获取结果行。

```
$result=mysql_query($header,$link) // execute statement
or die("Unable execute 2 \n");
```

完成后，我们必须解锁表以便处理其他订单。在向 Order_Detail 表插入记录时，我们需要使用生成的 Order_Number 值。

```
$unlock="unlock tables"; // unlock table
```

执行 LOCK 语句。现在，Order_Header 表可以被他人读取和写入。

```
$result=mysql_query($unlock);
```

初始化我们将用于循环遍历订单列表的变量。

```
$ii=0;$jj=0;
```

在到达订单表单的最后一行之前，`$num_products` 在订单表单最初显示时已在某些 PHP 代码中确定了。它是显示的商品数量，因此也是可能被订购的产品数量。

```
while($ii < $num_products) {
```

引用变量来自上一个 HTML 页面（用户点击购买按钮之前的同一个页面）。

接下来，我们将使用字符串拼接来实际创建一个变量。我们需要这样做，是因为当 PHP 生成此页面的 HTML 时，我们使用索引号为每个订单输入条目行字段命名。因此，在用户输入值后，我们需要进行类似的操作来获取这些值。

```
$qref='quantity_'.$ii;
```

通过对该变量进行解引用获取数量。

```
$quantity=$($qref);
```

再次使用字符串拼接创建一个变量名。我们需要这样做是因为当 PHP 生成此页面的 HTML 时，每个订单输入条目行字段（在此例中为 sku 属性）使用了索引号。因此，在用户输入值后，我们需要进行类似的操作来获取这些值。

```
$sref='sku_'.$ii;
```

通过对我们使用字符串拼接创建的变量名进行解引用获取部分。

```
$sku=$($sref);
```

再次使用字符串拼接创建一个变量名。我们需要这样做是因为当 PHP 生成此页面的 HTML 时，每个订单输入条目行字段（此处为 sku 属性）使用了索引号。因此，在用户输入值后，我们需要进行类似的操作来获取这些值。

```
$pref='price_'.$ii;
```

通过解引用此变量获取价格。

```
$price=$($pref);
```

## 612 第 IV 部分：应用程序

确定扩展价格。

```
$ext_price=$price*$quantity;
if($quantity > 0) { // 如果至少有一个
```

```php
$discount = 0;
if ($ext_price > 150) {
    $discount = $ext_price * 0.25;
}
$final_price = $ext_price - $discount;
```

对于扩展价格大于零的每个项目，向我们的详情表插入：订单号；SKU；价格以及扩展价格。

```php
$insert_detail="insert into Order_Detail
(Order_Number,SKU,Price,Extended_Price)
values ($order_number[0],'$sku',$quantity,$final_price)";
mysql_query($insert_detail,$link);
```

```php
$jj++;
}
```

完成订单详情后，我们关闭数据库的连接。`$link` 的值是到此数据库的指针。

```php
mysql_close($link); // close link
```

在订单表单上打印退出消息。此时，订单表单不再包含项目，只有标题。查看此示例开头的 HTML 行：<h2>Order Form</h2>

在默认可用的最大字体打印“感谢”消息。
