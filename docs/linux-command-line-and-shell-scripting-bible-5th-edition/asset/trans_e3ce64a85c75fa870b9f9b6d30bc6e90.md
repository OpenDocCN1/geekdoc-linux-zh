
## 第三部分：高级 Shell 脚本

你可能已经注意到，正则表达式并不关心模式在数据流中的具体位置。同样，模式出现的次数也不重要。只要正则表达式能在文本字符串的任何位置匹配到该模式，它就会将该字符串传递给使用它的 Linux 实用程序。

关键在于将正则表达式模式与数据流文本进行匹配。必须记住的是，正则表达式在匹配模式时极其挑剔。第一条需要牢记的规则是正则表达式模式是**区分大小写**的。这意味着它们只会匹配字符大小写正确的模式：

```bash
$ echo "This is a test" | sed -n '/this/p'
$
$ echo "This is a test" | sed -n '/This/p'
This is a test
$
```

第一次尝试未能匹配，因为文本字符串中并没有全小写的单词“this”，而第二次尝试使用了模式中的大写字母，结果运行正常。

在正则表达式中，你不必局限于完整单词。如果定义的文本出现在数据流的任何位置，正则表达式就会匹配以下内容：

```bash
$ echo "The books are expensive" | sed -n '/book/p'
The books are expensive
$
```

即使数据流中的文本是“books”，由于流中的数据包含正则表达式“book”，因此正则表达式模式与数据匹配。当然，如果你尝试反过来，正则表达式就会失败：

```bash
$ echo "The book is expensive" | sed -n '/books/p'
$
```

完整的正则表达式文本并未出现在数据流中，因此匹配失败，sed 没有显示该文本。

此外，你也不必在正则表达式中局限于单个文本单词。你可以在文本字符串中包含空格和数字：

```bash
$ echo "This is line number 1" | sed -n '/ber 1/p'
This is line number 1
$
```

在正则表达式中，空格与其他字符的处理方式相同：

```bash
$ echo "This is line number1" | sed -n '/ber 1/p'
$
```

如果你在正则表达式中定义了空格，它必须出现在数据流中。你甚至可以创建一个匹配多个连续空格的正则表达式模式：

```bash
$ cat data1
This is a normal line of text.
This is a line with too many spaces.
$ sed -n '/  /p' data1
This is a line with too many spaces.
$ 
```

单词之间有两个空格的那一行匹配了正则表达式模式。这是捕获文本文件中空格问题的绝佳方法！

### 特殊字符

当你在正则表达式模式中使用文本字符串时，有几点需要注意。在正则表达式中定义文本字符时，有一些**例外**情况。正则表达式模式赋予某些字符特殊的含义。如果你试图在文本模式中使用这些字符，将无法获得预期的结果。

正则表达式识别以下特殊字符：

```text
. * [ ] ^ $ ( ) { } \ ? | ( )
```

随着章节内容的深入，你将了解这些特殊字符在正则表达式中的具体作用。然而，目前只需记住，你不能单独在文本模式中使用这些字符。

如果你想将其中一个特殊字符作为普通文本字符使用，你需要对其进行*转义*。当对特殊字符进行转义时，需在其前面添加一个特殊字符，以指示正则表达式引擎将下一个字符解释为普通文本字符。执行此操作的特殊字符是反斜杠字符（\）。

例如，如果你想在文本中搜索美元符号，只需在其前面加上一个反斜杠字符：

```bash
$ cat data2
The cost is $4.00
$ sed -n '/\$/p' data2
The cost is $4.00
$ 
```

由于反斜杠本身是特殊字符，如果你需要在正则表达式模式中使用它，也需要对其进行转义，从而产生双反斜杠：

```bash
$ echo "\\ is a special character" | sed -n '/\\\\/p'
\\ is a special character
$ 
```

最后，虽然正斜杠不是正则表达式的特殊字符，但如果你在 `sed` 或 `gawk` 的正则表达式模式中使用它，将会导致错误：

```bash
$ echo "3 / 2" | sed -n '///p'
sed: -e expression #1, char 2: No previous regular expression
$
```

若要使用正斜杠，同样需要对其进行转义：

```bash
$ echo "3 / 2" | sed -n '/\/\/p'
3 / 2
$
```

