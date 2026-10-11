

## 注意：始终了解状态

在*orders*表中有一个名为*status*的字段。此字段的目的是指示用户在购物车中的哪个环节。该字段有四种可能的值：

- 0 用户仍在向购物车中添加商品。
- 1 用户已输入其地址。
- 2 用户已支付商品款项。
- 10 管理员已确认交易并发送了商品。

## *admins*表

- `id`: 将此字段设为 TINYINT（因为可能有大量用户）并开启 auto_increment。将此字段设为主键。
- `username`: 将此字段设为 VARCHAR，长度为 10。
- `password`: 将此字段设为 VARCHAR，长度为 10。

## *categories*表

- `id`: 将此字段设为 TINYINT（因为类别数量较少）并在 Extras 列中开启 auto_increment。将此字段设为主键。
- `name`: 将此字段设为 VARCHAR，并将大小设为 20。（类别标题不太可能超过 20 个字符。）

## *customers*表

- `id`: 将此字段设为 INT（因为可能有大量用户）并开启 auto_increment。将此字段设为主键。
- `forename`: 将此字段设为 VARCHAR，长度为 50。
- `surname`: 将此字段设为 VARCHAR，长度为 50。
- `add1`: 将此字段设为 VARCHAR，长度为 50。
- `add2`: 将此字段设为 VARCHAR，长度为 50。
- `add3`: 将此字段设为 VARCHAR，长度为 50。
- `postcode`: 将此字段设为 VARCHAR，长度为 10。
- `phone`: 将此字段设为 VARCHAR，长度为 20。
- `email`: 将此字段设为 VARCHAR，长度为 100。
- `registered`: 将此字段设为 TINYINT。

## *delivery_addresses*表

- `id`: 将此字段设为 INT（因为可能有大量用户）并开启 auto_increment。将此字段设为主键。
- `forename`: 将此字段设为 VARCHAR，长度为 50。
- `surname`: 将此字段设为 VARCHAR，长度为 50。
- `add1`: 将此字段设为 VARCHAR，长度为 50。
- `add2`: 将此字段设为 VARCHAR，长度为 50。
- `add3`: 将此字段设为 VARCHAR，长度为 50。
- `postcode`: 将此字段设为 VARCHAR，长度为 10。
- `phone`: 将此字段设为 VARCHAR，长度为 20。
- `email`: 将此字段设为 VARCHAR，长度为 100。

## *logins*表

- `id`: 将此字段设为 INT（因为可能有大量用户）并开启 auto_increment。将此字段设为主键。
- `customer_id`: 将此字段设为 INT。
- `username`: 将此字段设为 VARCHAR，长度为 10。
- `password`: 将此字段设为 VARCHAR，长度为 10。

## *orderitems*表

- `id`: 将此字段设为 INT（因为可能有大量商品）并开启 auto_increment。将此字段设为主键。
- `order_id`: 将此字段设为 INT。
- `product_id`: 将此字段设为 INT。
- `quantity`: 将此字段设为 INT。

## *orders*表

- `id`: 将此字段设为 INT（因为可能有大量订单）并开启 auto_increment。将此字段设为主键。
- `customer_id`: 将此字段设为 INT。
- `registered`: 将此字段设为 INT。
- `delivery_add_id`: 将此字段设为 INT。
- `payment_type`: 将此字段设为 INT。
- `date`: 将此字段设为 DATETIME。
- `status`: 将此字段设为 TINYINT。
- `session`: 将此字段设为 VARCHAR，并将大小设为 50。
- `total`: 将此字段设为 FLOAT。

## *products*表

- `id`: 将此字段设为 INT（因为可能有大量图片）并开启 auto_increment。将此字段设为主键。
- `cat_id`: 将此字段设为 TINYINT。
- `name`: 将此字段设为 VARCHAR，长度为 100。很可能会有较长的产品名称。
- `description`: 将此字段设为 TEXT。
- `image`: 将此字段设为 VARCHAR，并将大小设为 30。
- `price`: 将此字段设为 FLOAT。

## 插入示例数据

当具备一组稳固的表后，添加一些示例数据以开始工作。请记住，不要在 `id` 列中填写数字；这是由 `auto_increment` 处理的。您可以自由添加自己的示例数据，或使用建议的信息。

### *admins*表的示例数据

为管理员创建一个用户名和密码。本示例使用 `jono` 作为用户名，`bacon` 作为密码。

### *categories*表的示例数据

添加两个类别：饮料和蛋糕。

### *customers*表的示例数据

添加以下客户，如表 6-1 所示。

**表 6-1** customers 和 logins 表存储有关注册用户的信息。

