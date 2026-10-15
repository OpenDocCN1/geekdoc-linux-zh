
# 使用 grep 进行正则表达式搜索

除了使用 grep 搜索简单的文本字符串外，你还可以使用 grep 搜索正则表达式。正则表达式有点像花哨的通配符，你使用符号来表示字符、数字或其他符号。使用正则表达式，你可以搜索文件的不同部分，例如行的末尾或与另一个指定文本字符串相邻的文本字符串。表 6.1 列出了一些更常见的正则表达式。

```
[e]r@hobbes manipulate]$ grep .logan limerick
Worked hard all day on a slogan,
You see, the slogan's still brogan.
[e]r@hobbes manipulate]$
```

代码清单 6.9 使用 grep 与正则表达式创建花哨的通配符命令。

## 使用 grep 进行正则表达式：

- grep .logan limerick

输入 grep，后跟正则表达式和文件名。在这里，我们使用了正则表达式 .logan 来查找所有前面有一个字符的 "logan" 实例（代码清单 6.9）。请注意，这种使用 . 来匹配单个字符的方式与使用 ls 时的 ? 通配符非常相似。

你也可以使用多个句点来指定特定数量的字符。例如，要查找 "Dogbert" 和 "Dilbert"，你可能会使用 grep D..bert plagiarized.sayings。

在某些情况下，你可能需要根据使用的表达式和要查找的信息稍微不同地构建搜索字符串。查看表 6.1 中的其他示例以获取更多信息。

## 提示

- "正则表达式" 在 Unix 文档和互联网讨论中通常缩写为 "regexp"。
- 命令 egrep 与 grep 密切相关，为扩展正则表达式增加了一些灵活性，但从根本上工作方式相同。在许多系统上，grep 命令实际上是 egrep——当你输入其中任何一个时，你实际上运行的是 egrep。
- 如果你需要在大型文件中搜索整个单词，请使用 fgrep 进行更快的搜索。它使用与 grep 相同的通用语法，但只搜索整个单词（而不是正则表达式），因此速度快得多。
- 有关通配符的详细信息，请参阅第 1 章。

## 表 6.1

## 正则表达式、示例和解释

| 正则表达式 | 功能 | 示例 | 解释 |
|---|---|---|---|
| . | 匹配任意字符 | b.*rry | 这会找到 "berry" 或 "barry" 的所有实例。 |
| * | 匹配前一项的零个或多个实例，因此 a*b 会找到 "b" 以及 "ab" 和 "aaab"，但找不到 "acb" | grep "s*day" /home/ejr/schedule | 在这里，* 匹配 * 前面紧跟的项目的零个或多个。 |
| ^ | 仅匹配行开头处的字符串实例 | grep "^Some" sayings | 使用 ^，你指定搜索字符串必须出现在行的开头。示例会找到以 "Some" 开头的行，但不会找到以 "Read Some" 开头的行。 |
| $ | 仅匹配行末尾处的字符串实例 | grep "ach$" sayings | 使用 grep ach$ sayings，你可以找到 sayings 文件中所有以 "ach" 结尾的行。 |
| \ | 转义（引用）下一个字符——因此你可以搜索 * 或 $ 等也是运算符的字面字符 | grep "\*" sayings | grep "* sayings 搜索 sayings 文件中 * 的所有实例。\ 告诉 grep 将 * 字面解释为星号字符，而不是通配符。 |
| [ ] | 匹配集合中的任何成员，如 [a-z]、[0-6] 或 [321]（三或二或一） | grep "number[0-9]" specifications | 使用方括号 ([ ]) 括起一组选项。这里，number[0-9] 会匹配 specifications 文件中 number 1、number 2、number 3 等的所有实例。 |

## 使用其他正则表达式示例

在上一节中，我们向你展示了如何使用 grep 命令进行正则表达式搜索。不过，你也可以执行其他很棒的查找任务，我们将在本节中讨论。

## 查找具有特定特征的行：

- `grep '^Nantucket' limerick`
  在这里，我们使用 grep 查找 limericks 中所有以 Nantucket 开头的行，如果有的话。

- `grep 'Nantucket$' limerick`
  同样，你可以找到以 Nantucket 结尾的行。

- `grep '^[A-Z]' limerick`
  或者，你可以通过包含 [A-Z] 正则表达式来查找以大写字母开头的行。

- `grep '^[A-Z,a-z]' limerick`
  在这里，你可以找到所有以任何字母开头但不是数字或符号的行。很花哨，对吧？

## 提示

- 你也可以将正则表达式与 awk 和 sed 一起使用。有关详细信息，请参阅本章中的 使用 sed 进行全局更改 和 使用 awk 修改文件。

