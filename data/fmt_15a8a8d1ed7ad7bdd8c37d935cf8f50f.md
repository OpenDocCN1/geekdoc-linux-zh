
## 14.4 标准条件语句和循环

shell、awk 和 C 中使用的大多数控制结构都被 Perl 支持。然而，Perl 在大括号上与这些语言有显著区别。在每个条件或循环中执行的语句体必须包含在大括号中，即使正体只包含一条语句。Perl 还具有一个用于数组的 `for` 结构，我们将在 14.10 节中讨论。其他结构对你来说已经很熟悉，因此我们将通过简短示例介绍它们的语法。

### 14.4.1 条件语句

对于决策判断，Perl 支持 `if` 和 `unless` 条件语句。我们不需要讨论 `unless`，因为它与使用布尔运算符的 `if` 几乎完全相同。Perl 中的 `if` 结构有三种形式，如图 14.2 所示。除了强制提供大括号外，第一种形式与 awk 中使用的相同。第二种形式使用了 `elsif` 关键字（shell 中的 `elif`），这是一种紧凑的单行写法，是 Perl 特有的。Perl 还支持使用 `while` 循环的 `while`。它还有一个 `until` 循环，其行为类似于 shell 中的对应物。第三种形式也不需要在条件周围使用括号。

### 14.4.2 while、do-while 和 for 循环

像 awk 一样，Perl 支持 `while` 和 `do-while` 循环。像结构的第三形式一样，Perl 也支持使用 `while` 循环的单行写法。它还有一个 `until` 循环，其行为类似于 shell 中的对应物。图 14.3 所示的前两种形式使用无限循环在屏幕上打印无限数量的星号。第三种形式仅打印。

同样的工作可以通过 `for` 循环完成，这在 Perl 中没有特殊特征。该循环也打印了五个星号：

图 14.2 if 条件语句的三种形式

| 形式 1 | 形式 2 | 形式 3 |
| :--- | :--- | :--- |
| `if ($x > 1) { printf("a"); } else { printf("b"); }` | `if ($x > 5) { printf("a"); } elsif ($x > 3) { printf("b"); } else { printf("c"); }` | `printf("") if $x > 3;` |

图 14.3 while 和 do-while 循环

```perl
for ($i = 0; $i < 5; $i++) {
    print("*");
}
```

重复运算符（`x`），在 14.3.2 节中讨论的，可以用单行代码完成这项工作。所有循环都支持 `next`（重启循环迭代）和 `last`（跳出循环）。Perl 在这里偏离了传统：它不使用 `continue` 和 `break`。可以使用 `while (1)` 或 `for (;;)` 设置无限循环。`if` 和 `while` 结构出现在下一个程序 `leap_year.pl`（图 14.4）中，该程序判断你输入的数字是否为闰年。

图 14.4 leap_year.pl

```perl
#!/usr/bin/perl

# leap_year.pl: 确定年份是否为闰年

while (1) {
    $yesorno = "not";
    printf("Enter a year: ");
}
```

整个程序在无限循环中运行，底部的最后语句会在你输入 n 或 N 时终止循环：

```bash
$ leap_year.pl
Enter a year: 2004
2004 is certainly a leap year
Wish to continue? y
Enter a year: 2001
2001 is not a leap year
Wish to continue? y
Enter a year: 1900
1900 is not a leap year
Wish to continue? n
$
```

## 14.5 从命令行参数读取文件

Perl 支持命令行参数。由于它既是过滤器又是脚本语言，Perl 使用特殊的记法（我们将讨论）来标识文件名。14.9.1 节讨论了通用参数。我们首先使用单行代码读取文件，然后学习使用脚本。

### 14.5.1 使用单行代码读取文件

菱形运算符 `<>` 用于从文件中读取行。例如，`<STDIN>` 从标准输入读取一行，而 `<>` 从作为参数指定的文件中读取一行。要读取并打印文件的所有行，请使用以下两种方式之一：

```bash
perl -e '$x="sun"; $y="com"; print ($x . $y . "\n");'
```

sun.com

注意 `$y` 本身包含一个点，因此它的值必须放在引号中。为了可读性，最好使用空白符代替点运算符。Perl 使用 `x` 运算符来重复字符串。以下语句在屏幕上打印了 40 个星号：

```bash
perl -e 'print "*" x 40;'
```
