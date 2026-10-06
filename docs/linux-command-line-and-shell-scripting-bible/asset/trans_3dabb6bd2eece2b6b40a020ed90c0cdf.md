

# 第三部分 高级 Shell 脚本

你可以在单个表达式中使用多个一个字符类：

```
$ echo "Yes" | -n '/[Yy][Ee][Ss]/p'
Yes
$ echo "yEs" | -n '/[Yy][Ee][Ss]/p'
yEs
$ echo "yES" | -n '/[Yy][Ee][Ss]/p'
yES
```

该正则表达式使用了三个字符类来涵盖所有三个位置的大写和小写字母。

字符类并不非只包含字母；你可以在它们使用数字，例如：

```
$ cat data7
This line doesn't contain a number.
This line has 1 number on it.
This line has a number 2 on it.
This line has a number 4 on it.
$ sed -n '/[0123]/p' data7
This line has 1 number on it.
This line has a number 2 on it.
$
```

正则表达式模式匹配任何包含 0, 1, 2 或 3 的行。其他数字都会被忽略，因为它们中不包含这些数字。

你可以结合字符类来检查格式正确的数字，例如电话号码和邮政编码。然而，当你尝试匹配特定格式时，必须小心。这里有一个邮政编码匹配失败的示例：

```
$ cat data8
60633
46201
223001
4353
22203
$ sed -n '/^[0123456789][0123456789][0123456789][0123456789][0123456789]$/p' data8
60633
46201
223001
22203
$
```

这可能不是你想要的结果。它很好地过滤掉了太短而无法作为邮政编码的数字，因为最后一个字符类没有用于匹配的字符。然而，它仍然通过了六位数的数字，尽管我们只定义了五个字符类。

记住，正则表达式模式可以在数据流文本的任何地方找到。除了匹配模式字符之外，总会有额外的字符。如果你想确保匹配的是五个数字，你需要以某种方式定界，要么使用空格，要么像这个示例中通过显示它们位于行首行尾：

```
$ sed -n '$
> /[0123456789][0123456789][0123456789][0123456789][0123456789]$/p
> data8
60633
46201
22203
$
```

现在这样好多了！稍后我们将查看如何进一步简化它。

字符类的一个极佳用途是解析可能拼错误的单词，例如从用户表单输入的数据。你可以轻松创建可以接受数据中常见拼写错误的正则表达式：

```
$ cat data9
I need to some maintenance done on my car.
I'll pay that in seperate invoice.
After I pay for the maintenance my car will be as good as new.
$ sed -n '$
/aint[ea][n]nce/p
/sep[ea][r]te/p
data9
I need have some maintenance done on my car.
I'll pay that in seperate invoice.
After I pay for the maintenance my car will be as good as new.
$
```

此示例中的两个 `sed` 打印命令利用正则表达式字符类来帮助文本中的拼错单词保持和分离。相同的正则表达式也匹配拼写正确的 `maintenance` 出现的情况。

# 反转字符类

在表达式模式中，你也可以反转字符类的效果。与其寻找包含在类中的字符，不如寻找不在类中的任何字符。要这样做，只需在字符范围的开头放置一个脱符号 `^` 即可：

```
$ sed - '/[^ch]at/p' data6
This test is.
$
```

# 使用范围

你可能已经注意到，当我之前展示邮政编码示例时，在每个字符类中列出所有可能的数字是很尴尬的。坦率地说，你可以使用快捷方法来避免这样做。你可以在字符类中使用连字符 `-` 来使用字符范围。只需指定范围内的第一个字符、一个连字符，然后是最后一个字符。正则表达式将根据 Linux 系统使用的字符集包含指定范围内的任何字符（见第 2 章）。现在你可以通过指定数字范围来简化邮政编码示例：

```
$ sed -n '/^[0-9]{5}$/p' data8
60633
46201
$
```

这节省了大量的输入工作！每个字符类将匹配从 0 到 9 的任何数字。如果数据中任何地方出现字母，模式将失败：

```
$ echo "a" | sed -n '/^[0-9]$/p'
$ echo "1832" | sed -n '/^[0-9]$/p'
$ echo "1892a" | sed -n '/^[0-9]$/p'
$
```
```

同样的技术也适用于字母：

```
$ sed -n '/[c-h]/p' data6
The cat is sleeping.
That is very nice hat.
$
```

新模式 `[c-h]` 匹配第一个字母在 c 和 h 之间的单词。在这种情况下，只有包含一个单词的行没有匹配到模式。你还可以在单个字符类中指定多个连续的范围：

```
$ sed -n '/[a-m]/p' data6
The cat is sleeping.
That is very nice hat.
$
```

# 正则表达式

字符类允许 c 到 h 以及 h 到 m 的范围出现在文本之前。此范围将拒绝任何在 d 和 g 之间的字母：

```
$ echo "I'm getting too fat." | sed -n '/[a-m]/p'
$
```

该模式拒绝了 `fat` 文本，因为它们不在指定的范围内。

# 特殊字符类

除了定义你自己的字符类外，BRE（基本正则表达式）包含了你可以用于匹配特定类型字符的特殊字符类。表 17-1 描述了你可以使用的特殊字符。你就像使用普通字符类一样在正则表达式中使用特殊字符类：

```
$ echo "abc" | sed -n '/[:digit:]/p'
$
$ echo "abc" | sed -n '/[:alpha:]/p'
$ echo "abc23" | sed -n '/[:digit:]/p'
abc23
$ echo "This is a test" | sed -n '/[:punct:]/p'
This is a test
$ echo "This is a test" | sed -n '/[:space:]/p'
This is a test
$
```

### 表 17-1 BRE 特殊字符类

| 类 | 描述 |
| :--- | :--- |
| [[:alpha:]] | 匹配字母，大写或小写。 |
| [[:alnum:]] | 匹配数字 0–9、A–Z 或 a–z。 |
| [[:blank:]] | 匹配空格或制表符。 |
| [[:digit:]] | 匹配数字 9。 |
| [[:lower:]] | 匹配小写字母 a–z。 |
| [[:print:]] | 匹配打印字符。 |
| [[:punct:]] | 匹配标点字符。 |
| [[:space:]] | 匹配空白字符：空格、制表符、NL、FF、CR。 |
| [[:upper:]] | 匹配大写字母 A–Z。 |

# 星号

使用特殊字符类是定义范围的简单方法。与其使用范围 `[0-9]`，你可以直接使用 `[:digit:]`。

在字符后放置星号表示该字符在文本中出现零次或多次即可匹配模式：

```
$ echo "ik" | sed -n '/ie*k/p'
ik
$ echo "iek" | sed -n '/ie*k/p'
iek
$ echo "ieek" | sed -n '/ie*k/p'
ieek
$ echo "ieeeec" | sed -n '/ie*k/p'
ieec
$ echo "ieeeec" | sed -n '/ie*k/p'
eeeec$
```

这种模式通常用于处理常见的拼写错误或语言差异单词。例如，如果你需要编写一个可以在美式或英式英语使用的脚本，你可以写：

```
$ echo "I'm getting too fat." | sed -n '/colou*r/p'
I'm getting a color TV
$ echo "I'm getting a colour TV" | sed -n '/colou*r/p'
I'm getting a colour TV
```

模式中的 `u*` 表示字母 u 可能不出现在文本中。同样，如果你知道一个经常拼错误的单词，你可以通过使用星号来适应它：

```
$ echo "I ate a potatoe with my lunch." | sed -n '/potatoe*/p'
I ate a potatoe with my lunch.
$ echo "I ate a potato with my lunch." | sed -n '/potatoe*/p'
I ate a potato with my lunch.
```

