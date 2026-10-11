

花点时间回顾一下关于 *header.php* 的几个有趣要点：

- 在文件顶部，会检查一个名为 SESS_CHANGEID 的会话变量。如果它存在，会话将被 unset（删除），并且会话 ID 会重新生成。稍后，当订单完成时，SESS_CHANGEID 会在需要重置会话系统时创建。
- 会检查 SESS_LOGGEDIN 变量是否存在。如果存在，则表明用户当前已登录，并将显示其用户名和一个注销链接。用户名存储在 SESS_USERNAME 中；该变量在 login.php 中创建，稍后会详细介绍。
- 这里使用的是本书之前项目中相同的 *stylesheet.css* 文件。

标题文件还包含一个名为 *bar.php* 的文件。该文件包含在示例 6-4 中显示的类别列表。

### 示例 6-4
虽然 *bar.php* 中的代码本可以添加到 *header.php* 中，但你可以使用此文件在需要时干净地添加其他内容。

```php
<h1>Product Categories</h1>
<ul>
<?php
$catsql = "SELECT * FROM categories";
$catres = mysql_query($catsql);
while($catrow = mysql_fetch_assoc($catres))
{
    echo "<li><a href='" . $config_basedir . "/products.php?id=" . $catrow['id'] . "'>" . $catrow['name'] . "</a></li>";
}
?>
</ul>
```

bar.php 中的代码执行 SELECT 查询以收集所有类别，并在无序列表中显示它们。每个类别都链接到稍后创建的 products.php。

创建 footer.php 并添加示例 6-5 中显示的代码。

### 示例 6-5
当管理员登录时，页脚文件会添加管理员链接。

```php
<?php
echo "<p><i>All content on this site is &copy; "
. $config_sitename . "</i></p>";

if($_SESSION['SESS_ADMINLOGGEDIN'] == 1)
{
    echo "[<a href=" . $config_basedir . "adminorders.php>admin</a>]
[<a href=" .
    $config_basedir
. "adminlogout.php'>admin logout</a>]";
}
?>
</div>
</div>
</body>
</html>
```

创建主索引文件 index.php，使用示例 6-6 中显示的代码。

### 示例 6-6
看到如此精简的 index.php 文件可能会让人惊讶。该文件实际上旨在提供关于商店的通用信息。

```php
<?php
require("header.php");
?>
<h1>Welcome!</h1>
Welcome to the <strong>
<?php echo $config_sitename; ?> </strong> website.
Click on one of the pages to explore the site.
We have a wide range of different products available.

<?php
require("footer.php");
?>
```

随着主要设计完成，你的浏览器应该会显示类似于图 6-2 的内容。

![](img/c75d0c4fa51711b62f211459ae794f3f_194_0.png)

**图 6-2** 主页面为购物车提供了简单而干净的界面。

## 管理用户登录

用户是购物车的关键组成部分，跟踪已注册用户和未注册用户非常重要。构成站点的许多不同脚本具有两种功能分支：一种是用户已登录时的处理，另一种是未登录时的处理。

登录页面与书中的其他页面类似。创建一个名为 `login.php` 的文件并添加表单：

```html
<form action="<?php echo $SCRIPT_NAME; ?>" method="POST">
<table>
  <tr>
    <td>Username</td>
    <td><input type="text" name="userBox"/>
  </tr>
  <tr>
    <td>Password</td>
    <td><input type="password" name="passBox"/>
  </tr>
  <tr>
    <td></td>
    <td><input type="submit" name="submit" value="Log in"/>
  </tr>
</table>
</form>
```

移动到文件开头并开始添加代码：

```php
<?php
session_start();
require("db.php");

if(isset($_SESSION['SESS_LOGGEDIN']) == TRUE) {
    header("Location: " . $conf_basedir);
}
```

检查用户是否已经登录。如果是，加载登录页面没有意义，因此页面将重定向到站点的基准 URL。

处理表单：

