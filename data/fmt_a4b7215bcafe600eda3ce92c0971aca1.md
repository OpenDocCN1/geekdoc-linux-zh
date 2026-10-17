
```perl
my ($match) = "A to Z, a to z" ~ m/(a.*?)/i; # $match 获取 'A to Z'
my ($match) = "Excited!!!!" ~ m/(I{3,5})?; # $match 获取 '!!!'
my ($match) = "Anne" ~ m/(Anne??); # $match 获取 'Ann'
```

注意，在这个例子中，问号承担了两个不同的功能：首先作为重复元字符，意味着“匹配 0 次”；然后作为非贪婪量词（它本质上强制迫前的元字符匹配 0 次）。

# 使用默认变量 `$_` 的正则表达式

如果你使用正则表达式来匹配默认变量 (`$_`) 的内容，你可以简化代码，因为在没有指定其他变量的情况下，匹配运算符将检查此变量：

```perl
# 普通用法
print "Match\n" if ($text ~ m/\w{3,5}/);
# 使用默认变量
print "Match\n" if m/\w{3,5}/;
```

注意，如果你使用默认变量，就不需要包含绑定运算符 (`=`)。当使用 `<>` 操作遍历文件时，你可以写出非常简洁的代码。假设我们正在处理一个文件，并将任何编码为“today”的行改为“yesterday”。

```perl
#!/usr/bin/perl
# back_in_time.pl
use strict; use warnings;

while(<>) {
    next if m/^\$/; # 跳过空行
    s/today\.\yesterday\./;
    print;
}
```

在这个例子中，匹配运算符、替换运算符以及 `print` 函数都在对 `$_` 操作。

# 匹配规则

正则表达式会尝试在目标字符串尽可能尽早进行匹配。根据模式的不同，这有时会与正则匹配的其他原则产生冲突。考虑以下内容：

```perl
my ($match) = "The fat cat sat on the mat" ~ m/(([mcf]at)/;
```

这个例子中的字符类意味着 “mat” 将是 Perl 优先考虑的第一个模式，且 “mat” 是输入字符串的有效匹配。“mat” 匹配

- 如果你想从每行输入中删除换行符，也可以使用 `chop`，这是另一个在没有指定其他变量的情况下与默认变量协作的函数。

```perl
my $text = "Bruce Wayne is Batman";
while ($text ~ /(\w+)/) {
  $position = pos($text);
  print "Word '\1' ends at position $position\n";
}

# 输出
Word 'Bruce' ends at position 5
Word 'Wayne' ends at position 11
```

```text
Word ‘is’ ends at position 14
Word ‘Batman’ ends at position 21
Word ‘is’ ends at position 14
Word ‘Batman’ ends at position 21
```

即使你没有使用变量，也可能找到匹配的内容。例子中的正则表达式可以匹配两个不同字符串之一：

```perl
"Peter Parker is Spider-man" ~ m/(.*)er(.*);
# $1 获取 ‘Peter Parker is Spid’
# $2 获取 ‘-man’，尽管这个模式也匹配 Parker is Spider-man
```

```perl
sub gc {
    my ($seq) = @_;

    $seq = uc($seq); # 转换为大写以确保正确
    my $g = $seq ~ tr/G/G/;
    my $c = $seq ~ tr/C/C/;
    my $gc = ($g + $c) / length($seq);

    return $gc;
}
```

## 理解代码

第 1 行包含 `package` 语句中的库名。通常情况下，每个文件只有一个 `package` 语句。第 2 行确保即使主程序中没有使用，库中也会使用 `strict` 和 `warnings` 预指令。第 4 到 14 行定义了一个用于计算核苷酸序列 GC 含量的函数。库必须返回“真”（true），而第 15 行确保了这一点发生。

`Library.pm` 中的 `gc()` 函数现在可以用于你编写的任何程序。之前的语法很熟悉：我们直接使用该库。

### 示例 6.2.2

```perl
#!/usr/bin/perl
# library_test.pl
use strict; use warnings;
use Library;

my ($seq) = @ARGV;
my $gc = Library::gc($seq);
```

### 理解脚本

第 4 行包含 `use Library` 语句。注意，它位于头部，与其他 `use` 语句在了一起；当 Perl 看到这一行时，它将尝试导入`Library.pm` 的内容。在指示 Perl 使用库时，你不需要包含 `.pm` 后缀。

一旦导入了库，其所有函数对程序都可用。函数的调用方式与我们调用子程序（subroutine）的方式相同；唯一的区别是，我们必须像第 7 行所示，在前面也加上库名。⁴

> ^· 可以自动导入函数，这样你就不需要前缀库名。这是一种危险的做法，我们不提倡这样做（甚至不描述它）。如果你想尝试冒险，请自行查找。

# 库路径 `PATH`

从本书的 Unix 章节中，你应该熟悉你的 `$PATH` 环境变量（第 3.28 节）。就像 Unix 命令一样，Perl 库可以存在计算机上的各个位置。在示例中，我们看到 `Library.pm` 和 `library_test.pl` 两个文件位于同一个目录下（我们希望它们如此）。如果你没有将它们保存在同一个目录，你将看到类似下面的错误：⁵

```text
Can't locate Library.pm in @INC @INC contains: /path1/:path2
```

Perl 在多个地方查找库，包括当前工作目录。如果你想查看 Perl 查找的所有位置，尝试打印 `@INC` 变量。

```perl
#!/usr/bin/perl
print join("\n", @INC), "\n";
```

如果你将 `Library.pm` 移动到 `@INC` 数组列出的任何位置，Perl 都能找到它。然而，这些位置中的某些位置可能是受保护的，你不应该把库放在那里。相反，你应该将你的个人库位置添加到 `@INC` 中。对于这一点，有多种方法可以实现。首先，让我们 `Library.pm` 移动到另一个位置，让 Perl 找不到它。

```bash
$ mkdir lib
$ mv Library.pm lib/
$ perl library_test.pl
```

现在再次运行 `library_test.pl`。如果你之前没有看到错误信息，现在应该能看到了。Perl 再也找不到 `Library.pm` 了。有几种方法可以告诉 Perl 它在何。一种方法是在脚本的头部使用 `use` 语句。⁷

```perl
use "/complete/path/to/your/code/directory/lib";
```

这种做法的缺点是，如果你将脚本移动到另一台电脑，`Library.pm` 文件可能会出现在新的位置，因此你可能需要相应地编辑脚本。另一种方法是使用 Perl 的 `-I` 命令行，它允许你指定 Perl 库的位置：

```bash
$ perl -I /path/to/library script.pl
```

你也可以将此 `-I` 作为“shebang”行的一部分：

```bash
#!/usr/bin/perl -I /path/to/library
```

然而，这引发了与之前相同的问题——你可能需要根据你正在使用的电脑来编辑脚本。设置 Perl 库路径的最佳方法是使用 `$PERLLIB` 环境变量。它的工作原理与你的 `$PATH` 变量类似。

> ⁵ 你的错误信息看起来会不同。可能会显示许多路径，并带有很长且可能奇怪的名字。

> ⁷ 你可能需要使用 `push()` 函数将你的个人库目录添加到 `@INC` 数组中，但这是不可行的，因为库是在编译期间加载的，而 `push()` 发生在之后，即运行时。

# 函数库 259

变量（该变量允许你提供一个用冒号分隔的目录列表）。通过这种策略，你不需要修改脚本，只需要修改你的 `.profile` 或 `.cshrc`。

```bash
export PERLSLIB=/path/to/library:${PERLSLIB} # bash
setenv PERLSLIB /path/to/library:${PERLSLIB} # csh
```

# `package` 语句
