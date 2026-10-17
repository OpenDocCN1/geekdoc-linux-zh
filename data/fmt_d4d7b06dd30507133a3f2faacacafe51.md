
这可能不是你预期的结果。三个字符串被正确排序了，但数字似乎是序的。这是因为所有元素都是根据它们的 ASCII 值按字母顺序排序的（参见第 4.9 节）。在 ASCII 中，1 小于 2，2 小于 3。按字母顺序来说，1000 小于 21。如果我们想按数值进行排序，就必须更改 Perl 的默认排序行为。

## 数字排序 vs 字符串排序

排序函数必须将一个值与另一个值进行比较。在 Perl 中，有两个运算符允许你比较成对的值：

```
<= 比较数字；
cmp 比较字符串。
```

这些运算符返回 -1、0 或 +1，取决于左侧操作数是小于还是大于右侧操作数。

- `"a" cmp "b"; # -1，因为 "a" 在字母顺序上小于 "b"`
- `"b" cmp "a"; # +1"`
- `"a" cmp "a"; # 0"`
- `1 <=> 2; # -1，因为数值上 1 小于 2`
- `2 <=> 1; # 1`
- `1 <=> 1; # 0`
- `"a" <=> "b"; # 0，因为字符串在数值上为零`
- `100 cmp 2; # -1，因为字母顺序上 100 小于 2`

要更改 Perl 中的排序行为，你必须给 `sort()` 函数提供替代语法。Perl 的 `sort()` 预留了两个变量 `$a` 和 `$b` 用于排序。当我们使用默认排序行为时，我们并不使用这些特殊变量，但以下两行代码是等价的：

```
@data = sort @data; # 基础字母排序
@data = sort {$a cmp $b} @data; # 相同，但显示了所有细节
```

比较程序是 `sort` 之后大括号内发生的部分。修改你示例 4.18.1 代码中的第 6 行，分别尝试这两种排序赋值：

```
@data = sort {$a cmp $b} @data; # 字母排序
@data = sort {$a <=> $b} @data; # 数值排序
```

你会发现每次按数值排序都会产生警告。数字被正确排序了，但字符串是：

```
before: 3.14 1000 21 red blue yellow
Argument "red" isn't numeric in sort at sort.pl line 6.
Argument "blue" isn't numeric in sort at sort.pl line 6.
Argument "yellow" isn't numeric in sort at sort.pl line 6.
after: red blue yellow 3.14 21 1000
```

这个警告信息非常通俗易懂；只有当你对数字而不是字符串排序时，才按数值排序。如果你有字符串和数字的混合，可以这样进行排序：

```
@data = sort {$a <=> $b} or {$a cmp $b} @data;
```

这使用了布尔运算符来连接两次比较。如果数值排序的结果为零，则改用字母比较。遗憾的是，仍然会有警告，因为我们正在把字符串当作数字比较。我们可以通过临时关闭警告来消除这些。这是通过在 `sort` 之前放置 "no warnings;" 并在 `sort` 之后使用 "use warnings;" 来的：

```perl
no warnings;
@data = sort {$a <=> $b} or {$a cmp $b} @data;
use warnings;
```

出于这个原因，请不要将变量命名为 `$a` 或 `$b`。注意你你不需要用运算符声明它们。

你可以在大括号之间放入任何内容，以便更有想象力的方式对数据。让我们尝试按每个字符串的长度进行排序（对于数字，则是其数字字符串表示的长度）。

```
@data = sort {length($a) <=> length($b)} @data;
```

输出如下：

```
before: 3.14 1000 21 red blue yellow
after: 21 red 3.14 1000 blue yellow
```

## 反序排序

有时你想执行反序排序。只需交换顺序即可实现：

```
@data = sort {$b cmp $a} @data; # 反向字母排序
@data = sort {$b <=> $a} @data; # 反向数值排序
```

有时你想执行反序排序。只需交换顺序即可实现：

