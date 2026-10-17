
```
$myarray = array("state"=>"Illinois", "city"=>"Chicago", "zip"=>"60633");
foreach ($myarray as $key => $value)
{
 echo "The $key value is $value<br>\n";
}
```

现在你可以在数组中同时访问键和数据值。同样，`$key` 和 `$value` 变量是普通变量，可以在 `foreach` 循环内的任何位置使用来表示键和数据值。

# 结构化命令

PHP 编程语言使用结构化命令支持程序流程控制。最常见的方法是 if-then 语句和各种循环语句。本节讨论这两种结构化命令语句。

## if-then 语句

标准的 if-then 语句根据条件求值的结果执行一个或多个语句。如果条件为真，则执行语句。此功能允许你根据比较结果执行 PHP 代码，例如仅在项目为奢侈品时才对价格加税。PHP 中 if-then 语句的基本格式为

```
if (condition)
{
    code block 1
} elseif {
    code block 2
} else {
    code block 3
}
```

if-then 语句将它控制的语句包含在大括号中，并将它求值的条件包含在括号中。条件必须是结果为真或假布尔值的表达式。

你可以检查各种条件，例如数字是否为特定值或是否在值范围内，或字符串值是否等于特定文本（例如，检查标记为活动状态的数据库记录）。

让我们创建一个测试文件来演示使用 if-then 语句。按照以下步骤操作：

1. 打开文本编辑器并输入以下代码：

```
<html>
<body>
<h1>Random number test</h1>
<?php
$value = rand(0, 100);
if ($value > 50) {
    echo "<h2>The value is big: $value</h2>\n";
} elseif ($value > 25) {
    echo "<h2>The value is medium: $value</h2>\n";
} else {
    echo "<h2>The value is small: $value</h2>\n";
}
?>
</body>
</html>
```

2. 将文件保存在 `/var/www` 文件夹中，文件名称为 `randomtest.php`。

3. 打开浏览器窗口并访问 URL `http://localhost/randomtest.php`。

此脚本使用 `rand()` PHP 函数生成 0 到 100 之间的随机整数值，并将其存储在变量 `$value` 中。然后脚本在三个单独的 if-then 语句中使用该变量。

你可以通过点击浏览器上的重新加载按钮多次运行 PHP 脚本。每次重新加载网页时，脚本都会生成一个新的随机数，从而产生不同的答案。

## `while` 循环

`while` 循环允许你在满足特定条件之前重复处理一组语句：

```
while ( condition )
{
    statements to repeat
}
```

通常，在重复的语句中会有一个语句改变条件中变量的值。以下是一个简单的示例，说明其工作原理：

```
$count = 0;
while ($count < 10)
{
    echo "the value is $count";
    $count = $count + 1;
}
```

只要 `$count` 变量小于值 10，`while` 循环就会继续执行这两个语句。

# 包含外部文件

PHP 的一个特性是许多 Web 开发人员所喜爱的，那就是能够创建包含文件。你可能也听说过它们被称为服务器端包含。`include()` 语句允许你仅通过引用文件名，就将一个网页的内容包含到另一个网页中。此过程有点像在 HTML 中使用框架或 iframe，但它更简单，而且你可以更确信 Web 浏览器会按你想要的方式显示所有内容。

## The `include()` 语句

PHP 处理器会将 include 文件中的所有行直接插入到 PHP 代码中，就在你放置 `include()` 语句的位置。它就像你自己将这些行代码输入到正在显示的页面中一样。然后服务器将包含的行作为普通的 PHP 代码进行处理。include 文件中的任何变量都将被处理，就好像它们是在主脚本中定义的一样。

开发人员使用此功能来创建标准页眉和页脚包含文件，然后他们可以轻松地将其合并到所有 Web 页面中。想象一下，只需添加两行代码，就可以在所有 Web 页面上拥有标准页眉和页脚部分！

你可以一次性创建网站的导航，然后保证它在每个页面上都以完全相同的方式显示。如果你需要更改导航中的某些内容，你只需在唯一代码的一个位置进行一次更改。还能有什么更好呢？

`include()` 语句的格式很简单：

```
include("filename");
```

你只需将 `filename` 替换为文件的实际名称。就这么简单。让我们通过以下步骤试用一下：

- 1. 在 `/var/www` 文件夹中创建一个名为 `header.inc.php` 的示例文件，其中包含以下文本：

```
<?php
echo "<h1 align=\"center\">This is a test header</h1>\n";
echo "<a href=main.php>Main</a>\n";
?>
```

开发人员通常为包含文件添加 `.inc` 扩展名，以表明它们本身并不是完整的网页。你也可以附加 `.php` 文件扩展名，以表明文件包含 PHP 代码。由于服务器本身并不处理实际的包含文件，因此这样做不是必需的。相反，它会将其插入到主 PHP 文件中。

- 2. **在同一文件夹中创建另一个文件并命名为 `main.php`。** 在其中输入以下代码和文本：

```html
<html>
<body>
<?php include("header.inc.php"); ?>
<br><br>
<h2>This is the body of the main page</h2>
</body>
</html>
```

- 3. **打开浏览器并查看 URL** `http://localhost/main.php`。

你应该会看到页眉文件信息，然后是主文件信息，如图 30-5 所示。

![](img/39e65eeb4f54001ede08c6114ae3cc6c_786_0.png)

**Figure 30-5:** 使用 `include()` 函数包含 PHP 文件。

## 引用 `include()` 文件

现在，如果你想为所有应用程序页面使用一个公共页眉，你所需要做的就是使用 `include()` 函数来包含相同的 `header.inc.php` 代码。当你需要更改页眉内容时，只需更改一个文件，更改就会应用于所有页面！

> **Secret**
>
> 这个小例子也演示了另一个需要记住的 PHP 细节。请注意在步骤 1 中，你必须使用反斜杠字符转义 h1 标签中的双引号。这样做可以防止 `echo` 语句认为引号代表字符串的结束。

上一节中显示的简单示例仅通过文件名引用了包含文件。没有提供路径信息。只要包含文件位于与主文件相同的目录中，你就可以这样做。

但一些 Web 程序员更喜欢将包含文件与主文件分开，将它们放在文档根目录下的一个文件夹中。要引用这些包含文件，你必须使用路径名以及文件名一起引用。然而，这可能是一件棘手的事情，会导致有趣的结果。

你可以使用两种路径名方法来引用包含文件：

- 绝对路径名
- 相对路径名

绝对路径名从系统上的根文件夹引用包含文件。如果你使用绝对路径名引用包含文件，文件名必须以斜杠开头：

```
include("/var/www/includes/header.inc.php");
```

在此示例中，`header.inc.php` 文件位于 `includes` 文件夹中，而 `includes` 文件夹位于 `www` 文件夹下。

相对路径名方法基于使用 `include()` 函数的主程序代码的当前位置来引用包含文件。例如，如果你想从位于 `www` 文件夹中的 `main.php` 文件引用 `header.inc.php` 包含文件，你将使用相对路径名：

```
include("includes/header.inc.php");
```

此相对路径名假定 `includes` 文件夹位于当前文件夹下，并且 `header.inc.php` 包含文件位于那里。

如果 `include()` 函数找不到你要引用的文件，它会在网页上产生两个错误：
