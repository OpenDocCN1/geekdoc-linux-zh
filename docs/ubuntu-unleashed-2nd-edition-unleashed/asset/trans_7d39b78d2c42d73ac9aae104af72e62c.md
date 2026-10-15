

Perl 数组用 @ 字符表示，如 @fish。数组是由索引号引用的值列表，从第一个元素编号 0 开始，就像在 C 和 awk 中一样。数组中的每个元素都是一个标量值。因为标量值用 $ 字符表示，所以数组中的单个元素也用 $ 字符表示。

例如，$fish[2] 引用 @fish 数组中的第三个元素。这往往会让一些人感到困惑，但与 C 中的数组类似，其中第一个数组元素是 0。

哈希用 % 字符表示，如 %employee。哈希是名称和值对的列表。哈希中的单个元素按名称引用而不是按索引引用（不像数组）。同样，因为值是标量，所以单个元素使用 $ 字符。

例如，$employee{name} 给出哈希中的一个值。处理哈希的两个非常有用的函数是 keys 和 values。keys 函数返回包含哈希所有键的数组，而 values 返回哈希值的数组。使用这种方法，清单 27.2 中的 Perl 程序显示环境中的所有值，很像输入 bash shell 的 env 命令。

```perl
#!/usr/bin/perl
foreach $key (keys %ENV) {
    print "$key = $ENV{$key}\n";
}
```

## 特殊变量

Perl 有各种各样的特殊变量，通常看起来像标点符号——$_, $!, 和 $_——并且都非常有用，可用于简写代码。$_ 是默认变量，$! 是操作系统返回的错误消息，而 $] 是 Perl 版本号。

$_ 也许是这些中最有用的，你将在本章中经常看到该变量的使用。$_ 是 Perl 默认变量，当未指定参数时使用。例如，以下两个语句是等价的：

```perl
chomp;
chomp($_);
```

以下循环是等价的：

```perl
for $cow (@cattle) {
    print "$cow says moo.\n";
}
for (@cattle) {
    print "$_ says moo.\n";
}
```

要获得特殊变量的完整列表，你应该查看随 Perl 发行版提供的 perlvar 文档（如 perlvar 手册页），或者你可以在线访问 http://theoryx5.uwinnipeg.ca/CPAN/perl/pod/perlvar.html。

## 运算符

Perl 支持多种运算符来执行各种操作。有 *比较* 运算符（用于比较值，正如名称所示），*复合* 运算符（用于组合操作或多个比较），*算术* 运算符（用于执行数学运算），以及特殊字符串常量。

### 比较运算符

Perl 使用的比较运算符与 C、awk 和 csh shell 中使用的类似，用于指定和比较值（包括字符串）。最频繁地，比较运算符用于 if 语句或循环中。Perl 有用于数字和字符串的比较运算符。表 27.1 显示了数字比较运算符及其行为。

TABLE 27.1 Numeric Comparison Operators in Perl

| Operator | Meaning |
|---|---|
| == | Is equal to |
| < | Less than |
| > | Greater than |
| <= | Less than or equal to |
| >= | Greater than or equal to |
| != | Not equal to |
| .. | Range of >= first operand to <= second operand |
| <=> | Returns -1 if less than, 0 if equal, and 1 if greater than |

表 27.2 显示了字符串比较运算符及其行为。

TABLE 27.2 String Comparison Operators in Perl

| Operator | Meaning |
|---|---|
| eq | Is equal to |
| lt | Less than |
| gt | Greater than |
| le | Less than or equal to |
| ge | Greater than or equal to |
| ne | Not equal to |
| cmp | Returns -1 if less than, 0 if equal, and 1 if greater than |
| =~ | Matched by regular expression |
| !~ | Not matched by regular expression |

### 复合运算符

Perl 使用复合运算符，与 C 或 awk 中使用的类似，可用于将其他操作（如比较或算术）组合成更复杂的逻辑形式。表 27.3 显示了复合模式运算符及其行为。

TABLE 27.3 Compound Pattern Operators in Perl

| Operator | Meaning |
|---|---|
| && | Logical AND |
| || | Logical OR |
| ! | Logical NOT |
| () | Parentheses; used to group compound statements |

### 算术运算符

Perl 支持各种数学运算。表 27.4 总结了这些运算符。

TABLE 27.4 Perl Arithmetic Operators

| Operator | Purpose |
|---|---|
| x**y | Raises x to the y power (same as x^y) |
| x%y | Calculates the remainder of x/y |
| x+y | Adds x to y |
| x-y | Subtracts y from x |
| x*y | Multiplies x times y |
| x/y | Divides x by y |
| -y | Negates y (switches the sign of y); also known as the unary minus |
| ++y | Increments y by 1 and uses value (prefix increment) |
| y++ | Uses value of y and then increments by 1 (postfix increment) |
| --y | Decrements y by 1 and uses value (prefix decrement) |
| y-- | Uses value of y and then decrements by 1 (postfix decrement) |
| x=y | Assigns value of y to x. Perl also supports operator-assignment operators (+=, -=, *=, /=, %=, **=, and others) |

你也可以在算术语句中使用比较运算符（如 == 或 <）和复合模式运算符（&&、|| 和 !）。它们在假时求值为 0，在真时求值为 1。

### 其他运算符

Perl 支持一些不适合之前任何类别的运算符。表 27.5 总结了这些运算符。

