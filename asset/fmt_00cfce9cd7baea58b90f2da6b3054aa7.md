
`preg_replace()` 使用的语法包含 `/e` 修饰符开关。当您使用此修饰符时，给定的替换文本被视为 PHP 代码并求值，以确定实际的替换文本应是什么。但是试图塞入所有必要的代码很容易变得麻烦。因此实现了 `preg_replace_callback()`，使得您不需要将替换代码直接写入函数调用，只需提供回调即可。这可以用于大大简化复杂的正则表达式。由于回调函数可以包含任意数量的字符串处理和模式识别代码，`preg_replace_callback()` 中使用的正则表达式只需复杂到足以保证找到所有期望的匹配项即可，即使一些不需要的匹配项也通过了。可以在回调中进行进一步测试；如果进一步测试失败，回调只需返回未更改的匹配项。（但请注意，如果一个不需要的匹配项恰好覆盖一个

后续期望的匹配项，后者将被错过。`preg_replace_callback()` 并不知晓后续测试是否“成功”。）

例如，匹配电子邮件地址以便将其包装在 “mailto:” 链接中，如果你想做得彻底，可能会导致一些令人望而生畏的正则表达式。分阶段处理要容易得多。你可以先简单地尝试定位 `@` 字符，确保其两侧是非空白字符，如下所示：

```php
preg_replace_callback('/\S+@\S+/', $text, $wrap_emails');
```

将验证匹配字符串是否真的是电子邮件的繁重工作留给回调函数：

```php
function wrap_emails($possible_match)
{
    $possible_email = $possible_match[0]; // 回调函数将接收一个数组
    if (is_rfc822_compliant($possible_email)) { // 一个假设的函数，
        // 执行所有琐碎的工作
        return '<a href="mailto:' . $possible_email . '">' . $possible_email . '</a>';
    } else {
        return $possible_email; // 不是电子邮件，原样返回子字符串。
    }
}
```

使用 `preg_replace_callback()` 的第二个例子是与模板系统结合使用。`preg_replace_callback()` 仅负责识别模板中的槽位，它传递给回调函数的匹配项随后会对槽位进行更细致的检查——由于这些槽位已经被一个同时记录它们在模板中位置的功能从模板的其余部分中分离出来，这项任务变得更加容易。这是一个示例：

```php
function include_templates($template_name)
{
    if (is_string($template_file)) {
        $template_file = $template_name;
    } else {
        $template_file = $template_name[1] . 'tpl';
        $template = file_get_contents($template_file);
    }
    return preg_replace_callback('/\{include:\s*\[([^\s]+)\]/', 'include_templates', $template);
}
```

这个递归函数假设你的模板文件都具有 ‘.tpl’ 扩展名，并且你在模板中用于包含 foo.tpl 的语法是 ‘{include: foo}’。不用说，如果 foo.tpl 本身包含其他包含关系，你希望这些也被包含进来。

如果传递给该函数的是一个字符串，则该字符串被解释为模板文件的名称。如果传递的是一个数组（原因很快会明了），则所需的文件名是数组的第二个元素，并追加 `.tpl`。然后，指定文件的内容被读取到 `$template` 中。（这里几乎没有错误检查。）

对 `preg_replace_callback()` 的调用会在 `$template` 中搜索匹配 `{include: foo}` 语法的字符串。包含匹配字符串的数组（其中第 0 个元素包含整个匹配字符串，第 1 个元素包含第一个括号内的子字符串），然后逐个传递给 `include_templates()`，该函数从数组中提取模板文件的名称，在调用 `preg_replace_callback()` 后，返回模板文件的内容——其中所有 `{include: foo}` 部分都被替换为对应模板文件的内容。

不幸的是，没有 `preg_match_callback()` 或 `preg_match_all_callback()`。但由于回调函数可以执行任何操作，它也可以将其收到的匹配项存储在某处（也许是全局变量，或者更最好是类或对象属性）。然后，它只需返回其参数的第 0 个元素，导致 `preg_replace_callback()` 用自身替换任何匹配的子字符串，保持不变。因此，一个地址收集对象可能包含一个像这样工作的方法：

```php
function collect_email($possible_match)
{
    $possible_email = $possible_match[0];
    if (self::is_rfc822_compliant($possible_email))
        $this->emails[] = $possible_email;
    return $possible_email; // 原样返回匹配项
}
```

无论上述方法是否存储电子邮件地址，它都会原样返回。因此，`preg_replace_callback()` 将用自身替换匹配的子字符串，保持原始文本完整。

### `call_user_func_array()` 和 `call_user_func()`

回顾一下在 `array_map()` 章节末尾讨论的两个明显限制。第一个限制已由 `array_walk()` 解决。第二个是你需要预先知道正在一起映射的数组数量，并在函数调用中显式列出它们所有。有时你可能直到运行时才知道这一点。在我的一个程序中，我有一个数字矩阵（大小可变），存储为行的数组（每行本身也是一个数组），我需要对其进行转置（以便最终得到列的数组）。我本可以写一个双重嵌套循环，一个用于迭代行，另一个用于在每个行内进行迭代，类似于这样：

```php
$transposed_matrix = array();
for ($row = 0, $row_count = count($matrix); $row < $row_count; $row++)
{
    for ($column = 0, $column_count = count($matrix[$row]); $column < $column_count; $column++)
    {
        $transposed_matrix[$column][$row] = $matrix[$row][$column];
    }
}
```

即使是在写出那段示例代码时，我也不得不暂停几次，以确保我的行和列方向正确，但期望的效果可以通过编写以下代码来实现：

```php
$temp = $matrix;
array_push(null, $temp);
$transposed_matrix = call_user_func_array('array_map', $temp);
unset($temp);
```

`call_user_func_array()` 是另一个接受回调的函数。它的第二个参数是一个数组，列出了要传递给回调函数的所有参数（如果你从回调函数内部调用 `func_get_args()`，得到的就是同样的数组）。为了举例，假设 `$matrix` 是 `((1,2), (3,4))`，看看发生了什么：

```php
$matrix = array(array(1, 2), array(3, 4));
$temp = $matrix;
array_push(null, $temp);
$transposed_matrix = call_user_func_array('array_map', $temp);
```

`array_map()` 的第一个参数是回调函数的名称，因此将 `$temp` 的第一个参数设置为该回调（在这种情况下，是一个 null 回调）。这就是为什么我需要临时变量；`array_push()` 修改原始数组，而不是返回一个副本。我本可以冒风险直接使用 `$transposed_matrix` 代替 `$temp`，从而省去变量和最后的 `unset()`。这是危险的，因为它会略微降低代码的可读性（将变量创建为一件事（`array_map()` 的参数列表），然后两行之后又将其用于完全不同的目的（`array_map()` 调用的结果））。

```php
$temp = array(null, array(1, 2), array(3, 4));
$transposed_matrix = call_user_func_array('array_map', $temp);
```
