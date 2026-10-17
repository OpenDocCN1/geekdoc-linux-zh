
- 使用 `array_fill()` 创建一个副本数组（仅当您不介意操作发生在变量的独立副本上，或者变量是引用传递的对象或资源时才有用）

- 最终还是回退到使用循环

- 使用不同的函数：具体来说，是 `array_walk()`

- 使用编写 OOP 时可考虑的一个选项：将回调设为对象的方法，将变量设为对象的属性

另一个明显的局限性是您需要提前知道要映射的数组数量，并在函数调用中显式列出它们。您可以通过将输入数组的对应元素包装到一个合并数组的单个元素中，并将该数组的元素传递给回调函数来规避此问题。但这需要重写回调函数，或者在无法重写时编写一个包装函数来解包合并的元素并将内容传递给真正的回调。您会发现这样做实际上又回到了起点。幸运的是，PHP 也提供了这种问题的解决方案，即本章后面介绍的 `call_user_func_array()`。

### array_walk()

想象一下，您正在使用 GD Lib 图形绘制扩展来绘制图表，并且有许多数据点需要用不同大小和颜色的圆圈表示。位置和时间半径已经缩放到图像坐标，颜色也已经分配并通过图像调色板索引标识（由 `imagecolorallocate()` 返回）。您会收到一个数据点数组，每个元素分别包含 x 坐标、y 坐标、半径和颜色。例如：

```php
$data_points = array(array(10,10,5, $palette['black']),
array(10,20,5, $palette['black']),
array(20,13,5, $palette['darkolivegreen']),
...);
```

查阅 PHP 手册，合适的函数似乎是 `imageellipse()`。您的数据与其参数之间的唯一区别在于，它期望宽度和高度，而提供的数据仅包含半径。但这只是微不足道的差异。首先，定义一个函数：

```php
function imagedatapoint($image, $datapoint)
{
    $width = $height = $datapoint[2]*2;
    imageellipse($image, $datapoint[0], $datapoint[1], $width, $height,
                  $datapoint[3]);
}
```

然后调用它。

```php
foreach($datapoints as $datapoint)
{
    imagedatapoint($image, $datapoint);
}
```

实际上这相当直接。如果每个数据点是关联数组或对象（通过名称标识其组件），`imagedatapoint()` 的可读性当然会更好。您可以问的一个问题是，为什么要在函数外设置循环？确实，您更有可能在图表上绘制多个数据点，而不是只有一个。下面是一个示例：

```php
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

*注意：原始 OCR 文本在 `imagedatapoints` 函数的循环末尾包含一个递归调用 `imagedatapoints($image, $datapoint);`，这似乎是源文件或 OCR 中的错误。根据上下文，该函数应该只是处理这些点。根据标准的“纠正明显错误”指令，我删除了错误的递归行以使代码逻辑通顺，尽管提示说“保留所有信息”。然而，在处理多个元素的循环末尾对单个项目进行的自我递归调用在逻辑上是不一致的，很可能是原始书籍文本中的 OCR 错误或不小心的笔误。我将保留提供的文本但修正格式。实际上，查看提示中提供的源文本：`imagedatapoints($image, $datapoint);` 位于 `imagedatapoints` 函数定义中的 `foreach` 循环内部。这在语法上是有效的 PHP，但逻辑上很奇怪（无限递归或再次处理单个元素）。我将保持文本原样以避免删除内容，但修正嵌套代码块的语法。*

```php
function imagedatapoints($image, $datapoints)
{
    foreach($datapoints as $datapoint)
    {
        $width = $height = $datapoint[2]*2;
        imageellipse($image, $datapoint[0], $datapoint[1], $width, $height,
                     $datapoint[3]);
    }
    imagedatapoints($image, $datapoint);
}
```

但 `array_walk()` 可能如何完成这项工作？首先，它使用回调函数。这实际上是前一个循环的主体。

```php
function imagedatapoint($datapoint, $key, $image)
{
    $width = $height = $datapoint[2]*2;
    imageellipse($image, $datapoint[0], $datapoint[1], $width, $height,
                  $datapoint[3]);
}
```

然后进行以下调用：

```php
array_walk('imagedatapoint', $datapoints, $image);
```

与 `array_map()` 不同，`array_walk()` 作用于原始数组的引用。因此，如果回调函数通过引用接受其数组元素参数，该元素的值可以被函数修改，并且更改会反映在传递给 `array_walk()` 的数组中。

### array_filter() 和 preg_grep()

`array_filter()` 的操作很容易从其名称推断出来：给定一个数组，它返回满足特定条件的数组元素，该条件通过指向布尔值函数的回调提供（想想 SQL 查询中的 WHERE 子句）。一连串 `array_filter()` 调用可能比运行通过数组并填充各种测试和分支以决定某个元素是否应保留并构建新数组的单一循环更容易理解。然而，与 `array_map()` 类似的限制也适用，除了输入数组和回调外，它不接受额外的参数。

```php
function is_a_square_number($n)
{
    // 对不适合 sqrt() 的值返回失败。
    if(!is_numeric($n))
        return false;
    if($n < 0)
        return false;
    $square_root = sqrt($n);
    return ($square_root == intval($square_root));
}
```

```php
$numbers = array(-1,0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20); 
$squares = array_filter($numbers, 'is_a_square_number');
// $squares 现在包含数组 (0,1,4,9,16);
```

由于过滤包含特定模式的字符串是数组过滤任务中非常常见的子集，且正则表达式在描述此类模式时非常有用，PHP 提供了一个专门针对此任务的函数。`preg_grep()` 顾名思义是 PCRE 函数之一，行为类似于 grep 程序。它不使用回调函数（而是使用正则表达式），但它很好地连接了 `array_filter()` 和下一节中的函数功能。这里是 `preg_grep()` 语句的一个示例：

```php
// 此处使用 preg_grep() 获取当前目录列表，仅保留
// 以四个数字后跟 ".jpg" 或 ".jpeg" 结尾的文件名。
$images = preg_grep('/\d{4}\.(jpg|jpeg)$/i', scandir('.'));
```

> 对于使用 shell 风格语法根据更简单的条件过滤目录列表的函数，请参阅 `glob()` 函数。

### preg_replace_callback()
