

## 解释

- 1. 标量变量 $num 被赋值为 5。
- 2. 数组被赋予三个颜色。@ 是一个用于创建值列表的特殊字符。@ 在双引号内被解释。
- 3. 字符串被双引号包围。标量变量的值被打印。字符串字面量 \n 被解释。
- 4. @ 被评估，值的数组被打印。
- 5. 当美元符号 ($) 前面有一个反斜杠时，它作为一个字面量的美元符号被打印；换句话说，变量替换被忽略。
- 6. 特殊字面量 \t 和 \n 在双引号内被解释。

**单引号**。如果字符串被单引号包围，它将按字面打印（所见即所得）。如果需要在字符串内部使用单引号，它可以嵌入在双引号内或加上反斜杠转义。如果双引号需要按字面处理，它们可以嵌入在单引号内。

## 示例 4.4

```perl
(脚本)
use warnings;
# 单引号
1 print 'I need $100.00.', "\n";
2 print 'The string literal, \\t, is used to represent a tab.', "\n";
3 print 'She cried, "Help me!"', "\n";
```

```text
(输出)
1 I need $100.00.
2 The string literal, \\t, is used to represent a tab.
3 She cried, "Help me!"
```

## 解释

- 1. 美元符号按字面解释。在双引号中，它会被解释为标量。这里的 \n 在双引号中，以便进行反斜杠解释。
- 2. 字符串字面量 \t 不会被解释为制表符，而是按字面打印。
- 3. 当双引号被单引号包围时受到保护（即，它们按字面打印）。

**反引号**。放在反引号内的 UNIX/Windows 命令由 Shell 执行，输出作为字符串返回给 Perl 程序，通常被赋值给变量或作为 *print* 字符串的一部分。当命令的输出被赋值给变量时，上下文是标量（即，赋值给单个值）。[^4] 为了进行命令替换，反引号不能被封闭在双引号或单引号中。（请注意：UNIX Shell 程序员：反引号不能像在 Shell 程序中那样被封闭在双引号中。）

> 3. 如果使用其他操作系统，如 Microsoft 或 Mac OS 9.1 及以下版本，你的系统可用的 OS 命令将有所不同。

## 示例 4.5

```perl
(Unix/Linux 的脚本)
use warnings;
# 反引号和命令替换
1  print "The date is `date`.\n";
2  print "The date is `date`\n";       # 反引号按字面处理
3  $directory=`pwd`;                    # Windows 用户：`cd`
4  print "The current directory is $directory.\n";
```

```text
(输出)
1  The date is Mon Jun 25 17:27:49 PDT 2014.
2  The date is `date`.
3  The current directory is /home/jody/ellie/perl.
```

## 解释

- 1. UNIX `date` 命令将由 Shell 执行，其输出将返回到 Perl 的 `print` 字符串中。`date` 命令的输出包括换行符。对于 Windows 用户，命令是 `date /T`。
- 2. 当反引号被封闭在单引号或双引号中时，不会发生命令替换。
- 3. 标量变量 `$directory`（包括换行符）被赋予 UNIX `pwd` 命令（即，当前工作目录）的输出。对于 Windows 用户，命令是 `cd`。
- 4. 标量 `$directory` 的值被打印到屏幕上。

## Perl 的替代引号

Perl 提供引号的替代形式——`q`、`qq`、`qx` 和 `qw` 结构。

- `q` 代表单引号。
- `qq` 代表双引号。
- `qx` 代表反引号。
- `qw` 代表带引号的单词列表。（参见表 4.1。）

### 表 4.1 替代引号结构

| 引号结构 | 它代表的含义 |
| :--- | :--- |
| `q/Hello/` | `'Hello'` |
| `qq/Hello/` | `"Hello"` |
| `qx/date/` | `` `date` `` |
| `@list=qw/red yellow blue;/` | `@list=('red', 'yellow', 'blue');` |

