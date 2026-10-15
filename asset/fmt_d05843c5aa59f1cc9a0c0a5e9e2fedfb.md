
# unless

`unless` 的工作方式与 `if` 相似，只是方向相反。当条件为假时，`unless` 执行语句或代码块：

```perl
unless ($name eq "Rich") {
    print "Go away, you're not allowed in here!\n";
}
```

### 注意

你可以像下面这样用更自然的语言重述前面的示例：

```perl
print "Go away!\n" unless $name eq "Rich";
```

# 循环

循环是一种多次重复程序操作的方法。一个非常简单的例子是倒计时计时器，它在告诉你鸡蛋已经煮好之前，会执行 300 次任务（等待一秒）。

循环结构（也称为控制结构）可用于在满足特定条件时迭代代码块，或者让循环遍历（评估）一个值列表（value list），并可能将该列表作为参数。Perl 有四种循环结构：`for`、`while` 和 `until`。

## for

`for` 结构按照定义的定义的条件执行语句（代码块）：

```perl
for (start condition; end condition; increment function) {
    statement(s)
```

起始条件在循环开始时设置。每次执行循环时，都会执行增量函数，直到达到结束条件。这看起来非常传统的 `for/next` 循环。下面的代码是 `for` 循环的示例：

```perl
for ($i=1; $i<=10; $i++) {
    print "\$i\n"
}
```

## foreach

`foreach` 结构对列表或数组中的每个元素执行一次语句：

```perl
@names = ("alpha","bravo","charlie");
foreach $name (@names) {
    print "\$name sounding off!\n"
}
```

循环变量（示例中的 `$name`）不仅仅是设置为数组元素的值；它还是该元素的别名（aliased）。这意味着如果你修改了循环变量，你实际上修改了数组。如果没有指定循环数组，可以使用 Perl 的默认变量 `$_`：

```perl
@names = ("alpha","bravo","charlie");
foreach (@names) {
    print "$_ sounding off!\n";
}
```

这种语法可以非常方便，但也可能导致无法访问的代码。请为以后要维护你代码的可怜的人考虑一下（那个人可能你自己）。

### 注意

`foreach` 经常缩写为 `for`。

## while

`while` 在特定条件为真（true）时持续执行语句块：

```perl
while($x<10) {
    print "$x\n";
    $x++;
}
```

记住，条件可以是任何返回真值或假值的表达式。例如，它可以是一个函数调用：

```perl
while (InvalidPassword($user, $password)) {
    print "You've entered an invalid password. Please try again.\n";
    $password = GetPassword();
}
```

## until

`until` 与 `while` 语句完全相反。它在特定条件为假（false）时持续执行语句块——或者说，直到该条件变为真（true）为止：

```perl
until (ValidPassword($user, $password)) {
    print "You've entered an invalid password. Please try again.\n";
    $password = GetPassword();
}
```

## last and next

你可以使用 `last` 语句强制 Perl 提前结束循环。`last` 类似于 C 语言的 `break` 命令——退出循环。如果你决定跳过循环的剩余内容而不结束循环本身，可以使用 `next`，它类似于 C 语言的 `continue` 命令。遗憾的是，这些语句在 `do ...while` 中不起作用。

另一方面，你可以使用 `redo` 跳转到循环（由标签标记处）或调用它的循环内部：

```perl
$a = 100;
while (1) {
  print "start\n";
  TEST:
  if (($a = $a / 2) > 2) {
    print "$a\n";
    if (--a < 2) {
      exit;
    }
    redo TEST;
  }
}
```

在这个简单的示例中，变量 `$a` 在无限循环中被反复操作和测试。单词 "start" 只会被打印一次。

### ... while and do ... until

`while` 和 `until` 循环首先评估条件。你通过在条件之前应用 `do` 块来改变行为。通过 `do` 块，条件在最后被评估，这导致块的内容至少执行一次（即使条件为假）。这类似于 C 语言中的 `do ... while (conditional)` 语句。

## 正则表达式

Perl 最强大的地方在于文本文本和文件处理，这是通过使用正则表达式（regex）库实现的。正则表达式与 shell 的通配符处理和文件名扩展能力非常不同，它允许高效且方便地进行复杂的模式匹配和替换。例如，下面这段代码替换了文本行中每个字符串 `bob` 或字符串 `mary` 为 `fred`：

```perl
$string =~ s/bob|mary/fred/gi;
```

在不涉及过多细节的情况下，表 25.7 解释了上述行的含义。

## 表 25.7 `$string =~ s/bob|mary/fred/gi;` 的解释

| 元素 | 解释 |
| --- | --- |
| `$string =~` | 对名为 `$string` 的变量中找到的文本执行此模式匹配。 |
| `s` | 用另一个文本字符串替换另一个。 |
| `/` | 开始要匹配的文本。 |
| `bob|mary` | 匹配文本 bob 或 mary。你应该记住它寻找的是文本 `mary`，而不是单词 `mary`；换句话说，它也会匹配单词 `maryland` 中的文本。 |
| `/` | 结束要匹配的文本。 |
| `g` | 全局执行（globally）。 |
| `i` | 忽略大小写。 |
| `;` | 表示表达式的结束。 |

输入以下命令将你进入一个交互式 shell，通过它可以访问 CPAN。你可以在提示符处输入 `help` 来获取有关如何使用 CPAN 程序的更多信息。

```
$ perl -MCPAN -e shell
```

从 CPAN 安装一个模块（或自己编写一个模块）后，你可以将其加载到内存中，并通过 `use` 函数使用它：

```
use Time::CTime;
```

`use` 会在变量 `$INC` 列出的目录中查找模块。在这个示例中，`use` 查找名为 `Time` 的目录，其中包含一个文件 `CTime.pm`，该文件被认为包含一个名为 `Time::CTime` 的包。每个模块的发行版都包含关于使用该模块的文档。

要查看所有标准 Perl 模块（安装 Perl 时自带的），请参考 Perl 文档中的 `permodlib`。你可以在命令行提示符输入 `perldoc permodlib` 来阅读本文。

### 相关 Fedora 和 Linux 命令

- 在 Linux 上使用 Perl 时，你将使用这些命令和工具：

- `a2p`—用于将 awk 脚本翻译为 Perl 的过滤器

- `find2perl`—一个使用 `find` 命令从命令行创建 Perl 代码的工具

- `pcregrep`—一个使用与 Perl 兼容的正则表达式搜索数据的工具

- `percc`—一个 Perl 程序的编译器

- `perdoc`—一个读取 Perl 文档的工具

- `s2p`—用于将 sed 脚本翻译为 Perl 的过滤器

- `vi`—vi（实际上是 vim）文本编辑器

## 引用

- [http://www.perl.com/](Tom Christians 维护着 Perl 语言主页。这里可以找到关于 Perl 的各种信息，从它的历史和文化到实用的技巧。这里也是为你的系统下载 Perl 解释器的地方。)

- [http://www.perl.com/CPAN](这是上述网站的一个部分，但值得单独提及。CPAN（全面 Perl 归档网络）是你寻找 Perl 模块和程序的地方。如果你用 Perl 写了你认为特别有用的东西，可以在这里提供给 Perl 社区。)

- [http://www.perl.com/pub/q/FAQs](常见 Perl 查询的常见问题索引；该网站提供了一种快速搜索 Perl 相关答案的方便方法。)
