

$currentcat = $_GET['parentcat'];

$_SESSION['SESS_PARENT'] = $_GET['parentcat'];
$_SESSION['SESS_CHILD'] = 0;
}
else {
$currentcat = 0;
}

系统会检查这两个变量是否都存在。如果存在，将检查这些变量是否为数值类型，如果是，则会话变量被赋值为每个 GET 变量的值。如果仅有 parentcat 这个 GET 变量可用，则应用相同的流程。

$currentcat 变量决定了当前类别。有三种可能的选项：

- 如果仅存在 parentcat 变量，$currentcat 被设置为 parentcat 的值。
- 如果存在 childcat 变量，$currentcat 被设置为 childcat 的值。
- 如果没有任何变量存在，$currentcat 被设置为 0。

检查 $currentcat 是否设置为 0。如果是，创建一条查询以返回最新的五篇文章：

```php
$currentcat = 0;
}

require("header.php");

if($currentcat == 0) {
$sql = "SELECT * FROM stories ORDER BY dateposted DESC LIMIT 5;";
}
```

如果 $currentcat 被设置为某个类别，则运行一条查询以确定 parent 字段被设置为什么：

```php
$sql = "SELECT * FROM stories ORDER BY dateposted DESC LIMIT 5;";
}
else {
$parentsq1 = "SELECT parent FROM categories WHERE id = " . $currentcat . ";";
$parentres = mysql_query($parentsq1);
$parentrow = mysql_fetch_assoc($parentres);
```

现在检查 parent 是否设置为 1。如果是，说明用户点击了一个可以包含多个子类别的类别。当这种情况发生时，显示父类别中的所有文章以及所有子类别的文章。如果所选类别不是父类别，则返回该特定类别的文章。为此添加相应的 SQL 语句：

```php
$parentres = mysql_query($parentsql);
$parentrow = mysql_fetch_assoc($parentres);

if($parentrow['parent'] == 1) {
    $sql = sprintf("SELECT stories.* FROM stories INNER JOIN cat_relate ON stories.cat_id = cat_relate.child_id WHERE cat_relate.parent_id = %d UNION SELECT stories.* FROM stories WHERE stories.cat_id = %d;", $currentcat, $currentcat);
} else {
    $sql = "SELECT * FROM stories WHERE cat_id = " . $currentcat . ";";
}
```

如果该类别是父类别，则构建一条大型查询以返回所有文章。这条查询实际上是由两条巧妙结合的查询组成的。第一部分（`SELECT stories.* FROM stories INNER JOIN cat_relate ON stories.cat_id = cat_relate.child_id WHERE cat_relate.parent_id = <id>`）使用连接来获取所有 parent_id 设置为 $currentcat 的文章。第二部分（`SELECT stories.* FROM stories WHERE stories.cat_id = <id>`）选择属于父类别的文章。

这两部分通过使用 UNION 关键字在同一条查询中拼接在一起，该关键字将使用相同类型列的两条查询连接起来。在需要针对相同表执行两条 SELECT 查询的情况下（如此处），这非常有用。

这条大型查询在 `sprintf()` 函数内部构建。当你想用另一个字符串或变量替换字符串的一部分时，会使用此函数。在此情况下，你希望在查询的相应位置添加 $currentcat。为此，字符串中的 `%d`（称为*类型说明符*）被 `sprintf()` 末尾指定的变量替换——在此情况下是 $currentcat。不同类型的变量使用不同的类型说明符，你可以访问 www.php.net/sprintf 来满足对类型说明符的好奇心。

在 else 分支中，如果所选类别不是父类别，则构建一条查询，它简单地返回该特定类别的文章。

运行相关的查询：

```php
$sql = "SELECT * FROM stories WHERE cat_id = " . $currentcat . ";";
}
}

$result = mysql_query($sql);
$numrows = mysql_num_rows($result);
```

手头有了丰富的结果集，将其显示给用户：

