
```php
echo "<tr>";
    echo "<td>";
    
    if($_SESSION["ADMIN"]) {
        echo "[<a href='delete.php?func=thread&id=" . 
        $topicrow['topicid'] . "&forum=" . $valforum . ">X</a>] -";
    }
    
    echo "<strong><a href='viewmessages.php?id=" . 
        $topicrow['topicid'] . ">" . $topicrow['subject'] . 
        "</a></strong>";
    
    echo "</td></tr>";
```

创建一个名为 `delete.php` 的新文件，并添加以下代码：

```php
<?php
    
include("config.php");

$db = mysql_connect($dbhost, $dbuser, $dbpassword);
mysql_select_db($dbdatabase, $db);
```

按照惯例验证 `id` GET 变量：

```php
$db = mysql_connect($dbhost, $dbuser, $dbpassword);
mysql_select_db($dbdatabase, $db);

if(isset($_GET['id']) == TRUE) {
if(is_numeric($_GET['id']) == FALSE) {
    $error = 1;
} 

if($error == 1) { 
  header("Location: " . $config_basedir); 
} 
else { 
  $validid = $_GET['id']; 
} 
else { 
  header("Location: " . $config_basedir); 
} 
```

要执行删除操作，将 `func` GET 变量通过 `switch` 语句进行运行，以确定其值，然后发出相关的删除指令：

```php
else { 
  header("Location: " . $config_basedir); 
}

switch($_GET['func']) { 
  case "cat": 
    $delsql = "DELETE FROM categories WHERE id = " . $validid . ";"; 
    mysql_query($delsql); 
    header("Location: " . $config_basedir); 
    break; 

  case "forum": 
    $delsql = "DELETE FROM forums WHERE id = " . $validid . ";"; 
    mysql_query($delsql); 
    header("Location: " . $config_basedir); 
    break; 

  case "thread": 
    $delsql = "DELETE FROM topics WHERE id = " . $validid . ";"; 
    mysql_query($delsql); 
    header("Location: " . $config_basedir 
      . "/viewforum.php?id=" 
      . $_GET['forum']); 
    break; 

  default: 
    header("Location: " . $config_basedir); 
    break; 
} 
?>
```

删除 SQL 语法相当简单：`DELETE FROM <table> WHERE id = <the id of the thing you want to delete>`。删除完成后，页面会重定向到页面层级中的上一级。例如，当你删除一个主题时，论坛主题页面会被删除。参见图 5-12。

| 主题 | 回复数 | 作者 | 发帖日期 |
| :--- | :--- | :--- | :--- |
| [5] 经典喜剧 | 1 | johnsent | 2006年8月10日 星期四 12:47PM |
| [5] 优秀的喜剧演员/趣事 | 1 | johnsent | 2006年8月10日 星期四 12:47PM |

**图 5-12**

删除内容很简单。

**提示**

*在 `delete.php` 中，删除帖子时，使用 `$_GET['forum']` 在帖子删除后重定向到论坛页面。不必过分担心验证此变量；它不引用进入数据库的数据，仅用于显示页面。但如果你仍然担心，为了双重防范 SQL 注入攻击，请验证该变量。*

## 总结

随着另一个项目的完成，在构建论坛的过程中，许多基本主题都得到了实践和精炼。你参与的每个项目都会带来一系列具体的挑战，从而进一步深化你对 PHP 和 MySQL 的知识和经验，本书中的项目旨在探索这些技能。

除了学习新主题外，现有技能的重复使用也有助于加深你对这些技能的理解。举个例子，每次执行 SQL 查询时，你都在巩固你对 PHP 这一部分知识的掌握。不知不觉中，你不再需要查阅书籍或现有代码来连接 MySQL——你将能够自动完成这一操作。

不多说了，是时候开始下一个项目了。

# 第 6 章

## 创建购物车

对于许多开发者来说，朴素的购物车在他们心中占据着特殊的地位。尽管 PHP 和 MySQL 是构建各种 Web 应用程序的基础，但许多开发者都是怀揣着编写无处不在的购物车的梦想入行的。如果 Web 开发有禅意，那很可能是在编写购物车时体验到的。

虽然购物车在网络上很常见，但它们的种类繁多。各种变体通常根据使用该软件的特定业务类型而有所不同。例如，书籍、CD 和 DVD 的销售与电缆、食品、建筑材料和清洁用品的销售不同。核心区别在于数量：你通常一次只买一本书或一张 DVD，但餐馆一次购买 10 包晚餐面包并不罕见。

### 项目概览

在本项目中，你将创建购物车的核心功能。为了清楚了解该项目的运作方式，请查看以下用例：

John 需要为他的移动咖啡馆购买一些茶包。他进入了一家由本书作者经营的热门在线商店。John 在该网站上没有用户账户，但开始购物。他点击“饮料”类别，看到了茶包列表。他点击“购买”链接，被带到另一个页面，在那里他可以选择数量。他选择了 10 盒茶包并将其添加到购物车。页面刷新后，他看到了购物车的内容。John 随后购买了咖啡，他的购物车再次更新。John 意识到他其实不需要咖啡，因此他点击“X”链接将咖啡从购物车中删除。John 选择完商品后点击“去结账”链接。系统提示他输入地址，他填写后被带到付款屏幕。John 可以选择使用 PayPal 或支票付款。John 点击 PayPal 按钮，被带到 paypal.com 的 PayPal 付款屏幕，在那里他完成了订单付款。

Pauline 也需要一些茶包。Pauline 在该站点已经有一个账户，所以她登录了。她将所需的商品添加到购物车，并点击“去结账”链接。在地址页面，她可以选择新地址或用户账户中存储的地址。她选择了账户地址，随后被带到付款屏幕。Pauline 选择用支票付款，并获得了关于支票寄送地点和收款人的说明。

Ken 管理着该网站，他想查看所有当前订单。他使用管理员用户名和密码登录，系统向他提供了一份订单列表。Ken 查看每项商品，打包订单，并在包裹上写上地址。为了确认订单完成，Ken 点击“确认付款”链接。订单现在已完工。

本章构建的购物车满足了前述用例中讨论的所有功能，但仍有巨大的开发空间。购物车可以成为庞大且复杂的系统，甚至一整本书都无法完全涵盖构建购物车的主题。本项目将提供一个坚实的基础，你可以在此基础上继续构建更多功能。

## 构建数据库

你要创建的数据库如图 6-1 所示。

![](img/c75d0c4fa51711b62f211459ae794f3f_185_0.png)

**图 6-1** 数据库模式围绕主要的 *orders* 表。

整个项目从根本上依赖于存储在 *orders* 表中的订单。该表关联到 *customers*（包含注册客户的地址详情）和 *delivery_addresses*（包含未注册和备用地址）表。订单中的每个产品（存储在 *products* 表中）都存储在 *order_items* 表中。其他表包括 *logins*（存储注册用户的登录详情）、*categories*（包含产品所属的类别）和 *admins*（存储管理员登录详情）。

### 实现数据库

启动 `phpMyAdmin`，创建一个名为 *shoppingcart* 的新数据库，并添加以下表：

#### 注意：始终了解状态

在 *orders* 表中有一个名为 *status* 的字段。此字段的目的是指示用户在购物车中的哪个环节。该字段有四种可能的值：

- 0 用户仍在向购物车中添加商品。
- 1 用户已输入其地址。
- 2 用户已支付商品款项。
- 10 管理员已确认交易并发送了商品。