```php
if(isset($_SESSION['SESS_LOGGEDIN']) == TRUE) {
    header("Location: " . $conf_basedir);
}

if($_POST['submit'])
{
    $loginsql = "SELECT * FROM logins
WHERE username = '" . $_POST['userBox']
."' AND password = '" . $_POST['passBox']
." '";
    $loginres = mysql_query($loginsql);
    $numrows = mysql_num_rows($loginres);
    
    if($numrows == 1)
    {
        $loginrow = mysql_fetch_assoc($loginres);
        
        session_register("SESS_LOGGEDIN");
        session_register("SESS_USERNAME");
        session_register("SESS_USERID");
        
        $_SESSION['SESS_LOGGEDIN'] = 1;
        $_SESSION['SESS_USERNAME'] = $loginrow['username'];
        $_SESSION['SESS_USERID'] = $loginrow['id'];
        
        $ordersql = "SELECT id FROM orders
WHERE customer_id = " . $_SESSION['SESS_USERID']
." AND status < 2";
        $orderres = mysql_query($ordersql);
        $orderrow = mysql_fetch_assoc($orderres);
        
        session_register("SESS_ORDERNUM");
        $_SESSION['SESS_ORDERNUM'] = $orderrow['id'];
        
        header("Location: " . $config_basedir);
    }
    else
    {
        header("Location: http://" . $_SERVER['HTTP_HOST']
. $SCRIPT_NAME . "?error=1");
    }
}
else
{
    require("header.php");
?>
<h1>Customer Login</h1>
Please enter your username and password to
log into the website. If you do not
have an account, you can get one for free by <a href="register.php">registering</a>.

<?php
if($_GET['error']) {
echo "<strong>Incorrect username/password</strong>";
}
?>
<form action="<?php echo $SCRIPT_NAME; ?>" method="POST">
<table>
<tr>
<td>Username</td>
<td><input type="text" name="userBox"/></td>
</tr>
<tr>
<td>Password</td>
<td><input type="password" name="passBox"/></td>
</tr>
<tr>
<td></td>
<td><input type="submit" name="submit" value="Log in"/></td>
</tr>
</table>
</form>

<?php
}
?>
require("footer.php");
```

此代码使用前面提到的相同技术来登录用户。当登录成功时，会创建三个会话变量：

- SESS_LOGGEDIN。设置为 1 以指示用户当前已登录。
- SESS_USERNAME。包含用户的用户名。
- SESS_USERID。包含用户的 ID。

除了这些变量之外，一条 SELECT 语句会从 orders 表中拉取 customer_id 字段与当前用户 ID 匹配的 ID。然后，另一个名为 SESS_ORDERNUM 的会话变量被设置为该查询返回的 ID。此过程可能产生两种结果之一：

- 不存在订单。如果 orders 表中没有订单，则 SESS_ORDERNUM 不会被设置为任何值。
- 存在订单。如果查询返回了 ID，则 SESS_ORDERNUM 被设置为该 ID。如果用户之前选择了购物车中的商品然后注销，这将很有用。当用户再次登录时，购物车中将包含上次访问时的相同商品，用户可以继续选择商品。此功能提供了一定的连续性。

当表单成功提交并且会话变量设置完成后，页面将重定向到站点的基准 URL。页将在侧边栏显示文本“Logged in as </foo>”（以...身份登录）。

最终结果应类似于图 6-3 中显示的页面。

![](img/c75d0c4fa51711b62f211459ae794f3f_197_0.png)

**图 6-3** 完成的登录屏幕

## 注销用户

注销用户的过程与书中的一些早期项目略有不同。你不是使用 `session_destroy()` 销毁整个会话，而是注销用户的会话变量。当管理员同时作为普通用户和管理员登录时，你不能运行 `session_destroy()`，因为这会销毁管理员的登录会话。

创建 `logout.php` 并添加代码：

```php
<?php
session_start();
require("config.php");

session_unregister("SESS_LOGGEDIN");
session_unregister("SESS_USERNAME");
session_unregister("SESS_USERID");

header("Location: " . $config_basedir);
?>
```

## 显示和选择产品

购物车最核心的功能是向用户展示一系列产品，并允许她选择产品，将它们添加到隐喻的购物车中。这涉及几个不同的过程：

- 用户点击产品类别以查看可用产品。要选择产品，她点击购买链接。
- 接下来，用户选择商品数量。
- 页面显示当前购物车的内容和总价。用户还可以点击 X 符号从购物车中删除任何项目并重新计算总价。

此过程中的第一步是显示类别内可用的产品。在开始编写代码之前，你需要使用在第 5 章论坛项目中编写的 `pf_validate_number()` 函数。创建一个名为 `functions.php` 的新文件并将代码复制进去：

```php
<?php
function pf_validate_number($value, $function, $redirect) {
    if(isset($value) == TRUE) {
        if(is_numeric($value) == FALSE) {
```

