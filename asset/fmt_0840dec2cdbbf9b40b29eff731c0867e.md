
`delivery_addresses` 表包含未注册用户以及选择不同地址的注册用户地址列表。当信息添加到表中时，`strip_tags()` 函数会移除可能添加的任何 HTML 标签，而 `addslashes()` 函数会转义任何引号。最后，使用 `delivery_addresses` 中记录的 id 更新 `orders` 表，并将状态更改为 1。完成后，页面重定向到 `checkout-pay.php`。

如果用户已登录但选择使用已存档的地址，`orders` 表也会更新：

```php
header("Location: " . $config_basedir . "checkout-pay.php");
}
else
{
    $cursql = "UPDATE orders SET delivery_add_id = 0, status = 1 WHERE id = " . $_SESSION['SESS_ORDERNUM'];
    mysql_query($cursql);
    header("Location: " . $config_basedir . "checkout-pay.php");
}
```

如果没有用户登录，则验证表单并将地址添加到数据库：

```php
header("Location: " . $config_basedir . "checkout-pay.php");
}
else
{
    if(empty($_POST['forenameBox']) ||
       empty($_POST['surnameBox']) ||
       empty($_POST['add1Box']) ||
       empty($_POST['add2Box']) ||
       empty($_POST['add3Box']) ||
       empty($_POST['postcodeBox']) ||
       empty($_POST['phoneBox']) ||
       empty($_POST['emailBox']))
    {
        header("Location: " . "checkout-address.php?error=1");
        exit;
    }

    $addsql = "INSERT INTO delivery_addresses(forename, surname, add1, add2, add3, postcode, phone, email) VALUES("
    . $_POST['forenameBox'] . ","
    . $_POST['surnameBox'] . ","
    . $_POST['add1Box'] . ","
    . $_POST['add2Box'] . ","
    . $_POST['add3Box'] . ","
    . $_POST['postcodeBox'] . ","
    . $_POST['phoneBox'] . ","
    . $_POST['emailBox'] . ")";
    mysql_query($addsql);

    $setaddsql = "UPDATE orders SET delivery_add_id = " . mysql_insert_id() . ", status = 1 WHERE session = " . session_id();
    mysql_query($setaddsql);

    header("Location: " . $config_basedir . "checkout-pay.php");
}
```

在这段代码中，地址被添加到 `delivery_addresses` 表，并使用 `delivery_addresses` 的 id 更新 `orders` 表，状态设置为 1。开始表单代码块：

```php
header("Location: " . $config_basedir . "checkout-pay.php");
}
}
else
{
    require("header.php");
    echo "<h1>Add a delivery address</h1>";
```

最后，在表单之后添加代码：

```php
</table>
</form>
<?php
}
    require("footer.php");
?>
```

地址代码完成后，您的浏览器应显示类似于图 6-7 的页面——当用户已登录时。

![](img/c75d0c4fa51711b62f211459ae794f3f_216_0.png)

**图 6-7** 当用户已登录时，单选按钮提示用户选择使用哪个地址。

## 支付

结账流程的最后部分是收取付款。网站上的支付处理可以走多种不同的路线：PayPal、NOCHEX、Worldpay 等。本项目提供两种支付方式：PayPal 和支票。这两种方法演示了如何处理自动（PayPal）和手动（支票）购买。

创建一个名为 `checkout-pay.php` 的新文件并添加表单：

```html
<h2>Select a payment method</h2>
<form action='checkout-pay.php' method='POST'>
    <table cellspacing=10>
        <tr>
            <td><h3>PayPal</h3></td>
            <td>
                This site uses PayPal to accept Switch/Visa/Mastercard cards. No PayPal account is required - you simply fill in your credit card details and the correct payment will be taken from your account.
            </td>
            <td><input type="submit" name='paypalsubmit' value='Pay with PayPal'></td>
        </tr>
        <tr>
            <td><h3>Cheque</h3></td>
            <td>
                If you would like to pay by cheque, you can post the cheque for the final amount to the office.
            </td>
            <td><input type='submit' name='chequesubmit' value='Pay by cheque'></td>
        </tr>
    </table>
</form>
```

这个简单的表单仅提供两个提交按钮——一个用于通过 PayPal 支付，另一个用于通过支票支付。处理表单包括两个主要部分——一个用于 PayPal，一个用于支票。

在文件顶部，开始添加代码：

```php
<?php
session_start();
require('db.php');
require('functions.php');
```

如果用户点击 PayPal 按钮，处理订单：

```php
if($_POST['paypalsubmit'])
{
    $supsql = "UPDATE orders SET status = 2, payment_type = 1 WHERE id = " . $_SESSION['SESS_ORDERNUM'];
    $upres = mysql_query($supsql);

    $itemsmsql = "SELECT total FROM orders WHERE id = " . $_SESSION['SESS_ORDERNUM'];
    $itemsres = mysql_query($itemsmsql);
    $row = mysql_fetch_assoc($itemsres);
}
```

`orders` 表被更新以反映订单的完成。`status` 字段更改为 2，`payment_type` 字段设置为 1（PayPal）。然后通过查询从订单中获取总价，以便稍后构建 PayPal 链接。

重置订单会话：

```php
if($_SESSION['SESS_LOGGEDIN'])
{
    unset($_SESSION['SESS_ORDERNUM']);
}
else
{
    session_register("SESS_CHANGEID");
    $_SESSION['SESS_CHANGEID'] = 1;
}
```
