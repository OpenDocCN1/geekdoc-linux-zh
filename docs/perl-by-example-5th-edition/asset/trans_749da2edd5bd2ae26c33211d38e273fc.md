
## 示例 9.21

**脚本**

```perl
use warnings;
# Repeating patterns
while(<DATA>) {
    print if /5{3}/;
}

__DATA__
Steve Blenheim 1.10
Betty Boop .5
Igor Chevaky 555.100
Norma Cord 4.01
Jonathon DeLoach .501
Karen Evich 601
```

**输出**

Igor Chevaky 555.100

## 解释

该表达式读作：查找数字 5 的三次连续出现。这并不意味着字符串中必须恰好包含三个且仅三个数字 5。它的意思只是必须至少有三个数字 5 连续出现。如果字符串包含 5555555，匹配仍然会成功。若要查找恰好三个数字 5，该模式必须以某种方式锚定，要么使用 `^` 和 `$` 锚点，要么在三个 5 的前面或后面放置其他字符，例如 `/5{3}5/` 或 `/5{3}898/` 或 `/95{3}\n56/`。

## 示例 9.22

**脚本**

```perl
use warnings;
# Repeating patterns
while(<DATA>) {
    print if /5{1,}/;
}

__DATA__
Steve Blenheim 1.10
Betty Boop .5
Igor Chevaky 555.100
Norma Cord 4.01
Jonathon DeLoach .501
Karen Evich 601
```

**输出**

Betty Boop .5
Igor Chevaky 555.100
Jonathon DeLoach .501

## 解释

该表达式读作：查找数字 5 至少一次或多次重复出现。

### 9.2 正则表达式元字符

**关闭贪婪模式的元字符。** 通过在贪婪量词后添加一个问号，贪婪模式就会被关闭，搜索将在第一次匹配后结束，而不是在最后一次匹配后结束。表 9.6 描述了用于关闭贪婪模式的元字符。

![](img/8556abcb353c0991f12099420ec28735_296_0.png)

**脚本**

```perl
1   use warnings;
2   # greedy and not greedy
3   $_ = "abcdefghijklmnopqrstuvwxxyz";
4   s/[a-z]+/XXX/;
5   print $_, "\n";
6
7   $_ = "abcdefghijklmnopqrstuvwxxyz";
8   s/[a-z]+?/XXX/;
9   print $_, "\n";
```

**输出**

9   XXX
10  XXXabcdefghijklmnopqrstuvwxxyz

![](img/8556abcb353c0991f12099420ec28735_296_1.png)

- 1. 标量 `$_` 被赋值一个由小写字母组成的字符串。
- 2. 正则表达式读作：查找一个或多个小写字母，并将它们替换为 XXX。`+` 元字符是贪婪的。它会获取尽可能多的匹配表达式的字符；也就是说，它从字符串的左侧开始，尽可能多地获取小写字母，直到字符串末尾。
- 3. 替换后，打印 `$_` 的值。整个字符串已被替换为 XXX。
- 4. 标量 `$_` 再次被赋值一个由小写字母组成的字符串。
- 5. 正则表达式读作：查找一个或多个小写字母，并在找到第一个后，**停止**搜索并将其替换为 XXX。附加在 `+` 后的 `?` 关闭了该元字符的贪婪性。搜索最少数量的字符。字母 a 被替换为 XXX，字符串其余部分保持不变。
- 6. 替换后，打印 `$_` 的值。

![](img/8556abcb353c0991f12099420ec28735_296_2.png)

| 元字符 | 匹配内容 |
| :--- | :--- |
| x?? | 匹配 x 的 0 次或 1 次出现 |
| (xyz)?? | 匹配模式 xyz 的 0 次或 1 次出现 |
| x*? | 匹配 x 的 0 次或多次出现 |
| (xyz)*? | 匹配模式 xyz 的 0 次或多次出现 |
| x+? | 匹配 x 的 1 次或多次出现 |

| 元字符 | 匹配内容 |
| :--- | :--- |
| (xyz)+? | 匹配模式 xyz 的 1 次或多次出现 |
| x{m,n}? | 匹配至少 m 次且不超过 n 次的 x |
| x{m,}? | 匹配至少 m 次的 x |
| x{m}? | 匹配恰好 m 次 |

## 示例 9.24

**脚本**

```perl
1  # A Greedy quantifier
2  $string="I got a cupful of sugar and two cups of flour from the cupboard.";
3
4  $string =~ s/cup.*/tablespoon/;
5  # Turning off Greed
6  $string="I got a cupful of sugar and two cups of flour from the cupboard.";
7  $string =~ s/cup.*?/tablespoon/;
8  print "$string\n";
```

**输出**

5 I got a tablespoon
6 I got a tablespoonful of sugar and two cups of flour from the cupboard.

## 解释

