

如果用户输入不同的数字，if...else 结构会报告哪个数字更大。因为 *expr* 执行数值比较，所以该程序接受包含小数点的数字。

```perl
$ cat ifelse.pl
#!/usr/bin/perl -w
print "Enter a number: ";
$num1 = <>;
print "Enter another, different number: ";
$num2 = <>;

if ($num1 == $num2) {
    die ("Please enter two different numbers.\n");
}
if ($num1 > $num2) {
    print "The first number is greater than the second number.\n";
}
else {
    print "The first number is less than the second number.\n";
}
```

```
$ ./ifelse.pl
Enter a number: 8
Enter another, different number: 8
Please enter two different numbers.
```

```
$ ./ifelse.pl
Enter a number: 5.5
Enter another, different number: 5
The first number is greater than the second number.
```

## if...elsif...else

与 bash 的 if...then...elif 控制结构（第 961 页）类似，Perl 的 if...elsif...else 控制结构是一种复合语句，它使用以下语法实现嵌套的一组 if...else 结构：

`if` (*expr*) {…} `elsif` (*expr*) {…} … `else` {…}

下一个程序使用 if...elsif...else 结构实现了前面 ifelse.pl 程序的功能。由于程序中的最后一条语句会显示错误消息，因此用 **print** 语句替代了 **die** 语句；无论如何，执行完该语句后程序都会终止。你可以使用 STDERR 句柄（第 1066 页）来使 Perl 将这条消息发送到标准错误输出而不是标准输出。

```perl
$ cat ifelsif.pl
#!/usr/bin/perl -w
print "Enter a number: ";
$num1 = <>;
print "Enter another, different number: ";
$num2 = <>;

if ($num1 > $num2) {
    print "The first number is greater than the second number.\n";
}
elsif ($num1 < $num2) {
    print "The first number is less than the second number.\n";
}
else {
    print "Please enter two different numbers.\n";
}
```

## foreach/for

Perl 的 `foreach` 和 `for` 关键字是同义词；你可以在任何上下文中用其中一个替换另一个。这些结构是复合语句，具有两种语法。有些程序员对 `foreach` 使用一种语法，对 `for` 使用另一种语法，尽管没有必要这样做。本书在两种语法中都使用 `foreach`。

### foreach：语法 1

`foreach` 结构的第一个语法类似于 shell 的 for...in 结构（第 967 页）：

```
foreach (var) (list) { ... }
```

其中 *list* 是一个表达式或变量的列表。Perl 会针对 *list* 中的每一项执行一次语句块，并在每次迭代中按顺序将 *list* 中一项的值分配给 *var*，从第一项开始。如果你没有指定 *var*，Perl 会将值分配给 `$_` 变量（第 1065 页）。

下面的程序演示了一个简单的 `foreach` 结构。在第一次循环中，Perl 将字符串 `Mo` 分配给变量 `$_`，并且 `say` 语句会显示该变量的值以及一个新行。在第二次和第三次循环中，`$_` 被分别赋值 `Larry` 和 `Curly`。当列表中再也没有项时，Perl 继续执行 `foreach` 结构之后的语句。在这种情况下，程序终止。如果该程序抱怨 `say` 不可用，请参见第 1047 页的 use feature 'say'。

```perl
$ cat foreach.pl
foreach $item ("Mo", "Larry", "Curly") {
    say "$item says hello.";
}

$ perl foreach.pl
Mo says hello.
Larry says hello.
Curly says hello.
```

使用 `$_`（第 1065 页），你可以按以下方式编写此程序：

```perl
$ cat foreacha.pl
foreach ("Mo", "Larry", "Curly") {
    say "$_ says hello.";
}
```

以下是使用数组的程序：

```perl
$ cat foreachb.pl
@stooges = ("Mö", "Larry", "Curly");
foreach (@stooges) {
    say "$_ says hello.";
}
```

以下是使用 **foreach** 后缀语法的程序：

```perl
$ cat foreachc.pl
@stooges = ("Mö", "Larry", "Curly");
say "$_ says hello." foreach @stooges;
```

循环变量（前面示例中的 *$item* 和 *$*_）引用括号中 *list* 内的元素。当你修改循环变量时，你就修改了列表中的元素。*uc* 函数返回其参数的大写版本。

下一个示例表明，修改循环变量 **$stooge** 会修改 **@stooges** 数组：

```perl
$ cat foreachd.pl
@stooges = ("Mö", "Larry", "Curly");
foreach $stooge (@stooges) {
    $stooge = uc $stooge;
    say "$stooge says hello.";
}
say "$_ is uppercase" foreach @stooges;
```

