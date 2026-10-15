
- `array_splice`—例如，`$arr1=array_slice($arr, $pos, $n, $newarr);` 将从 `$arr` 中从 `$pos` 开始的 `$num` 个 元素提取出来，并用元素 `$newarr` 中的元素替换它们。返回的数组包含了被替换的元素。

- `array_values`—例如，`$values = array_values($arr);` 将返回一个非关联数组，其中仅包含 `$arr` 的值。

- `in_array`—例如，`in_array($elem, $arr);` 将检查 `$elem` 是否在 `$arr` 内部。如果找到返回 TRUE，否则返回 FALSE。

这里是一个使用 `sort` 的示例：

```php
<?PHP
// 我们假设我们有一个包含整数的数组 Arr
// 我们使用我们的比较函数进行排序（这将
// 产生一个倒序排序）
// 然后我们打印结果
usort($arr, "compare");
foreach ($arr as $key=>$elem)
    echo "$key=$elem";
function compare($sa, $b) {
    if ($sa==$b)
        return 0;
    elseif ($sa < $b)
        return 1;
    else
        return -1;
}
?>
```

# PHP 程序结构与控制流

PHP 程序基本上是一组指令。可以使用大括号将指令分组在一个块（block）中，正如我们在 `foreach` 示例中看到的那样。将指令分组在单个块中允许将整个块视为单个指令。这种行为在循环中特别有用，正如我们之前看到的 true。

# 条件

你可以根据自己的条件让程序在程序中选择不同的路径。你可以使用 `if... elseif...else` 语句来实现。基本结构如下：

```php
if (condition)
instruction1;
elseif (condition2)
instruction2;
else
instruction3;
```

每个条件都应该是一个布尔表达式。如果 `condition` 为真，则执行 `instruction1`，程序跳转到 `instruction3` 之后的指令。如果为假，则测试 `condition2`；如果为真，执行 `instruction2`；如果为假，将运行 `instruction3`。注意，你可以使用任意数量的 `elseif`，甚至省略它。在 `if...else` 块中不应该多于一个 `else`。注意，任何 `else` 或 `elseif` 都会引用上一个创建的且没有 `else/elseif` 的 `if` 或 `elseif`。为了避免在所有的 `if` 和 `else` 语句中迷路，最好的办法是将每个写在它所引用的 `if` 下方。检查这个示例：

```php
<?php
if ($a < $b) // 检查 $a 是否小于 $b
echo $a. " is less than " .$b;
elseif ($a > $b) // 只有当 $a 不
//小于 $b 时我们才会这里
echo $b. " is less than " .$a;
else // $a 既不小于大于 $b
echo $a. " is equal to " .$b;
?>
```

注意！！如果你想比较相等性，请确保使用双等号或三等号检查相等或相同的变量。看这个示例：

```php
<?php
if ($i = 34567)
echo "This is always true!!!";
?>
```

记住 FALSE 等于 0，因此只有当条件等于 0 时，条件才被视为 FALSE。执行 `($i = 34567)` 会将 34567 复制到 `$i` 内部并检查 `$i` 的值。如果 `$i` 不同于 0，它将被视为 TRUE。

每个 `if...elseif...else` 组都作为一个单一指令工作。检查这个示例：

```php
<?php
if ($a < 100) // 第一个条件
if ($b < 100) // 这个语句是
    // 块的开头，如果第一个
    // 指令为真则运行
    echo "both numbers are less than 100";
else // 这个 else 指向上一个 if，并且
    // 仍然是第一个
    // 条件内部同一个块的一部分
    echo "Only the first number is less than 100";
elseif ($a == 100) // 上一个 if 完成了
    // 第二 if
    // 块，所以这个 elseif 指向第一个
    // 条件
    echo "The first number was 100";
else // 这个 else 指向 elseif，并且是
    // 从第一个条件开始的
    // 块
    echo "The first number was greater than 100";
?>
```

通过简单使用大括号以便查看每个块，你可以避免头疼和困惑。通用结构看起来像：

`if (condition)`

{ 如果为真则执行语句

}

`elseif (condition2)`

{ 如果 `condition` 为假且 `condition2` 为真则执行语句

}

`elseif (condition3)`

{ 如果 `condition` 和 `condition2` 为假但 `condition3` 为真则执行语句

}

`else`

{ 如果所有条件为假则执行语句

}

有很多嵌套 `if` 或 `elseif` 语句通常被认为是糟糕编程习惯。如果你试图寻找变量的匹配项，你可以使用不同的替代方案：`switch... case`。`switch...else` 的通用语法如下：

```php
switch ($variableToCheck) {
    case value1:
        statements
        break;
    case value2:
        statements
        break;
    default:
        statements
}
```

程序将连续比较 `$variableToCheck` 与写在 `case` 关键字旁的所有不同值。如果找到匹配项，程序将运行位于后续冒号符号之间的每个指令。

程序将连续比较 `$variableToCheck` 与写在 `case` 关键字旁的所有不同值。如果找到匹配项，程序将运行位于后续冒号符号之间的每个指令。程序将连续比较 `$variableToCheck` 与写在 `case` 关键字旁的所有不同值。如果找到匹配项，程序将运行位于后续冒号符号之间的每个指令。
