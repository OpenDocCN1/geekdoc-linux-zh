

## 随机数

在编程中，始终需要生成随机数。这不仅对于需要在游戏期间引入一定变化的电脑游戏至关重要，对于加密和安全通信也极为重要。

PHP 提供两种生成随机数的方法：速度快且更具可预测性，速度慢且不易预测。请记住，真正的随机性在计算机上很难实现，因此许多人将随机数生成器称为*伪随机*，意思是它们看起来是随机的，但并非真正随机。

基本的随机数生成器是*rand()*函数，它接受两个数字作为参数：您想要的最低随机数和最高随机数。因此，使用*rand(1, 10)*可能返回 1、10 或两者之间的任何整数。“更随机”的随机数生成器使用梅森旋转算法（Mersenne Twister），因此被称为*mt_rand()*。如果您只是想在网站访问者每次访问主页时打印一条不同的问候语，*rand()*就足够了！

列表 31.7 演示了一个使用*rand()*函数的脚本，但你可以通过用*mt_rand()*替换*rand()*切换到梅森旋转算法。

### 列表 31.7 变化访客的问候语

```php
<?php
    switch (rand(1,4)) {
        case 1:
            echo "Hello!";
            break;
        case 2:
            echo "Welcome!";
            break;
        case 3:
            echo "Greetings!";
            break;
        case 4:
            echo "Salutations!";
            break;
    }
?>
```

## 数组

处理数组并非易事，但 PHP 通过提供一组可以排序、洗牌、取交集和过滤数组的函数使其变得更容易。与其他函数一样，这里只能选择一些进行介绍；这绝不意味着是 PHP 数组函数的完整参考。

最简单使用的函数是*array_unique()*，它接受一个数组作为唯一参数，并返回去除所有重复值后的相同数组。同样处于“简单到不需要代码示例”领域的还有*shuffle()*函数，它接受一个数组作为参数，并随机化其元素的顺序。请注意，`shuffle()`不会返回随机化后的数组；它使用您的参数作为引用并直接对其打乱。最后一个太简单而无法演示的函数是`in_array()`，它接受一个值作为第一个参数，一个数组作为第二个参数，如果该值在数组中则返回 true。

处理完这些之后，我们可以关注更有趣的函数，其中两个是`array_keys()`和`array_values()`。它们都接受一个数组作为唯一参数，分别返回由数组中的键或值组成的新数组。`array_values()`函数是一种创建相同数据新数组的简单方法，只是没有键。这通常用于当你给数组键编号，删除了多个元素，并希望重新排序时。

`array_keys()`函数创建了一个新数组，其中的值是旧数组中的键，如下所示：

```php
<?php
  $myarr = array("foo" => "red", "bar" => "blue", "baz" => "green");
  $mykeys = array_keys($myarr);
  foreach($mykeys as $key => $value) {
    echo "$key = $value\n";
  }
?>
```

这会打印 "0 = foo"、"1 = bar" 和 "2 = baz"。

有几个函数专门用于数组排序，但只有两个经常使用：`asort()`和`ksort()`，前者按值排序数组，后者按键排序数组。给定上一个示例中的数组`$myarr`，按值排序将生成一个元素顺序为 bar/blue、baz/green 和 foo/red 的数组。按键排序将给出元素顺序为 bar/blue、baz/green 和 foo/red。与`shuffle()`函数一样，`asort()`和`ksort()`都是就地完成工作，意味着它们不返回值，直接改变你传入的参数。出于兴趣起见，你还可以使用`arsort()`和`krsort()`分别进行反向值排序和反向键排序。

下面的代码示例按值反向排序数组，然后如前所述打印它：

```php
<?php
  $myarr = array("foo" => "red", "bar" => "blue", "baz" => "green");
  arsort($myarr);
  foreach($myarr as $key => $value) {
    echo "$key = $value\n";
  }
?>
```