```
$ perl foreachd.pl
MÖ says hello.
LARRY says hello.
CURLY says hello.
LARRY is uppercase
```

参见第 **1069** 页，了解遍历命令行参数的示例。

## last 和 next

Perl 的 **last** 和 **next** 语句允许你中断循环；它们类似于 Bourne Again Shell 的 **break** 和 **continue** 语句（第 **976** 页）。**last** 语句将控制权转移到由循环结构控制的语句块之后的语句，从而终止循环的执行。**next** 语句将控制权转移到语句块的末尾，从而以下一次迭代继续执行循环。

在以下程序中，*if* 结构测试 *$item* 是否等于字符串 **two**；如果是，该结构执行 **next** 命令，该命令会跳过 *say* 语句并继续循环的下一次迭代。如果你将 **next** 替换为 **last**，Perl 将退出循环并且不会显示 **three**。如果该程序抱怨 *say* 不可用，请参见第 **1047** 页的 **use feature 'say'**。

```perl
$ cat foreach1.pl
foreach $item ("one", "two", "three") {
    if ($item eq "two") {
        next;
    }
    say "$item";
}

$ perl foreach1.pl
one
three
```

## foreach：语法 2

foreach 结构的第二个语法类似于 C 的 for 结构：

```
foreach (expr1; expr2; expr3) { ... }
```

expr1 初始化 foreach 循环；Perl 在执行语句块之前评估 expr1 一次。expr2 是终止条件；Perl 在每次执行语句块之前评估它，如果 expr2 评估为真，则执行语句块。Perl 在每次执行语句块之后评估 expr3——它通常递增 expr2 中的一部分变量。

在下一个示例中，foreach2.pl 程序提示输入三个数字；显示第一个数字；反复将该数字加上第二个数字以递增，显示每个结果，直到结果将大于第三个数字；然后退出。关于魔术文件句柄（<>）的讨论，请参见第 1066 页。

```perl
$ cat ./foreach2.pl
#!/usr/bin/perl -w
print "Enter starting number: ";
$start = <>;

print "Enter ending number: ";
$end = <>;

print "Enter increment: ";
$incr = <>;

if ($start >= $end || $incr < 1) {
    die ("The starting number must be less than the ending number\n",
        "and the increment must be greater than zero.\n");
}

foreach ($count = $start + 0; $count <= $end; $count += $incr) {
    say "$count";
}
```

```
$ ./foreach2.pl
Enter starting number: 2
Enter ending number: 10
Enter increment: 3
2
5
8
```

在提示输入三个数字后，前面的程序测试起始数字是否大于或等于结束数字，或者增量是否小于 1。|| 是逻辑或运算符；if 之后括号内的表达式，如果该运算符之前的表达式或之后的表达式任一评估为 *true*，则该表达式评估为 *true*。

*foreach* 语句开始时将 *$start*+0 的值分配给 *$count*。向字符串 *$start* 加上 0（零）迫使 Perl 在数值上下文中工作，在分配时去除尾部的 NEWLINE。如果没有此修正，程序将在显示的第一个数字后显示一个额外的 NEWLINE。

## while/until

*while*（第 970 页）和 *until*（第 974 页）控制结构是复合语句，使用以下语法实现条件循环：

```
while (expr) { ... }
until (expr) { ... }
```

这些结构仅在终止条件的意义上有所不同。*while* 结构重复执行语句块，只要 *expr* 评估为 *true*；*until* 继续执行，直到 *expr* 评估为 *true*（即，在 *expr* 保持 *false* 期间）。

以下示例演示了一种读取和处理输入的技术，直到没有更多输入为止。虽然该示例显示输入来自用户（标准输入），但该技术对于来自文件的输入同样有效（参见第 1068 页的示例）。用户在一行中单独输入 CONTROL-D 来指示文件结束。

在此示例中，*expr* 是 *$line* = *<>*。该语句使用魔术文件句柄（*<>*；第 1066 页）从标准输入读取一行，并将其读取的字符串赋值给 *$line* 变量。只要它读取到数据，该语句就评估为 *true*。当到达文件末尾时，该语句评估为 *false*。只要仍有数据可读，*while* 循环就会继续执行语句块（在此示例中，仅有一条语句）。

```perl
$ cat while1.pl
#!/usr/bin/perl -w
$count = 0;
while ($line = <>) {
    print ++$count, ", $line";
}
print "\n$count lines entered.\n";
```

