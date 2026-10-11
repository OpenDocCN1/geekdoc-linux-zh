
## 查询数据库

当您需要获取、设置或更新数据库中的信息时，请使用 SQL 查询。之前您在 phpMyAdmin 中创建表格时已经对 SQL 进行了一些实践。深呼吸一下，因为现在您将开始手写具体的 SQL 查询语句。别担心，这听起来可能没有您想象的那么可怕。

在 `mysql_select_db` 行下方，添加以下代码：

```php
$db = mysql_connect($dbhost, $dbuser, $dbpassword);
mysql_select_db($dbdatabase, $db);
```

```php
$sql = "SELECT * FROM products";
$result = mysql_query($sql);
```

第一行（`$sql` 行）只是设置了另一个变量，但这个变量包含的是您要发送给 MySQL 的查询所用的 SQL 语句。SQL 是一门非常简单且有效的语言，您将在整本书中用到它——并且书中的每一段 SQL 代码都会在讲解过程中得到充分说明。在这一特定行中，您正在从 products 表中选择所有行。您可以从左到右阅读 SQL 语句来理解其工作原理：

- 首先选择（SELECT）products 表（products）中（FROM）的所有内容（*），然后结束查询（;）。

每条 SQL 语句都应以分号结尾。虽然您在 PHP 脚本中不需要显式添加分号，但这样做是个好习惯。这有助于养成添加分号的习惯，特别是当您使用命令行 MySQL 客户端时。

### 注意

#### 其他客户端

与 MySQL 交互的方式有很多种。其中一些是基于 Web 的（如 phpMyAdmin），一些是图形化桌面应用程序（如 MySQL 控制中心），还有一些是基于命令行的（如 mysql 命令）。

此时，SQL 查询实际上尚未发送到服务器；您只是创建了一个包含该查询的变量。下一行代码才会真正将查询发送到数据库。`mysql_query()` 函数用于将 SQL（在 `$sql` 变量中）发送到数据库，并将查询结果放入 `$result` 变量中。

## 遍历查询结果

`$result` 中蕴藏着“圣杯”，即您查询结果的主要所在。尽管 `$result` 包含结果，但您可以将其视为一团杂乱无章的大结果集合。以当前形式而言，`$result` 并不是特别有用，为了真正实用，您需要遍历查询中的每一行。如果您遍历每一行，就可以将相关信息显示在页面上。这就是整体计划。

在文件的 `mysql_query` 行下方添加以下代码：

```php
$sql = "SELECT * FROM products;";
$result = mysql_query($sql);

while($row = mysql_fetch_assoc($result)) {
    echo $row['product'];
}
```

在这段代码中，您使用 `while` 循环来遍历结果集中的每一行。这是通过添加一个循环条件来实现的，该条件使用 `mysql_fetch_assoc` 从 `$result` 中提取每一行，然后将该行放入 `$row` 变量中。

`mysql_fetch_assoc()` 函数的目的是将结果制作成一个关联数组。这为您提供了一种方便的键值（前面“数组”部分已作解释）方式，用于提取信息。因此，如果您需要访问当前行中 product 字段的内容，您可以使用 `$row['product']`。

## 通过会话实现跨页面一致性

在进行任何形式的 Web 开发时，最大的挑战之一是在无状态的 Web 环境中维护跨页面的状态。这个宏大的说法基本上等同于“在不同页面之间共享信息”。造成这种困难的原因是，您创建的每个 Web 页面本质上都是一个独立的程序。当您构建跨越多个不同页面的 Web 应用程序时，除了使用 **GET** 和 **POST** 变量外，没有隐含的方式来在这些页面之间共享信息。会话（Sessions）改变了这一切。

**会话**提供了一种令人惊讶地简单且高效的手段，能够在不同页面之间真正地共享变量。这是通过一系列 PHP 函数实现的，这些函数赋予您启用页面会话、创建会话变量以及在脚本中使用这些会话变量的能力。会话可用于在不同页面之间共享您喜欢的任何 PHP 变量。

### 创建会话

要使用会话，首先需要在每个希望使用会话的页面开头添加 `session_start()` 函数。至关重要的是，`session_start()` 必须位于最开头——前面不能有华丽的 HTML，不能有您姑妈莫德的照片，甚至不能有空白。

为了说明这一点的重要性，创建一个名为 `sessions.php` 的新文件，并添加以下代码：