1. `#!/usr/bin/perl`
2. `use strict; use warnings;`
3. 
4. `my @data = qw(3.14 1000 21 red yellow);`
5. `print "before: @data\n";`
6. `@data = sort @data;`
7. `print "after: @data\n";`

### 理解脚本

第 4 行创建了一个同时包含数字和字符串的数组。

第 6 行使用相应的 `sort()` 函数执行实际排序。注意，我们将排序后的输出赋值回了相同的数组，但也可以将其赋值 de新数组（例如，`@sorted_array`）。

程序的输出应该如下：

```
before: 3.14 1000 21 red yellow
after: 1000 21 3.14 red yellow
```

这可能不是你预期的结果。三个字符串被正确排序了，但数字似乎是序的。这是因为所有元素都是根据它们的 ASCII 值按字母顺序排序的（参见第 4.9 节）。在 ASCII 中，1 小于 2，2 小于 3。按字母顺序来说，1000 小于 21。如果我们想按数值进行排序，就必须更改 Perl 的默认排序行为。

## 数字排序 vs 字符串排序

排序函数必须将一个值与另一个值进行比较。在 Perl 中，有两个运算符允许你比较成对的值：

```
<= 比较数字；
cmp 比较字符串。
```

这些运算符返回 -1、0 或 +1，取决于左侧操作数是小于还是大于右侧操作数。

- `"a" cmp "b"; # -1，因为 "a" 在字母顺序上小于 "b"`
- `"b" cmp "a"; # +1"`
- `"a" cmp "a"; # 0"`
- `1 <=> 2; # -1，因为数值上 1 小于 2`
- `2 <=> 1; # 1`
- `1 <=> 1; # 0`
- `"a" <=> "b"; # 0，因为字符串在数值上为零`
- `100 cmp 2; # -1，因为字母顺序上 100 小于 2`

要更改 Perl 中的排序行为，你必须给 `sort()` 函数提供替代语法。Perl 的 `sort()` 预留了两个变量 `$a` 和 `$b` 用于排序。当我们使用默认排序行为时，我们并不使用这些特殊变量，但以下两行代码是等价的：

```
@data = sort @data; # 基础字母排序
@data = sort {$a cmp $b} @data; # 相同，但显示了所有细节
```

比较程序是 `sort` 之后大括号内发生的部分。修改你示例 4.18.1 代码中的第 6 行，分别尝试这两种排序赋值：

```
@data = sort {$a cmp $b} @data; # 字母排序
@data = sort {$a <=> $b} @data; # 数值排序
```

你会发现每次按数值排序都会产生警告。数字被正确排序了，但字符串是：

```
before: 3.14 1000 21 red blue yellow
Argument "red" isn't numeric in sort at sort.pl line 6.
Argument "blue" isn't numeric in sort at sort.pl line 6.
Argument "yellow" isn't numeric in sort at sort.pl line 6.
after: red blue yellow 3.14 21 1000
```

这个警告信息非常通俗易懂；只有当你对数字而不是字符串排序时，才按数值排序。如果你有字符串和数字的混合，可以这样进行排序：

```
@data = sort {$a <=> $b} or {$a cmp $b} @data;
```

这使用了布尔运算符来连接两次比较。如果数值排序的结果为零，则改用字母比较。遗憾的是，仍然会有警告，因为我们正在把字符串当作数字比较。我们可以通过临时关闭警告来消除这些。这是通过在 `sort` 之前放置 "no warnings;" 并在 `sort` 之后使用 "use warnings;" 来的：

```perl
no warnings;
@data = sort {$a <=> $b} or {$a cmp $b} @data;
use warnings;
```

出于这个原因，请不要将变量命名为 `$a` 或 `$b`。注意你你不需要用运算符声明它们。

你可以在大括号之间放入任何内容，以便更有想象力的方式对数据。让我们尝试按每个字符串的长度进行排序（对于数字，则是其数字字符串表示的长度）。

```
@data = sort {length($a) <=> length($b)} @data;
```
