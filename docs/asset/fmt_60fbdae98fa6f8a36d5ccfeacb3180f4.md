
最易用的是 `array_unique()`，它接收一个数组作为唯一参数，并返回一个除了所有重复值后的相同数组。在“你不需要代码示例”的领域是 `shuffle()` 函数，它接收一个数组作为参数并随机化元素的顺序。请注意，`shuffle()` 不返回随机后的数组；它使用你的参数作为引用并直接对其进行采样。太易于演示的函数是 `in_array()`，它接收一个值作为第一个参数，一个数组作为第二个参数，如果该值在数组中则返回 `true`。

处理完这些后，我们可以关注更有趣的函数，其中两个是 `array_keys()` 和 `array_values()`。它们都接收一个数组作为唯一参数，并分别返回由数组中的键或数组中的值组成的新数组。`array_values()` 函数是创建一个相同数据的新数组的简便方法，只是没有了键。如果你对数组键进行了编号、删除了元素并需要重新排序，通常会用到它。

`array_keys()` 创建一个新数组，其值是原数组的键，如下：

```php
<?php
$myarr = array("foo" => "red", "bar" => "blue", "baz" => "green");
$mykeys = array_keys($myarr);
foreach($mykeys as $key => $value) {
    echo "$key = \$value\n";
}
?>
```

这会输出 "0 = foo, 1 = bar, 2 = baz."

有几个函数专门用于数组排序，但只有两个被频繁使用：即 `asort()` 和 `ksort()`，前者按值对数组进行排序，后者按键对数组进行排序。给定上一个示例中的数组 `$myarr`，按值排序将产生一个元素顺序为 bar/blue, baz/green, foo/red 的数组。按键排序将得到元素顺序为 bar/blue, baz/green, foo/red。与 `shuffle()` 函数一样，`sort()` 和 `ksort()` 都是原地操作的，这意味着它们不返回值，而是直接修改你传递的参数。为了兴趣起见，你也可以使用 `asort()` 和 `krsort()` 分别进行反序排序和键排序。

这段代码示例按值对数组排序并像以前一样打印它：

```php
$myarr = array("foo" => "red", "bar" => "blue", "baz" => "green");
sort($myarr);
foreach($myarr as $key => $value) {
    echo $key = $value\n;
}
?>
```

之前在讨论常量时，我们提到 `extract()` 函数，它能将数组转换为独立的变量；现在是时候开始使用它了。你需要提供三个变量：要提取的数组、你希望为变量加什么前缀、以及你使用的前缀。从技术上讲，最后一个参数是可选的，但在实践中，你应该使用它们来正确为你的变量命名空间并保持它们整洁。

第二个参数可以是以下值之一：

- `EXTR_WRITE`—如果变量已存在，则覆盖它。
- `EXTR_SKIP`—如果变量已存在，则跳过它并处理下一个变量。
- `EXTR_PREFIX_SAME`—如果变量已存在，则使用第三个参数指定的前缀。
- `EXTR_PREFIX_ALL`—无论变量是否已存在，都为所有变量加上第三个参数中的前缀。
- `EXTR_PREFIX_INVALID`—仅当变量名无效时（例如以数字开头）才使用前缀。
- `EXTR_IF_EXISTS`—仅提取已经存在的变量。

你还可以可选地使用位或运算符 `|` 增加到 `EXTR_REFS` 中，以便让 `extract()` 对提取的变量使用引用。通常情况下，首选 `EXTR_PREFIX_ALL`，因为它能保证结果。只有当你需要修改变量并让更改反映在数组中时，才需要 `EXTR_REFS`。

接下来的脚本使用 `extract()` 将 `$myarr` 转换为独立的变量 `$arr_foo`、`$arr_bar` 和 `$arr_baz`：

```php
<?php
$myarr = array("foo" => "red", "bar" => "blue", "baz" => "green");
extract($myarr, EXTR_PREFIX_ALL, 'arr');
?>
```

