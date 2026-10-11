

检查用户是否已登录。如果是，则显示表单：

```php
echo "</table>";

if($ _SESSION['SESS_USERNAME']) {
echo "<h2>Add a comment</h2>";
echo "<form action='answer.php?id=' . $ _GET['id']
.” method='POST'>";
echo "<table width='100%'>";
echo "<tr>";
echo "<td>Title</td>";
echo "<td><input type='text' name='titleBox'></td>";
echo "</tr>";
echo "<tr>";
echo "<td>Comment</td>";
echo "<td><textarea rows=10 cols=50
name='commentBox'></textarea></td>";
echo "</tr>";
echo "<tr>";
echo "<td></td>";
echo "<td><input type='submit'
name='submit' value='Post Comment'></td>";
echo "</tr>";
echo "</table>";
echo "</form>";
}
```

如果用户未登录，则显示一条消息：

```php
echo "</form>";
} else {
echo "<p>&bull; You cannot post as you are
<strong>Anonymous</strong>. Please <a href='login.php'>login</a>
</p>";
}
```

最后，添加结束代码：

```php
echo "<p>&bull; You cannot post as you are
<strong>Anonymous</strong>. Please <a href='login.php'>login</a>
</p>";
}
}
}

require("footer.php");
?>
```

随着四个主要部分的添加，页面现在已完整。如果您有时间，请再浏览一遍本节，以熟悉这些不同部分是如何组合在一起的。

![](img/c75d0c4fa51711b62f211459ae794f3f_343_0.png)

## 注意
顺便提一下...

> 在本项目中，许多页面的章节并非按线性（从上到下）的方式布局。要完全理解这些不同部分是如何组合在一起的，请重读前面的章节并参考屏幕上的代码。

## 更新侧边栏

那些在本节开头查看过图 9-6 的细心读者可能已经注意到，侧边栏会显示同一主题下的其他问题。添加此功能是为了方便在同一主题内的不同问题之间进行导航。某主题的读者很可能希望阅读该主题中大部分甚至所有的问题。

加载 `bar.php` 并将光标移至文件开头以添加代码：

```php
<?php

if(basename($SCRIPT_NAME) == "answer.php") {
  echo "<h1>Other questions</h1>";
  $subsql = "SELECT topic_id FROM questions WHERE id = " . $_GET['id'] . ";";
  $subresult = mysql_query($subsql);
  $subrow = mysql_fetch_assoc($subresult);

  $othersql = "SELECT id, question FROM questions WHERE topic_id = " . $subrow['topic_id'] . " AND active = 1;";
  $otherresult = mysql_query($othersql);
```

第一个查询返回当前问题所属的主题，第二个查询返回该主题内的问题。

显示问题：

```php
$otherresult = mysql_query($othersql);

echo "<table width='100%'>";

while($otherrow = mysql_fetch_assoc($otherresult)) {
  echo "<tr>";
    echo "<td width='5%'>";

    if($otherrow['id'] == $_GET['id']) {
        echo "&bull;";
    }

    echo "<td><a href='answer.php?id=" . $otherrow['id'] . "'>"
        . $otherrow['question'] . "</a></td>";
    echo "</tr>";
}

    echo "</table>";
} else {
    $subsql = "SELECT * FROM subjects";
    $subres = mysql_query($subsql);
}
```

## 处理登录

在任何 CMS 中，用户都需要得到妥善管理。不同的系统有不同的用户要求，从简单的用户登录到多用户分层权限系统不等。拥有一份关于用户如何管理、谁可以访问什么以及存在何种限制的设计完善的计划至关重要。

本项目中的用户管理系统相当简单。该系统有两种类型的用户：*普通用户* 和 *管理员*。普通用户和管理员的主要区别在于它们所具备的功能（管理员显然可以管理系统的更多部分）。

### 普通用户登录

系统中绝大多数用户都是普通用户。普通用户可以执行以下操作：

- 浏览主题、专题和问题
- 为特定问题留下评论
- 提交问题以纳入某个专题

当用户提交问题以纳入某个专题时，主题的所有者或管理员可以审核该问题。任何用户都可以拥有一个主题；她可以申请拥有一个无人认领的主题，管理员将接受或拒绝该请求。这种申请主题所有权的机制将在后续章节中开发。

**注意**
**隐藏管理员登录界面**

那些关注细微细节的读者可能已经注意到，本章中的图表没有指向管理员登录页面的链接。这是一个刻意的且强制执行的决定，旨在提高网站的安全性。

