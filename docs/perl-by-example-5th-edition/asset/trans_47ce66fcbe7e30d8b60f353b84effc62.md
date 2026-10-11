

4.  要打印多个元素（即一个列表）：
`print "@colors[1,3]\n"; # 现在索引值位于列表中，因此需要使用 @ 符号而不是 $ 符号。`

![](img/8556abcb353c0991f12099420ec28735_125_0.png)

**图 5.3 数组元素。**

## 示例 5.5

```perl
# (The Script)
use warnings;
use strict; # 隐含或标准做法，尽管原文仅提及 "use warnings"，为了忠实于以 "use warnings" 开头的原始脚本块，保持原样

# 填充数组并打印其值
1  my @names=('John', 'Joe', 'Jake'); # @names=qw/John Joe Jake;/
2  print @names, "\n"; # 打印时不带分隔符
3  print "Hi $names[0], $names[1], and $names[2]\n";
4  my $number=@names; # 标量被赋值为数组中的元素数量
5  print "There are $number elements in the \@names array.\n";
6  print "The last element of the array is $names[$number -1].\n";
7  print "The last element of the array is $names[$#names].\n";
   # 记住，数组索引从零开始！
8  my @fruit = qw(apples pears peaches plums);
9  print "The first element of the \@fruit array is $fruit[0]; the second element is $fruit[1].\n";
10 print "Starting at the end of the array: $fruit[-1, -3]\n";
```

**(输出)**

```
2 JohnJoeJake
3 Hi John, Joe, and Jake!
4 There are 3 elements in the @names array.
6 The last element of the array is Jake.
7 The last element of the array is Jake.
9 The first element of the @fruit array is apples; the second element is pears.
10 Starting at the end of the array: plums pears
```

## 解释

-   @names 数组被初始化为三个字符串：John、Joe 和 Jake。
-   整个数组被显示出来，且各个元素之间没有空格。当数组包含在双引号中时（“@names”），输入字段分隔符（即空格）会被保留。
-   数组的每个元素都被打印出来，下标从编号 0 开始。
-   标量变量 $number 被赋值为数组 @names。所赋的值是数组 @names 中的元素数量。你也可以使用内置的标量函数来获取数组的大小，例如：`$size = scalar @names;`
-   打印了数组的最后一个元素。由于索引值从 0 开始，通过 1 确定的数组中元素的数量对应于最后一个下标号。
-   打印了数组的最后一个元素。`$#names` 的值对应于数组中最后一个下标号。使用该值作为下标将检索 @names 数组中的最后一个元素。
-   `qw` 结构根据提供的字符串创建一个由单引号单词组成的数组，使用空格作为单词分隔符。（你不需要给单词加引号，也不用逗号分隔单词。）`qw` 的分隔符可以是任意一对非字母数字字符。
-   打印了 @fruit 数组的前两个元素。
-   使用负偏移量作为索引值时，数组元素从数组的末尾开始选取。最后一个元素（$fruit[-1]）是 plums，从末尾数的第三个元素（$fruit[-3]）是 pears。请注意，当两个索引值都在同一对方括号内时，例如 @fruit[-1..-3]，引用的是一个列表而非标量；这就是为什么数组名称前使用 @ 符号而不是 $。

## 使用 foreach 循环遍历数组

遍历数组元素的最佳方式之一就是使用 Perl 的 `foreach` 循环。（有关详细讨论，请参见第 7 章“只有无条件、永远地”。）

这种控制结构使用一个标量变量作为循环变量，依次遍历列表（括号内）中的每个元素。循环变量每次引用列表中的一个元素，并且对于每个元素，执行列表后面的语句块。当所有列表项处理完毕后，循环结束。如果缺少循环变量，则使用默认标量 `$_`。你可以使用命名数组或在括号内创建一个列表。

你可能还会看到使用 `for` 代替 `foreach` 的代码。这是因为 `for` 和 `foreach` 是同义词。在这些示例中，使用 `foreach` 只是为了清楚地表明我们要逐个元素遍历列表；即“对于”列表中的“每个”元素。

## 示例 5.16

```perl
# (The Script)
use warnings;
use strict;

1  my @names = ('Tom', 'Dick', 'Harry', 'Pete');
2  foreach $pal (@names){
3     print "$pal\n";
   }

4  foreach ("red", "green", "yellow", "blue"){
5     print "$_\n";
   }
```

**(输出)**

```
3  Tom
   Dick
   Harry
   Pete

5  red
   green
   Yellow
   blue
```

## 解释

-   数组 @names 被赋予一个列表：'Tom'、'Dick'、'Harry' 和 'Pete'。
-   使用 `foreach` 循环逐个单词遍历列表。
-   标量 $pal 用作循环变量，称为迭代器。如果是这样，它在循环的每次迭代中指向列表中的下一个元素。如果你不提供迭代器变量，Perl 会使用主题变量 `$_` 代替。在循环的每次迭代中，花括号内封闭的语句块都会执行。
-   在这个例子中，`foreach` 循环没有提供迭代器变量，因此 Perl 会使用 `$_` 变量代替，即使你看不到它。
-   每次循环时都会打印 `$_` 的值。（这次我们必须显式使用 `$_`，因为在字符串中添加了 `\n`。）

## 数组复制和切片

当你将一个数组赋值给另一个数组时，数据会被复制。就这么简单。与许多语言不同，你无需负责新数组将保存的数据类型或需要多少个元素。Perl 处理内存分配以及新数组每个元素中存储的数据类型。

切片使用一组索引值同时访问列表、数组或哈希中的多个元素。你可以使用切片将数组中的某些元素复制到另一个数组中。切片也可以赋值给切片。如果赋值运算符右侧的数组比左侧的数组大，未使用的值将被丢弃。如果它较小，则剩余的值被设置为 `undef`。

最小值，分配的值是未定义的。如下面的例子所示，切片中的数组索引不必是连续编号的；每个元素被赋值为赋值运算符右侧数组中的对应值。

## 示例 5.17

```perl
# (The Script)
use warnings;
# 数组复制和切片
1 my @names=('Tom', 'Dick', 'Harry', 'Pete');
2 @newnames = @names; # 数组复制
3 print "@newnames\n";
4 @pal=@names[1,2,3]; # 数组切片 -- @names[1..3] 也是可以的
5 print "@pal\n";
6 ($friend[0,1,2])=@names; # 赋值给数组切片
7 print "$friend\n";
```

**(输出)**

```
3 Tom Dick Harry Pete
5 Dick Harry Pete
7 Tom Dick Harry
```

## 解释

-   数组 @names 被赋予了元素 'Tom'、'Dick'、'Harry' 和 'Pete'。
-   数组 @pal 被赋予了 @names 数组的元素 1、2 和 3。@names 数组的元素被选中并复制到 @pal 数组中。
-   @friend 数组是通过从 @names 数组复制所有值并将它们赋值给 @friend 的元素 0、1 和 2 而创建的。

## 多维数组——列表的列表

多维数组有时被称为 *表格* 或 *矩阵*。它们由行和列组成，可以用多个下标表示。在二维数组中，第一个下标代表行，第二个下标代表列。

Perl 允许这种类型的数组，但它需要理解引用。我们将在第 12 章“这项工作是否需要引用？”中详细讨论这一点。

## 5.2.3 哈希——无序列表

*哈希*（在某些语言中称为关联数组、映射、表或字典）是一个由一对或多对标量（字符串或数字）组成的变量。哈希通常用于创建表格、复杂数据结构、查找文件或数组中的重复条目，或者创建 Perl 对象。我们将在第 14 章“祝福那些事物！（面向对象 Perl）”中详细介绍对象。

