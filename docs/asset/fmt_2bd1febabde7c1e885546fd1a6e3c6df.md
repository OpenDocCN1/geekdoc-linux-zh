
这个循环遍历我们之前创建的 `$myarr` 数组，将每个值放入 `$value` 变量中。我们可以修改它以便同时从数组中获取键和值，如下：

```php
<?php

foreach($myarr as $key => $value) {
    echo "$key is set to $value\n";
}

?>
```

# PHP 简介

正如你所猜到的，这些数组的键进入 `$key`，数组值进入 `$value`。`foreach` 循环的一个重要特性是它从数组的开始到结束，然后停止——这里说的“开始”是指添加的第一个项目，而不是最小的索引数字。这个脚本展示了这种行为：

```php
<?php

$array = [6 => "Hello", 4 => "World", 2 => "Wom", 0 => "Bat\n"];

foreach($array as $key => $value) {
    echo "$key is set to $value\n";
}

?>
```

如果你尝试这个脚本，你会发现 `foreach` 按照 6, 4, 2, 0 的原始顺序打印数组，而不是 0, 2, 4, 6 的数字顺序。

`do...while` 循环的作用与 `while` 循环类似，但条件出现在代码块的末尾。这种微小的语法差异意义重大，因为 `do...while` 循环至少会被执行一次。考虑这个脚本：

```php
<?php

$i = 10;

do {
    $i -= 1;
    echo $i;
} while ($i < 10);

?>
```

在不运行脚本的情况下，你认为它会做什么？

```php
break;
case 4:
    echo "Cat age is 4";
    break;
default:
    echo "Cat age is unknown";
}

?>
```

虽然只短了一点点，但可读性高得多，也更容易维护。`switch/case` 组由 `switch()` 语句组成，在其中你提供想要检查的变量，后面跟着许多 `case` 语句。注意每个 `case` 结尾的 `break` 语句。如果没有它，PHP 将执行每一个匹配的 `case` 语句。调用 `break` 会导致 PHP 退出 `switch/case`。同样注意最后有一个 `default` 情况，用于捕获所有没有匹配 `case` 的情况。

重要的是不要使用 `case default:`，而要使用 `default:`。此外，它是最后一个标签，所以不需要 `break` 语句，因为 PHP 在那里会自动退出 `switch/case` 块。

# 循环

PHP 有四种可以多次执行代码块：`while`、`for`、`foreach` 和 `do...while`。在这四种方法中，只有 `do...while` 很少使用；其他的都很流行，你肯定会在别人的脚本中遇到它们。

最基础的循环是 `while` 循环，只要给定的条件为真，它就会执行代码块。因此，我们可以用下面这段 PHP 代码写一个无限循环——一个永远运行的代码块：

```php
<?php

$i = 10;

while ($i >= 0) {
    $i += 1;
    echo $i;
}

?>
```