```php
$result = mysql_query($sql);
$numrows = mysql_num_rows($result);

if($numrows == 0) {
  echo "<h1>No Stories</h1>";
  echo "<p>There are currently no stories in this category. </p>";
}
else {
  while($row = mysql_fetch_assoc($result)) {
    if($_SESSION['SESS_USERLEVEL'] == 10) {
      echo "<a href='deletestory.php?id=" . $row['id'] . "'><X></a> ";
    }

    echo "<strong><a href='viewstory.php?id=" . $row['id'] . "'>" . $row['subject'] . "</a></strong><br />";
    echo date("D jS F Y g.iA", strtotime($row['dateposted']));
    echo "<p>" . $row['body'] . "</p>";
  }
}
```

最后，添加结束代码：

```php
  echo "<p>" . $row['body'] . "</p>";
}
}

require("footer.php");
?>
```

你的努力结果应与图 11-2 中所示的页面类似。

![](img/c75d0c4fa51711b62f211459ae794f3f_454_0.png)

**图 11-2** 该界面简单高效，但将在本章后续部分进行扩充。

## 处理用户登录

与本书中的许多其他项目一样，用户登录功能是一个基本特性。本项目中用户登录的代码和功能与书中其他项目的代码几乎完全相同。其中大部分内容你应该已经很熟悉了，如果还不是，请回头练习一下之前的项目。

此登录方式的核心区别在于，添加用户时使用了加密密码。创建用户时，使用 md5() MySQL 命令对密码进行哈希处理。为了验证在登录表单中输入用户名和密码的用户，首先对表单中输入的密码进行哈希处理，然后比较这两个哈希后的密码。如果匹配，则密码有效。

*创建 userlogin.php* 并添加表单：

```php
<form action="<?php echo $SCRIPT_NAME ?>" method="post">
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
<td><input type="submit" name="submit" value="Login!" ></td>
</tr>
</table>
</form>
```

该表单提示用户输入用户名和密码。当用户点击提交按钮时，页面重定向到自身以处理数据。

跳转到文件顶部，在处理表单之前添加一些 include 语句和对已存在登录的检查：

```php
<?php

session_start();

require("config.php");
require("db.php");
require("functions.php");

if($_SESSION['SESS_USERNAME']) {
    header("Location: " . $config_basedir . "userhome.php");
}
```

如果 SESS_USERNAME 会话变量可用，则页面重定向到另一个可以包含选项的脚本（虽然在本项目中未创建 userhome.php，但它可用作用户的控制面板）。

开始处理表单：

```php
header("Location: " . $config_basedir . "userhome.php");
}

if($_POST['submit']) {
    $sql = "SELECT * FROM users WHERE username = '" . pf_fix_slashes($_POST['username']) . "' AND password = '" . md5(pf_fix_slashes($_POST['password'])) . "'";
    $result = mysql_query($sql);
    $numrows = mysql_num_rows($result);
```

该查询将输入的用户名和密码与 users 表中的记录进行比较。在构建查询时，使用 md5() PHP 命令首先对密码进行哈希处理，以便比较哈希后的密码（表中现有的密码和刚输入表单的密码）。

检查是否返回了任何结果：

```php
$result = mysql_query($sql);
$numrows = mysql_num_rows($result);

if($numrows == 1) {
    $row = mysql_fetch_assoc($result);

    session_register("SESS_USERNAME");
    session_register("SESS_USERID");
    session_register("SESS_USERLEVEL");

    $_SESSION['SESS_USERNAME'] = $row['username'];
    $_SESSION['SESS_USERID'] = $row['id'];
    $_SESSION['SESS_USERLEVEL'] = $row['level'];

    header("Location: " . $config_basedir);
}
else {
    header("Location: " . $config_basedir . "/userlogin.php?error=1");
}
```

如果返回了一行数据，则注册并设置会话变量。否则，页面将重新加载并附带一个错误 GET 变量。

在显示表单之前显示错误信息：

```php
header("Location: " . $config_basedir . "/userlogin.php?error=1");
}
else {
    require("header.php");

    echo "<h1>Login</h1>";

    if($_GET['error']) {
        echo "<p>Incorrect login, please try again!</p>";
    }

?>
<form action="<?php echo $SCRIPT_NAME ?>" method="post">
<table>
<tr>
```

最后，在表单之后关闭脚本：

