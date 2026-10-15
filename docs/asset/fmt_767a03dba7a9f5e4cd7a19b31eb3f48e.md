
```text
此脚本应该产生：
I used to get paid in pounds
But now I get paid in dollars
Ideally, I'd like to get paid in donuts
```

> ¹ 该操作符的语法与 Unix `sed` 命令的语法非常相似，该命令执行非常相似的功能（在许多其他方面）。我们将在第 5.8 章中简要提到 sed。

# 理解脚本

我们从一个存储在 `$currency` 变量中的字符串 `'pounds'` 开始。第 8 行使用 `'pounds'` 作为模式并将其替换为字符串 `'dollars'`。更具体地说，Perl 首先会询问：“我能在变量 `$currency` 中的任何地方找到模式 `'pounds'` 吗？”如果存在匹配项，Perl 就会继续执行替换步骤。

第 12 行执行了另一次替换，但这次的替换模式实际上是一个变量而不是一个固定字符串。你可以在替换操作符的匹配或替换部分（或两者都）使用变量。请注意，第二次替换只影响了输入字符串的一部分。

# 在绑定操作符中使用选项

让我们来看在默认模式下使用替换操作符时出现的一个非常常见的问题。幸运的是，这是一个非常容易修复的问题。

## 示例 4.11.4

此脚本尝试将 DNA 序列转换为 RNA 序列。37 在运行此脚本之前，尝试预测该脚本的输出将是什么。

```perl
1. #!/usr/bin/perl
2. # dna_to_rna.pl
3. use strict; warnings;
4.
5. my $dna = "ATCGAGGATGGCTTTATTGA";
6. my $rna = $dna;
7. $rna ~ s/T/U/; # 将胸腺啶转为尿嘧啶
8. print "$dna\n$rna\n";
```

> 37 RNA 使用核苷酸尿嘧啶 (U) 而不是胸腺啶 (T)

### 理解脚本

在这个脚本中，我们创建了 `$dna` 变量的副本并将其赋值给新变量 `$rna`。当你编写修改数据的 Perl 脚本时，你通常希望保留原始的、未更改的数据。

你可能已经注意到输出并没有将所有的“T”都更改为“U”。事实上，替换操作符只更改模式第一次出现的地方。

显然，我们想要更改模式的所有出现处，而不仅仅是第一个。我们经常想做的另一件事是无论文本是大写还是小写，都更改（或匹配）文本。Perl 通过允许你在指定匹配或替换之后指定额外的选项，让你非常容易地完成这两件事情。以下是你如何使用 Perl 替换所有匹配项（所谓的“全局替换”）并同时忽略字符串的大小写：

```perl
$string ~ s/T/U/g; # 'T' 到 'U' 的全局替换
$string ~ s/T/U/i; # 替换字符串中的第一个 'T' 或 't' 为 U
$string ~ s/T/U/g; # 'T' 或 't' 到 'U' 的全局替换
```

`g` 选项告诉 Perl 进行全局替换，即替换匹配的所有出现处。`i` 选项指示 Perl 忽略匹配的大小写。注意，你可以同时使用多个选项（指定选项的顺序并不重要）。还有几个可用选项，但这两个是你使用得最频繁的。是时候看另一个例子了！

## 示例 4.11.5

希望你正开始越来越擅长在运行这些脚本之前预测它们将做什么。

```perl
1. #!/usr/bin/perl
2. # revelation.pl
3. use strict; use warnings;
4.
5. my $text = "TREESWTESOTREESDTREES";
6. $text ~ s/TREES//g;
7. print "text\n";
```

### 理解脚本

你应该意识到此脚本的第 6 行正在执行替换。但请注意这里没有替换模式。当你不指定替换模式时，你实际上是指定了“空”。因此，这段 Perl 代码将字符串 `"TREES"` 的所有出现处替换为空——即它将删除 `"TREES"`。因为我们包含了全局选项，我们删除了该字符串的所有出现处，从而揭示了一个新词。³38

你认为这个脚本会做什么？它会打印任何内容吗？

```perl
1. #!/usr/bin/perl
2. # will_I_print_anything.perl
3. use strict; use warnings;
4.
5. my $sequence = "AACTCGGAATTCCACGT";
6. my $empty_sequence = "";
7.
8. if ($sequence ~ m//)
9. print "I am here, therefore m// must match '$sequence\n";
10. }
11.
12. if ($empty_sequence ~ m//);
13. print "I am here, therefore m// must match 'empty_sequence\n";
14. }
```

> ³3⁸ 这个例子是在玩习语“井者不见林”（Can't see the word for the trees.）。

# 4.12 置换操作符

置换字面上说是一个独立的章节，因为它与我们在上一章介绍的两个匹配操作符略有不同。如果你已经读了本书的第五部分，你可能看到 Unix 中有一个 `tr` 命令（见第 5.5 节）。Perl 的置换操作符的行为与此命令相同。它接收一个字符列表，并将列表中的每个项目更改第二个列表中的字符，尽管我们通常在每个列表中只用一个字符。它会自动对字符串中的所有字符执行此操作（因此不需要“全局”选项）。

## 示例 4.12.1

此脚本演示了置换操作符的全方位能力。注意末尾的注释。

```perl
1. #!/usr/bin/perl
2. # transliterate.pl
3. use strict; use warnings;
4.
5. my $text = "abcdefghijklmnopqrst";
6. $text ~ tr/a-z/A-Z; # 将小写字母转为大写
7. print "$text\n";
```

## 转义运算符

替换操作符本身的一部分？简而言之，Perl 无法处理这种情况。这个问题有两个解决方案。第一种涉及字符的转义过程。我们之前在第 4.10 节中见过这个，当时我们在转义某些打印字符。然而，你也可以在匹配运算符中对字符转义：

```perl
$text ~ s:http:\\\///;
```
