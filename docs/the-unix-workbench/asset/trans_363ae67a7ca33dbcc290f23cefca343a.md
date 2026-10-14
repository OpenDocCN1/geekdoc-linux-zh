

```text
New Hampshire
New Jersey
New Mexico
New York
```

在前面的例子中，我们使用的正则表达式仅仅是 "New"，它表示字符串 "New" 的出现。正则表达式并不局限于单个字符或单词，它们也可以表示单词的一部分。例如，我可以用以下命令搜索包含字符串 "nia" 的所有州名：

```text
grep "nia" states.txt
```

```text
California
Pennsylvania
Virginia
West Virginia
```

上面的所有州名都以字符串 "nia" 结尾。

## 元字符

正则表达式不仅仅局限于使用字符和字符串进行搜索，正则表达式的真正威力来自于使用元字符。记住，元字符是可以用来表示其他字符的字符。为了充分利用所有元字符，我们应该使用 grep 的表亲 egrep，它只是扩展了 grep 的功能。

我们首先要讨论的元字符是 "."（句点）元字符，它表示**任意**字符。例如，如果我想在 states.txt 中搜索字符 “i”，后跟任意字符，后跟字符 “g”，我可以用以下命令实现：

```text
egrep "i.g" states.txt
```

```text
Virginia
Washington
West Virginia
Wyoming
```

正则表达式 “i.g” 在 Virginia 和 West Virginia 中匹配子字符串 “irg”，在 Washington 和 Wyoming 中匹配子字符串 “ing”。在上面的例子中，句点元字符是 “irg” 中的 “r” 和 “ing” 中的 “n” 的替代。句点元字符非常宽松，例如命令 egrep "." states.txt 将返回 states.txt 的每一行，因为正则表达式 "." 将匹配每行上的任意一个字符的出现（每行上至少有一个字符）。

除了可以表示其他字符的字符之外，还有一种称为 **量词** 的元字符，它允许你指定特定正则表达式在字符串中应出现的次数。其中最基本的量词是 "+"（加号），它表示前一个表达式的一个或多个出现。例如，正则表达式 “s+as” 的意思是：一个或多个 “s” 后跟 “as”。让我们看看是否有任何州名匹配此表达式：

```text
egrep "s+as" states.txt
```

```text
Arkansas
Kansas
```

Arkansas 和 Kansas 都匹配正则表达式 "s+as"。除了加号元字符之外，还有 "*"（星号）元字符，它表示前一个表达式的零个或多个出现。让我们看看如果我们将 "s+as" 改为 "s*as" 会发生什么：

```text
egrep "s*as" states.txt
```

```text
Alaska
Arkansas
Kansas
Massachusetts
Nebraska
Texas
Washington
```

正如你所见，星号元字符在匹配方面要宽松得多，因为有更多州名被 "s*as" 匹配。除了 "零个或多个" 或 "一个或多个" 表达式出现之外，你还可以使用更具体的量词。你可以使用大括号 ({ }) 来指定表达式的确切出现次数。例如，正则表达式 "s{2}" 指定字符 "s" 恰好出现两次。让我们尝试使用此正则表达式：

```text
egrep "s{2}" states.txt
```

```text
Massachusetts
Mississippi
Missouri
Tennessee
```

请注意，正则表达式 "s{2}" 等同于正则表达式 "ss"。我们也可以使用正则表达式 "s{2,3}" 搜索具有两个到三个相邻字母 "s" 出现的州名：

```text
egrep "s{2,3}" states.txt
```

```text
Massachusetts
Mississippi
Missouri
Tennessee
```

当然结果是相同的，因为没有州名有 "s" 重复三次。

你可以使用捕获组来搜索字符串的多次出现。你可以通过使用括号 "( )" 在正则表达式中创建捕获组。例如，如果我想在 states.txt 中搜索州名中出现两次的字符串 "iss"，我可以使用捕获组和量词，如下所示：

