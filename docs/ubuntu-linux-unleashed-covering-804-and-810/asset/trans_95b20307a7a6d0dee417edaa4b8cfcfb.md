
- a—只写；追加到文件
- a+—读写；追加到文件
- x—只写，但仅当文件不存在时
- x+—读写，但仅当文件不存在时

你也可以选择添加 b（例如 a+b 或 rb）来切换到二进制模式。如果你希望脚本及其写入的文件能在其他平台上顺利运行，建议这样做。

调用 fopen() 时，应该存储它的返回值。这是一个称为文件句柄的资源，其他文件函数都需要用它来完成工作。例如，fread() 函数将文件句柄作为第一个参数，将要读取的字节数作为第二个参数，并在返回值中返回内容。fclose() 函数只接受文件句柄作为唯一参数，并释放该文件。

因此，我们可以编写一个简单的循环来打开文件，逐块读取，打印这些块，然后关闭句柄：

```
<?php
$file = fopen("filea.txt", "rb");
while (!feof($file)) {
    $content = fread($file, 1024);
    echo $content;
}
fclose($file);
?>
```

这样就只剩下 fwrite() 函数了，它接受文件句柄作为第一个参数，要写入的字符串作为第二个参数。你还可以提供第三个整数参数，指定要写入该字符串的字节数，但如果你省略此参数，fwrite() 将写入整个字符串。

如果你还记得，可以使用 a 作为 fopen() 的第二个参数来向文件追加数据。因此，我们可以将其与 fwrite() 结合使用，让脚本在每次执行时向文件添加一行文本：

```
<?php
$file = fopen('filea.txt', "ab");
fwrite($file, "Testing\n");
fclose($file);
?>
```

为了让这个脚本更有趣一些，我们可以引入一个新函数 filesize()，它只接受一个文件名（不是文件句柄，而是实际的文件名字符串）作为参数，并以字节为单位返回文件的大小。使用这个新函数后，脚本变成：

```
<?php
$file = fopen("filea.txt", "ab");
fwrite($file, "The filesize was " . filesize("filea.txt") . "\n");
fclose($file);
?>
```

尽管 PHP 会自动为你清理文件句柄，但最好还是自己使用 fclose()，这样你始终能掌控一切。

## 杂项

有几个函数不属于其他类别，因此在这里介绍。第一个是 isset()，它接受一个或多个变量作为参数，如果这些变量已被设置，则返回 true。需要注意的是，一个变量即使被设置为会被求值为 false 的值（例如 0 或空字符串），isset() 仍然返回 true，因为它不检查变量的值，而只是检查它是否被设置；这正是它名字的由来。

unset() 函数同样接受一个或多个变量作为参数，简单地删除变量并释放内存。有了这两个函数，我们可以编写一个脚本来检查变量是否存在，如果存在就删除它（参见清单 25.5）。

### 清单 25.5 设置和取消设置变量

```
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

该脚本运行了两次相同的 isset() 检查，但在第一次检查后就 unset() 了该变量。因此，它会先输出 "Name was set to Ildiko"，然后输出 "Name was not set"。

也许 PHP 中最常用的函数是 exit，尽管纯粹主义者会告诉你它实际上是一种语言结构，而不是函数。exit 一旦执行，就会立即终止脚本的处理，这意味着后续的代码行不会被执行。其实就这么简单；它几乎不值得一个示例，但为了确保无误，这里还是给出一个：

```php
<?php
    exit;
    echo "Exit is a language construct\n";
?>
```

该脚本不会输出任何内容，因为 exit 在 echo 之前。

我们可以保证你一定会经常使用的一个函数是 var_dump()，它将变量的信息（包括它的值）转储到屏幕上。这对于数组来说尤其宝贵，因为它会打印每一个值，如果其中有一个或多个元素是数组，它还会打印出这些数组的所有元素，依此类推。要使用这个函数，只需将一个变量作为它的唯一参数传递给它：

```php
<?php
    $drones = array("Graham", "Julian", "Nick", "Paul");
    var_dump($drones);
?>
```

该脚本的输出如下：

```text
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

var_dump() 函数作为一种基本的调试技术被广泛使用，因为它是将变量数据打印到屏幕上进行验证的最简单方法。

最后，我们简要讨论一下正则表达式，强调“简要”，因为正则表达式的语法在本书其他地方有讲解，与 PHP 相关的唯一独特之处是你用来运行这些表达式的函数。你可以选择 Perl 兼容正则表达式（PCRE）或 POSIX 扩展正则表达式，但在提供的功能方面，它们之间确实没什么可选择的。在本章中，我们使用 PCRE 表达式，因为据我们所知，其他 PHP 程序员使用它们更多。

主要的 PCRE 函数是 preg_match()、preg_match_all()、preg_replace() 和 preg_split()。我们将从 preg_match() 开始，因为它提供了最基本的功能：如果一个字符串匹配某个正则表达式，它就返回 true。preg_match() 的第一个参数是你要搜索的正则表达式，第二个参数是
