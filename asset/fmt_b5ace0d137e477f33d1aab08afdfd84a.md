
`foreach` 关键字是 `for` 关键字的同义词，你可以使用任何一个。
`VAR` 是省略的，`$_` 被设置为每个值。

如果任何列表是左值（lvalue），你可以通过修改循环内部的 `VAR` 来修改它。
反之，如果任何列表不是左值，则任何修改它的尝试将失败。
换句话说，`foreach` 索引变量是你正在循环的列表中的每个项的隐式别名。

如果某个 `LIST` 是一个数组，如果你在循环体中添加或删除元素（例如使用 `splice`），`foreach` 可能会变得非常困惑。不要这样做。

如果 `VAR` 是一个绑定变量（tied variable）或其他特殊变量，`foreach` 的行为可能不会像你预期的那样工作。不要这样做。

从 Perl 5.22 开始，这种循环有一个实验性变体（experiential variant），它接受一个带有反斜杠的变量作为 `VAR`，在这种情况下，`LIST` 中的项必须是引用。带反斜杠的变量将是列表中每个引用项的别名，这些项必须是正确的类型。在这种情况下，变量不需要是标量，且反斜杠后面可以跟 `my`。要了解用法，请参见 `perlref` 中的“赋值给引用”（Assigning to References）。

### 示例

```
for (@) { $s foo/bar/ for my $elem (@elements) { $elem *= 2; for $count

(reverse(1..10), "BOOM") print $count, "\n"; 1); for (1..15) { print

"Merry Christmas\n"; foreach $item (split(/:\\n:]*/, $ENV{TERMCAP})) {

print "Item\n"; use feature "refaliasing"; for no warnings

# experiential::refaliasing; foreach \y %hash (@array_of_hash-references) {

# do something which each is %hash
```

以下是 C 程序如何在 Perl 中实现这种特定的算法：

```
for ($my $i = 0; $i < @array1; $i++) { for ($my $j = 0; $j < @array2; $j++) if

$array1[$i] += $array2[$j]; } # can't go out to :- ($array1[$i] +=

$array2[$j]]; # this is that last takes
```

而这里是 Perl 程序如何更方便地使用惯用法来完成：

```
OUTER: for $wid (@array1); for my $jet (@array2) next OUTER if

$wid > $jet; $wid = $jet;
```

看这有多简单？它更简洁、更安全、更快。它更快是因为它的噪音更少。如果在内层和外层循环之间添加代码，它是更安全的，因为新代码不会意外执行。它是显式地执行另一个循环，而不是终止内部循环。而且 Perl 执行 `foreach` 语句比执行等效的 `for` 循环更快。

敏锐的 Perl 黑客注意到循环是有返回值的，这个值可以通过将循环封装在 `do` 块中来捕。。发现的奖励是这条警告建议：循环的返回值是不未指定的，并且可能会在不通知的情况下更改。不要依赖它。

# 基础 BLOCK

任何循环控制语句的 `BLOCK`（无论是否有标签）在语义上都等同于执行一次的循环。因此，你可以使用它（注意：这不是 `eval()`、`sub()`，或者与大众认知不同，`do{}` 块并不被视为循环）。`continue` 块是可选的。

`BLOCK` 结构可以用于分支结构。

```
SWITCH: if (/^abc/) { $abc = 1; last SWITCH; if (/^def/) { $def = 1;

last SWITCH; if (/^xyz/) { $xyz = 1; last SWITCH; } $nothing = 1; }
```

你还会发现用 `foreach` 循环来创建一个可视化器和一个 `switch`：

```
SWITCH: if (/^abc/) { $abc = 1; last SWITCH; if (/^def/) {

$def = 1; last SWITCH; if (/^xyz/) { $xyz = 1; last SWITCH; } $nothing

1; } }
```

此类结构被频繁使用，因为旧版本的 Perl 没有官方的 `switch` 状态，而且因为新版本 `rains remains` 令人困惑。

# Switch 语句

从 Perl 5.10 开始（好吧，5.10.0 并没有正常工作），你可以使用 `use feature "switch";` 来启用实验性的 `switch` 功能。这粗略基于旧版本的 Perl 6 提案，但不再需要 `switch` 结构。每当你的代码倾向于在 5.10 或更高版本的 Perl 下运行时，例如：

```
use v5.14;
```

在 `"switch"` 功能下，Perl 获得了实验性的 `given`、`when`、`default`、`continue` 和 `break`。从 Perl 5.16 开始，可以在关键字前加上 `CORE:` 在不使用 `use` 语句的情况下访问该功能。`given` 和 `when` 关键字类似于其他语言中的 `switch`，因此在 `foreach` 循环中的代码可以重写为：

```
use v5.10.1; for ($var) when (/^abc/) { $abc = 1 } when (/^def/) {

$def = 1 } when (/^xyz/) { $xyz = 1 } default { $nothing = 1 }
```

`foreach` 是非实验性的设置方式。如果你想使用实验性的 `given`，可以这样写：

```
use v5.10.1; for ($var) when (/^abc/) { $abc = 1 } when (/^def/) {

$def = 1 } when (/^xyz/) { $xyz = 1 } default { $nothing = 1 }
```

在 5.14 之后，也可以这样写：

```
use v5.14; for ($var) when (/^abc/) { $abc = 1 } when (/^def/) {

$def = 1 } when (/^xyz/) { $xyz = 1 } default { $nothing = 1 }
```

或者如果你为了安全，可以这样做：

```
use v5.14; given ($var) { $abc = 1 } when (/^abc/) when (/^def/) {

$def = 1 } when (/^xyz/) { $xyz = 1 } default { $nothing = 1 } }
```

`given` 和 `when` 的参数在标量上下文中，`given` 分配 `$_` 值。`when` 的 `EXPR` 参数很难描述，但通常它会尝试你想执行的操作。`$_` 被解释为 `$EXPR`，而 `when` 也不是。它在被词法封装的 `given` 块中的行为与被动态封装的 `foreach` 循环中不同。这里的规则太难以理解了。参见后文的“given 和 when 的实验性细节”。由于在 5.10 到 5.16 之间 `given` 实现方式的一个意外 Bug，在这些实现中 `given` 是原始的词法作用域副本，是原始的动态别名，就像 `foreach` 或当前的 Perl 6 规范一样。这个 Bug 在 Perl 5.18 中被修复了。如果你真的想要，但注意 `$_` 现在已弃用，除非禁用了警告否则会警告：

```
given( EXPR) { ... }
```

如果你的代码仍在旧版本上运行，请坚持使用 `foreach`，否则解析器会不高兴。

# Goto

虽然不适合胆子小的人，但 Perl 支持 `goto`。有三种形式：`goto-LABEL`、`goto-EXPR` 和 `goto-NAME`。循环实际上不是 `goto` 的有效目标；这只是它的本质。

`goto-LABEL` 形式找到带有 `LABEL` 的语句并从那里恢复执行。它可能无法进入任何需要初始化的结构，例如子程序或 `foreach` 循环。它不能用于进入被优化的结构。它可以跳转到动态作用范围内的任何地方，包括退出子程序，但通常使用其他结构如 `last` 或 `die` 更好。Perl 的作者从未觉得有必要使用这种形式的 `goto`（在 Perl 中，那是另一回事）。

`goto-EXPR` 形式期望一个标签，其作用域将动态解析。这允许为 FORTRAN 使用计算 `goto`，但如果你是为了可维护性进行优化，则不推荐：
