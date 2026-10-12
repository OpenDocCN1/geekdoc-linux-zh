
}
$shell_script = file('foo.sh');
$tidied_script = array_map(array('Parser', 'strip_comments'), $shell_script);

在类内部以及对象中，魔术的 self 和 $this 可以在回调中正常工作，表现正如你所期望的那样：`array($this, 'method')` 和 `array('self', 'method')` 将分别被解释为指向 `$this->method()` 和 `self::method()`。关于不允许静态函数使用 $this 等常规限制依然适用。例如：

```
// An object is able to use its own methods in array callbacks, // both on arguments passed to it and on its own properties.
$tidied_code = array_map(array($this, 'tidy'), $this->code_array);
// Class methods are also accessible as callbacks within the class.
```

如果你想检查某个给定的 $variable 的内容是否确实指定了一个可调用函数或方法，布尔函数 `is_callable($variable)` 可以说明这一点。

## array_map()

你刚才看到了 array_map() 最简单的应用之一，但它可以做得更多。

最重要的是，它可以同时操作多个数组。假设你有两个数组——$arr1 和 $arr2——你想要构建一个由 `func($arr1[0], $arr2[0])`、`func($arr1[1], $arr2[1])`、... `func($arr1[n], $arr2[n])` 组成的数组。作为循环的代码可能类似于以下内容：

```
$new_array = array(); 
for($i=0, $limit=max(count($arr1), count($arr2)); $i<$limit; $i++) { 
    $arg1 = isset($arr1[$i]) ? $arr1[$i] : null; 
    $arg2 = isset($arr2[$i]) ? $arr2[$i] : null; 
    $new_array[$i] = func($arg1, $arg2); 
}
```

请注意，当数组长度不同时，需要测试以确保循环不会因 `func()` 的参数耗尽而运行失败。

现在将其与使用 array_map() 产生的等效代码进行对比：

```
$new_array = array_map('func', $arr1, $arr2);
```

如果那样不起作用，你有权在 bugs.php.net 上提交报告。而且，六个月后当你回来查看代码时，哪一个更难重新熟悉？

array_map() 的另一个技巧源于它能够将 null 作为回调。在这种情况下，其行为可以描述为“接收一堆事物的数组，并返回一堆事物数组的数组”。每个数组的第 0 个元素组合成一个数组，成为结果数组的第 0 个元素；每个数组的第一个元素组合成一个数组，成为结果数组的第一个元素；以此类推。换句话说，如果你将其数组参数视为矩阵的列，`array_map(null, ...)` 返回转置矩阵。这实际上是如果你被允许使用 'array' 作为回调时，`array_map('array', $arr1, $arr2)` 所期望得到的结果。

这个技巧也不局限于每次只能组合两个数组。如果回调函数需要 $n$ 个参数，那么 `array_map()` 需要传入 $n$ 个数组。因此，如果你有一个接受六个参数的函数，以及一组六元组（sextets）的数组，每个六元组你都希望运行该函数并收集所有结果到一个新数组中，`array_map()` 将适用。

> 严格来说，有两个对 `array_map()` 的调用。第一个使用 null 回调，将原始数组 [0…n] [0…5] 取出来并返回转置数组 [0…5] [0…n]，第二个使用回调函数作用于 array[0]、array[1]、… array[5] 的连续元素。

`array_map()` 有两个明显的限制。首先，回调后的每个参数必须是数组。如果你想在整整一个数组的运算中使用单个变量（例如，将数组的所有值限制为某个最大值），那么你必须执行以下操作之一：

- 在全局范围内声明该变量，并在回调函数内部使用 global（这不是最吸引人的选项）
- 使用 `array_fill()` 制作一个重复项的数组（仅当你不介意在变量的独立副本上执行操作，或者变量是一个按引用传递的对象或资源时才有用）
- 最终还是回到使用循环
- 使用其他函数：具体来说，是 `array_walk()`
- 使用编写 OOP 时可考虑的一个选项：将回调设为方法，将变量设为对象的属性

另一个明显的限制是你需要预先知道要映射在一起的数组数量，并在函数调用中明确列出它们所有。你可以通过将输入数组的对应元素包装进一个合并数组的单个元素中，并将该数组的元素传递给回调函数来绕过此问题。但这需要重写回调函数，或者在无法重写时，编写一个包装函数来解包合并的元素并将内容传递给真正的回调。你会意识到，那样做后你就回到了原点。幸运的是，PHP 也提供了解决方案，即本章后面介绍的 `call_user_func_array()`。

## array_walk()

想象一下，你正在使用 GD Lib 图形绘制扩展来绘制图表，并且有很多数据点需要用不同大小和颜色的圆圈来指示。位置和半径已经按比例缩放到图像坐标，颜色已经分配并通过图像调色板索引（由 `imagecolorallocate()` 返回的）识别。你被提供一个数据点数组，每个元素分别包含 $x$ 坐标、$y$ 坐标、半径和颜色。例如，

