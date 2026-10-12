
## 第 9 章

```php
for ($i=0; $i<100; $i++)
{
  if ($foo [$i] !=0)
    continue;
  //...etc.
}
```

请注意，`if` 语句中的测试条件已被取反，并且循环剩余部分的缩进层级减少了一级。这也可以用于降低测试的复杂性。回想一下前面讨论中的另一个例子：

```php
for ($i=0; $i<100; $i++)
{
  if (($a==$i || $b==$i)
      &&
     ($c!=$i || $d!=$i))
  {
    echo "Either $a or $b is equal to $i, ";
    echo "and either $c or $d is not.";
  }
}
```

你可以立刻看出，这是另一种循环内部只有一个 `if` 语句的情况，因此可以改写为如下形式：

```php
for ($i=0; $i<100; $i++)
{
  if (! (($a==$i || $b==$i) && ($c!=$i || $d!=$i)))
    continue;
  echo "Either $a or $b is equal to $i, ";
  echo "and either $c or $d is not.";
}
```

通过运用一点布尔代数，该测试条件可以简化为：

```php
if (($a!=$i && $b!=$i) || ($c==$i && $d==$i))
```

因此，如果 `$a` 和 `$b` 都不等于 `$i`，或者 `$c` 和 `$d` *都*等于 `$i`，循环将执行 `continue`。但是，如果你先测试 `$a` 和 `$b` 是否都不等于 `$i`，你就可以立即知道是否应该继续执行，而无需继续检查 `$c` 或 `$d`。因此，可以将测试拆分为两个独立的语句：

```php
for ($i=0; $i<100; $i++)
{
  if ($a!=$i && $b!=$i)
    continue;
  if ($c==$i && $d==$i)
    continue;
  echo "Either $a or $b is equal to $i, ";
  echo "and either $c or $d is not.";
}
```

由于 PHP 允许 `continue` 或 `break` 接受一个参数，以表达需要跳过或终止多少层循环，因此在 C 或 Java 中需要使用额外变量来携带嵌套循环中是否应终止循环信息的情况下，或者使用 `goto` 跳转到外层循环后的标签时（除了 Java，因为它没有 `goto` 结构），可以使用简单的 `continue` 或 `break`。你可以这样写：

```text
$position = null;
for($i=0; $i<100; $i++)
{
    for($j=0; $j<100; $j++)
    {
        if($array[$i][$j]==$what_we_wanted)
        {
            $position = array($i,$j);
            break 2;
        }
    }
}
if(null===$position) // $what_we_wanted was not found.
```

而不是这样写：

```text
$position = null;
$found_what_we_wanted = false;
for($i=0; $i<100; $i++)
{
    for($j=0; $j<100; $j++)
    {
        if($array[$i][$j]==$what_we_wanted)
        {
            $position = array($i,$j);
            $found_what_we_wanted = true;
            break;
        }
    }
    if($found_what_we_wanted)
        break;
}
if(null===$position) // $what_we_wanted was not found.
```

关于 `continue` 和 `break` 的最后一点观察是，常见的做法是将这些语句与决定是否执行它们的那个测试条件写在同一行，特别是当这些测试条件简短且简单时。因此，你可能需要考虑采用或允许这种书写方式：

```text
if($a==$1 && $b!=$1) continue;
if($c==$1 && $d==$1) continue;
```

*关于使用相等运算符 `==` 的插曲是，常见的拼写错误是本来想使用 `==` 却误用了 `=`。在某些情况下，你可以保护自已免受由此类误用赋值代替比较所导致的 bug 的影响。当将变量与函数的结果或字面量值进行比较时，如果你将变量放在相等运算符的右侧，误将运算符本身写成 `=` 而不是 `==` 会导致解析错误：`null===$position` 是无效语法。这些错误比那些由本不该发生的赋值和未正确进行的比较所导致的微妙错误更容易调试。*

## 注释

除了 PEAR 强制要求的作者和许可信息外，顶部注释中还可以包含代码功能的概要。如果概要较长，在其前面添加一两行摘要来综合该概要，将有助于后来想要了解该文件用途的开发者。

