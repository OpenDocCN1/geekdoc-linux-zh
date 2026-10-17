
将会话变量命名为大写并非强制要求，但这样做很有用，因为这有助于使它们在代码中作为不同类型的变量脱颖而出。

接下来的两行代码使用 `_SESSION`（代表用户的会话信息）来使用变量并将来自 SQL 查询的信息（用户名和 id）存储在其中。最后一行执行到 `index.php` 的头部重定向。

如果未点击提交按钮，在表单显示之前会执行一小段代码：

```php
header("Location: " . $config_basedir . "/login.php?error=1");
}
} 
else { 
require("header.php");
if($ GET['error']) { 
echo "Incorrect login, please try again!";
}
?>
```

包含 `header.php` 文件，然后检查是否存在名为 `error` 的 GET 变量。如果存在，则显示错误消息以指示用户输入了无效的用户名或密码。

在页面底部，HTML 之后，添加最后几行代码：

```php
}
require("footer.php");
```

## 注销用户

既然用户现在能够登录，你还需要赋予他注销的能力——通过销毁登录时创建的会话。创建一个新的名为 `logout.php` 的文件并添加以下代码：

```php
<?php

session_start();
session_destroy();
require("config.php");

header("Location: " . $config_basedir);
?>
```

要注销用户，只需使用 `session_destroy()` 函数来删除所有已注册的会话变量。会话现在已被销毁，用户不再处于登录状态。然后你可以执行到 `index.php` 的头部重定向。

## 注意

### 会话的生存与死亡

在处理基于会话的代码时，测试代码时应该始终清除任何会话。除了创建 `logout.php` 脚本外，另一个选项是关闭 Web 浏览器。会话仅在与浏览器打开期间存在，当你关闭浏览器（而不仅仅是*窗口*）时，会话就会丢失。

在开发代码时，当你想清除会话时关闭浏览器可能会让人非常沮丧。为了减轻这种痛苦，请使用适用于所有平台的 Mozilla Firefox 的 Web Developers Toolbar 扩展程序。你可以从 Mozilla Extensions 网站 http://extension-room.mozdev.org 下载它。

## 为应用程序添加会话支持

凭借新的成员登录功能，你可以为你的当前页面“充电”，使其在成员登录时做出不同的反应。可以检查登录页面中创建的会话变量，并在适当的地方添加额外的选项。

### 在头部文件中附加选项

第一个需要编辑的文件是 `header.php`。在 `login.php` 和 `logout.php` 中，你在页面开头添加了 `session_start()`。由于你将在大多数页面中使用 `session_start()`，因此将其添加到 `header.php` 的顶部：

```php
<?php

session_start();
```

此文件已经包含了一个可供网站不同部分访问的链接列表。当用户登录时，应显示注销链接；如果未登录，则应显示登录链接。在 *categories* 链接下方的 PHP 块内添加以下代码：

```php
[<a href="viewcat.php">categories</a>]
<?php

if(isset($_SESSION['USERNAME']) == TRUE) {
    echo "[<a href=\"logout.php\">logout</a>]";
}
else {
    echo "[<a href=\"login.php\">login</a>]";
}
```

`isset()` 函数用于检查是否设置了 `USERNAME` 会话变量。如果已设置，则显示注销链接；否则，显示登录链接。

对添加额外链接使用相同的方法：

```php
if(isset($_SESSION['USERNAME']) == TRUE) {
    echo " - ";
    echo "[<a href=\"addentry.php\">add entry</a>]";
    echo "[<a href=\"addcat.php\">add category</a>]";
}
?>
```

### 添加用于更新博客条目的链接

在使用 Blogtastic 时，你需要编辑现有的博客条目。与其仅仅在 `header.php` 中添加一个编辑博客条目的链接，不如在博客条目主题旁边添加编辑链接，这样更直观。（在项目后期，你将创建一个名为 `updateentry.php` 的文件来编辑博客条目。）使用类似检查会话变量是否存在的技术，在 `index.php` 中，在分类和日期行之后添加以下代码：

```php
echo "</i>In <a href=\"viewcat.php?id=\" . $row["cat_id"] . "\">"
. $row['cat'] . "</a> - Posted on " . date("D jS F Y g.iA", strtotime($row['dateposted'])) . "</i>";

if(isset($_SESSION['USERNAME']) == TRUE) {
    echo " [<a href=\"updateentry.php?id=\" . $row["id"] . "\">Edit</a>]";
}
```

`updateentry.php` 文件接收一个包含要编辑的博客条目 ID 的 `id` 变量。将此相同代码块复制到 `viewentry.php` 中，在列出发布日期行的相同位置之后。图 4-9 显示了这些链接。

![](img/c75d0c4fa51711b62f211459ae794f3f_115_0.png)

图 4-9 添加上下文链接来管理博客将使应用程序更容易使用。

## 创建自己的分类

添加博客分类是下一部分的重点。这个页面类似于用于添加评论的页面。

首先，在一个名为 `addcat.php` 的新文件中创建表单：

```html
<form action="<?php echo $SCRIPT_NAME ?>" method="post">

<table>
<tr>
<td>Category</td>
<td><input type="text" name="cat"></td>
</tr>
<tr>
<td></td>
<td><input type="submit" name="submit" value="Add Category!"></td>
</tr>
</table>
</form>
```

在文件开头，任何 HTML 之前添加常见的代码行：

```php
<?php

session_start();

require ("config.php");

$db = mysql_connect($dbhost, $dbuser, $dbpassword);
mysql_select_db($databasename, $db);
```

由于此页面仅对受限用户可用，你需要检查用户是否已登录。通过检查其中一个会话变量是否存在来完成此操作；如果不存在，则重定向到另一个页面：

```php
if (isset($_SESSION['USERNAME']) == FALSE) {
    header("Location: " . $config_basedir);
}
```

> **注意**
>
> **切勿假设**
>
> 似乎不点击链接就无法到达此页面，而这是否意味着用户已经登录？虽然这听起来合乎逻辑，但某人仍然可以直接输入 URL。最好始终明确检查以确保用户已登录，而不是信任其他页面为你完成这项工作。

添加当用户点击提交按钮时的逻辑：

```php
if(isset($_SESSION['USERNAME']) == FALSE) {
    header("Location: " . $config_basedir);
}

if($_POST['submit']) {
    $sql = "INSERT INTO categories(cat) VALUES('" . $_POST['cat'] . "');";
    mysql_query($sql);
    header("Location: " . $config_basedir . " viewcat.php");
}
else {
    require("header.php");
?>
```

在此代码中，创建了一个 INSERT 查询并发送到数据库。查询执行后，浏览器重定向到 `viewcat.php` 页面以查看新创建的分类。

最后，关闭 **else** 并包含 `footer.php` 文件（均在表单之后）：

```php
<?php
}
require("footer.php");
?>
```

## 创建新的博客条目