现在 `sed` 可以正确解释正则表达式模式，一切恢复正常。

## 锚点字符

如“普通文本”部分所示，默认情况下，当你指定一个正则表达式模式时，如果该模式出现在数据流的任何位置，就会匹配。你可以使用两个特殊字符将模式锚定到数据流中行的开头或结尾。

### 从开头开始

脱字符（`^`）定义了一个模式，该模式匹配数据流中每行文本的开头。如果模式位于行文本的任何其他位置，正则表达式模式匹配失败。

要使用脱字符，必须将其放置在正则表达式中指定的模式之前：

```bash
$ echo "The book store" | sed -n '/^book/p'
$
$ echo "Books are great" | sed -n '/^Book/p'
Books are great
$
```

脱字符锚点字符根据换行符确定的每行新数据开头来检查模式：

```bash
$ cat data3
This is a test line.
This is another test line.
A line that tests this feature.
Yet more testing of this
$ sed -n '/^this/p' data3
This is a line that tests this feature.
$
```

只要模式出现在新行的开头，脱字符锚点就能捕获它。

如果你将脱字符字符放置在模式开头以外的任何位置，它将像普通字符一样行动，而不是作为特殊字符：

```bash
$ echo "This ^ is a test" | sed -n '/s ^/p'
This ^ is a test
$
```

由于脱字符在正则表达式模式中列在最后，`sed` 将其用作普通字符来匹配文本。

> **注意**
> 如果你需要仅使用脱字符指定正则表达式模式，则不需要用反斜杠对其进行转义。但是，如果你先指定脱字符，随后在模式中附加更多文本，则需要在脱字符之前使用转义字符。

### 查找结尾

查找行首模式的操作相反，是查找行尾。美元符号（$）特殊字符定义了结尾锚点。在文本模式后添加此特殊字符，以指示数据行必须以该文本模式结尾：

```bash
$ echo "This is a good book" | sed -n '/books$/p'
This is a good book
$ echo "This book is good" | sed -n '/books$/p'
$
```

使用结尾文本模式的问题在于，你必须小心你要查找的内容：

```bash
$ echo "There are a lot of good books" | sed -n '/books$/p'
$
```

将单词“book”在行末变为复数形式意味着它不再匹配正则表达式模式，即使“book”在数据流中。文本模式必须是该行上的最后一个内容，模式才能匹配。

### 组合锚点

在某些常见情况下，你可以在同一行中组合开头和结尾锚点。第一种情况，假设你想查找仅包含特定文本模式的数据行：

```bash
$ cat data4
this is a test of using both anchors
I said this is a test
this is a test
I'm sure this is a test.
$ sed -n '/^this is a test$/p' data4
this is a test
$
```

`sed` 会忽略包含指定文本以外其他文本的行。

第二种情况乍一看可能有点奇怪，但非常有用。通过在一个没有文本的模式中组合两个锚点，你可以从数据流中过滤掉空行。考虑以下示例：

```bash
$ cat data5
This is one test line.

This is another test line.
$ sed '/^$/d' data5
This is one test line.
This is another test line.
$ 
```

定义的正则表达式模式查找那些在行开始和行结束之间没有任何内容的行。由于空行在两个换行符之间不包含任何文本，因此它们匹配正则表达式模式。`sed` 使用 `d` 命令删除匹配正则表达式模式的行，从而移除文本中的所有空行。这是从文档中移除空行的一种有效方法。

## 点字符

点号特殊字符用于匹配除换行符以外的任何单个字符。然而，点号必须匹配一个字符；如果在点号的位置没有字符，则模式匹配失败。

让我们看几个在正则表达式模式中使用点字符的示例：

```bash
$ cat data6
This is a test of a line.
The cat is sleeping.
That is a very nice hat.
This test is at line four.
at ten o'clock we'll go home.
$ sed -n '/,at/p' data6
The cat is sleeping.
That is a very nice hat.
This test is at line four.
$ 
```

你应该能够推断出为什么数据文件中的第一行未能匹配，以及为什么第二行和第三行通过了。第四行有点棘手。注意，它匹配了 at，但它前面没有字符来匹配点号。啊，但有的！在正则表达式中，空格也被视为字符，因此 at 前面的空格匹配了该模式。第五行证明了这一点，因为 at 位于行首，未能匹配该模式。

