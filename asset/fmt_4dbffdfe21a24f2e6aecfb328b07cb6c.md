
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
```

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

## 示例 9.29

```perl
# 脚本：
use warnings;

# 锚点与 m 修饰符
1 $_="Today is history.\nTomorrow will never be here.\n";
2 print if /Tomorrow/; # 嵌入的换行符
3 $_="Today is history.\nTomorrow will never be here.\n";
4 print if /\ATomorrow/; # 嵌入的换行符
5 $_="Today is history.\nTomorrow will never be here.\n";
6 print if /Tomorrow/m;
7 $_="Today is history.\nTomorrow will never be here.\n";
8 print if /\ATomorrow/m;
9 $_="Today is history.\nTomorrow will never be here.\n";
10 print if /history\.$/m;

# 输出
6 Today is history.
Tomorrow will never be here.

10 Today is history.
Tomorrow will never be here.
```

### 解释

- 向标量 `$_` 赋值一个包含嵌入换行符的字符串。
- 元字符 `^` 将搜索锚定到行的开头。由于该行并非以 *Tomorrow* 开头，搜索失败，因此不会返回任何内容。
- 向标量 `$_` 赋值一个包含嵌入换行符的字符串。
- 断言 `\A` 仅匹配字符串的开头，无论情况如何。由于该字符串并非以 *Tomorrow* 开头，搜索失败，因此不会返回任何内容。
- 向标量 `$_` 赋值一个包含嵌入换行符的字符串。
- `m` 修饰符将字符串视为多行，每行以换行符结尾。在此示例中，`^` 锚点匹配这些多行中任意一行的开头。模式（`^Tomorrow`）在第二行中被找到。
- 向标量 `$_` 赋值一个包含嵌入换行符的字符串。
- 断言 `\A` 仅匹配字符串的开头，无论嵌入多少个换行符，且 `m` 修饰符不起作用。由于 *Tomorrow* 未出现在字符串的开头，因此没有匹配项。
- 向标量 `$_` 赋值一个包含嵌入换行符的字符串。
- 元字符 `$` 将搜索锚定到行的末尾。使用 `m` 修饰符时，嵌入的换行符会产生多行。模式（`history\.$`）在第一行的末尾被找到。使用断言 `\Z` 也能正常工作，但 `\.` 则不行。

### 交替

交替允许正则表达式包含多个可匹配的替代模式。例如，正则表达式 `/John|Karen|Steve/` 将匹配包含 *John*、*Karen* 或 *Steve* 的行。如果 *Karen*、*John* 或 *Steve* 分别位于不同的行，则所有这些行都会被匹配。每个替代表达式之间通过垂直线（管道符）分隔，表达式可以由任意数量的字符组成，而字符类仅匹配单个字符；例如，`/a|b|c|/` 等同于 `/[abc]/`，但 `/a|b|c|d/` 不能表示为 `/[abcd]/`。模式 `/a|b|c|/` 是 *ac* 或 *d*，而类 `/[abcd]/` 仅代表集合中的**一个**字符，即 a、b、c 或 d。

```perl
# 示例 9.30
# 脚本：
use warnings;

# 交替：this, that, 和 the other thing
while(<$DATA>){
    print if /Steve|Betty|Jon/;
}

__DATA__
Steve Blenheim
Betty Boop
Igor Chevesky
Norma Cord
Jonathan DeLoach
Karen Ewich

# 输出：
Steve Blenheim
Betty Boop
Jonathan DeLoach
```

### 解释

管道符 `|` 用于在正则表达式中匹配一组替代模式。如果找到 *Steve*、*Betty* 或 *Jon* 中的任何一个模式，匹配即成功。

### 分组或聚类

如果正则表达式模式被括号包围，则创建一个子模式。然后，例如，贪婪元字符不再匹配前一个单个字符的零次、一次或多次，而是可以匹配前一个子模式。如果模式被括号包围，也可以控制交替。Perl 高手也将这种将字符组合在一起的过程称为**聚类**。

## 示例 9.31

```perl
# 脚本
use warnings;

# 聚类或分组
1 $_=qw/The baby says, "Mama, Mama, I can say Papa!"\n/;
2 print if s/\b(\bm|pa\b)+/goo/gi;

# 输出
The baby says, "goo, goo, I can say goo!"
```

### 解释

- 向标量 `$_` 赋值双引号字符串。
- 正则表达式包含一个由括号包围的模式，后跟元字符 `+`。括号将由 `+` 元字符控制的字符进行分组。该表达式读作：查找模式 `ma` 或 `pa` 的一次或多次出现，并将其替换为 `goo`。

## 示例 9.32

```perl
# 脚本
use warnings;

# 聚类或分组
1 while(<DATA>)
2 {
    print if /\b(12){3}$/;
}

__END__
Steve Blenheim        121212
Betty Boop            123
Igor Chevsky          123444123
Norma Corg            51235
Jonathan DeLoach      123456
Karen Evich           121212456

# 输出
Steve Blenheim        121212
```

### 解释

- 模式 `12` 被分组在括号中。它受量化器 `{3}` 控制；这意味着，行尾（`$`）处恰好出现 3 次数字 `12` 的行将被匹配。

## 示例 9.33

```perl
# 脚本
use warnings;

# 分组
1 $_="Tom and Dan Savage and Ellie Main are cousins.\n";
2 print if s/\bTom|\bEllie Main/Arch/gi;
3 $_="Tom and Dan Savage and Ellie Main are cousins.\n";
4 print if s/(Tom|Ellie) Main/Archie/gi;

# 输出
2 Archie and Dan Savage and Archie are cousins.
4 Tom and Dan Savage and Archie are cousins.
```
