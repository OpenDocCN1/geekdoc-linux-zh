
## 创建表格后更改表格类型
如果您想更改现有表格的类型，请在 phpMyAdmin 中点击“Operations”（操作）标签页，然后使用该页面上的框选择不同的表格类型。

此时，表之间的参照完整性尚未设置，也没有强制实施任何参照完整性。在项目后期，您将添加一些 SQL 来强制执行它。

# 向数据库添加示例数据
手动向数据库添加数据时，您需要小心确保所有数据都能正确关联；否则，论坛将会崩溃。为了开始，先添加一个用户，然后添加几个类别、论坛和主题。

### 不要填写 id 字段
当您向这些表中的任何一个添加数据时，请记住将 id 字段留空；auto_increment 会为您处理这部分工作。

# *users*（用户）表
向 users 表添加表 5–1 中显示的详细信息。

**表 5-1 示例用户**

| 字段 | 值 |
| :-- | :-- |
| Username | Johnsmith |
| Password | Password |
| Email | john@foo.com |
| Verifystring | <留空> |
| Active | 1 |

# categories（类别）表
如果您参考图 5-4，categories 表位于相关表树的顶部。您需要首先向此表添加数据，然后依次向下处理其他表。向表中添加表 5-2 中的两条记录。

**表 5-2 示例类别**

| **字段** | **值** |
|---|---|
| Name | Movies |
| Name | Documentaries |

# forums（论坛）表
在定义了一些类别后，添加 forums 时请使用这些类别的 id。根据表 5-3 中的信息，在 Movies 类别（其 id 为 1）中创建两个论坛；不要向 Documentaries 类别添加任何论坛。

**表 5-3 示例论坛**

| **字段** | **值** |
|---|---|
| Cat_id | 1 |
| name | Comedy |
| description | Films that make you laugh |
| Cat_id | 1 |
| name | Horror |
| description | Movies to hide behind the couch |

请注意，在此处，您通过将 Comedy 类别的 id 放入此表中的 cat_id 字段来引用该类别。

# topics（主题）表
topics 表和 messages 表作为主题在内在上是相关联的，如果没有至少一条消息，它们就无法存在。topics 表仅包含要讨论的主题；您需要在 *messages* 表中创建至少一条消息。将表 5-4 中的两个主题添加到 *Comedy* 类别中。

**表 5-4 示例主题**

| **字段** | **值** |
| --- | --- |
| Date | 从 Functions 框中选择 NOW |
| User_id | 1 |
| Forum_id | 1 |
| Subject | Classic comedy |
| Date | 从 Functions 框中选择 NOW |
| User_id | 1 |
| Forum_id | 1 |
| Subject | Fave comedy actor/actress |

# messages（消息）表
在主题创建完成后，为它们创建表 5-5 中所需的消息。

**表 5-5 示例消息**

| **字段** | **值** |
| --- | --- |
| Date | 从 Function 框中选择 NOW |
| User_id | 1 |
| Topic_id | 1 |
| subject | Classic comedy |
| Body | Which black and white comedies do you like? |
| Date | 从 Function 框中选择 NOW |
| User_id | 1 |
| topic_id | 2 |
| Subject | Fave comedy actor/actress |
| Body | Who is your fave funny man/women? |

# 创建站点设计
编写代码的第一步是创建设计。创建一个名为 `config.php` 的新文件，并添加示例 5-1 中显示的代码。

> 示例 5-1 配置文件存储有关站点的设置。

```php
<?php

$dbhost = "localhost";
$dbuser = "root";
$dbpassword = "";
$database = "forum";

// Add the name of the forums below
$config_forumsname = "CineForums";

// Add your name below
$config_admin = "Jono Bacon";
$config_adminemail = "jono AT jonobacon DOT org";

// Add the location of your forums below
$config_basedir = "http://127.0.0.1/sites/forums/";
?>
```

在此文件中，您指定了用于连接数据库的变量以及用于配置站点名称和作者的变量。此外，`$config_basedir` 包含论坛的 URL；这主要用于执行重定向时。

