
例如，假设你有一个包含元素 "1"、"2"、"3"、"4"、"5" 和 "cool" 的数组，你想移除 "1" 元素。你会使用这段代码：

```php
$sample = array(1, 2, 3, 4, 5, "cool");
$first = array_shift($sample);
```

你可以使用下面的脚本打印 `$sample` 数组的“之前”和“之后”版本以及 `$first` 的值：

```php
<?php
// 打印之前
$sample = array(1, 2, 3, 4, 5, "cool");
echo "BEFORE:<br>";
while (list($key, $value) = each($sample)) {
    echo "$key : $value<br>";
}
// 重置指针到起始位置
reset($sample);
// 移除现有数组的开头
$first = array_shift($sample);
// 打印之后
echo "AFTER:<br>";
echo "first: $first<br>";
while (list($key, $value) = each($sample)) {
    echo "$key : $value<br>";
}
?>
```

上述脚本将输出：

```
BEFORE:
0: 1
1: 2
2: 3
3: 4
4: 5
5: cool
AFTER:
first: 1
0: 2
1: 3
2: 4
3: 5
4: cool
```

# `array_slice()`

`array_slice()` 函数的语法是：

```php
array_slice(array_name, start_position, offset, length);
```

例如，你可能有一个包含元素 "1"、"2"、"3"、"4"、"5" 和 "cool" 的数组，你想提取该数组的某些部分。示例：

```php
$sample = array(1, 2, 3, 4, 5, "cool");
// 从第二个位置开始
$slice1 = array_slice($sample, 1);
// 从第二个位置开始，到倒数第二个之前
$slice2 = array_slice($sample, 1, -1);
// 从第五个位置开始
$slice3 = array_slice($sample, 4);
// 从第一个位置开始，取 3 个元素
$slice4 = array_slice($sample, 0, 3);
```

```php
$sample = array(1, 2, 3, 4, 5, "cool");
```

```php
echo "BEFORE:<br>";
while (list($key, $value) = each($sample)) {
    echo "$key : $value<br>";
}
```

```php
// reset array pointer to first position
reset($sample);
```

```php
// extract slices of existing array
$slice1 = array_slice($sample, 1);
$slice2 = array_slice($sample, 1, -1);
$slice3 = array_slice($sample, 4);
$slice4 = array_slice($sample, 0, 3);
```

```php
// echo slice1
echo "<br>slice1 (start at 2nd position) looks like:<br>";
while (list($key, $value) = each($slice1)) {
    echo "$key : $value<br>";
}
```

```php
// echo slice2
echo "<br>slice2 (start at 2nd pos, go to next to last) looks like:<br>";
while (list($key, $value) = each($slice2)) {
    echo "$key : $value<br>";
}
```

```php
// echo slice3
echo "<br>slice3 (start at 5th pos) looks like:<br>";
while (list($key, $value) = each($slice3)) {
    echo "$key : $value<br>";
}
```

```php
// echo slice4
echo "<br>slice4 (start at 1st pos, print 3 elements) looks like:<br>";
while (list($key, $value) = each($slice4)) {
    echo "$key : $value<br>";
}
?>
```

上述脚本将输出：

# BEFORE:
+   0: 1
1: 2
2: 3
3: 4
4: 5
5: cool

slice1 (start at 2nd position) looks like:
+   0: 2
1: 3
2: 4
3: 5
4: cool

slice2 (start at 2nd pos, go to next to last) looks like:
+   0: 2
1: 3
2: 4
3: 5

slice3 (start at 5th pos) looks like:
+   0: 5
1: cool

slice4 (start at 1st pos, print 3 elements) looks like:
+   0: 1
1: 2
2: 3

# 附录 A：PHP 语言核心参考

![](img/f8bb5053a1d20d75df488da4d4dbfceb_327_0.png)

`array_merge()` 函数允许你合并两个或多个数组。

### `array_merge()`

`array_merge()` 函数的语法为：

```php
array_merge(array1, array2, ...arrays);
```

例如，假设你有一个数组包含元素 "1", "2", "3", "4", "5" 和 "cool"，另一个数组包含元素 "a", "b", "c", "d", "e" 和 "cooler"，你想你想合并这两个数组。你可以使用以下代码段：

```php
$sample1 = array(1, 2, 3, 4, 5, "cool");
$sample2 = array("a", "b", "c", "d", "e", "cooler");
$merged = array_merge($sample1, $sample2);
```

你可以使用下面的示例脚本来打印数组的“之前”和“之后”版本：

```php
<?php
// 打印之前的样本
$sample1 = array(1, 2, 3, 4, 5, "cool");
echo "BEFORE - SAMPLE1:<br>";
while (list($key,$value) = each($sample1)) {
    echo "$key : \$value<br>";
}
reset($sample1);
$sample2 = array("a", "b", "c", "d", "e", "cooler");
echo "<BEFORE - SAMPLE2:<br>";
while (list($key,$value) = each($sample2)) {
    echo "$key : \$value<br>";
}
reset($sample2);
// 合并 $sample1 和 $sample2
$merged = array_merge($sample1, $sample2);
// 打印之后的
echo "<AFTER:<br><br>";
while (list($key,$value) = each($merged)) {
    echo "$key : $value<br>";
}
?>
```
