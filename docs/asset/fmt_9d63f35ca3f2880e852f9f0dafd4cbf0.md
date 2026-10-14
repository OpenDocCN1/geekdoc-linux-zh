
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

`var_dump()`函数被经常作为基础调试工具使用。

PHP手册页面的 URL 将采用 `http://www.php.net/<somefunc>` 的形式——例如，`http://www.php.net/preg_replace`。我们需要匹配的字符串是一个函数名，它由字母组成，其中可能混合了数字和下划线，并以两个括号 `()` 结尾。作为替换，我们将使用找到的方法，将其包裹在 HTML 实体标签 `<em>em</em>` 中，并带上一个指向相关手册页面的链接。以下是代码中的写法：

```php
<?php

$regex = "/([A-Za-z0-9_]*)\\\\*/";

$replace = "<em>\$1</em><a href=\"http://www.php.net/\$1\">manual</a></a>";

$haystack = "File_get_contents() is easier than using fopen().";

$result = preg_replace($regex, $replace, $haystack);

echo $result;

?>
```

`$1`是我们的反向引用；它将被用第一个子表达式的结果替换。我们编写的正则表达式非常精确。紧接着是 `[A-Za-z0-9]*` 部分，它匹配函数名，并被标记为子表达式。其后是 `\(`，这意味着精确的符号本身，而不是它们在正则表达式中的含义，这意味着替换中的 `$1` 将包含短语，而不是 `fopen()`，这正是我们预期的。当然，替换中任何未被反向引用的内容都会被删除，因此我们必须在第一个 `$1` 之后（不在超链接内）放入一个 `)` 来修复函数名。

在完成所有这些工作后，输出为：
<em>File_get_contents()</em> (<a href="http://www.php.net/file_get_contents()/manual">manual</a>) is easier than using <em>fopen()</em></em> (<a href="http://www.php.net/fopen">manual</a>).

# 处理 HTML 表单

鉴于 PHP 的首要作用是处理网页，你可能会奇怪为什么这一节被放在本章的最后。这是因为处理 HTML 表单对于 PHP 来说是如此核心，以至于它基本上是自动完成的。

考虑这个表单：

```html
<form method="POST" action="tispage.php">
User ID: <input type="text" name="UserID" /><br />
Password: <input type="password" name="Password" /><br />
<input type="submit" />
</form>
```
