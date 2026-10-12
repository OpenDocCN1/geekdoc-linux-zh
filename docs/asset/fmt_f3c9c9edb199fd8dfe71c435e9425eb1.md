
```php
while($itemrow = mysql_fetch_assoc($itemsres))
{
    $quantitytotal = $itemrow['price'] * $itemrow['quantity'];
    echo "<tr>";

    if(empty($itemrow['image'])) {
        echo "<td><img src='./productimages/dummy.jpg' width='50' alt='" . $itemrow['name'] . "'></td>";
    } else {
        echo "<td><img src='./productimages/" . $itemrow['image'] . "' width='50' alt='" . $itemrow['name'] . "'></td>";
    }

    echo "<td>" . $itemrow['name'] . "</td>";
    echo "<td>" . $itemrow['quantity'] . "</td>";
    echo "<td><strong>&pound;" . sprintf('%.2f', $itemrow['price']) . "</strong></td>";
    echo "<td><strong>&pound;" . sprintf('%.2f', $quantitytotal) . "</strong></td>";
    echo "<td><a href='" . $config_basedir . "delete.php?id=" . $itemrow['itemid'] . ">X</a></td>";
    echo "</tr>";

    $total = $total + $quantitytotal;
    $totalsql = 'UPDATE orders SET total = ' . $total . ' WHERE id = ' . $_SESSION['SESS_ORDERNUM'] . ';';
    $totalres = mysql_query($totalsql);
}

echo "<tr>";
echo "<td></td>";
echo "<td></td>";
echo "<td></td>";
echo "<td><strong>TOTAL</strong></td>";
echo "<td><strong>&pound;" . sprintf('%.2f', $total) . "</strong></td>";
echo "</tr>";

echo "</table>";
echo "<p><a href='checkout-address.php'>Go to the checkout</a></p>";
}
```

## 删除商品

`showcart()`函数包含一个指向`delete.php`的链接，您可以通过该链接从购物车中移除商品。点击该链接后，商品将从`orderitems`表中删除，并且`orders`表中的总价将被更新。

创建`delete.php`并开始添加代码：

```php
<?php

require("config.php");
require("db.php");
require("functions.php");

$validid = pf_validate_number($_GET['id'], "redirect", $config_basedir . "showcart.php");

$itemsql = "SELECT * FROM orderitems WHERE id = " . $_GET['id'] . ";";
$itemres = mysql_query($itemsql);
$numrows = mysql_num_rows($itemres);

if($numrows == 0) {
    header("Location: " . $config_basedir . "showcart.php");
    exit();
}

$itemrow = mysql_fetch_assoc($itemres);
```

在这段代码中，查询从`orderitems`表中拉取商品，并检查返回的行数。此检查可以防止某人修改 URL 并在没有`id`为 73 的商品时添加`delete.php?id=73`。如果没有返回行，头部重定向将跳转到`showcart.php`。如果返回了行，脚本将继续执行：

```php
$itemrow = mysql_fetch_assoc($itemres);

$prodsql = "SELECT price FROM products WHERE id = " . $itemrow['product_id'] . ";";
$prodres = mysql_query($prodsql);
$prodrow = mysql_fetch_assoc($prodres);

$sql = "DELETE FROM orderitems WHERE id = " . $_GET['id'] . ";";
mysql_query($sql);
```

在此代码块中，首先选择商品价格，然后使用单独的查询从`orderitems`中删除该商品。

使用新的总价更新`orders`表：

```php
$totalPrice = $prodrow["price"] * $itemrow["quantity"];
$sql = "UPDATE orders SET total = total - " . $totalPrice . " WHERE id = " . $_SESSION["SESS_ORDERNUM"] . ";";
mysql_query($sql);

header("Location: " . $config_basedir . "/showcart.php");

exit();
?>
```

随着购物车摘要函数和页面的完成，您的浏览器应显示类似于图 6-6 所示的页面。

![](img/c75d0c4fa51711b62f211459ae794f3f_210_0.png)

**图 6-6** 购物车摘要显示当前商品列表以及移除它们的功能。

## 结账

用户完成向购物车添加商品后，就可以开始结账流程。此过程涉及两个步骤：

- 提示用户提供送货地址。如果用户已登录，应询问他们是使用注册地址还是使用其他地址。应验证所有地址。
- 提示用户选择支付方式，PayPal 或支票。

创建`checkout-address.php`并添加表单：
