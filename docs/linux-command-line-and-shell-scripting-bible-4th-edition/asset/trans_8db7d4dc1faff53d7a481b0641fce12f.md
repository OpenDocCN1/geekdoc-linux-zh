

## 特殊字符类

除了定义自己的字符类，BRE（基本正则表达式）还包含一些特殊的字符类，你可以使用它们来匹配特定类型的字符。表 20.1 描述了你所能使用的 BRE 特殊字符。

### 表 20.1 BRE 特殊字符类

| 类 | 描述 |
|---|---|
| [[:alpha:]] | 匹配任意字母字符，包括大写或小写 |
| [[:alnum:]] | 匹配任意字母数字字符 0-9, A-Z, 或 a-z |
| [[:blank:]] | 匹配空格或 Tab 字符 |
| [[:digit:]] | 匹配 0 到 9 之间的数字字符 |
| [[:lower:]] | 匹配任意小写字母字符 a-z |
| [[:print:]] | 匹配任意可打印字符 |
| [[:punct:]] | 匹配标点符号字符 |
| [[:space:]] | 匹配任意空白字符：空格、Tab、NL（换行）、FF（换页）、VT（垂直制表符）、CR（回车） |
| [[:upper:]] | 匹配任意大写字母字符 A-Z |

在正则表达式模式中使用特殊字符类的方式与普通字符类完全相同：

```
$ echo "abc" | sed -n '/[[:digit:]]/p'
$
$ echo "abc" | sed -n '/[[:alpha:]]/p'
abc
$ echo "abc123" | sed -n '/[[:digit:]]/p'
abc123
$ echo "This is, a test" | sed -n '/[[:punct:]]/p'
This is, a test
$
$ echo "This is a test" | sed -n '/[:punct:]/p'
$
```

使用特殊字符类是定义范围的一种简便方法。你不必使用范围 $[0-9]$，可以直接使用 $[:digit:]$。

## 星号

在字符后放置星号表示该字符必须出现零次或多次才能匹配该模式：

```
$ echo "ik" | sed -n '/ie*k/p'
ik
$ echo "iek" | sed -n '/ie*k/p'
iek
$ echo "ieek" | sed -n '/ie*k/p'
ieek
$ echo "ieeeek" | sed -n '/ie*k/p'
ieeeek
$ echo "ieeeeek" | sed -n '/ie*k/p'
ieeeeek
$
```

该模式符号常用于处理那些常见拼写错误或在不同语言中拼写存在变体的单词。例如，如果你需要编写一个可能用于美式英语或英式英语的脚本，你可以这样写：

```
$ echo "I'm getting a color TV" | sed -n '/colou*r/p'
I'm getting a color TV
$ echo "I'm getting a colour TV" | sed -n '/colou*r/p'
I'm getting a colour TV
$
```

模式中的 $u$* 表示字母 $u$ 在文本中可能出现在匹配模式中，也可能不出现。同样，如果你知道某个单词常被拼错，你可以通过使用星号来适应这种情况：

```
$ echo "I ate a potatoe with my lunch." | sed -n '/potatoe*/p'
I ate a potatoe with my lunch.
$ echo "I ate a potato with my lunch." | sed -n '/potatoe*/p'
I ate a potato with my lunch.
$
```

在可能的额外字母旁放置星号，使你能够接受拼写错误的单词。

另一个实用功能是组合点号特殊字符和星号特殊字符。这种组合提供了匹配任意数量的任意字符的模式。它常用于两个文本字符串之间，这两个字符串在数据流中可能相邻，也可能不相邻：

```
$ echo "this is a regular pattern expression" | sed -n '/regular.*expression/p'
this is a regular pattern expression
$
```

使用该模式，你可以轻松搜索数据流中一行文本中可能出现在任意位置的两个或多个单词。

星号还可以应用于字符类。这样做允许你指定一组或在文本中可能出现一次以上的字符范围：

```
$ echo "bt" | sed -n '/b[ae]*t/p'
bt
$ echo "bat" | sed -n '/b[ae]*t/p'
bat
$ echo "bet" | sed -n '/b[ae]*t/p'
bet
$ echo "btt" | sed -n '/b[ae]*t/p'
btt
$ echo "baat" | sed -n '/b[ae]*t/p'
baat
$ echo "baaaeeet" | sed -n '/b[ae]*t/p'
baaaeeet
$ echo "baeeeaeeat" | sed -n '/b[ae]*t/p'
baeeeaeeat
$ echo "baakeeet" | sed -n '/b[ae]*t/p'
$
```

