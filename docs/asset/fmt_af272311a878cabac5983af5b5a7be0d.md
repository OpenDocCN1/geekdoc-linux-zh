
# PHP 常用函数与表单处理

PHP 中可能最频繁使用的函数是 `exit`，尽管纯主义者会告诉你，它实际上是一个语言结构而不是函数。`exit` 在执行时会立即终止脚本的运行，这意味着后续代码行不会被执行。其实就是这么简单；它几乎不值得举例，但这里提供一个以防万：

```php
<?php
exit;
echo "Exit is a language construct!\n";
?>
```

此脚本什么都不打印，因为 `exit` 在 `echo` 之前。

一个我们可以保证你会经常用的函数是 `var_dump()`，它会将变量的信息（包括它的值）转到屏幕。这个函数对于数组来说无价，因为它会打印每一个值，如果一个或多个元素是数组，它会打印这些数组的所有元素，以此此类推。要使用此函数，只需将变量作为唯一参数传递给它，如下：

```php
<?php
    $drones = array("Graham", "Julian", "Nick", "Paul");
    var_dump($drones);
?>
```

该脚本的输出如下：

```
array(4) {
    [0]=>
    string(6) "Graham"
    [1]=>
    string(6) "Julian"
    [2]=>
    string(4) "Nick"
    [3]=>
    string(4) "Paul"
}
```

`var_dump()` 函数被广泛用作基础调试技术，因为使用它是将变量数据打印到屏幕上进行验证的最简单方法。

最后，`var_dump()` 函数被广泛使用作为一种基础调试技术，因为使用它是将变量数据打印到屏幕上进行验证的最简单方法。最后，`var_dump()` 函数被广泛使用作为一种基础调试技术，因为使用它是将变量数据打印到屏幕上进行验证的最简单方法。最后，`var_dump()` 函数被广泛使用作为一种基础调试技术。

最后，在正则表达式中，你可以选择使用 Perl 兼容正则表达式（PCRE）还是 POSIX 扩展表达式。主要的函数有 `preg_match()`、`preg_match_all()`、`preg_replace()` 和 `split()`。`preg_match()` 的第一个参数是你想搜索的正则表达式，第二个是字符串。如果你想检查某个字符串是否匹配正则表达式，可以使用：

```php
$result = preg_match("/[a-z]/", "This is a test");
```

`preg_match()` 返回 `1`（匹配成功）或 `0`（未匹配）。`preg_match_all()` 则更有用，它通过引用参数填充所有匹配项。为了感受 `preg_match_all()` 的工作方式，这里有一个很好的开始：

```php
<?php
$string = "This is the best test";
$result = preg_match_all("/[a-z]/", $string, $matches);
var_dump($matches);
?>
```

它输出如下：

```
array(1) {
  [0]=>
    array(3) {
      [0]=>
        string(4) "best"
      [1]=>
        string(4) "test"
      [2]=>
        string(4) "west"
    }
}
```

注意 `$matches` 数组实际上是多维的，因为它包含一个元素，该元素本身是一个数组。这是因为该表达式没有子表达式（即没有括号内的独立匹配）。如果你有子表达式，每个子表达式在 `$matches` 数组中都会有自己的元素，并包含自己的数组数组。

接下来，`preg_replace()` 用于更改所有匹配正则表达式的字符串。使用它的基本方法非常简单：你用正则表达式搜索内容，并为其提供替换内容。然而，一种更有用的变体是反向引用，将匹配项作为替换的一部分。为了方便演示，假设你写了一篇关于 PHP 的教程，但想处理文本，使每个函数引用后面跟着一个指向 PHP 手册的链接。

PHP 手页面 URL 的格式为 `www.php.net/<somefunc>`（例如 `www.php.net/preg_replace`）。你需要匹配的字符串是函数名，它由字母组成，可能也混合数字和下划线，并以括号 `()` 结尾。作为替换，你可以使用找到的匹配，将其包裹在 HTML 强调标签 `<em>` 中，然后加上指向相关 PHP 手册页面的链接。所有这些代码如下：

