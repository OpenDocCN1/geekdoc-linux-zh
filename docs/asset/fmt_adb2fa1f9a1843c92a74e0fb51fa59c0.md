
通常更推荐使用 `//` 因为它是一个已知量。另一方面，使用 `/* */` 很容易引入编码错误，因为难以追踪注释的开始和结束位置。

### NOTE

> 与普遍的看法相反，在 PHP 脚本中添加注释对脚本执行速度几乎没有影响。如果使用代码缓存，微小的速度差异也会完全消失。

### 转义序列

有些字符无法直接输入，但你几乎肯定会不时想要使用它们中的一些。例如，你可能想要使用 ASCII 换行字符，但你无法输入它。相反，你需要使用转义序列：`\n`。同样，你可以使用 `\r` 打印回车字符。了解这两者很重要，因为在 Windows 平台上，你需要使用 `\r\n` 才能得到一个新行。如果你不打算在其他地方运行脚本，就不必担心这个问题！

回到我们写的第一个脚本，回忆它打印了 2010，因为我们计算了 10 + 10 然后 10 + 0。我们可以使用转义序列重写它，如下所示：

```php
<?php
$ i = 10;
$ j = "10";
$ k = "Hello, world";
echo $ i + $ j;
echo "\n";
```
```
echo $i + $k;
echo "\n";
?>
```

这次 PHP 在每个数字后打印一个新行，很明显输出是 20 和 10 而不是 2010。请注意，转义序列必须在双引号中使用，因为它们在单引号中不起作用。

三种常见的转义序列是 `\\`，意思是“忽略反斜杠”；`\"`，意思是“忽略双引号”；和 `\'`，意思是“忽略单引号”。当字符串内部包含引号时，这一点很重要。如果我们有一个像 'are you really Bill O'Reilly?' 这样的字符串，其中包含单引号，那么这段代码将无法工作：

```php
<?php
echo 'Are you really Bill O'Reilly?';
?>
```

PHP 会看到开头的引号，一直读到 O'Reilly 中的 O，然后把 O 之后的引号视为字符串的结束。Reilly? 部分看起来像是文本片段，会导致错误。你有两种选择：你可以将字符串用双引号包围，或者用 `\'` 转义单引号。

如果你选择转义的方式，它看起来会像这样：

```
echo 'Are you really Bill O\'Reilly?';
```

虽然它们对于小的文本字符串来说是一个干净的解决方案，但要小心过度使用转义序列。HTML 特别充满了引号，转义它们会变得很混乱：

```
$mystring = "<img src=\"foo.png\" alt=\"My picture\" width=\"100\" height=\"200\" />";
```

在这种情况下，你最好使用单引号来包围文本，因为这样对眼睛来说容易得多！

### 变量替换

PHP 允许你使用三种方法定义字符串：单引号、双引号或 heredoc 记法。Heredoc 在这里没有讨论，因为它相比其他两种方法来说相当罕见，但单引号和双引号的工作方式基本相同，只有一个小例外——变量替换。

考虑以下代码：

```php
<?php
$age = 25
```
```
echo "You are ";
echo $age;
?>
```

这是一种特别笨拙的方式来在字符串的一部分中打印变量。幸运的是，如果你把一个变量放在字符串内部，PHP 会执行变量替换，用变量的值替换变量。这意味着我们可以重写代码如下：

```php
<?php
$age = 25
echo "You are $age";
?>
```

输出是相同的。单引号和双引号之间的区别在于，单引号字符串不会进行变量替换。举个例子：

```php
<?php
$age = 25
echo "You are $age";
echo 'You are $age';
?>
```

第一个 `echo` 打印 "You are 25"，但第二个打印 "You are $age"。

### 运算符

现在我们有了要操作的数据值，我们也需要一些运算符。我们已经使用 `+` 来相加变量，但 PHP 中还有许多其他运算符处理算术、比较、赋值和其他操作。运算符只是执行操作的东西的 fancy 名称，例如加法或减法。然而，操作数可能对你来说是新的。考虑这个操作：

```
$a = $b + c;
```

在这个操作中，`=` 和 `+` 是运算符，而 `$a`、`$b` 和 `$c` 是操作数。除了 `+` 之外，你也已经知道 `–`（减法）、`*`（乘法）和 `/`（除法），但这里还有一些其他的。

| Operator | What It Does |
|---|---|
| = | Assigns the right operand to the left operand. |
| == | Returns true if the left operand is equal to the right operand. |
| != | Returns true if the left operand is not equal to the right operand. |
| === | Returns true if the left operand is identical to the right operand. This is not the same as ==. |
| !== | Returns true if the left operand is not identical to the right operand. This is not the same as !=. |
| < | Returns true if the left operand is smaller than the right operand. |
| > | Returns true if the left operand is greater than the right operand. |
| <= | Returns true if the left operand is equal to or smaller than the right operand. |
| && | Returns true if both the left operand and the right operand are true. |
| || | Returns true if either the left operand or the right operand is true. |
| ++ | Increments the operand by one. |
| -- | Decrements the operand by one. |
| += | Increments the left operand by the right operand. |
| -= | Decrements the left operand by the right operand. |
| . | Concatenates the left operand and the right operand (joins them together). |
| % | Divides the left operand by the right operand and returns the remainder. |
| | | Performs a bitwise OR operation. It returns a number with bits that are set in either the left operand or the right operand. |
| & | Performs a bitwise AND operation. It returns a number with bits that are set both in the left operand and the right operand. |

至少还有 10 个其他运算符没有列出；公平地说，你不太可能使用它们。即使是这个列表中的一些运算符也很少使用——例如按位与。话虽如此，按位或运算符被经常使用，因为它允许你组合值。

这里有一个演示部分运算符的代码示例：

```php
<?php
$i = 100;
$i++; // $i is now 101
$i--; // $i is now 100 again
$i += 10; // $i is 110
$i = $i / 2; // $i is 55
$j = $i; // both $j and $i are 55
$i = $j % 11; // $i is 0
?>
```

最后一行使用了取模运算，这让一些人需要一点努力才能理解。`$i % 11` 的结果是 0，因为 `$i` 被设为 55，而取模运算是通过将左操作数（55）除以右操作数（11）并返回余数来工作的。55 正好可以被 11 整除 5 次，因此余数为 0。

连接运算符，一个句点，听起来比实际更可怕：它只是将字符串连接在一起。例如：

```php
<?php
echo "Hello, ". "world!";
echo "Hello, world!" . "\n";
?>
```
