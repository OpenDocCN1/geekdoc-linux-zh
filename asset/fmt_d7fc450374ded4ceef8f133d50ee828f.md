
```
system('cp /home/httpd/logs/access.log /tmp/httpd.log') == 0

or die "system failed: $?";
```

然而，你无法捕获通过 `system` 函数执行的命令输出。

# 模块和 CPAN

Perl 社区（以及 Linux 社区）的一大优势是它是一个开源社区。通过全面 Perl 存档网络 (CPAN) 支持 Perl，CPAN 是代码镜像网络。大多数 CPAN 由模块组成，这些模块是可重用的代码块，可以执行有用操作，就像程序员的函数一样。这些模块在构建 Perl 程序时有助于加速开发并避免重复造轮子。

Perl 自带了一套标准模块。这些模块包含了你最初使用 Perl 需要的大部分功能。如果你需要使用 Ubuntu 未安装的模块，可以使用 `CPAN`（标准模块之一）将其他模块下载并安装到你的系统中。在 www.perl.com 上，可以使用 `CPAN`（标准模块之一）下载并安装其他模块到你的系统中。

# 使用 Perl 安装 `CPAN` 模块

你可以使用 Perl 交互式地从 CPAN 存档下载并安装 Perl 模块，使用 `-M` 和 `-e` 命令。通过如下方式使用 Perl 开始：

```
# perl -CPAN -e shell
```

当你按下回车时，你会看到一些介绍信息，并被要求选择初始自动或手动配置，这在下载或安装之前是必须的。输入 no 并按回车让 Perl 自动配置下载和安装过程；或者如果你愿意，直接按回车手动配置下载和安装。如果你使用手动配置，必须回答关于路径、缓存、终端设置、程序位置等的问题。设置保存在当前目录下的 `.cpan` 目录中。

完成后，你会看到 CPAN 提示符：

```
cpan>
```

2.  如果你决定需要跳过循环的剩余内容而不结束循环本身，可以使用 `next`，它类似于 C 语言中的 `continue` 命令。遗憾的是，这些语句在 `do ... while` 中不起作用。不过，你可以使用 `redo` 跳转到循环（由标签标记）或跳转到调用它的循环内部：

```
$a = 100;

while (1) {

    print "start\n";

TEST: {

    if ($a = $a / 2) > 2) {

        print "$a\n";

        if (-a < 2) {

            exit;

        }

        redo TEST;

    }

}
```

在这个简单的示例中，变量 `$a` 在循环中被反复操作和测试。单词 `start` 只会被打印一次。

# `do ... while` 和 `do ... until`

`while` 和 `until` 循环首先评估条件。通过在条件之前应用一个 `do` 块，这种行为发生了改变。使用 `do` 块后，条件最后被评估，这导致循环内容至少执行一次（即使条件为假）。这与 C 语言中的 `do ... while (conditional)` 语句类似。

# 正则表达式

Perl 最大的优势在于文本和文件处理

例如，下面这行代码将文本中每次出现的字符串 `bob` 或字符串 `mary` 替换为 `fred`：

```
$string =~ s/bob|mary/fred/gi;
```

在不涉及过多细节的情况下，表 45.7 解释了上述行的含义。

| 元素 | 解释 |
| --- | --- |
| `$string` -- | 对名为 `$string` 的变量找到的文本执行此模式匹配。 |
| `s /` | 开始要匹配的文本。 |
| `bob|mary` | 匹配文本 `bob` 或 `mary`。你应该记住，它寻找的是文本 `mary` 而不是单词 `mary`；也就是说，它也会匹配单词 `myriad` 中的文本 `mary`。 |
| `fred` | 将任何匹配到的内容替换为文本 `fred`。 |
| `g` | 全局执行此替换；也就是说，它替换字符串中匹配到的任何位置的文本（任意多次）。 |
| `i` | 搜索文本不区分大小写。它匹配 `bob`、`Bob` 或 `BOB`。表示行代码的结束。 |