注意数组键是 "foo", "bar", "baz"，前缀是 "arr"，但最终变量是 `$arr_foo`、`$arr_bar` 和 `$arr_baz`。PHP 在前缀和数组键之间插入下划线。

## 文件

正如你从书中其他地方学到的，UNIX 哲学是万物皆文件。在 PHP 中情况也是如此：一组基本的文件函数适用于打开和操作文件，但这些相同的函数也可以用于打开和操作网络套字。我们在这里这两者都涵盖。

两个基础的文件读写函数让这些基本操作变得简单。是 `file_get_contents()`，它接收文件名作为参数并返回文件内容；以及 `file_put_contents()`，它接收文件名作为第一个参数，要写入的数据作为第二个参数。

使用这两个函数，我们可以轻松编写一个读取 `filea.txt` 并写入 `fileb.txt` 的脚本：

```php
<?php
$text = file_get_contents("filea.txt");
file_put_contents("fileb.txt", $text);
?>
```

由于 PHP 允许我们像处理文件一样处理网络 socket，我们还可以使用 `file_get_contents()` 读取文本，如下：

```php
<?php
$text = file_get_contents("http://www.php.net"); // 此处仅为示例逻辑
?>
```

`file_get_contents()` 的问题是它会一次性将整个文件加载到内存中；对于大文件，这是不可行的。替代方案是分段加载文件，可以通过以下函数实现：`fopen()`、`fclose()`、`fread()` 和 `feof()`。

当你调用 `fopen()` 时，应该存储其返回值。这是一个被称为 *句* 的资源，其他函数都需要它。例如，`fread()` 函数接收句作为第一个参数，要读取的字节数作为第二个参数，返回内容。`fclose()` 函数接收句作为唯一参数并释放文件。

所以，我们可以写一个简单的循环来打开文件、分段读取、打印片段并关闭句：

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

剩下的就是 `fwrite()` 函数，它接收文件句作为第一个参数，要写入的字符串作为第二个参数。你还可以提供一个整数作为第三参数，指定想要写入字符串的字节数，但如果你排除此项，`fwrite()` 会写入整个字符串。

如果你记得，可以使用 `fopen()` 的第二个参数向文件追加数据。所以我们可以结合 `fwrite()` 使用每次执行都向文件添加文本行的脚本：

```php
<?php
$file = fopen("filea.txt", "ab");
fwrite($file, "Testing\n");
fclose($file);
?>
```

## 基础函数

- `r`—只读；它覆盖文件
- `r+`—读写；它覆盖文件
- `w`—只写；它删除现有内容并覆盖文件
- `w+`—读写；它删除现有内容并覆盖文件
- `a`—只写；它追加到文件末
- `a+`—读写；它追加到文件末
- `x`—只写，但仅当文件不存在时创建
- `a+`—读写，但仅当文件不存在时创建

可选，你可以添加 `b`（例如 `a+b` 或 `rb`）来切换到二进制模式。如果你希望你的脚本及其写入的文件在不同平台上平滑运行，建议这样做。

# 第 32 章 编写 PHP 脚本

为了让脚本变得更有趣，我们可以引入一个新函数 `filesize()`，它接受一个文件名（不是文件句柄，而是实际文件名字符串）作为唯一参数，并返回文件以字节为单位的大小。使用这个新函数可以将脚本变成如下所示：

```php
<?php
$file = fopen("filea.txt", "ab");
fwrite($file, "The filesize was " . filesize("filea.txt") . "\n");
close($file);
?>
```

虽然 PHP 会自动为你清理文件句柄，但最好还是由自己使用 `fclose()`，以确保你始终掌控一切。

## 杂项

有几个函数不属于其他类别，在这里将进行介绍。第一个是 `isset()`，它接受一个或多个变量作为参数，如果这些变量已设置，则返回 `true`。需要注意的是，如果变量的值被设置为会被评估为 `false` 的值（例如 `0` 或空字符串），`isset()` 仍然会返回 `true`，因为它并不检查变量的值。它只是检查变量是否已设置，这也是其命名的由来。