- 1. 标量 $string 被赋值一个包含 *cup* 模式三次的字符串。
- 2. *s*（替换）运算符查找模式 *cup* 后跟零个或多个字符；即，*cup* 及其后直到行末的所有字符都被匹配并替换为字符串 *tablespoon*。`*` 被称为贪婪量词，因为它匹配最大的可能模式。
- 3. 输出显示了贪婪替换的结果。
- 4. 标量 $string 被重置。
- 5. 这次搜索不是贪婪的。通过在 `*` 后添加一个问号，匹配 *cup* 后跟零个或多个字符的最小模式被替换为 *tablespoon*。只有第一个 *cup* 会被替换为 *tablespoon*，结果是 *tablespoonful*。此示例旨在展示贪婪元字符的工作方式。另一种写法是：`s/cup\S*/tablespoonful/`
- 6. 打印新的字符串。

### 9.2 正则表达式元字符

**锚定元字符。** 通常需要锚定元字符，使其仅在模式位于行、单词或字符串的开头或末尾时匹配。这些元字符基于正在匹配的字符左侧或右侧的位置。锚点（见表 9.7）在技术上被称为**零宽断言**，因为它们对应的是位置，而不是字符串中的实际字符。例如，`/^abc/` 的意思是：在行首查找 *abc*，其中 `^` 代表一个位置，而不是实际字符。

| **元字符** | **匹配内容** |
| :--- | :--- |
| `^` | 匹配行首或字符串首 |
| `$` | 匹配行尾或字符串尾 |
| `\A` | 仅匹配字符串开头 |
| `\Z` | 匹配字符串或行尾 |
| `\z` | 仅匹配字符串末尾 |
| `\G` | 匹配上一次 `m/g` 操作停止的位置 |
| `\b` | 匹配单词边界（当不在 `[]` 内部时） |
| `\B` | 匹配非单词边界 |

**脚本**

```perl
use warnings;
# Beginning-of-line anchor
1   while (<DATA>) {
2       print if /^ [JK]/;
    }
__DATA__
Steve Blenheim 1.10
Betty Boop  .5
Igor Chevaky 555.100
Norma Cord 4.01
Jonathan DeLoach .501
Karen Evich 601
```

**输出**

Jonathan DeLoach .501
Karen Evich 601.100

## 解释

正则表达式包含脱字符（^）元字符，仅当它是模式中的第一个字符时，才代表行首锚点。该表达式读作：在行首查找 J 或 K。在此示例中，^ 与脱字符产生的结果相同。表达式 `/[^J]K/` 读作：在行首查找非 J 或非 K 字符。请记住，当脱字符位于字符类内部时，它会取反该字符类。它仅在紧跟在左定界符之后时才作为行首锚点。

## 示例 9.26

**脚本**

```perl
use warnings;
# End-of-line anchor
while(<DATA>){
    print if /10$/;
}
__DATA__
Steve Blenheim 1.10
Betty Boop .5
Igor Chevyvsky 555.10
Norma Cord 4.01
Jonathan DeLoach .501
Karen Evich 601
```

**输出**

Steve Blenheim 1.10
Igor Chevyvsky 555.10

## 解释

正则表达式包含 $ 元字符，仅当 $ 是模式中的最后一个字符时，才代表行尾锚点。该表达式读作：查找后跟换行符的 1 和 0。

## 示例 9.27

**脚本**

```perl
use warnings;
# Word anchors or boundaries
while(<DATA>){
    print if /\bJon/;
}

_DATA_
Steve Blenheim 1.10
Betty Boop .5
Igor Chevyvsky 555.100
Norma Cord 4.01
Jonathan DeLoach .501
Karen Evich 601
```

**输出**

Jonathan DeLoach .501

## 解释

正则表达式包含 `\b` 元字符，代表单词边界。该表达式读作：查找以模式 *Jon* 开头的单词。

## 示例 9.28

**脚本**

```perl
use warnings;
# Beginning- and end-of-word anchors
1 while (<DATA>){
2 print if /\bJon\b/;
}

_DATA_
Steve Blenheim 1.10
Betty Boop .5
Igor Chevyvsky 555.100
Norma Cord 4.01
Jonathan DeLoach .501
Karen Evich 601
```

**输出**

<无输出>

## 解释

正则表达式也包含 `\b` 元字符，代表单词边界。该表达式读作：查找以 *Jon* 开头且以 *Jon* 结尾的单词。未找到任何匹配。

***m* 修饰符。** *m* 修饰符用于控制 `$` 和 `^` 锚点元字符的行为。包含换行符的字符串将被视为多行。如果正则表达式使用 `^` 元字符锚定，并且该模式在任何一行的行首被找到，则匹配成功。同样，如果正则表达式使用 `$` 元字符（或 `\Z`）锚定在任何一行的行尾，并且模式被找到，也会返回匹配成功。*m* 修饰符对 `\A` 和 `\z` 没有影响。

