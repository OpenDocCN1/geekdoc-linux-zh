
`do { next if $x = \$; # 这里什么都不做 } until $x++ > $z;`

对于 `last`，你需要详细说明：

```
LOOP: { do if $x = **; # 这里执行某些操作 $x <= $z; }
```

注意：带有修饰符条件或循环（`for`）修改的 `my`、`state` 或 `our`（例如 `my $x if ...`）的行为是未定义的。变量的值可能变为 `undef`、之前的任何赋值值，或可能是其他任何值。不要依赖它。未来版本的 `perl` 可能会与你在此尝试的版本不同。

`when` 修饰符是首次出现在 Perl 5.14 中的实验性功能。要使用它，应该包含 `v5.14` 声明。（技术上讲，它只需要 `switch`，但它的某些方面在 5.14 之前是不可用的。）仅在 `foreach` 或 `given` 块内部有效，仅当 `smartmatch$_ --- EXPR` 为真时执行语句。如果语句执行，随后将紧跟来自内部的 `next` 和来自内部的 `break`。

在当前实现下，`foreach` 循环可以在 `we` 修饰符动态作用范围内的任何地方，但必须在 `given` 块的词法作用范围内。这种限制在未来的发布中可能会放宽。参见下方的“Switch Statements”。

# 复合语句

在 Perl 中，定义作用域的语句序列称为块（block）。由包含它的文件界定（对于加载的文件，或整个程序而言），每个块由字符串的范围界定（对于 `eval` 而言）。

但通常，块由大括号（也称为 braces）界定。我们将这种语法结构称为 `BLOCK`。

可以使用以下复合语句来控制流：

```
if (EXPR) BLOCK if (EXPR) BLOCK elsif (EXPR) ELSE (EXPR)
BLOCK... if (EXPR) BLOCK elsif (EXPR) BLOCK... else BLOCK unless (EXPR) BLOCK
unless (EXPR) BLOCK ELSE unless (EXPR) BLOCK elsif (EXPR) BLOCK...
unless (EXPR) BLOCK elsif (EXPR) BLOCK... else BLOCK given (EXPR) BLOCK LABEL
while (EXPR) BLOCK LABEL until (EXPR) BLOCK continue BLOCK LABEL for; EXPR;
(EXPR) BLOCK LABEL for VAR (LIST) BLOCK for VAR (LIST) BLOCK
BLOCK fetch for (EXPR; EXPR) BLOCK fetch VAR (LIST) BLOCK
LABEL fetch VAR (LIST) continue BLOCK BLOCK BLOCK
continue PHASE BLOCK
```

实验性的 `given` 语句不会自动启用；参见下方的“Switch Statements”如何这样做，以及它创建了

```
if (!open(FO)) { die "Can't open FO: $$" } die "Can't open FO: $$"
unless open(FO); open(FO) || die "Can't open FO: $$"; open(FO) ? ( :
die "Can't open FO: $$"; # 最后一个有点奇特
```

该语句是直观的。`BLOCKS` 总是由大括号界定，对于 `if` 是否跟在它后面没有任何歧义。如果你使用 `unless` 代替它，测试的含义就会反转。如果像 `like`，`unless` 后面可以跟 `else`。`unless` 甚至可以跟一个或多个语句，尽管在你使用那个特定的语言结构之前你可能想想两次，因为你代码的阅读者至少得想两次才能理解发生了什么。

`while` 语句只要表达式为真就执行块。`until` 在表达式为假时一直执行块。`LABEL` 是可选的，如果存在，它由一个标识符后跟冒号组成。`LABEL` 为循环语句 `next`、`last` 和 `redo` 标识循环。如果省略 `LABEL`，循环控制将指向最内层的闭包。这动态地回溯调用栈以找到 `LABEL`。这种欺骗性行为在你使用 `-w` 标志时触发警告。

如果存在 `continue BLOCK`，它在评估条件之前总是执行。因此，它可以用于递增循环变量，即使循环通过 `next` 语句继续。当块被 `BEGIN`、`END`、`INIT`、`CHECK` 或 `UNITCHECK` 等关键字修饰时，它将在相应的执行阶段运行。扩展模块也可以钩入 Perl 解析器以定义新类型的复合语句。这些由扩展识别。如果你正在使用此类模块，参见 `permod` 关于其定义的语法的细节。

# 循环控制

`next` 命令开始循环的下一次迭代：

```
LINE: while (<STDIN>) { next if /\/; # 跳过 ... }
```

`last` 命令立即退出所处的循环。

```
LINE: while (<STDIN>) { last if /^$/; # 完成 ... }
```

`Redo` 命令在不重新评估条件的情况下重启循环。如果存在 `continue BLOCK`，则不执行。此命令通常用于那些对输入“撒谎”的程序。例如，在处理文件 `/etc/termcap` 时，如果你的输入可能以反斜杠结尾以表示延续，你想跳过它们并获取下一行：

```
while (<>) { chop; if (s/$/) { $_ .=; redo unless eof(); } # 现在处理 $_
```

这是显式编写版本的简写：

```
LINE: while (defined($line = <ARGV>)) { chop($line); if ($line =~ s/$/)
$line .= <ARGV>; redo unless eof(); # 现在处理 $line
```

注意，如果代码上方有 `continue BLOCK`，它只在被正则表达式丢弃的行上执行：

```
# 灵感来自 :1,$fred/s//WILMA/ while (<>) { m?(fred)? && s///WILMA $1
WILMA/; m?(barney)? && s///BETTY BETTY/; m?(hor)? && s///MARGE /
} continue { print "$ARGV: $$"; close ARGV if eof; # reset. if\eof;
```

如果单词替换为顺序，循环的含义就会反转，但条件仍然在之前测试。循环控制语句在 `if` 或 `unless` 中不起作用，它们不是循环。你可以：

`if (/pattern/) { last if /fred/; next if /barney/; # 效果相当于 "last"; 但没有良好的文档 # 什么都不做 else`

这是由于块本身充当执行一次的循环，参见“Basic Blocks”。

在 Perl 4 中提供的 `while BLOCK` 形式不再可用。将任何 `BLOCK` 出现处替换为 `if (do)`。

# For 循环

Perl 的 C 风格 `for` 循环工作方式与相应的 `while` 循环相同：

```
for ($i = 1; $i < 10; $i++) { ... }
```

等同于：

```
$i = 1; while ($i < 10) { ... } continue { $i++; }
```

有一个微小的区别：如果变量在 `for` 的初始化部分用 `my` 声明，变量的词法作用域就是整个 `for` 循环（循环的体和控制部分）。否则，变量是循环局部的，并在退出循环时恢复其 `for` 值。如果变量之前用 `my` 声明，它将使用它 全局变量，但它仍然被限制在循环中。这种隐式局部化仅发生在 `foreach` 循环中。

作为一个特殊情况，如果此类 `for` 循环（或相应的 `while` 循环）中的测试为空，它被视为真。也就是说，两者

```
for (;;) { ... }
```

和

```
while () { ... }
```

都被视为无限循环。

除了普通的数组索引，`for` 自身可以用于许多有趣的应用程序。这里是你显式测试交互式文件描述符时会遇到的问题之一，这会导致你的程序看起来挂起了。

```
$on_a_tty = -t STDIN & -t STDOUT; sub print "yes? " if $on_a_tty
} for (print()); <STDIN>; print() { # 做 something }
```

使用 `readline`（运算符形式，`<EXPR>`）作为 `for` 循环的条件是以下内容的简写。这种行为与 `while` 循环条件相同。

```
for (print()); defined($_ = <STDIN>); print() { # 做 something }
