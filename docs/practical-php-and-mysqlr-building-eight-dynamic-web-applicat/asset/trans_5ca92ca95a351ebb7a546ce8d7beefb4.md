
## 注销用户

要注销用户，需注销登录页面中创建的三个会话。请记住，菜单栏使用会话来跟踪当前选中的选项，因此你无法简单地销毁会话。请将示例 11-6 中的以下代码添加到 `userlogout.php` 中。

> **示例 11-6** 不要销毁会话，因为菜单使用会话变量。

```php
<?php
session_start();
require("config.php");

session_unregister("SESS_USERNAME");
session_unregister("SESS_USERID");
session_unregister("SESS_USERLEVEL");

header("Location: " . $config_basedir);
?>
```

## 更新侧边栏

如果用户已登录，你希望在侧边栏中添加一个框，以指示用户已登录，然后列出可供其使用的选项。与之前的某些项目类似，这显示为一个类似于图 11-3 所示的框。

侧边栏显示用户可用的选项。

![](img/c75d0c4fa51711b62f211459ae794f3f_458_0.png)

打开 `bar.php`，跳转到文件顶部，并添加示例 11-7 中显示的代码。

"visible" 类可与通用网站项目中显示的表格样式一起使用。

```php
<?php
session_start();

require("db.php");

echo "<table class='visible' width='100%' cellspacing=0 cellpadding=5>";
echo "<tr><th class='visible'>登录详情</th></tr>";
echo "<tr><td>";

if($_SESSION['SESS_USERNAME']) {
    echo "已登录为 <strong>". $_SESSION['SESS_USERNAME'] . "</strong> - <a href='userlogout.php'>注销</a>";
    echo "</p>";

    if($_SESSION['SESS_USERLEVEL'] > 1) {
        echo "<a href='addstory.php'>发布新故事</a><br />";
    }

    if($_SESSION['SESS_USERLEVEL'] == 10) {
        echo "<a href='addcat.php'>添加新类别</a><br />";
    }
    echo "</p>";
} else {
    echo "<a href='userlogin.php'>登录</a>";
}

echo "</td></tr>";
echo "</table>";

echo "<h1>主题</h1>";

$sql = "SELECT * FROM categories WHERE parent = 1";
```

表格中的选项取决于登录用户的级别。任何级别 1 或更高的用户都可以添加故事。如果用户是管理员（级别 10），他还可以添加类别。（你将稍后创建 `addstory.php` 和 `addcat.php` 页面。）

## 查看和评价故事

当用户点击某个类别并查看可用故事列表时，每个故事的主题都链接到包含完整故事文本的页面。该页面不仅展示完整的故事，还包含一个功能，允许已登录的用户对故事进行评价。这样你就可以知道你的编辑们写的是否是垃圾故事了。

评价功能专门限制为已登录用户。这种限制的原因微妙但很重要。你需要防止“手快”的用户对同一故事投多次票。为了防止这种滥用，你需要以某种方式跟踪用户是否已经投票。为了解决这个问题，你有多种选择，每种选择都有优缺点：

- 通过用户的会话 ID 跟踪用户。你可以将当前的会话 ID 存储在一个表中，并防止同一 ID 进行多次投票。该会话 ID 可以可靠地跟踪当前正在查看网站的用户。问题在于，用户可以通过重启浏览器生成新的会话 ID，从而绕过你的系统。
- 使用 Cookie。Cookie 允许你存储一个很小的文本文件，你可以用它来在用户的硬盘上存储少量信息。这种技术的问题是，当用户清除历史记录时，Cookie 会被删除，这样莫德姑妈就不会看到任何让她脸红的已访问网站了。
- 仅允许已登录用户投票。这种技术提供了一种跟踪用户的可靠手段，而且评价系统无法被伪造。这种方法的明显缺点是，用户需要在另一个网站上注册。

像这样的技术决策通常很难做出，因为没有明确的解决方案。为了确保评价系统完全准确且不受滥用，你将使用第三种技术——要求用户登录。

