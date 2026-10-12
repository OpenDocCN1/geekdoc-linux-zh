
完成后的评分显示效果应类似于图 11-5 中所示的样子。

![](img/c75d0c4fa51711b62f211459ae794f3f_463_0.png)

**图 11-5** 在此示例中，评分为 10 分制中的 8 分。

在评分图片之后，添加允许已登录用户投票的代码：

```php
echo "<br />";

echo "<strong>请给此故事评分</strong>: ";

if($_SESSION['SESS_USERNAME']) {
    for($i=1;$i<=10;$i++) {
        echo "<a href='ratestory.php?id=" . $validid . "&rating=" . $i . ">" . $i . "</a>";
    }
} else {
    echo "若要投票，请 <a href='userlogin.php'>登录</a>。";
}
```

如果用户已登录，`for` 循环将创建从 1 到 10 的 10 个链接，每个链接都指向 `ratestory.php`，并向其传递故事的 `id` 和评分数字。

最后，添加关闭代码：

```php
echo "</p>";
require("footer.php");
?>
```

## 执行评分

当用户点击其中一个评分数字时，`ratestory.php` 会将该评分添加到数据库中。此脚本相当简单，并包含少量的错误检查。

创建 `ratestory.php`。首先，包含常规文件并验证 GET 变量：

```php
<?php
require('db.php');
require('functions.php');

if(pf_check_number($_GET['id']) == TRUE) {
    $validid = $_GET['id'];
} else {
    header("Location: " . $config_basedir);
}

if(pf_check_number($_GET['rating']) == TRUE) {
    $validrating = $_GET['rating'];
} else {
    header("Location: " . $config_basedir);
}

require('header.php');
```

此脚本必须传递 `id` 和 `rating` GET 变量。如果变量不存在或不是数字，页面将重定向。

检查用户是否已经投票：

```php
$checksql = "SELECT * FROM ratings WHERE user_id = "
    . $_SESSION['SESS_USERID'] . " AND story_id = "
    . $validid . ";";
$checkresult = mysql_query($checksql);
$checknumrows = mysql_num_rows($checkresult);
```

该查询检查当前故事的 `ratings` 表中是否包含该用户的 `id`。如果是，则显示一条消息，告知用户其已经投票：

```php
if($checknumrows == 1) {
    echo "<h1>已投票</h1>";
} else {
    echo "<p>您尚未对此故事进行投票。</p>";
    
    // 如果用户尚未投票，将评分添加到表中：
    $inssql = "INSERT INTO ratings(user_id, story_id, rating) VALUES("
        . $_SESSION['SESS_USERID'] . ","
        . $validid . ","
        . $validrating . ");";
    mysql_query($inssql);
    
    echo "<h1>谢谢！</h1>";
    echo "<p>感谢您的投票。</p>";
}
?>
```

## 管理故事

为了简化表单的创建和处理，使用了 `HTML_QuickForm`。`HTML_QuickForm` 简化了表单的显示和验证，并且还具有减少脚本代码量的附带好处，使代码看起来稍微整洁一些。

`HTML_QuickForm` 采用了一种称为面向对象编程（`OOP`）的技术。`OOP` 的理念是你拥有一系列描述常见操作类型的类，你可以将这些类作为蓝图来创建对象。想象你是一位高级存在者，能够创建一个充满动物的农场。你可能会有一个名为 `Mammal` 的类，创建一个具有哺乳动物特征的对象。你可能还会有另一个名为 `Dog` 的类，它继承 `Mammal` 类但添加了 `Dog` 特有的特征。这就是 `OOP` 工作原理的基础。在技术环境中，你可能有一个名为 `Button` 的类，指定非常通用的按钮概念，然后拥有继承 `Button` 的不同 `PushButton` 和 `ToggleButton` 类。

![](img/c75d0c4fa51711b62f211459ae794f3f_465_0.png)

### 为什么要使用传统的过程式方法？

`OOP` 是一个庞大且多样的主题，虽然 `PHP` 可以用于 `OOP`，但本书回归传统的过程式开发方法，因为它更容易理解和使用。此外，创建 `PHP` 脚本的 `OOP` 方式并没有过程式方法使用得那么广泛。

`HTML_QuickForm` 的工作方式与常规表单处理类似，尽管方式略有不同：

- 包含 `HTML_QuickForm` 类。
- 创建一个 `HTML_QuickForm` 对象。
- 创建表单元素。
- 创建验证规则。
- 显示表单并指定应处理它的函数。

尽管 `HTML_QuickForm` 一开始可能看起来有点不寻常，但在你编写了一些使用它的脚本之后，你会发现它在许多情况下非常实用。

## 添加故事

添加故事涉及创建一个相当常见的表单，接收信息并将其放入数据库中。创建 `addstory.php` 并开始包含你的文件：

```php
<?php
session_start();

require("config.php");
require("functions.php");
require('db.php');
```

除了常规的包含文件外，还要包含 `HTML_QuickForm`：

```php
require_once 'HTML/QuickForm.php';
```

当你安装 PEAR 模块时，`php.ini` 已更新，以确保 PHP 可以轻松找到 PEAR 扩展，从而能够使用 `HTML/QuickForm.php` 作为位置和文件。

通过锁定没有 1 级或更高用户级别的任何人来保护该页面：

```php
if($_SESSION['SESS_USERLEVEL'] < 1) {
   header("Location:" . $config_basedir);
}
```

接下来，从 `HTML_QuickForm` 类创建一个对象：

```php
$form = new HTML_QuickForm('firstForm');
```

这行代码创建了一个名为 `$form` 的 `HTML_QuickForm` 对象。该对象具有一系列可用的方法，你可以在 `http://pear.php.net/package/HTML_QuickForm/docs` 上了解更多信息。

要创建一个表单，你需要添加常规的文本框和提交按钮，以及一个包含用户可从中选择类别列表的 `select` 框。手动创建表单时，你添加一个 `<select>` 标签，然后循环查询结果以添加 `<select>` 框的内容。

使用 `HTML_QuickForm` 时，过程略有不同。你需要执行查询，然后构建一个包含项的数组。此数组稍后会被添加到表单中。

添加构建数组的代码：

```php
$catsql = "SELECT id, category FROM categories ORDER BY category";
$catres = mysql_query($catsql);

while($catrow = mysql_fetch_assoc($catres)) {
   $catarr[$catrow['id']] = $catrow['category'];
}
```

首先创建查询，然后 `while` 循环创建数组。数组键（方括号中的部分）设置为 `id`，值设置为类别名称。例如，如果你有类别 *Music*（`id` 为 1）和 *Fashion*（`id` 为 20），数组将如下所示：

```php
$catarr[1] = "Music";
$catarr[20] = "Fashion";
```

创建表单元素并加载数组：
