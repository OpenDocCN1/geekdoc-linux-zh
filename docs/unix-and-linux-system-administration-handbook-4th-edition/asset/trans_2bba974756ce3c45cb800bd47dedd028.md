
当 shell 解释诸如 **-l*.pl** 之类的命令行时，它所执行的文件名匹配和扩展并不是正则表达式匹配的一种形式。它是一个称为“shell 通配”的不同系统，使用一种不同且更简单的语法。

正则表达式功能强大，但无法识别所有可能的语法。它们最显著的弱点是无法识别嵌套分隔符。例如，当允许使用括号进行分组时，不可能编写一个能够识别有效算术表达式的正则表达式。

正则表达式在 Perl 中达到了其力量和完美的顶峰。事实上，Perl 的模式匹配功能非常复杂精细，称其为正则表达式的实现并不准确。Perl 模式可以匹配嵌套分隔符、识别回文，以及匹配由任意数量的 A 后跟相同数量的 B 组成的字符串——这些都是正则表达式无法企及的功能。然而，Perl 同样可以处理普通正则表达式。

Perl 的模式匹配语言仍是行业基准，并已被其他语言和工具广泛采用。Philip Hazel 的 PCRE（Perl 兼容正则表达式）库使开发者能够相对容易地将这一语言集成到他们自己的项目中。

正则表达式本身并不是一种脚本语言，但它们非常有用，因此在任何有关脚本的讨论中都值得专门介绍；因此就有了这一节。在这里，我们将以其基本形式讨论它们，并加入 Perl 的一些改进。

## 匹配过程

评估正则表达式的代码会尝试将给定的单个文本字符串与给定的单个模式进行匹配。要匹配的“文本字符串”可以很长，并且可以包含嵌入的换行符。使用正则表达式来匹配整个文件或 HTML 文档的内容通常很方便。

匹配器要声明成功，整个搜索模式必须与搜索文本的某个连续部分匹配。但是，模式可以匹配任意位置。成功匹配后，评估器会返回匹配文本，以及模式中任何特殊定界子部分的匹配列表。

## 字面字符

通常，正则表达式中的字符匹配它们自身。所以模式

`I am the walrus`

匹配字符串“I am the walrus”，并且只匹配该字符串。由于它可以匹配搜索文本中的任意位置，该模式可以成功匹配字符串“I am the egg man. I am the walrus. Koo koo ka-choo!”。然而，实际的匹配仅限于“I am the walrus”部分。匹配区分大小写。

> 9. Perl 大师 Tom Christiansen 评论道：“我不知道什么是脚本语言，但我同意正则表达式既不是过程式语言也不是函数式语言。相反，它是一种基于逻辑或声明式的语言，这一类语言还包括 Prolog 和 Makefile，以及 BNF。也可以称它们为基于规则的语言。我个人更愿意称它们为声明式语言。”

## 特殊字符

表 2.4 展示了一些常见特殊符号在正则表达式中的含义。这些只是基础——还有很多很多。

### 表 2.4 正则表达式中的特殊字符（常见）

| Symbol | What it matches or does |
|---|---|
| . | Matches any character |
| [chars] | Matches any character from a given set |
| [^chars] | Matches any character not in a given set |
| ^ | Matches the beginning of a line |
| $ | Matches the end of a line |
| \w | Matches any "word" character (same as [A-Za-z0-9_]) |
| \s | Matches any whitespace character (same as [ \t\n\r])a |
| \d | Matches any digit (same as [0-9]) |
| | | Matches either the element to its left or the one to its right |
| (expr) | Limits scope, groups elements, allows matches to be captured |
| ? | Allows zero or one match of the preceding element |
| * | Allows zero, one, or many matches of the preceding element |
| + | Allows one or more matches of the preceding element |
| {n} | Matches exactly n instances of the preceding element |
| {min,} | Matches at least min instances (note the comma) |
| {min,max} | Matches any number of instances from min to max |

a. 即空格、换页符、制表符、换行符或回车符。

许多特殊结构，如 + 和 |，会影响其左侧或右侧“事物”的匹配。通常，“事物”是单个字符、括在括号中的子模式或括在方括号中的字符类。然而，对于 | 字符，“事物性”会无限地向左右两侧延伸。如果要限制竖线的范围，请将该竖线和两侧的事物各自括在一组括号中。例如，

```
I am the (walrus|egg man)\.
```

匹配“I am the walrus.”或“I am the egg man.”。这个示例还演示了特殊字符的转义（这里是点号）。模式

```
(I am the (walrus|egg man)\.) ?{1,2}
```

匹配以下任意一项：

- I am the walrus.
- I am the egg man.
- I am the walrus. I am the egg man.
- I am the egg man. I am the walrus.