在开始编写代码之前，你应首先创建一些图像，以直观地展示故事的平均评分。这些图像应该相当小（大约 20x20 像素），并传达图 11-4 中显示的三种状态。

### 图 11-4

评分系统由三张图像组成。

![](img/c75d0c4fa51711b62f211459ae794f3f_460_0.png)

平均评分计算出来后，会四舍五入到最接近的 0.5（例如 7.5 或 8.0）。为了显示评分，将显示 10 张图像，在需要时使用上述图像。例如，平均评分为 8 时将显示 8 张“满格”和 2 张“关闭”图像。评分为 6.5 时将显示 5 张“满格”、1 张“半格”和 3 张“关闭”图像。

通过创建 `viewstory.php` 开始构建页面，然后添加介绍性和验证代码：

```php
<?php
require("config.php");
require("functions.php");

if(pf_check_number($_GET['id']) == TRUE) {
   $validid = $_GET['id'];
} else {
   header("Location: " . $config_basedir);
}

require("header.php");
```

在获取评价之前，你需要显示主要故事文本。运行一个查询来收集这些信息，然后显示它：

```php
$sql = "SELECT * FROM stories WHERE id = " . $validid . "";
$result = mysql_query($sql);
$row = mysql_fetch_assoc($result);

echo "<h1> " . $row['subject'] . " </h1>";
echo date("D jS F Y g:iA", strtotime($row['dateposted'])) . " <br />";
echo nl2br($row['body']);
```

在显示信息时，日期被格式化为可读状态，`nl2br()` 函数将正文中的空行转换为 `<br>` 标签。这种转换确保了原始文本中的空行得以保留。

当对故事进行评价时，评价表存储分数。使用此表，获取评价数量以及故事的平均评分：

```php
$avgsql = "SELECT COUNT(id) AS number, AVG(rating) AS avg FROM ratings WHERE story_id = " . $validid . ";";
$avgresult = mysql_query($avgsql);
$avgrow = mysql_fetch_assoc($avgresult);

echo "<p>";
echo "<strong>评分：</strong> ";
```

此查询使用 `COUNT()` 和 `AVG()` MySQL 函数返回投票数和平均值。`AVG()` 函数返回你指定字段的平均值。在这种情况下，你需要的是评分字段的平均值。

然而，并非每个故事都有评分的可能性很大，因此你需要考虑这种情况：

```php
if($avgrow['number'] == 0) {
    echo "暂无评分！";
}
```

如果存在评分，则根据需要向上或向下四舍五入平均值：

```php
else {
    $a = (round($avgrow['avg'] * 2) / 2);
}
```

这一行使用 `round()` 对平均值进行四舍五入，将结果乘以 2，然后除以 2 以确定最终评分。这种简单的数学技巧是获取最终值的好方法。

确定最终结果是否为 0.5 的数值（例如 7.5，而非 8）：

```php
else {
  $a = (round($avgrow['avg'] * 2) / 2) ."<br>";
  $a *= 10;
  if($a%5 == 0 && $a%10 != 0) {
    $range = ($a / 10) - 0.5;
  } else {
    $range = $a / 10;
  }
}
```

为了计算 $a 是否包含 0.5 值（例如 6.5），首先将 $a 的值乘以 10 ($a *= 10)，然后在 if 语句的括号内检查 $a 是否能被 5 整除。如果能，则 $a 除以 10 恢复其原始值，并减去 0.5。生成的 $range 变量指示要显示的“满格”图像数量。

创建一个 for 循环来显示每张图片：

```php
for($i=1;$i<=$range;$i++) {
  echo "<img src=" . $config_basedir . "siteimages/rating_full.png>";
}
```

for 循环在 1 到 $range 内的值之间遍历，每次显示 `rating_full.png`。

再次检查平均值是否为浮点数，以确定是否应添加“半格”图像：

```php
if($a%5 == 0 && $a%10 != 0) {
  echo "<img src=" . $config_basedir . "siteimages/rating_half.png>";
}
$a = $a / 10;
```

通过从 10 中减去四舍五入后的平均值，计算应显示多少张“关闭”图像：