```php
<?php
session_start();
?>
```

当运行脚本时，您不会看到任何内容；会话支持已顺利地集成到了您的页面中。现在调整代码，在 `<?php` 标签前添加一个空格：

```php
 ?>
<?php
session_start();
?>
```

当您做出这个微小的改动时，会得到一条特别恶毒的错误信息：

> 警告: session_start() [function.session-start]: Cannot send session cookie - headers already sent by (output started at /opt/lampp/htdocs/sites/startingchapter/sessions.php:1) in /opt/lampp/htdocs/sites/startingchapter/sessions.php on line 3

之所以非常重要不要在 `session_start()` 之前放置任何内容，是因为会话框架利用了构成 Web 页面机制的 HTTP 头部（headers）。这些特殊头部分别预置在每个 Web 页面的前面，因此，如果您在 `session_start()` 之前添加了任何内容，脚本将尝试先发送内容（如空格），然后是头部，最后是主要内容。这不是 Web 的工作方式，因此 PHP 会以之前警告信息的形式向您抗议。

## 关于头部的一切

互联网上的每个 Web 页面都有一些称为**头部**（headers）的信息，大多数用户看不见它们。头部存储了浏览器关心的许多信息片段。以下是一些头部示例：

```
GET / HTTP/1.1
Host: www.yourfavewebsite.org
Connection: close
Accept-Encoding: gzip
Accept: text/xml, application/xml, application/xhtml+xml, text/html;q=0.9,text/plain;q=0.8,image/png, */*;q=0.5
Accept-Language: en-gb, en;q=0.5
Accept-Charset: ISO-8859-1, utf-8;q=0.7, *;q=0.7
User-Agent: Mozilla/5.0 (X11; U; Linux i686; en-GB; rv:1.8.0.3) Gecko/20060523 Ubuntu/dapper Firefox/1.5.0.3
Referer: http://www.someotherwebsite.net/
```

头部下面是内容。当向页面添加内容时，头部分自动添加。因此，当数据被添加到页面时，头部也会被发送，并且在发送后无法再被修改。

当您使用会话时，会话系统会修改其中的一些头部，这就是为什么必须在向页面添加任何数据之前添加 `session_start()` 的原因。

## 使用会话变量

在使用会话变量之前，您需要注册它。这是通过名称颇为直观的 `session_register()` 函数实现的。要使用它，请在括号内指定要创建的变量名。为了演示这一点，在 `sessions.php` 中的 `session_start()` 之后添加以下代码行：

```php
session_register("userid");
```

这一行向会话处理系统注册了 `userid` 变量可以跨页面共享。下一步是实际将这个变量设置为有用的值。添加这一行代码：

```php
$_SESSION['userid'] = 10;
```

在这一行中，您使用特殊的 `$_SESSION` 超全局变量来引用 `userid` 变量。`$_SESSION` 语法应该看起来相当熟悉，因为您之前使用 `$_GET` 和 `$_POST` 分别访问 GET 和 POST 变量。

为了测试您的会话变量是否可以在第二个页面上访问，创建一个名为 `sessions2.php` 的文件，并添加以下代码：

```php
<?php
session_start();
echo "The userid session variable is: " . $_SESSION['userid'];
?>
```

记得先访问 `sessions.php`（以便设置变量），然后访问 `sessions2.php` 以查看该变量是否在页面间共享。要访问会话变量，您只需在页面上包含 `session_start()`，然后使用 `$_SESSION` 引用该变量即可。

只要浏览器保持打开状态，会话信息即可用。当浏览器窗口关闭时，会话信息丢失。虽然这通常是销毁会话的合适方式，但有时您需要强制销毁会话数据。为此，您可以使用以下命令：

```php
session_destroy();
```

然后所有会话变量都会被适当地删除。

## 摘要

本章探讨了一些核心概念，这些概念需要在您继续前进并开始编写应用程序之前予以理解。我们没有花费数小时去涵盖 PHP 和 MySQL 的每个细微差别，而是学习了继续前进所需的基础知识，每个应用程序都将展示新的技能、技巧和想法。

就像任何编程语言或自然语言一样，熟能生巧。仅仅阅读如何在 PHP 中做某事，与真正理解它是两回事。熟悉这门语言的绝佳方式是创建许多小脚本来测试语言的不同方面。这些脚本不仅对学习有用，而且当您忘记如何做某事时，它们还可以作为日后很好的参考点。

