
首页现在已经完成了。该页面提供了一种简单且熟悉的方式来展示版块和论坛（见图 5-6）。

![](img/c75d0c4fa51711b62f211459ae794f3f_140_0.png)

**图 5-6** 这是用户访问论坛首页时所看到的内容。

接下来，你创建 `viewforum.php` 页面以显示所选版块中的主题。

## 查看版块主题

这个页面有一个简单的目的——列出属于该版块的所有主题，以及主题回复的数量、作者姓名和主题发布日期。

当此页面加载时，一个名为 `id` 的 GET 变量已被传递给它。对于任何 GET 变量，对其进行验证都是一个明智的做法。创建一个名为 `viewforum.php` 的新文件，并添加以下代码：

```php
<?php
include("config.php");

if(isset($_GET['id']) == TRUE) {
    if(!is_numeric($_GET['id']) == FALSE) {
        header("Location: " . $config_basedir);
    }
    $validforum = $_GET['id'];
} else {
    header ("Location: " . $config_basedir);
}
```

这段代码之前已用于执行相同类型的验证检查。

加载 `header.php` 文件：

```php
require("header.php");
```

在显示主题之前，先显示页面的一些通用信息，以便用户知道他们处于网站的哪个位置。这些信息包括当前版块名称和面包屑导航路径。

要添加这些信息，执行一个查询以获取具有 `$validforum` 标识符的版块名称，然后在一个二级标题中显示该版块名称：

```php
require("header.php");
$forumsql = "SELECT * FROM forums WHERE id = " . $validforum . ";";
$forumresult = mysql_query($forumsql);
$forumrow = mysql_fetch_assoc($forumresult);
echo "<h2>". $forumrow['name'] ."</h2>";
```

下一步是创建面包屑导航路径。面包屑导航路径提供了一系列链接，显示到达当前网站页面所经历的步骤。这个概念对于拥有许多部分的网站特别有用。

## **注意**

### **面包屑导航：有用还是无用？**

在 Web 开发社区中，对于面包屑导航是否真的有用存在不同的观点。对于一些开发者来说，面包屑导航被认为是一个难以导航的网站的借口。然而，其他开发者则认为这种路径是导航的有用辅助工具。

当你设计 Web 应用程序时，考虑一下导航，以及面包屑导航是否可以帮助你的用户。

在此页面上，面包屑导航很简单。提供一个链接以返回通用论坛页面：

```php
echo "<h2>" . $forumrow['name'] . "</h2>";

echo "<a href='index.php'>" . $config_forumsname . " forums</a><br /> <br />";
```

添加一个允许用户向此版块添加新主题的链接：

```php
echo "<a href='index.php'>" . $config_forumsname . " forums</a><br /> <br />";

echo "[<a href='newtopic.php?id=" . $validforum . ">New Topic</a>]";
echo "<br /> <br />";
```

现在你需要显示此版块内的主题。虽然这可能听起来像只是显示所有 `forum_id` 为 `$validforum` 的主题那么简单，但查询实际上更复杂。

在此页面上，你需要显示一系列信息，其中大部分来自不同的表：

- 主题名称位于 `topics` 表中。
- 作者姓名位于由 `topics` 表中的 `user_id` 链接到的 `users` 表中。
- 发布日期位于 `topics` 表中。

使生活更复杂的是，你还需要将最新发布的主题显示在列表的顶部。组织这些主题相当困难——实际的帖子存储在 `messages` 表中，然后通过 `topic_c_id` 关联到 `topics` 表。因此，你需要按最新主题排序显示的条目，即 `messages` 表中日期最新的消息。

为了解决这个排序问题，你将使用 MySQL 中的一个特殊函数 `MAX()`。该函数从 `messages` 表中选择最新的日期。此外，还选择了来自 `topics` 和 `users` 表的信息。然后，`messages` 和 `topics` 表在 WHERE 子句中链接起来。

现在，坐下来，屏住呼吸，执行这个史诗级的查询：

