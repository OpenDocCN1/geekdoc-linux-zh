

当你调用 fopen() 时，你应该保存其返回值。它是一个称为文件句柄的资源，其他文件函数都需要它来完成工作。例如，fread() 函数以文件句柄作为第一个参数，以要读取的字节数作为第二个参数，并将内容返回在其返回值中。fclose() 函数以文件句柄作为唯一参数并释放该文件。

因此，我们可以写一个简单的循环来打开文件，分块读取它，打印这些块，然后关闭句柄：

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

这就只剩下 fwrite() 函数了，它以文件句柄作为第一个参数，以要写入的字符串作为第二个参数。你也可以提供一个整数作为第三个参数，指定你想写入的字符串的字节数，但如果省略此参数，fwrite() 会写入整个字符串。

如果记得的话，你可以使用 a 作为 fopen() 的第二个参数来向文件追加数据。因此，我们可以将它与 fwrite() 结合起来，编写一个每次执行时都会向文件添加一行文本的脚本：

```
<?php
$file = fopen("filea.txt", "ab");
fwrite($file, "Testing\n");
fclose($file);
?>
```

为了让该脚本更有趣一些，我们可以加入一个新函数 filesize()，它以文件名（不是文件句柄，而是实际的文件名字符串）作为唯一参数，并返回文件的大小（以字节为单位）。使用这个新函数后，脚本变为如下：

```
<?php
$file = fopen("filea.txt", "ab");
fwrite($file, "The filesize was " . filesize("filea.txt") . "\n");
fclose($file);
?>
```

尽管 PHP 会自动为你清理文件句柄，但最好还是自己使用 fclose()，这样你才能始终保持控制。

## 杂项

有几个函数不属于其他类别，因此在此介绍。第一个是 isset()，它接受一个或多个变量作为参数，如果这些变量已被设置则返回 true。需要注意的是，一个变量的值被设置为会被求值为 false 的内容——例如 0 或空字符串——isset() 仍然返回 true，因为它不检查变量的值。它仅仅检查变量是否已设置；因此得名。

unset() 函数也接受一个或多个变量作为参数，简单地删除该变量并释放内存。借助这两个函数，我们可以编写一个脚本来检查变量是否存在，如果存在则删除它（参见清单 29.5）。

### LISTING 29.5 Setting and Unsetting Variables

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

该脚本运行了两次相同的 isset() 检查，但在第一次检查后 unset() 了该变量。因此，它会打印 "Name was set to Ildiko" 然后打印 "Name was not set"。

PHP 中使用频率最高的函数可能是 exit，尽管纯粹主义者会告诉你它实际上是语言结构而不是函数。exit 在执行后立即终止脚本的处理，意味着后续代码行不会被执行。这就是全部内容；它几乎不值得举例，但这里有一个例子以确保：

```
<?php
exit;
echo "Exit is a language construct!\n";
?>
```

该脚本不会打印任何内容，因为 exit 在 echo 之前。

我们可以保证你会大量使用的一个函数是 var_dump()，它会将变量的信息，包括其值，输出到屏幕上。对于数组来说这非常宝贵，因为它会打印每个值，如果其中一个或多个元素是数组，它会打印这些数组中的所有元素，以此类推。要使用此函数，只需将其唯一参数设为一个变量即可：

```
<?php
$drones = array("Graham", "Julian", "Nick", "Paul");
var_dump($drones);
?>
```

该脚本的输出如下所示：

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

var_dump() 函数作为一种基本调试技术被广泛使用，因为它是将变量数据打印到屏幕以验证其是否正确最简单的方法。

最后，我们简要讨论正则表达式，重点在于简要，因为正则表达式语法在本书其他地方有介绍，而与 PHP 相关的唯一独特之处就是运行表达式时使用的函数。你可以选择 Perl 兼容正则表达式（PCRE）或 POSIX 扩展正则表达式，但在提供的功能方面两者几乎没有区别。对于本章，我们使用 PCRE 表达式，因为据我们所知，它们被其他 PHP 程序员使用的频率更高。

主要的 PCRE 函数是 preg_match()、preg_match_all()、preg_replace() 和 preg_split()。我们将从 preg_match() 开始，因为它提供了最基本的功能，通过返回 true 来判断一个字符串是否匹配正则表达式。preg_match() 的第一个参数是你想要搜索的正则表达式，第二个是匹配的字符串。因此，如果我们想检查一个字符串是否包含 Best、Test、rest、zest 或任何其他以任意大小写字母开头后跟 est 的单词，可以使用以下 PHP 代码：

```
$result = preg_match('/[A-Za-z]est/', "This is a test");
```

由于测试字符串匹配该表达式，$result 被设置为 1（true）。如果你将字符串改为不匹配的结果，返回值为 0。

