
- `a+`—读和和写；它会追加到文件

- `x`—只写，但仅当文件不存在时

- `a+`—读和和写，但仅当文件不存在时

可选地，你可以添加 `b`（例如 `a+b` 或 `rb`）来切换到二进制模式。如果你写的脚本及其写入的文件在其他平台上平流畅运行，则建议这样做。

当你调用 `fopen()` 时，你应该存储它的返回值。它是一个被称为“文件句柄”的资源，其他文件函数需要它来完成工作。例如，`fread()` 函数将文件句柄作为第一个参数，将读取的字节数作为第二个参数，并在返回值中返回内容。`fclose()` 函数将文件句柄作为唯一参数并释放文件。

因此，我们可以写一个简单的循环来打开文件、分段读取、打印这些片段，然后关闭句柄：

```php
<?php
$file = fopen("filea.txt","rb");
while(!eof($file)) {
    $content = fread($file, 1024);
    echo $content;
}
fclose($file);
?>
```

剩下的只有 `fwrite()` 函数，它将文件句柄作为第一个参数，将要写入的字符串作为第二个参数。你也可以提供一个整数作为第三个参数，指定你想要写入字符串的字节数，但如果你省略了这一项，`fwrite()` 将写入整个字符串。

如果你还记得的话，你可以使用 `a` 作为 `fopen()` 的第二个参数来向文件追加数据。因此，我们可以结合 `fwrite()` 使用，编写一个脚本，该脚本在每次执行时都会向文件中添加有一行文本：

```php
<?php
$file = fopen("filea.txt","ab");
fwrite($file, "Testing\n");
fclose($file);
?>
```

为了让该脚本更有趣，我们可以引入一个新函数 `filesize()`，它接受一个文件名（不是文件句柄，而是实际文件名字符串）作为唯一参数，并返回文件的字节大小。使用这个新函数后，脚本变成了这样：

```php
<?php
$file = fopen("filea.txt", "ab");
fwrite($file,"The filesize was " . filesize("filea.txt") . "\n");
fclose($file);
?>
```

尽管 PHP 会自动为你清理文件句柄，但最好还是自己使用 `fclose()`，这样你就能始终保持控制。

# 杂杂项

有几个函数不属于其他类别，因此在这里进行了介绍。第一个函数是 `isset()`，它接受一个或多个变量作为参数，如果它们已被设置则返回 `true`。需要注意的是，一个值被设置为某些值的变量（例如 0 或空字符串）会被评估为 `false`——但 `isset()` 仍然会返回 `true`，因为它并不检查变量的值。它只检查它是否被设置；在这里，即变量名。

`unset()` 函数也接受一个或多个变量作为参数，简单地删除该变量并释放内存。通过这两个函数，我们可以编写一个脚本来检查变量是否存在，如果存在则将其删除（参见列表 32.5）。

# 列表 32.5 设置和取消设置变量

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

该脚本运行了两次 `isset()` 检查，但在第一次检查后 `unset()` 了该变量。因此，它会先打印 "Name was set to Ildiko"，然后打印 "Name was not set"。

PHP 中可能最频繁使用的函数也许是 `exit`，尽管纯主义者会告诉你，它实际上是一个语言结构而不是函数。`exit` 在执行时会立即终止脚本的处理，这意味着后续的代码行将不会执行。这其实就是全部了；它几乎不值得举例说明，但这里有一个以确保你理解了它：

```php
<?php
exit;
echo "Exit is a language construct!\n";
?>
```

我们可以保证你经常使用的一个函数是 `var_dump()`，它会将变量的信息（包括它的值）转到屏幕上。这对于数组来说非常有价值的，因为它会打印每一个值，如果其中一个或多个元素是数组，它会打印它们的所有元素，依此类推。要使用此函数，只需将变量作为唯一参数传递给它：

```php
<?php
$drones = array("Graham", "Julian", "Nick", "Paul");
var_dump($drones);
?>
```

该脚本的输出如下：

```
array(4) {
[0]->
string(6) "Graham"
[1]->
string(6) "Julian"
[2]->
string(4) "Nick"
[3]->
string(4) "Paul"
}
```

`var_dump()` 函数被广泛使用，它可以看到关于变量的信息，包括它的值，并输出到屏幕上。这对于数组非常有价值，因为它会打印每一个值，如果其中一个或多个元素是数组，它会打印它们的所有元素，依此类推。要使用此函数，只需将变量作为唯一参数传递给它：

```php
<?php
$drones = array("Graham", "Julian", "Nick", "Paul");
var_dump($drones);
?>
```

该脚本的输出如下：

```
array(4) {
[0]->
string(6) "Graham"
[1]->
string(6) "Julian"
[2]->
string(4) "Nick"
[3]->
string(4) "Paul"
}
```

`var_dump()` 函数被广泛使用，它可以看到关于变量的信息，包括它的值，并输出到屏幕上。这对于数组非常有价值，因为它会打印每一个值，如果其中一个或多个元素是数组，它会打印它们的所有元素，依此类推。要使用此函数，只需将变量作为唯一参数传递给它：

```php
<?php
$drones = array("Graham", "Julian", "Nick", "Paul");
var_dump($drones);
?>
```

该脚本的输出如下：

```
array(4) {
[0]->
string(6) "Graham"
[1]->
string(6) "Julian"
[2]->
string(4) "Nick"
[3]->
string(4) "Paul"
}
```

`var_dump()` 函数被广泛使用，它可以看到关于变量的信息，包括它的值，并输出到屏幕上。这对于数组非常有价值，因为它会打印每一个值，如果其中一个或多个元素是数组，它会打印它们的所有元素，依此类推。要使用此函数，只需将变量作为唯一参数传递给它：

```php
<?php
$drones = array("Graham", "Julian", "Nick", "Paul");
var_dump($drones);
?>
```

该脚本的输出如下：

```
array(4) {
[0]->
string(6) "Graham"
[1]->
string(6) "Julian"
[2]->
string(4) "Nick"
[3]->
string(4) "Paul"
}
```

`var_dump()` 函数被广泛使用，它可以看到关于变量的信息，包括它的值，并输出到屏幕上。这对于数组非常有价值，因为它会打印每一个值，如果其中一个或多个元素是数组，它会打印它们的所有元素，依此类推。要使用此函数，只需将变量作为唯一参数传递给它：

```php
<?php
$drones = array("Graham", "Julian", "Nick", "Paul");
var_dump($drones);
?>
```

该脚本的输出如下：

```
array(4) {
[0]->
string(6) "Graham"
[1]->
string(6) "Julian"
[2]->
string(4) "Nick"
[3]->
string(4) "Paul"
}
```

`var_dump()` 函数被广泛使用，它可以看到关于变量的信息，包括它的值，并输出到屏幕上。这对于数组非常有价值，因为它会打印每一个值，如果其中一个或多个元素是数组，它会打印它们的所有元素，依此类推。要使用此函数，只需将变量作为唯一参数传递给它：

```php
<?php
$drones = array("Graham", "Julian", "Nick", "Paul");
var_dump($drones);
?>
```

该脚本的输出如下：