```
$data_points = array(
    array(10, 10, 5, $palette['black']),
    array(10, 20, 5, $palette['black']),
    array(20, 13, 5, $palette['darkolivegreen']),
    ...
);
```

查看 PHP 手册，适当的函数似乎是 `imageellipse()`。你的数据与其参数之间的唯一区别在于它期望宽度和高度，而提供的数据只包含半径。但这只是微不足道的区别。首先，定义一个函数：

```
function imagedatapoint($image, $datapoint) 
{ 
    $width = $height = $datapoint[2]*2; 
    imageellipse($image, $datapoint[0], $datapoint[1], $width, $height, 
        $datapoint[3]); 
}
```

然后调用它。

```
foreach($datapoints as $datapoint) 
{ 
    imagedatapoint($image, $datapoint); 
}
```

这实际上相当简单。如果每个数据点是一个关联数组或对象，并且通过名称标识其组件，`imagedatapoint()` 当然会更具可读性。你可以问的一个问题是，为什么要在函数外部有循环？事实上，在图表上绘制多个数据点的可能性比只绘制一个更大。以下是一个示例：

```
function imagedatapoints($image, $datapoints) 
{ 
    foreach($datapoints as $datapoint) 
    { 
        $width = $height = $datapoint[2]*2; 
        imageellipse($image, $datapoint[0], $datapoint[1], $width, $height, 
            $datapoint[3]); 
    } 
}
```

那么 `array_walk()` 可能会怎么做呢？首先，它使用一个回调函数。这实际上是上一个循环的主体。

```
function imagedatapoint($datapoint, $key, $image) 
{ 
    $width = $height = $datapoint[2]*2; 
    imageellipse($image, $datapoint[0], $datapoint[1], $width, $height, 
        $datapoint[3]); 
}
```

然后它进行以下调用：

```
array_walk('imagedatapoint', $datapoints, $image);
```

与 `array_map()` 不同，`array_walk()` 针对原始数组的引用进行操作。因此，如果回调函数按引用接收其数组元素参数，函数可以修改元素的值，并且更改将反映回传递给 `array_walk()` 的数组中。

## array_filter() 和 preg_grep()

`array_filter()` 的操作很容易从其名称推断出来：给定一个数组，它返回满足给定条件的数组元素，该条件以返回布尔值的函数的回调形式提供（想想 SQL 查询中的 WHERE 子句）。一系列 `array_filter()` 调用可能比单个遍历数组的循环更容易理解，该循环充满了各种测试和分支，旨在决定是否保留特定元素并构建由成功元素组成的新数组。然而，类似于 `array_map()` 的局限性也适用于 `array_filter()`，除了输入数组和回调之外，它不接受任何额外参数。

```
function is_a_square_number($n)
{
    // Fail values unsuitable for sqrt().
    if(!is_numeric($n))
        return false;
    if($n<0)
        return false;

    $square_root = sqrt($n);
    return ($square_root == intval($square_root));
}

$numbers = array(-1, 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, '!');
$squares = array_filter($numbers, 'is_a_square_number');
// $squares now contains the array (0, 1, 4, 9, 16);
```

由于过滤包含特定模式的字符串是数组过滤任务中如此常见的子类，并且正则表达式在描述此类模式时也常常很有用，PHP 提供了一个专门针对该任务的函数。`preg_grep()`（正如名称所暗示，是 PCRE 函数之一，行为类似于 grep 程序）。它不使用回调函数（而是使用正则表达式），但它为 `array_filter()` 和下一节函数之间做了一个很好的过渡。以下是 `preg_grep()` 语句的示例：

```
// This use of preg_grep takes a listing of the current directory, and retains only
// those file names that end with four digits followed by ".jpg" or ".jpeg".
$images = preg_grep('/\d{4}\.jpe?g$/', scandir('.'));
```

> 对于使用类似 shell 的语法根据更简单的标准过滤目录列表的函数，请参见 glob() 函数。

## preg_replace_callback()

`preg_replace()` 使用的语法包含 `e` 修饰符开关。当你使用此修饰符时，给定的替换文本被视为 PHP 代码并进行评估，以确定实际的替换文本应该是什么。但试图塞入所有必要的代码很容易变得麻烦。因此，`preg_replace_callback()` 被实现，使得你只需提供一个回调，而无需直接将替换代码写入函数调用中。这可以极大地简化复杂的正则表达式。由于回调函数可以包含任意数量的字符串处理和模式识别代码，`preg_replace_callback()` 中使用的正则表达式只需复杂到足以保证找到所有期望的匹配项，即使某些不需要的匹配项也通过了即可。进一步的测试可以在回调中完成；如果进一步的测试失败，回调只需返回原样匹配即可。（但请注意，如果不需要的匹配项恰好与