之前在讨论常量时，我们提到了`extract()`函数，它可以将数组转换为独立变量；现在是时候真正开始使用它了。你需要提供三个变量：你要提取的数组、你希望变量如何前缀，以及你希望使用的前缀。从技术上讲，最后两个参数是可选的，但实际操作中你应该始终使用它们来正确命名空间你的变量并保持其组织性。

第二个参数必须是以下之一：

- `EXTR_OVERWRITE`—如果变量已经存在，则覆盖它。
- `EXTR_SKIP`—如果变量已经存在，则跳过并移动到下一个变量。
- `EXTR_PREFIX_SAME`—如果变量已经存在，则使用第三个参数中指定的前缀。
- `EXTR_PREFIX_ALL`—无论是否已经存在，都使用第三个参数中的前缀为所有变量添加前缀。
- `EXTR_PREFIX_INVALID`—仅当变量名称无效（例如，以数字开头）时使用前缀。
- `EXTR_IF_EXISTS`—仅提取已经存在的变量。我们从未见过这种用法。

你还可以选择性地使用按位 OR 运算符`|`，加入`EXTR_REFS`，使`extract()`对提取的变量使用引用。在一般使用中，`EXTR_PREFIX_ALL`更受青睐，因为它保证命名空间。只有当你需要能够改变变量并让这些改变反映在数组中时，才需要`EXTR_REFS`。

下一个脚本使用`extract()`将`$myarr`转换为独立变量`$arr_foo`、`$arr_bar`和`$arr_baz`：

```php
<?php
    $myarr = array("foo" => "red", "bar" => "blue", "baz" => "green");
    extract($myarr, EXTR_PREFIX_ALL, 'arr');
?>
```

请注意，数组键是 "foo"、"bar" 和 "baz"，前缀是 "arr"，但最终的变量将是`$arr_foo`、`$arr_bar`和`$arr_baz`。PHP 在前缀和数组键之间插入一个下划线。

我们要查看的最后一组函数用于数组游标，之前已经提到过。如果你还记得，数组游标是一个指向当前数组元素的不可见指针，但什么定义了当前元素？

默认情况下，这是数组中的第一个元素，但你可以通过`prev()`、`next()`、`end()`和`reset()`移动数组游标。前两个分别将游标向后移动一个位置和向前移动一个位置，每次返回游标处的值。后两个分别将游标移动到数组的最后一个元素和第一个元素，返回该位置的值。此外，`current()`函数返回当前由数组游标指向的值。

列表 31.8 演示了这四个函数的工作情况。

### 列表 31.8 使用数组游标浏览数组

```php
<?php
$array = array("first\n", "second\n", "third\n", "fourth\n", "fifth\n");
echo current($array);
echo next($array);
echo next($array);
echo end($array);
echo prev($array);
echo reset($array);
?>
```

其输出如下：

- first
- second
- third
- fifth
- fourth
- first

当`foreach`循环不切实际时，数组游标经常被使用，这种情况相当罕见。

## 文件

正如你将从本书其他地方学到的那样，UNIX 哲学是一切都是文件。在 PHP 中也是如此：一组基本的文件函数适合打开和操作文件，但相同的函数也可以用于打开和操作网络套接字。我们在这里涵盖这两者。

文件的两个基本读写功能使执行这些基本操作变得简单。它们是`file_get_contents()`，它接受文件名作为唯一参数并返回文件内容作为字符串，以及`file_put_contents()`，它接受文件名作为第一个参数，要写入的数据作为第二个参数。

使用这两个函数，我们可以编写一个脚本，从文件`filea.txt`读取所有文本，并将其写入另一个文件`fileb.txt`：

```php
<?php
$text = file_get_contents("filea.txt");
file_put_contents("fileb.txt", $text);
?>
```

由于 PHP 允许我们将网络套接字视为文件，我们也可以使用`file_get_contents()`从网站读取文本，如下所示：