要被引用的字符串被**正斜杠**包围，但你也可以使用所有四种 *q* 结构的替代分隔符。你可以使用非字母字符作为分隔符，例如 # 号、! 点，或配对的字符，如括号、方括号等。你也可以使用单个字符或配对的字符。例如：

q/Hello/
q#Hello#
q(Hello)
q[Hello]
q{Hello}
q(Hello)

## 示例 4.6

```perl
(脚本)
use warnings;
# 使用替代引号
1 print 'She cried, "I can't help you!"', "\n"; # 笨拙
2 print qq/She cried, "I can't help you!"\n/; # qq 代表双引号
3 print q(I need $5.00\n); # 真的需要单引号
4 print q(I need $5.00\n); # 为了打印字面量的美元符号
5 print qq(I need \$5.00\n); # 反斜杠解释怎么办？
6 print qq/\n/, q/I need $5.00/, "\n";
7 print qq/The present working directory is /, qx(pwd);
8 print qq/Today is /, qx(date +%H); # 对于 Windows 使用 qx(date +#
9 print "The hour is ", qx(date +%H); # 仅限 Unix
```

```text
(输出)
1 She cried, "I can't help you!"
2 She cried, "I can't help you!"
3 I need .00
4 I need $5.00\nI need $5.00
5 I need $5.00
6 I need $5.00
7 The present working directory is /home/jody/ellie/perl
8 Today is Mon Jun 25 17:29:34 PDT 2014
9 The hour is 17
```

## 4.3 print 函数

## 解释

字符串被单引号包围。这使得对话引号可以按字面打印。`can't` 中的单引号用反斜杠转义，以便它也能按字面打印。如果没有这样做，它将与第一个单引号配对。那么结束的单引号将没有配对，不幸的是，程序要么会告诉你有一个未闭合的引号，要么寻找其配对直到意外地到达文件末尾。

`qq` 结构替代双引号。现在使用括号作为字符串的分隔符。因为使用了 `qq`，$5.00 中的美元符号 ($) 被解释为一个值为 null 的标量变量。.00 被打印。（这不是处理你金钱的正确方式！）单个 `q` 替代单引号。$5 被视为字面量。不幸的是，\n 也是如此，因为反斜杠解释不会在单引号内发生。没有换行符，下一行将与第 4 行连在一起。在下一行中，如果美元符号前面有一个反斜杠，该反斜杠“转义”了 $ 的特殊含义。现在字符串将正确打印。

\n 通过 `qq` 结构使用双引号，字符串 *I need $5.00* 通过 `q` 结构使用单引号，第二个 \n 使用传统的旧式双引号。

替代分隔符，感叹号 (!)，用于 `q` 结构（而不是正斜杠）来分隔字符串。

字符串 *The present working directory* 被双引号包围；UNIX 命令 `pwd` 被封闭在反引号中以进行命令替换。`qq` 结构引用 *Today*；`qx` 结构替代用于命令替换的反引号。注意：为了在 MS-DOS 中获得相同的结果，date 命令使用 `/T` 选项。由于 `/T` 中有斜杠，使用了不同的分隔符。输入 `q\date//T` 会产生错误，所以将分隔符更改为其他字符，在这种情况下是 #。

替代分隔符，花括号，用于 `qx` 结构（而不是正斜杠）。UNIX `date` 命令的输出被打印。

引号规则影响你在 Perl 中做的几乎所有事情，特别是在打印单词字符串时。字符串通常由匹配的一对双引号或单引号分隔。当字符串被单引号包围时，所有字符都被视为字面量。然而，当字符串被双引号包围时，*几乎*所有字符都被视为字面量，除了用于变量替换和特殊转义序列的那些字符。我们将在本章中查看特殊转义序列，并在第 5 章“名字里有什么？”中讨论引号和变量。

Perl 使用某些字符作为特殊用途，例如美元符号 ($) 和 at (@) 符号。如果这些特殊字符需要被视为字面字符，它们前面可以加一个反斜杠 (`\`) 或封闭在单引号 (') 中。使用反斜杠来引用单个字符，而不是字符字符串。

