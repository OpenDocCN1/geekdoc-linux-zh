
```php
$childresult = mysql_query($childsql);

while($childrow = mysql_fetch_assoc($childresult)) {
  if($_SESSION['SESS_USERLEVEL'] == 10) {
    echo "<a href='deletecat.php?id=' . $childrow['id'] . '>[X]</a> ";
  }

  echo " &bull; <a href='index.php?parentcat=' . $row['id'] . "&amp;childcat=" . $childrow['id'] . "'>" . $childrow['category'] . "</a><br>";
}
```

结果会显示给用户，如果用户级别为 10，则再次添加删除链接。

关闭 `bar.php` 中的代码：

```php
echo " &bull; <a href='index.php?parentcat=' . $row['id'] . "&amp;childcat=' . $childrow['id'] . "'>" . $childrow['category'] . "</a><br>";
}
}
?>
```

最后，添加示例 11-5 中显示的底部代码。

### 示例 11-5 底部代码关闭了 `<div>` 区域。

```html
</div>
</div>
</body>
</html>
```

# 创建主页

我们的主页将是 `index.php`，它有三个主要目的：

- 将会话变量设置为当前选中的父类别和子类别。
- 当选择一个类别时，显示可用故事的摘要。
- 当未选择类别时，显示最新的新闻故事。

传递给页面的 GET 变量决定了加载哪个功能。如果没有 GET 变量，则显示最新故事。如果页面接收 `parentcat` 变量，则显示该类别的故事。如果同时存在 `parentcat` 和 `childcat` 变量，则显示子类别的故事。

创建 `index.php`，首先创建父/子会话变量，验证 GET 变量并将它们分配给 `SESS_PARENT` 或 `SESS_CHILD` 会话变量，如示例 11-6 所示。

```php
<?php

require("db.php");

session_register("SESS_PARENT");
session_register("SESS_CHILD");

if(isset($_GET['parentcat'])) && isset($_GET['childcat'])) {
   if(is_numeric($_GET['parentcat'])) {
      $_SESSION['SESS_PARENT'] = $_GET['parentcat'];
   }

   if(is_numeric($_GET['childcat'])) {
      $currentcat = $_GET['childcat'];

      $_SESSION['SESS_CHILD'] = $_GET['childcat'];
   }
}
else if(isset($_GET['parentcat'])) {
   if(is_numeric($_GET['parentcat'])) {
```

$currentcat = $_GET['parentcat'];

$_SESSION['SESS_PARENT'] = $_GET['parentcat'];

$_SESSION['SESS_CHILD'] = 0;

}

else {

$currentcat = 0;

}

系统会检查这两个变量是否都存在。如果存在，将检查这些变量是否为数值类型，如果是，则会话变量被赋值为每个 GET 变量的值。如果仅有 `parentcat` 这个 GET 变量可用，则应用相同的流程。

`$currentcat` 变量决定了当前类别。有三种可能的选项：

- 如果仅存在 `parentcat` 变量，`$currentcat` 被设置为 `parentcat` 的值。
- 如果存在 `childcat` 变量，`$currentcat` 被设置为 `childcat` 的值。
- 如果没有任何变量存在，`$currentcat` 被设置为 0。

检查 `$currentcat` 是否设置为 0。如果是，创建一条查询以返回最新的五篇文章：

```php
$currentcat = 0;
}

require("header.php");

if($currentcat == 0) {
$sql = "SELECT * FROM stories ORDER BY dateposted DESC LIMIT 5;";
}
```

如果 `$currentcat` 被设置为某个类别，则运行一条查询以确定 `parent` 字段被设置为什么：

```php
$sql = "SELECT * FROM stories ORDER BY dateposted DESC LIMIT 5;";
}
else {
$parentsq1 = "SELECT parent FROM categories WHERE id = " . $currentcat . ";";
$parentres = mysql_query($parentsq1);
$parentrow = mysql_fetch_assoc($parentres);
```

现在检查 `parent` 是否设置为 1。如果是，说明用户点击了一个可以包含多个子类别的类别。当这种情况发生时，显示父类别中的所有文章以及所有子类别的文章。如果所选类别不是父类别，则返回该特定类别的文章。为此添加相应的 SQL 语句：

```php
$parentres = mysql_query($parentsql);
$parentrow = mysql_fetch_assoc($parentres);

if($parentrow['parent'] == 1) {
    $sql = sprintf("SELECT stories.* FROM stories INNER JOIN cat_relate ON stories.cat_id = cat_relate.child_id WHERE cat_relate.parent_id = %d UNION SELECT stories.* FROM stories WHERE stories.cat_id = %d;", $currentcat, $currentcat);
} else {
    $sql = "SELECT * FROM stories WHERE cat_id = " . $currentcat . ";";
}
```

如果该类别是父类别，则构建一条大型查询以返回所有文章。这条查询实际上是由两条巧妙结合的查询组成的。第一部分（`SELECT stories.* FROM stories INNER JOIN cat_relate ON stories.cat_id = cat_relate.child_id WHERE cat_relate.parent_id = <id>`）使用连接来获取所有 `parent_id` 设置为 `$currentcat` 的文章。第二部分（`SELECT stories.* FROM stories WHERE stories.cat_id = <id>`）选择属于父类别的文章。

这两部分通过使用 `UNION` 关键字在同一条查询中拼接在一起，该关键字将使用相同类型列的两条查询连接起来。在需要针对相同表执行两条 `SELECT` 查询的情况下（如此处），这非常有用。

这条大型查询在 `sprintf()` 函数内部构建。当你想用另一个字符串或变量替换字符串的一部分时，会使用此函数。在此情况下，你希望在查询的相应位置添加 `$currentcat`。为此，字符串中的 `%d`（称为*类型说明符*）被 `sprintf()` 末尾指定的变量替换——在此情况下是 `$currentcat`。不同类型的变量使用不同的类型说明符，你可以访问 `www.php.net/sprintf` 来满足对类型说明符的好奇心。

在 `else` 分支中，如果所选类别不是父类别，则构建一条查询，它简单地返回该特定类别的文章。

运行相关的查询：

```php
$sql = "SELECT * FROM stories WHERE cat_id = " . $currentcat . ";";
}
}

$result = mysql_query($sql);
$numrows = mysql_num_rows($result);
```

手头有了丰富的结果集，将其显示给用户：
