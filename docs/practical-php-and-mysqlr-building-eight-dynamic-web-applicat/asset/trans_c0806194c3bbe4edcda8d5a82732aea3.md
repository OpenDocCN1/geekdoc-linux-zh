
在这一行中，一系列 GET 变量向 PayPal 网站传递数据。这些 GET 变量是保留字，PayPal 可以使用它们来处理订单。表 6-4 解释了每个变量的用途。

### 表 6-4 PayPal 变量说明

| PayPal 变量 | 设置 | 描述 |
|---|---|---|
| business | "you%40youraddress.com"& | 正在运行该网站的商业名称。 |
| item_name | urlencode($config_site-name) . "+Order" | 订单的小名称——在本例中为 <sitename> Order`。 |
| item_number | "PROD" . $row['id'] | 产品代码。在此处将 `PROD` 和订单编号连接起来（例如 PROD12）。 |
| amount | urlencode(sprintf('%.2f' , $row['total'])) | 订单金额。 |
| no_note | 1 | no_note 变量指定客户是否应随付款注明说明。将其设置为 1 表示无需说明。 |
| currency_code | GBP | 交易的货币类型。 |
| lc | GB | 交易的地域（locale）。 |

重要的是要记住，作为 GET 变量传输的任何文本信息都应通过 urlencode() 进行转义，以处理非标准字符。

开始编写处理支票付款的代码。这段代码与 PayPal 代码类似。

```php
header("Location: https://www.paypal.com/cgi-bin/webscr?cmd=_xclick&business=you%40youraddress.com&item_name=" . urlencode($config_sitename) . "+Order&item_number=PROD" . $row['id'] ."&amount=". urlencode(sprintf('%.2f', $row['total'])) . "&no_note=1&currency_code=GBP&lc=GB&submit.x=41&submit.y=15");
```

```php
else if($POST['chequesubmit'])
{
    $sql = "UPDATE orders SET status = 2, payment_type = 2 WHERE id = '$_SESSION['SESS_ORDERNUM']';
    $res = mysql_query($sql);
```

在此处再次更新订单表，但这次 `payment_type` 是 `2` 而不是 `1`。

像之前一样重置订单：

```php
$res = mysql_query($sql);
if($SESSION['SESS_LOGGEDIN'])
{
    unset($SESSION['SESS_ORDERNUM']);
}
else
{
    session_register("SESS_CHANGEID");
    $SESSION['SESS_CHANGEID'] = 1;
}
```

最后，显示用户应将支票寄往的地址详情：

```php
$SESSION['SESS_CHANGEID'] = 1;
? >

require("header.php");
?>
<h1>使用支票付款</h1>
请让支票的抬头为
<strong><?php echo $config_sitename; ?> </strong> .
<p>
将支票寄送至：
<p>
<?php echo $config_sitename; ?><br>
22, This Place,<br>
This town,<br>
This county,<br>
FG43 F3D.<br>
</p>
? >
}
```

处理现已完成。

打开显示表单的区块。然而，在到达表单之前，添加 `showcart()` 函数以汇总当前购物车：

```php
<?php
    }
    else
    {
        require("header.php");
        echo "<h1>Payment</h1>";
        showcart();
    }
?>

<h2>选择付款方式</h2>
<form action='checkout-pay.php' method='POST'>

    最后，添加闭合代码：

    </table>
    </form>

<?php
    }

    require("footer.php");
?>
```

你全新的、自制的付款界面现在应该类似于图 6-8。

![](img/c75d0c4fa51711b62f211459ae794f3f_221_0.png)

**图 6-8 完成的付款界面**

## 管理员页面

购物车的管理端非常简单。管理员的主要功能是查看和确认已完成的订单。当订单被确认后，管理员已成功发出产品。

第一步是提供管理员登录。创建一个名为 *adminlogin.php* 的新文件并添加以下代码：

```php
<?php
session_start();
require("db.php");

if(isset($_SESSION['SESS_ADMINLOGGEDIN']) == TRUE) {
	header("Location: " . $config_basedir);
}

