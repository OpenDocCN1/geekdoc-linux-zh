
> ⁷ 严格来说，** ** 是类似于 FORTRAN 的，而不是 C 语言，尽管这是一种损失。

# 第一部分 结构

给出结果：

```
$ ./operators.pl

$i + $j = 14

$i * $j = 40

$i / $j = 2.5

$i % $j = 2

$i ** $j = 10000
```

与 C 语言算术的一个区别是，当 Perl 除除整数时，结果会自动类型为浮点数——通常的 C 整数除法会将结果截断为整数。这要合理得多，Perl 还提供了幂运算符。要模拟整数除法，使用内置的 `int()` 函数：

```perl
$integer_value = int($sa / $sb);
```

## 字符串

正如其起源，Perl 拥有强大的内置字符串处理功能。Perl 有两个非常有字符串运算符：

- `.` 字符串拼接
- `x` 字符串重复

例如：

```perl
#!/usr/bin/perl -w
# file: string.pl
use strict;
my $sa = 'hello';
my $sb = 'world';
my $msg = $sa . ' ' . $sb;
print "\$msg : $msg\n";
my $sa = 'hi';
my $sb = $sa x 2;
my $sc = $sa x 5;
print "\$sb : $sb\n";
print "\$sc : $sc\n";
```

执行该代码得到：

```
$ ./string.pl
$msg : hello world
$b : hihi
$c : hihihihihi
```

## 真与假值

Perl 中有三个假值：

- `""` 空字符串
- `"0"` 单字符 0 的字符串
- `0` 数字 0

其他所有值都是真。因此在 Perl 中，以下所有都是真值：

- `1`
- `10`
- `"hi"`

## 数值比较

Perl 拥有常用的数值比较操作符，额外增加了一个比较操作符 `<>`。除了比较操作符外，所有这些操作符的求值结果为真 (`1`) 或假 (`0!`)。以下是操作符：

- `<` 小于
- `<=` 小于或等于
- `>` 大于
- `>=` 大于或等于
- `==` 等于
- `!=` 不等于
- `<>` 比较

这里是一些示例：

```perl
if ($i < 10) {
    print "\$i is less than 10\n";
}
if ($j >= 20) {
    print "\$j is greater than or equal to\n";
}
```

一个常见的错误（不仅在 Perl 中）是在比较时使用赋值符 `=` 而不是等价操作符 `==`。语句 `$sa = $sb` 会改变 `$sa` 的值，而后者返回真或假但不改变值。记住这两个操作是不同的，效果也不同。比较操作符 `<>` 的结果为 1、0 或 -1：

- 1 如果 `$a > b`
- 0 如果 `$a == b`
- -1 如果 `$a < b$`

## 字符串比较

由于标量可以是数字也可以是字符串，而我们已经知道如何比较数字，我们需要一种比较字符串的方法——字符串比较。这些与数值操作符类似，除了 `cmp` 外，它们返回真或假：

- `lt` 小于
- `le` 小于或等于
- `gt` 大于
- `ge` 大于或等于
- `eq` 等于
- `ne` 不等于
- `cmp` 比较

字符串比较是基于字符的 ASCII 值的（但不同于字母顺序）比较。

```perl
if ($name gt 'Joe') {
    print "$name comes after Joe\n";
}
```

```perl
if ($language ne 'Perl') {
    print "Your language is Perl.\n";
}
```

字符串比较操作符 `cmp` 的结果为 1、0 或 -1：

- 1 如果 `$a gt b`
- 0 如果 `$a eq b`
- -1 如果 `$a lt b`

## 自增自减

Perl 有以下自增和自减操作符：

- `++` 自增
- `--` 自减

这些操作符提供了一种对变量加 1 (`++`) 或减 1 (`--`) 的简单方法。操作符的位置很重要。如果放在变量左侧，它会在使用变量之前增加（前置自增）；在右侧，它会在使用变量之后增加（后置自增）。例如：

```perl
#! /usr/bin/perl -w
# file: increment.pl
use strict;
my $si = 10;
my $sj = ++$si;
print "\$si = $si, \$sj\n";
```

```perl
$si = 10;
$sj = ++$si;
print "\$si = $si, \$sj\n";
```

执行该代码得到：

```
$ ./increment.pl
$si = 11, $sj = 11
$si = 11, $sj = 10
```

为了说明前置和后置自增，考虑语句 `$sj = ++$si;` `$sj` 被赋值为 `++$si` 的结果。这个前置自增（因为 `++` 在 `$si` 的左侧）导致变量 `$si` 先增加到 11；然后将 `$si` 的值赋值给 `$sj`。结果是 `$si` 和 `$sj` 的值都是 11。

相反，考虑这个语句 `$sj = $i++;` 在后置自增中，`++` 在 `$i` 的右侧。`$i` 在取值后才增加。首先，`$sj` 被赋值为 `$i` 的当前值 10；然后 `$i` 增加到 11。

自减操作符 `--` 的工作方式类似：如果 `--` 在左侧，它是前置自减，先减 1；如果在右侧，它是后置自减，最后减 1。

## 逻辑

Perl 的逻辑操作符类似于 C 和 C++，增加了三个可读性更高的操作符：

- 逻辑 `and`
- 逻辑 `or`
- 逻辑 `not`

你可以根据自己的喜好使用其中一种或两者。优先级上存在差异。`and`、`or` 和 `not` 操作符优先级极低——它们位于优先级表的底部。详情请参见 `man perl`。

以下是它们使用的几个示例：

```perl
if ($si > 0 && $si <= 10) {
    print "\$si is between 0 and 100\n";
}
```

```perl
if ($answer eq 'y' or $answer eq 'Y') {
    print "\$answer equals 'y' or 'Y\n";
}
```

`and`、`or` 和 `not` 的低优先级并不能为我们有利（允许我们省略括号，稍后讨论短路逻辑操作符时会看到），但它可能也会带来问题。以下是一些陷阱：

| `$sa = $bb && $sc;` | # 如: `$sa = ($bb && $sc);` | 好的！ |
| `$sa = $bb and $sc;` | # 如: `($sa = $bb) and $sc;` | 错误！ |
| `$sa = $bb || $sc;` | # 如: `$sa = ($bb || $sc);` | 好的！ |
| `$sa = $bb or $sc;` | # 如: `($sa = $bb) or $sc;` | 错误！ |

## 4.3.6 流控制结构

流控制结构是我们熟悉的 `if`、`else`、`while` 等。如果某个条件不满足——则执行流控制。在 Perl 中，这些结构与 C 语言不同的一点重要性是：大括号 `{}` 是必须的。省略它们会导致语法错误。

### 条件结构

`if` 语句是最常见的条件结构。它的语法如下：

```perl
if ((condition) {
    statements
} else {
    statements
}
```

如果括号中的条件求值为真，则执行第一组语句；否则，执行第二组语句。`else` 部分是可选的。条件可以是任何求值为真或假的语句，例如 `$a < $b` 或者更复杂的内容。嵌套的 `if` 语句具有如下语法：

```perl
if (condition1) {
    statements
} elsif (condition2) {
    statements
} else {
    statements
}
```

这是一个 `if` 语句的示例：

```perl
if ($answer eq 'yes') {
    print "The answer is yes\n";
} else {
    print "The answer is NOT yes\n";
}
```

### 循环结构

`while` 循环：一种常见的循环结构，它的语法如下：

```perl
while (condition) {
    statements
}
```

对条件进行测试，如果为真，则执行语句；然后再次测试条件，如果为真，则执行语句……你懂其意了。当条件为假时，循环终止。例如：

```perl
$i = 1;
while ($i <= 5) {
```
