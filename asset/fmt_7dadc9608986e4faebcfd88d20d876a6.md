
由于 PHP 开发者无法预测你想对数组做什么，大多数数组函数，以及相关的数组，都接受一个称为回调（callback）的额外参数，它指定了另一个函数的名称。根据数组函数的功能，该函数将用于操作数组元素，或将它们相互比较或与你指定的某个标准进行比较。这样，PHP 只需提供数组操作更抽象方面的实现，例如映射和遍历，让你可以自由地提供你选择的具体细节。
事实上，回调在抽象功能方面非常有用，以至于提供了一些函数，使其几乎可以在任何情况下使用。实施你自己的 OOP 架构完全是可以想象的（尽管有些堂吉诃德式），其中对象的“方法”表示为回调数组。

## 使用回调

考虑以下脚本：

```php
$inup_file = file('generic.txt');
foreach($inup_file as $k=>$line)
{
   $inup_file[$k] = rtrim($line);
}
```

你正在将文本文件加载为单行字符串数组。PHP 不会丢弃末尾的换行符，所以既然它们已经完成使命，你想自己去掉它们。编写整个循环并在其中使用两个额外变量似乎很啰嗦。首先，你必须记住 `$line` 是副本，所以 `$line=rtrim($line);` 不起作用，这意味着你必须通过数组和键回到原始值。要么那样做，要么记得通过编写 `foreach($inup_file as &$line)` 将 `$line` 声明为引用。任何错误都意味着最终数组的行不会修剪。
现在考虑这个：

```php
$input_file = array_map('trim', file('generic.txt'));
```

这行代码达到了相同的效果。`file()` 返回包含 `generic.txt` 行的数组；`array_map()` 将函数 `trim()` 应用于该数组的每个元素，并返回修剪后的结果数组。
有几个函数抽象了遍历数组的最常见原因，减少了编写循环和其他流程控制语句的需求。虽然仅仅为了写单行代码而写单行代码可能导致难以阅读的代码，但减少程序中的“活动部件”有助于减少错误的发生。
当你有一个数组，需要对每个元素依次执行任务时，`array_map()` 和 `array_walk()` 值得考虑。还有其他函数以类似的方式使用所谓的回调函数，以省去你自己对数组每个元素调用函数的麻烦。
回调有两种形式。第一种，也是最常见的，是包含函数名称的字符串。在上一行代码中，它是 `'trim'`。
> 它必须是一个函数，这就是为什么 PHP 手册强调指出 `echo`、`empty`、`include`、`array` 等*不是*函数。传递 `'include'` 作为你的回调将失败。排除它们的原因是它们在解析期间受到特殊对待，拥有自己的内部结构。
第二种回调用于指定类和对象方法。两者都由双元素数组表示，其中第二个元素是作为字符串存储的方法名称。如果第一个元素是一个对象，则回调引用该对象的方法：`array($object, 'method')`。另一方面，如果第一个元素是字符串或字符串变量，则回调引用指定类的静态方法：`array('thing_factory', 'create_new')` 引用静态的 `thing_factory::create_new()` 方法。

```php
// 在 array_map() 中使用对象的方法作为回调。
// $untidy_array 的每个元素依次传递给 $parser->tidy()，
// 并返回值存储在 $tidied_array 中
$tidied_array = array_map(array($parser, 'tidy'), $untidy_array);

// 在 array_map() 中使用静态类方法作为回调。
// $untidy_array 的每个元素依次传递给 Parser::tidy()，
// 并返回值存储在 $tidied_array 中
$tidied_array = array_map(array('Parser', 'tidy'), $untidy_array);

class Parser
{
// 一个示例方法，修剪单行文本末尾的空格和
// 以‘#’开头的 shell 风格注释。
static function strip_comments($Element)
{
$Element = preg_replace('/#(.*)$/', '', $Element);
$Element = rtrim($Element);
return $Element;
}
}
```

```php
$shell_script = file('foo.sh');
$tidied_script = array_map(array('Parser', 'strip_comments'), $shell_script);
```

在类和对象中，魔术词 `self` 和 `this` 在回调中也能正常工作，其行为符合预期：`array($this, 'method')` 和 `array($work, 'method')` 分别被解释为引用 `$this->method()` 和 `self::method()`。关于诸如静态函数不允许使用 `$this` 等常规限制依然适用。例如：

```php
// An object is able to use its own methods in array callbacks,
// both on arguments passed to it and on its own properties.
$tidied_code = array_map(array($this, 'tidy'), $this->code_array);

// Class methods are also accessible as callbacks within the class.
```

如果你想检查给定的 `$variable` 的内容是否确实指定了一个可调用的函数或方法，布尔函数 `is_callable($variable)` 将说明这一点。

## array_map()

你刚刚看到了 `array_map()` 最简单的应用之一，但它的应用范围远不止于此。
最重要的是，它可以同时操作多个数组。假设你有两个数组——`$arr1` 和 `$arr2`——并且你想构建一个由 `func($arr1[0], $arr2[0])`、`func($arr1[1], $arr2[1])`、……、`func($arr1[n], $arr2[n])` 组成的数组。用循环实现这一点的代码大致如下：

```php
$new_array = array();
for($i=0, $limit=max(count($arr1), count($arr2)); $i<$limit; $i++)
{
    $arg1 = isset($arr1[$i]) ? $arr1[$i] : null;
    $arg2 = isset($arr2[$i]) ? $arr2[$i] : null;
    $new_array[$i] = func($arg1, $arg2);
}
```

注意，为了确保当数组长度不同时，循环不会因 `func()` 缺少参数而运行出错，需要进行上述测试。
现在，将其与使用 `array_map()` 产生的等效代码进行比较：

```php
$new_array = array_map('func', $arr1, $arr2);
```

如果这不起作用，你有权向 bugs.php.net 提交报告。而且，六个月后当你回过头来看你的代码时，哪一个需要更长的时间重新熟悉？
`array_map()` 可以实现的另一个技巧源于它可以接受 `null` 作为回调。在这种情况下，其行为可以描述为“接收一堆事物数组，返回一堆事物数组的数组”。每个数组的第 0 个元素组合成一个单独数组，成为结果数组的第 0 个元素；每个数组的第一个元素组合成一个单独数组，成为结果数组的第一个元素；以此类推。换句话说，如果你将其数组参数视为矩阵的列，`array_map(null, ...)` 返回的是转置矩阵。这实际上就是如果你被允许使用 `array` 作为回调时，你所期望的 `array_map('array', $arr1, $arr2)` 的行为。
这个技巧不仅限于一次只组合两个数组。如果回调函数需要 *n* 个参数，那么 `array_map()` 需要传入 *n* 个数组。因此，如果你有一个接受六个参数的函数，以及一个由六元组组成的数组，你想对每个六元组运行该函数，并将所有结果收集到一个新数组中，`array_map()` 将非常适用。
> 严格来说，这里有两处 `array_map()` 调用。第一处使用 null 回调，接收原始的 `array[0..n] [0..5]` 并返回转置的 `array[0..5] [0..n]`；第二处将回调函数应用于 `array[0], array[1], ...array[5]` 的连续元素。