现在，构建 header 文件。创建一个名为 `header.php` 的新文件，并添加以下代码：

```php
<?php

session_start();

require("config.php");

$db = mysql_connect($dbhost, $dbuser, $dbpassword);
mysql_select_db($database, $db);

?>
```

您首先使用 `session_start()` 添加会话支持，然后包含配置文件。在此之后，您创建到数据库的连接。

包含 header 的主要 HTML：

```html
?>

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
	<title><?php echo $config_forumname; ?></title>
	<link rel="stylesheet" href="stylesheet.css" type="text/css" />
</head>
<body>
<div id="header">
<h1><?php echo $config_forumname; ?></h1>
[<a href="index.php">Home</a>]
```

来自 *config.php* 的变量用于设置页面的标题和名称。

检查 USERNAME 会话变量并显示相关的登录/注销链接：

```php
<h1><?php echo $config_forumname; ?></h1>
[<a href="index.php">Home</a>]

<?php
if(isset($_SESSION['USERNAME']) == TRUE) {
    echo "[<a href='logout.php'>Logout</a>]";
} else {
    echo "[<a href='login.php'>Login</a>]";
    echo " [<a href='register.php'>Register</a>]";
}
?>
```

添加最后一个选项，以便用户可以发布新主题：

```php
}
?>
[<a href="newtopic.php">New Topic</a>]
</div>
<div id="main">
```

当 header 文件完成后，创建一个名为 *footer.php* 的新文件，并添加示例 5-2 中显示的 footer 代码。

**示例 5-2 Footer 代码显示在页面的底部。**

```html
</div>
<div id="footer">
&copy; 2005 <?php echo "<a href='mailto:"
. $config_adminemail . "'>" . $config_admin . "</a>"; ?>

</div>
</body>
</html>
```

在 footer 中添加了一个链接，包含 config.php 中的电子邮件地址和作者姓名。

# 显示论坛
随着基础设施的完成，您可以开始构建主论坛代码，以便在不同的页面上显示类别、论坛和主题。如果您回想一下对 phpBB 的学习，您会发现类别和论坛显示在一个页面上，而主题显示在另一个页面上，该页面在您点击论坛时显示。

## 创建首页
该网站的首页显示可用的论坛范围。创建一个名为 index.php 的文件，并首先包含 header.php：

```php
<?php
    require("header.php");
```

运行一个查询以获取所有类别：

```php
require("header.php");

$catsql = "SELECT * FROM categories;";
$catresult = mysql_query($catsql);

echo "<table cellspacing=0>";

while($catrow = mysql_fetch_assoc($catresult)) {
    echo "<tr class='head'><td colspan=2>";
    echo "<strong>" . $catrow['name'] . "</strong></td>";
    echo "<tr>";
```

在每个类别显示后，检查当前类别是否有任何论坛：

```php
echo "<tr>";

$sql1 = "SELECT * FROM
forums WHERE cat_id = " . $catrow["id"] . ";
$result1 = mysql_query($sql1);
$rownum = mysql_num_rows($result1);
if($rownum == 0) {
    echo "<tr><td>No Forums</td></tr>";
} else {
```

在执行了用于检查每个类别中的论坛的查询后，行数被计数并放入 $rownum。下一行检查此变量是否包含 0（没有行），如果是，则向表中添加 No forums!。如果有行，第二个 while 循环遍历论坛列表以将每个论坛添加到表中：

```php
echo "<td>";
while($row = mysql_fetch_assoc($result)) {
    echo "<tr>";
    echo "<td>";

echo "<strong><a
href="viewforum.php?id="
. $row["id"] . "</a> .
" . $row["name"] . "</strong>";
echo "<br><i>" . $row["description"] . "</i>";
echo "</td>";
echo "</tr>";
}
```

创建了指向 viewforum.php 的链接，并将论坛的 id 作为 GET 变量添加。在链接下方，显示描述。

最后，结束第一个 while 循环，关闭表格，并包含 footer 文件：

```php
}
}

echo "</table>";

require("footer.php");
?>
```