如果您为管理员提供登录网站的机会，请不要提供指向登录页面的链接。如果存在链接，互联网上的恶意用户可能会蜂拥而至并试图伪造登录。通过隐藏链接，上述恶意用户在试图破解之前必须先找到登录页面。这可能会让很多人感到沮丧而放弃。

这种技术绝对不应是您唯一的安全解决方案，但每一点小细节都有帮助。

永远记住，安全是由许多小步骤组成的，而不仅仅是一个大步骤。许多不同的措施，无论大小，都有助于提高您网站的安全性。

首先，创建登录页面。创建一个名为 `login.php` 的新文件，并添加示例 9-4 中所示的代码。

**示例 9-4** 这段代码与之前的登录页面几乎相同。

```php
<?php

session_start();

require("config.php");

if($_SESSION['SESS_USERNAME']) {
    header("Location: " . $config_basedir . "userhome.php");
}

$db = mysql_connect($dbhost, $dbuser, $dbpassword);
mysql_select_db($dbdatabase, $db);

if($_POST['submit']) {
    $sql = "SELECT * FROM users WHERE username = '" .
            $_POST['username'] . "' AND password = '" .
            $_POST['password'] . "';";

    $result = mysql_query($sql);
    $numrows = mysql_num_rows($result);

    if($numrows == 1) {
```

**示例 9-4  续。**

```php
$row = mysql_fetch_assoc($result);
session_register("SESS_USERNAME");
session_register("SESS_USERID");
$SESS_USERNAME = $_POST['username'];
$SESS_USERID = $row['id'];
    header("Location: " . $config_basedir . "userhome.php");
} else {
    header("Location: " . $config_basedir . "/login.php?error=1");
}
}
else {
    require("header.php");
    if($_GET['error']) {
        echo "Incorrect login, please try again!";
    }
?>

<h1>Login</h1>

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
<td><input type="submit" name="submit" value="Login!"></td>
</tr>
</table>
</form>

<?php
}

require("footer.php");
?>
```

当用户成功登录后，会创建两个会话变量：`SESS_USERNAME` 和 `SESS_USERID`。这些变量在整个代码中用于检查用户是否已登录，并引用用户的用户名和 ID。不过，在您实际登录之前，您需要创建用户的控制面板。

## 显示控制面板

当用户成功登录系统后，页面会重定向到一个控制面板，该面板显示与该特定用户相关的若干选项。该页面看起来如图 9-7 所示。

![](img/c75d0c4fa51711b62f211459ae794f3f_347_0.png)

**图 9-7** 控制面板为显示特定用户的相关选项提供了地方。

该页面提供了与所拥有主题相关的许多不同功能的链接。这些功能包括添加问题、移除所有权以及审核提交的问题的能力。此功能分布在若干页面上，这些页面将在后面讨论。

创建一个名为 *userhome.php* 的新文件，并添加以下代码：

```php
<?php

session_start();
require("config.php");

if(!$ _SESSION['SESS_USERNAME']) {
header("Location: " . $config_basedir . "login.php");
}

require("header.php");
```

您首先保护该页面，防止未登录的用户访问。如果不存在 `SESS_USERNAME` 变量，页面将重定向。

指定哪个用户已登录：

```php
require("header.php");
echo "<h1>Control Panel</h1>";
echo "Welcome <strong>" . $_SESSION['SESS_USERNAME']
. "</strong> [<a href='userlogout.php'>logout</a>]";
```

添加一条消息，例如“欢迎 Bob”，让用户知道他已成功登录，可以提高用户对网站的信心。

![](img/c75d0c4fa51711b62f211459ae794f3f_348_0.png)

**注意**
**用可用性来表达**
良好可用性中最关键的概念之一是反馈。

每当用户在系统中完成一项任务（例如登录）时，务必始终提供反馈，让用户确信她已成功完成该任务。在联网环境中（例如 Web），这一点尤为重要，因为您的计算机和 Web 服务器之间存在若干可能的障碍。

执行查询以收集用户拥有的主题：

```php
echo "Welcome <strong>" . $ _SESSION['SESS_USERNAME']
. "</strong> [<a href='userlogout.php'>logout</a>]";

echo "<h2>Subjects Owned</h2>";

$sql = "SELECT * FROM subjects WHERE owner_id ="
. $ _SESSION['SESS_USERID'] . "";
$result = mysql_query($sql);
```

在此查询中，您使用了 `SESS_USERID` 会话变量来引用当前用户的用户 ID。设置包含此信息的会话变量是一种有用的方法，可以避免添加另一个 SQL 查询来访问该值。只要用户处于
