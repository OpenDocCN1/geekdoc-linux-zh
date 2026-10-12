
```php
. "");
mysql_query($sql);

header("Location: " . $config_basedir .
    "itemdetails.php?id=" . $validid);

} else {
```

最后，在文件底部，添加一个大括号来关闭 `else` 块：

```php
echo "</ul>";
}
}

require("footer.php");
```

完成的页面应该类似于图 7-3。

![](img/c75d0c4fa51711b62f211459ae794f3f_254_0.png)

**图 7-3** 当用户登录时，显示出价框和出价历史。

## 处理用户

与本书中的许多其他项目一样，你需要添加功能，以便用户可以登录以访问网站的不同部分。用户登录的过程几乎与论坛项目中的 `login.php` 脚本相同。唯一的区别在于处理 **`ref`** **`GET`** 变量的引荐类型。参见示例 7-5。

### 示例 7-5 用户登录页面

```php
<?php
    session_start();
    require("config.php");
    require("functions.php");
    $db = mysql_connect($dbhost, $dbuser, $dbpassword);
    mysql_select_db($dmdatabase, $db);
    if($_POST['submit']) {

$sql = "SELECT * FROM users WHERE username = '"
. $_POST['username']."' AND password = '"
. $_POST['password']."';

$result = mysql_query($sql);
$numrows = mysql_num_rows($result);

if($numrows == 1) {
    $row = mysql_fetch_assoc($result);

    if($row['active'] == 1) {
        session_register("USERNAME");
        session_register("USERID");

        $_SESSION['USERNAME'] = $row['username'];
        $_SESSION['USERID'] = $row['id'];

        switch($_GET['ref']) {
            case "addbid":
                header("Location: " . $config_basedir . "/itemdetails.php?id=" . $_GET['id'] . "#bidbox");
                break;

            case "newitem":
                header("Location: " . $config_basedir . "/newitem.php");
                break;

            case "images":
                header("Location: " . $config_basedir . "/addImages.php?id=" . $_GET['id']);
                break;

            default:
                header("Location: " . $config_basedir);
                break;
        }
    }
    else {
        require("header.php");
        echo "This account is not verified yet. You were emailed a link to verify the account. Please click on the link in the email to continue.";
    }
}
else {
    header("Location: " . $config_basedir . "/login.php?error=1");
}
else {
    require("header.php");

    echo "<h1>Login</h1>";
```

### 示例 7-5 续

```php
if($_GET['error']) {
    echo "Incorrect login, please try again!";
}
?>
<form action="<?php echo pf_script_with_get($SCRIPT_NAME); ?>" method="post">
<table>
<tr>
    <td>Username</td>
    <td><input type="text" name="username"></td>
</tr>
<tr>
    <td>Password</td>
    <td><input type="password" name="password"></td>
</tr>
<tr>
    <td></td>
    <td><input type="submit" name="submit" value="Login!"</td>
</tr>
</table>
</form>
Don't have an account? Go and <a href="register.php">Register</a>!
<?php
}
require("footer.php");
?>
```

完成的登录页面应该与图 7-4 中显示的类似。

## 登出

登出页面 `logout.php` 也是相同的。参见示例 7-6。

### 示例 7-6 用户登出

```php
<?php

session_start();
session_unregister("USERNAME");
require("config.php");

header("Location: " . $config_basedir);

?>
```

![](img/c75d0c4fa51711b62f211459ae794f3f_257_0.png)

**图 7-4** 登录界面看起来与其他大多数类似。

## 用户注册

用户注册代码与论坛项目中的也相同。将 `register.php` 和 `validate.php` 文件复制到当前项目，并更改相关部分。

## 添加物品

向拍卖网站添加物品是一个相当简单的两步过程。第一步是向用户展示一个表单，将物品信息添加到数据库中（见图 7-5）。完成后，第二步是允许用户上传可以随物品一起显示的图片。

该表单提示用户输入以下信息：

- 物品所属的类别。这将以下拉组合框的形式呈现，并列出类别。
- 物品名称。
- 物品描述。
- 拍卖结束日期。这将呈现为用于日期不同部分的组合框数字。这将包括日、月、年，以及时分和分钟。
- 起拍价。

![](img/c75d0c4fa51711b62f211459ae794f3f_258_0.png)

**图 7-5** 添加物品的第一步是填写物品详细信息。

创建一个名为 `newitem.php` 的新文件并添加表单：

```html
<h1>Add a new item</h1>
<strong>Step 1</strong> - Add your item details.
<p>
<?php
switch($_GET['error']) {
    case "date":
        echo "<strong>Invalid date - please choose another!</strong>";
        break;
}
?>
</p>
<form action="<?php echo pf_script_with_get($SCRIPT_NAME); ?>" method="post">
<table>
<?php
$catsql = "SELECT * FROM categories ORDER BY category;";
$cateresult = mysql_query($catsql);
?>
<tr>
    <td>Category</td>
    <td>
        <select name="cat">
```

## 添加日期/时间输入

至此，该表单的大部分内容应该看起来都很直接了。唯一的新特性是日期结束框。在这些下拉框内部，一系列 `for` 循环从最小值遍历到最大值（例如，对于“日”来说，是从 1 到 31）。

开始添加处理表单的代码。在表单之前添加以下代码：

```php
<?php

session_start();

require("config.php");
require("functions.php");
```