```php
<?php
$regex = "/([A-Za-z0-9_]*)\\(\)/";
$replace = "<em>$1</em> (<a href=\"http://www.php.net/$1\">manual</a></a>";
$haystack = "File_get_contents() is easier than using fopen().";
$result = preg_replace($regex, $replace, $haystack);
echo $result;
?>
```

`$1` 是后向引用；它将被替换为第一个子表达式的结果。我们编写正则表达式的方式非常精确。匹配函数名的 `[A-Za-z0-9_]*` 部分被标记为子表达式。其后是 `\(\)`，这意味着精确的符号（圆括号），而不是它们在正则表达式中的含义，这意味着替换中的 `$1` 将包含 `fopen` 而不是 `fopen()`，这正是我们要求的。当然，替换中任何没有被后向引用的内容都会被删除，因此你必须在第一个 `$1` 之后加上 `()`（不在超链接中）来修复函数名。

完成这些工作后，输出是完美的：

```
<em>File_get_contents()</em> (<a href="http://www.php.net/file_get_contents">manual</A>) 比使用 <em>fopen()</em> (<a href="http://www.php.net/fopen">manual</A>) 更加容易。
```

## 处理 HTML 表单

鉴于 PHP 的主要作用是处理网页，你可能会奇怪为什么这一节留到章节的最后。这是因为处理 HTML 表单对 PHP 来说是如此核心，以至于基本上是自动的。

考虑这个表单：

```
<form method="POST" action="thispage.php">
User ID: <input type="text" name="UserID" /><br />
Password: <input type="password" name="Password" /><br />
<input type="submit" />
</form>
```

当访问者点击提交时，`thispage.php` 会被再次调用，这次 PHP 在 `$_REQUEST` 数组中拥有了可用变量。根据该脚本，如果用户输入 `12345` 和 `frosties` 作为用户 ID 和密码，PHP 提供的 `$_REQUEST['UserID']` 设置为 `12345`，`$_REQUEST['Password']` 设置为 `frosties`。注意，使用 HTTP POST 是重要的，除非你明确想用 GET。POST 允许你发送多得的数据，并防止人们通过篡改 URL 来尝试寻找脚本中的漏洞。

就这样吗？嗯，几乎如此。你现在知道如何检索用户数据了，但你应该确保对其进行清理，以防用户尝试将 HTML 或 JavaScript 溜进你的数据库，并将其伪装成你认为无害的东西。PHP 为你提供了 `strip_tags()` 函数来实现此目的。它接收一个字符串并返回删除所有 HTML 标签后的相同字符串。

## 数据库

PHP 可以轻松创建动态的、由数据库驱动的网站，这是许多人使用它的关键原因。PHP 的标准版本带有对 MySQL、PostgreSQL、SQLite、Oracle、Microsoft SQL Server、ODBC 以及其他几种流行数据库的支持，因此你一定能找到处理数据的工具。

如果你愿意，可以学习用于连接和操作 PHP 支持的每个数据库的单独函数，但一个更智能（或至少更简单）的想法是使用 `PEAR::DB`，它是 PHP 支持的数据库之上的抽象层。你只需要编写一次代码，——通过微小的更改——它就能在每个数据库服务器上运行。

PEAR 是 PHP 的脚本仓库，包含了许多针对常见问题的工具和预写解决方案。`PEAR::DB` 可能是 PEAR 项目中最流行的部分，但值得检查一下 PEAR 网站（`http://pear.php.net`），看看是否有其他内容吸引你的注意。

要学会使用 `PEAR::DB` 的基本功能，你需要学习如何连接数据库、运行 SQL 查询并处理结果。这不是 SQL 教程，所以我们假设你已经熟悉该语言。为了本教程，我们还假设你正在操作一个名为 `dentists` 的数据库以及一个名为 `patients` 的表，该表包含以下字段：

- ID—主键，自动递增整数，用于存储每个患者的唯一数字