PEAR 还建议你使用 Javadoc 风格的注释，以便易于转换为文档。在这一点上，与任何其他风格问题一样，观点也是分歧的。反对的一个理由是，由于它们带来的额外格式化，使得注释本身在源代码中更难阅读。另一种观点认为，既然每一个公开可访问的方法都应该以这种方式进行注释，这就鼓励了那些实际上既不构成注释也不构成文档的有效但无意义的注释：

```cpp
/*
 * Gets the number of elements in this Bundle.
 *
 * @return number of elements in this Bundle.
 */
public function Count()
{
    return count($this->elements);
}
```

但注释应有的作用是记录代码的 *意图*。如果代码本身构建良好，它自身就能很好地记录它 *做了什么*。它不会记录的是 *为什么要这样写*。

## 命名约定

拥有糟糕名称的变量和函数是许多故事的来源，这些故事从喜剧到恐怖不等。在任何具有一定规模的应用程序中，你都需要拥有一致的方式来命名。以下是一些建议。

用于控制 *for* 循环的通用计数器变量应短小精悍。除非上下文提供了明显的变量选择，否则惯例是先使用 *$i*。如果你嵌套了另一个循环，其变量为 *$j*，然后是 *$k* 和 *$l*。通常，如果你需要将循环嵌套得更深，你可能想要 *重新考虑* 你正在做的事情，并将除了最外层语句块之外的所有部分移入一个函数。如果循环不是嵌套的，则可以使用相同的变量，前提是正确的初始化。如果你使用 *foreach()* 循环遍历数组，对数组使用复数名称，对元素使用相应的单数名称，将明显体现两个变量之间的关系：*foreach($children as $child)*。

应特别避免过长的变量名。变量名越长，拼写错误导致混乱的机会就越大。毫无疑问，你进行所有 PHP 开发时都将错误报告设置为（至少）*E_ALL*，以便在你尝试使用未初始化变量时收到通知。这将捕捉到你在使用变量时拼写错误名称的情况，但如果你在使用 *赋值* 给变量时输错名称，它就不会帮到你。在前一节中，变量名称 *$found*，我们要 *wanted* 的变量被使用，但在一处拼写错误。由于这并不涉及使用未初始化变量，因此错误不会被捕捉到，只有后来——当你意识到有问题并且 *$i* 始终为 100 时——你才会发现这个错误。

## 代码效率

PHP 5 提供了将对象的可见属性和方法与类实现的属性和方法分离的机制，通过魔法方法 `__get()`、`__set()` 和 `__call()` 实现。由于变量和属性区分大小写，你可能需要考虑一种实践：将所有对象属性命名为小写名称，声明它们为 `private` 或 `protected`，然后编写例程通过标题大小写名称提供访问：

```
class foo
{
    protected $width, $height;

    public function __get($property)
    {
        switch($property)
        {
            case 'Width':
                return $this->width;
            case 'Height':
                return $this->height;
            case 'Area':
                return $this->width*$this->height;
        }
    }

    public function __set($property, $value)
    {
        switch($property, $value)
        {
            case 'Width':
                $this->width = $value;
                return;
        }
    }
}
```

这也让你对对象用户可以更改或查看的属性拥有更精细的控制。例如，请注意，`$object->Height` 可以被读取但不能被赋值——如果你只是简单地使 `$object->height` 变为 public，这种区别将不可能实现。

如果你在真实属性与通过 `__get()` 和 `__set()` 创建的综合属性之间做出风格上的区分，你应确保为真实属性提供综合访问，并最好禁止直接访问这些属性。这将允许你创建无论此类是否在内部使用相同的属性，都提供完全相同属性接口的类。例如，一个复数对象可以提供 `$num->Real`、`$num->Imag`、`$num->Arg` 和 `$num->Mag`；无论它是将数字存储为实部加虚部并提供综合的参数和模长，还是反过来。

> *合成属性的 `__get()` 访问器可以包含代码，以便将检索到的前一个值缓存在私有属性中*，以防 *再次被请求时，如果该属性依赖于某个属性并通过 `__set()` 发生改变，则清除缓存内容*。

在由多个单词组成函数和方法名称时，使用 `underscore_separation` 或 `TitleCase` 来显示一个单词在哪里结束，下一个单词从哪里开始。关于使用哪一种，观点分歧很大

