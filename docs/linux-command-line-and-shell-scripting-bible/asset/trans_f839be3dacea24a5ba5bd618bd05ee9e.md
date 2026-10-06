

# 正则表达式

星号也可以应用于字符类。这允许您指定一个在文本中可能出现多次的字符组或字符范围：

```
$ echo "bt" | sed -n '/b[ae]*t/p'
bt
$ echo "bat" | sed -n '/b[ae]*t/p'
bat
$ echo "bet" | sed -n '/b[ae]*t/p'
bet
$ echo "btt" | sed -n '/b[ae]*t/p'
$
$ echo "baat" | sed -n '/b[ae]*t/p'
baat
$ echo "baeeet" | sed -n '/b[ae]*t/p'
baeeet
$ echo "baaeeat" | sed -n '/b[ae]*t/p'
baaeeeat
$ echo "baabeeet" | sed -n '/b[ae]*t/p'
$
```

只要字符 a 和 e 在字符 b 和 t 之间以任何组合形式出现（也包括完全不出现），该模式就会匹配。如果出现了定义类之外的任何其他字符，模式将匹配失败。

## 扩展正则表达式

POSIX ERE 模式包含了某些 Linux 应用和工具使用的额外符号。`awk` 程序可以识别 ERE 模式，但 `sed` 编辑器不能。请记住，`sed` 编辑器和 `awk` 程序中的正则表达式引擎之间存在差异。`awk` 程序可以使用大多数扩展模式符号，并提供 `sed` 编辑器没有的一些额外功能。然而，由于由于，它在处理数据流时通常较慢。

## 问号

问号与星号相似，但略有不同。问号表示前面的字符可以出现零次或一次，但是：

```
$ echo "bt" | awk '/be?t/(print $0)'
bt
$ echo "bet" | awk '/be?t/(print $0)'
bet
```

就像星号一样，你可以在字符类一起使用问号：

```
$ echo "bt" | awk '/b[ae]?t/(print $0)'
bt
$ echo "bat" | awk '/b[ae]?t/(print $0)'
bat
$ echo "bot" | awk '/b[ae]?t/(print $0)'
$
$ echo "beet" | awk '/b[ae]?t/(print $0)'
$
$ echo "baet" | awk '/b[ae]?t/(print $0)'
$
$ echo "beat" | awk '/b[ae]?t/(print $0)'
```

如果字符类中出现了零次或一次字符，模式将被匹配。然而，如果两个字符都出现，模式匹配将失败。

## 加号

加号是另一个与星号相似的模式符号，但与问号不同。加号表示前面的字符可以出现一次或多次，但必须至少出现一次。如果字符不存在，模式匹配将失败。

```
$ echo "beet" | awk '/be+/(print $0)'
$
$ echo "beet" | awk '/be+/(print $0)'
$
$ echo "bet" | awk '/be+/(print $0)'
$
$ echo "bt" | awk '/be+/(print $0)'
```

加号同样可以与字符类一起工作，方式与星号和问号相同：

```
$ echo "bt" | awk '/b[ae]+/(print $0)'
$ echo "bat" | awk '/b[ae]+/(print $0)'
$ echo "bet" | awk '/b[ae]+/(print $0)'
$ echo "beet" | awk '/b[ae]+/(print $0)'
```

## 使用大括号

ERE 中的大括号允许你对可重复的正则表达式指定限制。这通常被称为“间隔”（interval）。你可以通过以下两种格式表示间隔：

- m：正则表达式恰好出现 m 次。
- n：正则表达式至少出现 m 次，但不超过 n 次。

此功能允许你精调字符（或字符类）在模式中允许出现的次数。注意：默认情况下，`gawk` 程序不识别正则表达式间隔。你必须指定 `--re-interval` 选项 `gawk` 才能识别正则表达式间隔。

这是一个使用单一值间隔的示例：

```
$ echo "bt" | awk --re-interval=1 '/be?t/(print $0)'
$ echo "bet" | awk --re-interval=1 '/be?t/(print $0)'
$ echo "beet" | awk --re-interval=1 '/be?t/(print $0)'
```

通过指定间隔，你限制了字符串匹配模式时字符出现的次数。如果出现次数过多，模式匹配将失败。在指定下限和上限时，这种情况非常有用：

```
$ echo "bt" | awk --re-interval=1,2 '/be?t/(print $0)'
$ echo "bet" | awk --re-interval=1,2 '/be?t/(print $0)'
$ echo "beet" | awk --re-interval=1,2 '/be?t/(print $0)'
$ echo "beeet" | awk --re-interval=1,2 '/be?t/(print $0)'
```

在这个示例中，字符 e 可以出现一次或两次才能通过模式匹配；否则，匹配将失败。

间隔模式匹配也适用于字符类：

```
$ echo "bt" | awk --re-interval=1,2 '/b[ae][1,2]t/(print $0)'
$ echo "bat" | awk --re-interval=1,2 '/b[ae][1,2]t/(print $0)'
$ echo "beet" | awk --re-interval=1,2 '/b[ae][1,2]t/(print $0)'
$ echo "beat" | awk --re-interval=1,2 '/b[ae][1,2]t/(print $0)'
$ echo "beet" | awk --re-interval=1,2 '/b[ae][1,2]t/(print $0)'
$ echo "beeet" | awk --re-interval=1,2 '/b[ae][1,2]t/(print $0)'
$ echo "baeet" | awk --re-interval=1,2 '/b[ae][1,2]t/(print $0)'
$ echo "baeaet" | awk --re-interval=1,2 '/b[ae][1,2]t/(print $0)'
```