| 名 | 姓 | 地址1 | 地址2 | 地址3 | 邮政编码 | 电话 | 电子邮件 | 已注册 |
|---|---|---|---|---|---|---|---|---|
| Craig | Tucker | 19, The Grove | Ziggy Road | Smalltown | T3 TR4 | 01234 567990 | craig@hissite.com | 1 |
| Lee | Jordan | 19, Oak Street | Booth Road | Thistown | T1 FG3 | 01234 098765 | lee@leetastic.com | 1 |

### *logins*表的示例数据

为每个客户添加表 6-2 中的登录详情。

**表 6-2** 确保将 *customer_id* 字段与 customers 表中的 *id* 字段匹配。

| **客户ID** | **用户名** | **密码** |
| :--- | :--- | :--- |
| 1 | Craig | Tucker |
| 2 | Lee | Jordan |

### *delivery_addresses*表的示例数据

保持此表为空。

### *products*表的示例数据

将表 6-3 中显示的产品添加到 *products* 表中。

**表 6-3** image 字段包含图片的名称（如果存在）。

| **类别ID** | **名称** | **描述** | **图片** | **价格** |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 最佳茶包 | 优质茶包。每盒 200 袋。 | <empty> | 2.99 |
| 1 | 最佳橙汁 | 一加仑优质挤压橙汁。 | bestorange-juice.jpg | 0.90 |

### *orders*表的示例数据

保持此表为空。

### *orderitems*表的示例数据

保持此表为空。

## 开始编写代码

创建购物车的挑战之一在于处理已注册和未注册用户。对于已注册的用户，没有问题，因为在向表中添加信息时，可以使用他们的 ID 来跟踪他们。挑战在于未注册的用户。如何跟踪他们？

解决方案是使用会话 ID。当用户加载使用 `session_start()` 函数的第一个页面时，会生成一个特殊的会话 ID。此 ID 对该特定用户是唯一的，并跟踪哪些会话变量分配给正在访问该网站的哪个用户。虽然您之前尚未引用会话 ID，但在这个项目中，您将大量使用会话 ID。

每当用户访问购物车并添加其第一件商品时，就会向 *orders* 表中添加一个订单。对于已注册的用户，该用户的 id 会被添加到表中的 *customer_id* 字段。对于未注册的用户，唯一的会话 id 会被添加到 *session* 字段。当此订单被添加到表中后，会创建一个名为 SESS_ORDERNUM 的会话变量，其中包含该订单的 id。现在可以使用 SESS_ORDERNUM 来跟踪订单在整个网站中的进度。

为了开始，构建通常的配置文件，该文件存储有关网站的通用信息。创建一个名为 *shoppingcart* 的新目录，并将示例 6-1 中显示的代码添加到 *config.php* 中。

**示例 6-1** 配置文件与书中的其他项目类似。

```php
<?php

$dbhost = "localhost";
$dbuser = "root";
$dbpassword = "";
$database = "shoppingcart";

$config_basedir = "http://localhost/sites/shoppingcart/";

$config_sitename = "BidTastic Auctions";
?>
```

为了简化处理重定向的过程，创建一个名为 *db.php* 的文件，其中仅包含数据库连接详细信息，如示例 6-2 所示。

**示例 6-2** 当您需要数据库连接但不想因为重定向而包含 header.php 时，将包含 db.php 文件。

```php
<?php

require("config.php");

$db = mysql_connect($dbhost, $dbuser, $dbpassword);
mysql_select_db($database, $db);
?>
```

创建 *header.php*，如示例 6-3 所示。

**示例 6-3** 头文件添加菜单选项，包含侧边栏，并添加一些登录/注销链接。

```php
<?php
session_start();
if(isset($_SESSION['SESS_CHANGEID']) == TRUE)
{
        session_unset();
        session_regenerate_id();
}
require("config.php");

$db = mysql_connect($dbhost, $dbuser, $dbpassword);
mysql_select_db($database, $db);
?>
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"
"http://www.w3.org/TR/html4/loose.dtd">
<head>
        <title><?php echo $config_sitename; ?></title>
        <link href="../stylesheet.css" rel="stylesheet">
</head>
<body>
        <div id="header">
                <h1><?php echo $config_sitename; ?></h1>
        </div>
        <div id="menu">
                <a href="<?php echo $config_basedir; ?>/">主页</a> -
                <a href="<?php echo $config_basedir;
                ?>/showcart.php">查看购物篮/结账</a>
        </div>
        <div id="container">
                <div id="bar">
                        <?php

                        require("bar.php");
                        echo "<hr>";

                        if(isset($_SESSION['SESS_LOGGEDIN']) == TRUE)
                        {
                                echo "已登录为 <strong>" . $_SESSION['SESS_USERNAME'] . "</strong> ";
                                echo "<a href=\"" . $config_basedir . "/logout.php\">注销</a>";
                        }
                        else
                        {
```