```php
echo "<br /> <br />";

$topicsql = "SELECT MAX(messages.date ) AS maxdate,
 topics.id AS topicid, topics.*, users.*
 FROM messages, topics, users WHERE messages.topic_id
 = topics.id AND topics.user_id = users.id AND
 topics.forum_id = " . $validforum . " GROUP BY
 messages.topic_id ORDER BY maxdate DESC;";
$topicresult = mysql_query($topicsql);
$topicnrows = mysql_num_rows($topicresult);
```

如果 `$topicnrows` 包含 0，则没有主题：

```php
$topicnrows = mysql_num_rows($topicresult);
if ($topicnrows == 0) {
    echo "<table width=300px><tr><td>No topics!</td></tr></table>";
}
```

这里有点取巧。正如你所见，你正在创建一个表格来添加一条记录。但你希望**没有主题**文本在表格中显示得井井有条。这是一点取巧，因为你没有将代码放在页面下方的其他表格中。这是为了清晰度。重要的是确保你理解代码，而不是陷入表格混乱之中。

如果存在主题，你将以表格形式呈现它们。创建表格和表头：

```php
if ($topicnrows == 0) {
    echo "<table width=300px><tr><td>No topics!</td></tr></table>";
}
else {
    echo "<table class='forum'>";
    echo "<tr>";
    echo "<th>Topic</th>";
    echo "<th>Replies</th>";
    echo "<th>Author</th>";
    echo "<th>Date Posted</th>";
    echo "</tr>";
```

在显示行之前，运行另一个查询来统计当前行中主题的消息数量：

```php
echo "</tr>";

while ($topicrow = mysql_fetch_assoc($topicresult)) {
    $msgsql = "SELECT id FROM messages WHERE
    topic_id = " . $topicrow['topicid'] . ";";
    $msgresult = mysql_query($msgsql);
    $msgnumrows = mysql_num_rows($msgresult);
```

显示这些行：

```php
echo "<tr>";
echo "<td>";
echo "<strong><a href="viewmessages.php?id=" . $topicrow['topicid'] . ">";
echo $topicrow['subject'] . "</a></strong></td>";
echo "<td>" . $msgnumrows ."</td>";
echo "<td>" . $topicrow['username'] ."</td>";
echo "<td>" . date("D jS F Y g.iA", strtotime($topicrow['date'])) ."</td>";
echo "</tr>";
}
```

这段代码添加了主题标题，并将其链接到 `viewmessages.php`，其中主题的 `id` 作为 GET 变量传递。还添加了线程中的消息数量、创建该主题的人的用户名以及主题日期。

最后，关闭表格并添加页脚：

```php
echo "</tr>";
}
echo "</table>";
}
require("footer.php");
?>
```

随着这段代码的运行，你可以看到图 5-7 中完成的论坛视图。项目真正开始成形了。

![](img/c75d0c4fa51711b62f211459ae794f3f_145_0.png)

**图 5-7** 查看版块

### 查看线程

下一页面显示与主题相关的讨论线程，这可能并不令人惊讶。当你创建 `viewforum.php` 时，你添加了一个链接到主题标题，指向名为 `viewmessages.php` 的页面，你现在将创建该页面。

创建一个名为 `viewmessages.php` 的新文件，并对 GET 变量进行一些验证：

```php
<?php
include("config.php");

if(isset($_GET['id']) == TRUE) {
    if(!is_numeric($_GET['id']) == FALSE) {
        $error = 1;
    }
}

if($error == 1) {
    header("Location: " . $config_basedir);
} else {
    $validtopic = $_GET['id'];
} else {
    header("Location: " . $config_basedir);
}
```

`require("header.php");`

通过在页面顶部首先选择当前主题标题、版块名称和主题标识符，添加主题名称和面包屑导航路径：

```php
require("header.php");

$topicsql = "SELECT topics.subject,
    topics.forum_id, forums.name FROM topics,
    forums WHERE topics.forum_id = forums.id
    AND topics.id = " . $validtopic . ";";
$topicresult = mysql_query($topicsql);

$topicrow = mysql_fetch_assoc($topicresult);
```

