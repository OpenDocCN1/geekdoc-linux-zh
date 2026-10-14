

被视为普通字符。例外是“$”、“\”（反斜杠）和“`”（反引号）。这意味着单词分割、路径名展开、波浪号展开和大括号展开被抑制，但参数展开、算术展开和命令替换仍然会执行。使用双引号，我们可以处理包含嵌入空格的文件名。假设我们不幸遇到了一个名为 `two words.txt` 的文件。如果我们试图在命令行中使用它，单词分割会使其被当作两个独立的参数，而不是我们想要的单个参数：

```
[me@linuxbox ~]$ ls -l two words.txt
ls: cannot access two: No such file or directory
ls: cannot access words.txt: No such file or directory
```

通过使用双引号，我们阻止了单词分割，得到了期望的结果；此外，我们甚至可以修复损害：

```
[me@linuxbox ~]$ ls -l "two words.txt"
-rw-rw-r-- 1 me me 18 2008-02-20 13:03 two words.txt
[me@linuxbox ~]$ mv "two words.txt" two_words.txt
```

瞧！现在我们不必再输入那些讨厌的双引号了。

请记住，参数展开、算术展开和命令替换在双引号内仍然会发生：

```
[me@linuxbox ~]$ echo "$USER $((2+2)) $(cal)"
me 4 February 2008
Su Mo Tu We Th Fr Sa
      1  2
 3  4  5  6  7  8  9
10 11 12 13 14 15 16
17 18 19 20 21 22 23
24 25 26 27 28 29
```

我们应该花点时间看看双引号对命令替换的影响。首先，让我们更深入地了解一下单词分割是如何运作的。在之前的例子中，我们看到单词分割似乎会移除文本中多余的空格：

```
[me@linuxbox ~]$ echo this is a    test
this is a test
```

默认情况下，单词分割会查找空格、制表符和换行符（换行字符），并将它们视为单词之间的分隔符。这意味着不带引号的空格、制表符和换行符不被视为文本的一部分，它们仅作为分隔符。由于它们将单词分隔成不同的参数，我们的示例命令行包含一个命令和四个独立的参数。如果我们加上双引号：

```
[me@linuxbox ~]$ echo "this is a      test"
this is a      test
```

单词分割被抑制，嵌入的空格不被视为分隔符，而是成为参数的一部分。一旦加上双引号，我们的命令行就包含一个命令和单个参数。

换行符被单词分割机制视为分隔符这一事实，对命令替换产生了一个有趣但微妙的效果。考虑以下例子：

```
[me@linuxbox ~]$ echo $(cal)
February 2008 Su Mo Tu We Th Fr Sa  1  2  3  4  5  6  7  8  9 10 11 12 13 14
15 16 17 18 19 20 21 22 23 24 25 26 27 28 29
[me@linuxbox ~]$ echo "$(cal)"
February 2008
Su Mo Tu We Th Fr Sa
          1  2
 3  4  5  6  7  8  9
10 11 12 13 14 15 16
17 18 19 20 21 22 23
24 25 26 27 28 29
```

在第一个例子中，不带引号的命令替换产生了包含三十八个参数的命令行。在第二个例子中，命令行只有一个参数，其中包含嵌入的空格和换行符。

## 单引号

如果我们需要抑制所有展开，我们使用单引号。以下是不加引号、双引号和单引号的对比：

```
[me@linuxbox ~]$ echo text ~/*.txt {a,b} $(echo foo) $((2+2)) $USER
text /home/me/ls-output.txt a b foo 4 me
```

```
[me@linuxbox ~]$ echo "text ~/*.txt {a,b} $(echo foo) $((2+2)) $USER"
text ~/*.txt {a,b} foo 4 me
[me@linuxbox ~]$ echo 'text ~/*.txt {a,b} $(echo foo) $((2+2)) $USER'
text ~/*.txt {a,b} $(echo foo) $((2+2)) $USER
```

正如我们所见，随着每一级引用的加深，越来越多的展开被抑制。

## 转义字符

有时我们只想引用单个字符。为此，我们可以在字符前面加上一个反斜杠，在这种情况下它被称为转义字符。这通常是在双引号内用来有选择地阻止展开：

```
[me@linuxbox ~]$ echo "The balance for user $USER is: \$5.00"
The balance for user me is: $5.00
```

使用转义来消除文件名中字符的特殊含义也是很常见的。例如，可以在文件名中使用通常对 shell 有特殊含义的字符。这些字符包括“$”、“!”、“&”、“ ”（空格）等。要在文件名中包含特殊字符，你可以这样做：

```
[me@linuxbox ~]$ mv bad\&filename good_filename
```

若要允许反斜杠字符出现，可以通过输入“\\”来转义它。请注意，在单引号内，反斜杠会失去其特殊含义，被视为普通字符。

## 反斜杠转义序列

除了作为转义字符外，反斜杠还用于表示某些称为控制代码的特殊字符的记号。ASCII 编码方案中的前三十二个字符用于向电传打字机类设备传输命令。其中一些代码是熟悉的（制表符、退格、换行和回车），而另一些则不是（空字符、传输结束和确认）。