只要 $a$ 和 $e$ 字符以任何组合形式出现在 $b$ 和 $t$ 字符之间（包括完全不出现），模式就会匹配。如果出现任何定义在字符类之外的其他字符，模式匹配就会失败。

## 尝试扩展正则表达式

POSIX ERE（扩展正则表达式）模式包含一些额外的符号，某些 Linux 应用程序和实用工具会使用这些符号。`gawk` 识别 ERE 模式，但 `sed` 不识别。

**注意**

请记住，`sed` 和 `gawk` 中的正则表达式引擎是不同的。`gawk` 可以使用大多数扩展正则表达式模式符号，并且可以提供一些 `sed` 不具备的额外过滤功能。然而，因此，它在处理数据流时通常更慢。

本节描述了你在 `gawk` 程序脚本中可使用的更常见的 ERE 模式符号。

### 问号

问号与星号类似，但略有不同。问号表示前面的字符可以出现零次或一次，仅此而已。它不会匹配该字符的重复出现：

```
$ echo "bt" | gawk '/be?t/{print $0}'
bt
$ echo "bet" | gawk '/be?t/{print $0}'
bet
$ echo "beet" | gawk '/be?t/{print $0}'
$
$ echo "beet" | gawk '/be?t/{print $0}'
$
```

如果 $e$ 字符在文本中不出现，或者在文本中仅出现一次，模式就会匹配。

与星号一样，你可以将问号符号与字符类一起使用：

```
$ echo "bt" | gawk '/b[ae]?t/{print $0}'
bt
$ echo "bat" | gawk '/b[ae]?t/{print $0}'
bat
$ echo "bot" | gawk '/b[ae]?t/{print $0}'
$
$ echo "bet" | gawk '/b[ae]?t/{print $0}'
bet
$ echo "baet" | gawk '/b[ae]?t/{print $0}'
$
$ echo "beat" | gawk '/b[ae]?t/{print $0}'
$
$ echo "beet" | gawk '/b[ae]?t/{print $0}'
$
```

如果字符类中零个或一个字符出现，模式匹配通过。然而，如果两个字符都出现，或者其中一个字符出现两次，模式匹配失败。

### 加号

加号是另一个与星号类似的模式符号，但与问号有不同的变化。加号表示前面的字符可以出现一次或多次，但必须至少出现一次。如果该字符不存在，模式不会匹配：

```
$ echo "beet" | gawk '/be+t/{print $0}'
beet
$ echo "bet" | gawk '/be+t/{print $0}'
bet
$ echo "bt" | gawk '/be+t/{print $0}'
$
```

如果 *e* 字符不存在，模式匹配失败。加号也能与字符类一起使用，方式与星号和问号相同：

```
$ echo "bt" | gawk '/b[ae]+t/{print $0}'
$
$ echo "bat" | gawk '/b[ae]+t/{print $0}'
bat
$ echo "bet" | gawk '/b[ae]+t/{print $0}'
bet
$ echo "beat" | gawk '/b[ae]+t/{print $0}'
beat
$ echo "beet" | gawk '/b[ae]+t/{print $0}'
beet
$ echo "beeat" | gawk '/b[ae]+t/{print $0}'
beeat
$
```

这次，如果字符类中定义的任意字符出现，文本就匹配指定模式。

### 使用花括号

在 ERE 中可以使用花括号来指定可重复正则表达式的限制。这通常被称为 *区间*。你可以用两种格式表示区间：

- *m*——正则表达式恰好出现 *m* 次。
- *m, n*——正则表达式至少出现 *m* 次，但不超过 *n* 次。

此功能允许你精细调整允许字符（或字符类）在模式中出现的次数。

> **注意**
>
> 默认情况下，`gawk` 不识别正则表达式区间。你必须为 `gawk` 指定 `--re-interval` 命令行选项，以识别正则表达式区间。

下面是一个使用单值简单区间的示例：

```
$ echo "bt" | gawk --re-interval '/be{1}t/{print $0}'
$
$ echo "bet" | gawk --re-interval '/be{1}t/{print $0}'
bet
$ echo "beet" | gawk --re-interval '/be{1}t/{print $0}'
$
```

通过指定区间为 1，你限制了字符串匹配模式时字符出现的次数。如果字符出现的次数更多，模式匹配失败。