if($_POST['submit'])
{
	$login_sql = "SELECT * FROM admins WHERE
username = '" . $_POST['userBox'] . "' AND
password = '" . $_POST['passBox'] . "'";
	$loginres = mysql_query($login_sql);
	$numrows = mysql_num_rows($loginres);

	if($numrows == 1)
	{
		$loginrow = mysql_fetch_assoc($loginres);
		session_register("SESS_ADMINLOGGEDIN");
		$_SESSION['SESS_ADMINLOGGEDIN'] = 1;

		header("Location: " . $config_basedir . "adminorders.php");
	}
	else
	{
		header("Location: " . $config_basedir
		. "adminlogin.php?error=1");
	}
}
else
{

	require("header.php");

echo "<h1>Admin Login</h1>";
```

```php
if($_GET['error'] == 1) {
    echo "<strong>Incorrect username/password!</strong>";
}
?>
<p>
<form action="<?php echo $SCRIPT_NAME; ?>" method="POST">
<table>
    <tr>
        <td>Username</td>
        <td><input type="textbox" name="userBox">
    </tr>
    <tr>
        <td>Password</td>
        <td><input type="password" name="passBox">
    </tr>
    <tr>
        <td></td>
        <td><input type="submit" name="submit" value="Log in">
    </tr>
</table>
</form>

<?php
}

require("footer.php");
?>
```

这部分代码的大部分对你来说应该很熟悉。当管理员成功登录后，会创建 SESS_ADMINLOGGEDIN 变量。

### 注销管理员

要注销管理员，创建一个名为 *adminlogout.php* 的文件并添加以下代码：

```php
<?php

session_start();

require("config.php");

session_unregister("SESS_ADMINLOGGEDIN");

header("Location: " . $config_basedir);
?>
```

与正常用户注销一样，你注销了该变量——而不是销毁整个会话。这防止了当管理员同时以管理员和用户身份登录时完全被注销。

### 管理已完成的订单

主要管理员页面显示已完成订单的列表。此页面的目的是使管理员能够查看哪些订单需要邮寄产品。然后，管理员可以创建包裹，并在邮寄后确认订单。

此页面相当直接；它只是从一些表中输出数据。脚本有两种主要状态：显示订单或确认它们。默认页面显示订单。如果你向该页面传递 `func=conf` GET 变量和订单编号，订单将被确认。

创建一个名为 *adminorders.php* 的新文件并开始添加代码：

```php
`<?php
session_start();

require("config.php");
require("db.php");
require("functions.php");

if(isset($_SESSION['SESS_ADMINLOGGEDIN']) == FALSE) {
header("Location: " . $config_basedir);
}`
```

在通常的引导代码之后，检查 func GET 变量是否存在：

```php
`if(isset($_GET['func']) == TRUE) {
if($_GET['func'] != "conf") {
header("Location: " . $config_basedir);
}

$validid = pf_validate_number($_GET['id'],
"redirect", $config_basedir);

$fmysql = "UPDATE orders SET
status = 10 WHERE id = " . $_GET['id'];
mysql_query($fmysql);

header("Location: " . $config_basedir . "adminorders.php");
}`
```

如果 func GET 变量存在，当变量被设置为 conf 以外的任何值时，页面会重定向；这防止了 SQL 注入攻击。接下来，验证 id GET 变量。最后通过更新订单表并将状态字段设置为 10 来确认订单。然后页面重定向到订单摘要。

如果不存在 func GET 变量，设置页面显示已完成的订单：

```php
else {
    require("header.php");
    echo "<h1>Outstanding orders</h1>";
    $orderssql = "SELECT * FROM orders WHERE status = 2";
    $ordersres = mysql_query($orderssql);
    $numrows = mysql_num_rows($ordersres);

    if($numrows == 0)
    {
        echo "<strong>No orders</strong>";
    }
    else
    {
        echo "<table cellspacing=10>";

        while($row = mysql_fetch_assoc($ordersres))
        {
            echo "<tr>";
            echo "<td><a
href="adminorderdetails.php?id=". $row['id']
.">View</a></td>";
            echo "<td>"
. date("D jS F Y g.iA", strtotime($row['date']))
. "</td>";
            echo "<td>";

            if($row['registered'] == 1)
            {
                echo "Registered Customer";
            }
            else
            {
                echo "Non-Registered Customer";
            }

            echo "</td>";

            echo "<td>&pound;" . sprintf('%.2f',
$row['total']) . "</td>";

            echo "<td>";

            if($row['payment_type'] == 1)
            {
```
