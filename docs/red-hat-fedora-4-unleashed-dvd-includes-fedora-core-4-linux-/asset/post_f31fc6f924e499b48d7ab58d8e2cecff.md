
## PHP 文件处理函数

```php
<?php
$text = file_get_contents("http://www.slashdot.org");
file_put_contents("fileb.txt", $text);
?>
```

使用 `file_get_contents()` 的问题是它会一次性将整个文件加载到内存中；如果你处理大文件或者有许多用户同时访问的小文件，这是不切实际的。一种替代方法是分块加载文件，这可以通过以下五个函数实现：`fopen()`、`fclose()`、`fread()`、`fwrite()` 和 `feof()`。这些函数名称中的 *f* 代表 *file*，因此它们用于打开、关闭、读取和写入文件和套接字。最后一个函数 `feof()` 如果在达到文件末尾则返回 *true*。

正确使用 `fopen()` 需要一些学习，但表面上看起来很简单。它的第一个参数是你想要打开的文件名，这很简单。然而，第二个参数是指定你想如何处理该文件的地方，你应该指定以下之一：

- r—只读；它会覆盖文件
- r+—读写；它会覆盖文件
- w—只写；它会擦除现有内容并覆盖文件
- w+—读写；它会擦除现有内容并覆盖文件
- a—只写；它会在文件末尾追加
- a+—读写；它会在文件末尾追加
- x—只写，但仅在文件不存在时
- a+—读写，但仅在文件不存在时

可选地，你也可以添加 *b*（例如，a+b 或 rb）来切换到二进制模式。如果你希望你的脚本和它们写入的文件在其他平台上顺畅工作，这被推荐。

当你调用 `fopen()` 时，你应该存储返回值。它是一个被称为 *file handle*（文件句柄）的资源，其他文件函数都需要它来完成它们的工作。例如，`fread()` 函数将文件句柄作为其第一个参数，将读取的字节数作为第二个参数，并在其返回值中返回内容。`fclose()` 函数将文件句柄作为其唯一参数并释放文件。

因此，我们可以编写一个简单的循环来打开文件，分块读取，打印这些块，然后关闭句柄：

```php
<?php
  $file = fopen("filea.txt", "rb");
  while (!feof($file)) {
    $content = fread($file, 1024);
    echo $content;
  }
  fclose($file);
?>
```

只剩下 `fwrite()` 函数，它取文件句柄作为第一个参数和要写入的字符串作为第二个参数。你也可以提供第三个参数，一个整数，指定你要写入的字符串的字节数，但如果省略，`fwrite()` 将写入整个字符串。

如果你回想起来，你可以使用 *a* 作为 `fopen()` 的第二个参数来追加数据到文件。因此，我们可以将其与 `fwrite()` 结合，编写一个脚本，使其每次执行时向文件添加一行文本：

```php
<?php
$file = fopen("filea.txt", "ab");
fwrite($file, "Testing\n");
fclose($file);
?>
```

为了使该脚本稍微有趣一些，我们可以引入一个新函数 `filesize()`，它取文件名（不是文件句柄，而是实际的文件名字符串）作为其唯一参数，并返回文件的字节大小。使用这个新函数，脚本变为：

```php
<?php
$file = fopen("filea.txt", "ab");
fwrite($file, "The filesize was" . filesize("filea.txt") . "\n");
fclose($file);
?>
```

虽然 PHP 会自动为你清理文件句柄，但最好还是自己使用 `fclose()`，这样你始终处于控制之下。

## Miscellaneous

有几个函数不属于其他类别，因此在这里介绍。第一个是 `isset()`，它取一个或多个变量作为参数，如果它们已被设置则返回 true。重要的是要注意，一个值被设置为评估为 false 的内容的变量——例如 0 或空字符串——仍然会从 `isset()` 返回 true，因为它不检查变量的值。它仅仅检查它是否被设置；因此，才有了这个名字。

`unset()` 函数也取一个或多个变量作为参数，简单地删除变量并释放内存。有了这两个函数，我们可以编写一个脚本来检查变量的存在，如果存在则删除它（参见 Listing 31.9）。

### LISTING 31.9 设置和取消设置变量

```php
<?php
  $name = "Ildiko";
  if (isset($name)) {
    echo "Name was set to $name\n";
    unset($name);
  } else {
    echo "Name was not set";
  }

  if (isset($name)) {
    echo "Name was set to $name\n";
    unset($name);
  } else {
    echo "Name was not set";
  }
?>
```

该脚本运行了两次相同的 `isset()` 检查，但在第一次检查后取消了该变量的设置。因此，它打印 "Name was set to Ildiko"，然后打印 "Name was not set"。

PHP 中最常使用的函数可能是 *exit*，尽管纯粹主义者会告诉你它实际上是一个语言构造而非函数。*exit* 在执行时立即终止脚本的处理，意味着后续的代码行不会被执行。这就是全部了；它几乎不值得举例，但为了确保清楚，这里有一个例子：

```php
<?php
  exit;
  echo "Exit is a language construct!\n";
?>
```

该脚本什么都不会打印，因为 *exit* 在 *echo* 之前。

我们可以保证你会大量使用的函数是 *var_dump()*，它输出关于变量的信息，包括其值，到屏幕上。这对数组非常有价值，因为它打印每个值，如果一个或多个元素是数组，它会打印这些数组的所有元素，以此类推。要使用此函数，只需传递一个变量作为其唯一参数：

```php
<?php
  $drones = array("Graham", "Julian", "Nick", "Paul");
  var_dump($drones);
?>
```

该脚本的输出看起来像这样：

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

`var_dump()` 函数作为一种基本的调试技术被大量使用，因为它是将变量数据打印到屏幕以进行验证的最简单方法。

最后，我们简要讨论正则表达式，重点在于*简要*，因为正则表达式语法在本书的其他地方有介绍，而唯一与 PHP 相关的独特之处是你将用来运行表达式的函数。你可以选择 Perl-Compatible Regular Expressions (PCRE) 或 POSIX Extended 正则表达式，但在提供的功能方面，它们之间实际上几乎没有区别。对于这一章，我们将使用 PCRE 表达式，因为据我们所知，其他 PHP 程序员更多地使用它们。

主要的 PCRE 函数是 `preg_match()`、`preg_match_all()`、`preg_replace()` 和 `preg_split()`。我们将从 `preg_match()` 开始，因为它提供最基本的功能，如果一个字符串匹配正则表达式则返回 *true*。`preg_match()` 的第一个参数是你想要搜索的正则表达式，第二个参数是要匹配的字符串。因此，如果我们想检查一个字符串是否包含单词 *Best*、*Test*、*rest*、*zes* 或其他包含 *est* 的单词，前面跟着任意大小写的任何字母，我们可以使用以下 PHP 代码：

```php
$result = preg_match("/[A-Za-z]est/", "This is a test");
```

因为测试字符串匹配表达式，$result 被设置为 *1*（true）。如果你将字符串更改为不匹配的结果，你会得到 *0* 作为返回值。

下一个函数是 `preg_match_all()`，它给出它找到的所有匹配项的数组。然而，为了最有用的，它取一个数组作为引用参数来填充匹配项，并将其返回值保留为找到的匹配项数量。

我们建议你先使用 `preg_match_all()` 和 `var_dump()` 来感受一下该函数的工作方式。这个例子是一个好的起点：

```php
<?php
  $string = "This is the best test in the west";
  $result = preg_match_all("/[A-Za-z]est/", $string, $matches);
  var_dump($matches);
?>
```