> 表 45.7 `$string ~ s/bob|mary/fred/gi;` 的解释

如果你对细节感兴趣，可以在命令行中输入 `man 7 regex`，通过手册页的 `regex (7)` 部分获取更多信息。

虽然将一个字符串替换为另一个似乎是一项相当细微的任务，但在另一种语言（例如 C）中实现相同功能所需的代码除非有外部库的额外子程序支持，否则是相当困难的。

# 访问 Shell

Perl 可以通过 `` ` `` 语法向 shell 输入命令，执行你通常可能执行的任何过程。例如，列表 45.4 中的代码打印了目录列表。

列表 45.4 使用反引号访问 Shell

```
$curr_dir = 'pwd';

@listing = 'ls -al';

print "Listing for $curr_dir\n";

foreach $file (@listing) {

    print "$file";

}
```

## 注意

`` ` `` 符号使用的是 Tab 键上方的反引号（在大多数键盘上），而不是单引号。

你也可以使用 `Shell` 模块来访问 shell。`Shell` 是 Perl 自带的标准模块之一；它允许创建和使用类似 shell 的命令行。查看下面的代码示例：

```
use Shell qw(cp);

cp ("/home/httpd/logs/access.log",

:/tmp/httpd.log");
```

这段代码看起来几乎是直接将命令行函数导入到 Perl 中。虽然实际上并没有这样发生，但你可以假装代码类似于命令行，并在你的 Perl 程序中使用这种方法。

访问 shell 的第三种方法是通过通过 `system` 函数调用：

```
$rc = 0xffff & system('cp

/home/httpd/logs/access.log /tmp/httpd.log');

if ($rc == 0) {

    print "system succeeded";

} else {

    print "system failed $rc";

}
```

该调用也可以配合 `or die` 子句使用：

```
system('cp /home/httpd/logs/access.log /tmp/httpd.log') == 0

or die "system failed: $?";
```

然而，你无法捕获通过 `system` 函数执行的命令输出。

# 模块和 CPAN

Perl 社区（以及 Linux 社区）的一大优势是它是一个开源社区。通过全面 Perl 存档网络 (CPAN) 支持 Perl，CPAN 是代码镜像网络。大多数 CPAN 由模块组成，这些模块是可重用的代码块，可以执行有用操作，就像程序员的函数一样。这些模块在构建 Perl 程序时有助于加速开发并避免重复造轮子。

Perl 自带了一套标准模块。这些模块包含了你最初使用 Perl 需要的大部分功能。如果你需要使用 Ubuntu 未安装的模块，可以使用 `CPAN`（标准模块之一）将其他模块下载并安装到你的系统中。在 www.perl.com 上，可以使用 `CPAN`（标准模块之一）下载并安装其他模块到你的系统中。

# 使用 Perl 安装 `CPAN` 模块

你可以使用 Perl 交互式地从 CPAN 存档下载并安装 Perl 模块，使用 `-M` 和 `-e` 命令。通过如下方式使用 Perl 开始：

```
# perl -CPAN -e shell
```

当你按下回车时，你会看到一些介绍信息，并被要求选择初始自动或手动配置，这在下载或安装之前是必须的。输入 no 并按回车让 Perl 自动配置下载和安装过程；或者如果你愿意，直接按回车手动配置下载和安装。如果你使用手动配置，必须回答关于路径、缓存、终端设置、程序位置等的问题。设置保存在当前目录下的 `.cpan` 目录中。

完成后，你会看到 CPAN 提示符：

`cpan>`

要让 Perl 检查你的系统并下载、安装大量模块，请使用 `install` 关键字，在提示处指定 `Bundle` 然后按回车，如下所示：

```
cpan> install Bundle::CPAN
```

要下载所需的模块（如列表 45.6 所示），按如下方式使用 `get` 关键字：

```
cpan> get Mail::Sendmail
```

该模块的源代码会被下载到 `.cpan` 目录。你可以使用 `install` 关键字来构建并安装该模块，如下：

```
cpan> install Mail::Sendmail
```
