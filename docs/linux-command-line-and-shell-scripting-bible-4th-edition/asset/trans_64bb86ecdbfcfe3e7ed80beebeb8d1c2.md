

...脚本。现在我们将在测试运行中尝试一下：

```bash
$ cat data2.txt
Header Line
First Data Line
Second Data Line
End of Data Lines
$
$ sed -n '{!G ; h ; $p }' data2.txt
End of Data Lines
Second Data Line
First Data Line
Header Line
$
```

`sed` 编辑器脚本按预期执行。脚本的输出反转了文本文件中的原始行。这展示了在 `sed` 脚本中使用保持空间（hold space）的强大功能。它为操纵脚本输出中的行顺序提供了一种简单的方法。

> **注意**
>
> 如果你想知道的话，一个 Bash shell 命令也可以执行反转文本文件的功能。`tac` 命令以相反的顺序显示文本文件。你可能已经注意到了该命令巧妙的命名，因为它执行的是 `cat` 命令的相反功能。

## 更改流程

通常情况下，`sed` 编辑器从顶部开始处理命令，并逐步处理到脚本的末尾（例外是 `d` 命令，它强制 `sed` 编辑器返回脚本顶部而不读取新的文本行）。`sed` 编辑器提供了一种改变命令脚本流程的方法，产生类似于结构化编程环境的结果。

## 分支

在上一节中，你看到了感叹号命令如何用于否定命令对某行文本的影响。`sed` 编辑器提供了一种否定整个命令部分的方法，基于地址、地址模式或地址范围。这允许你仅在数据流中的特定子集上执行一组命令。

分支（b）命令的格式如下：

```text
[address]b [label]
```

*address* 参数确定哪些数据行触发分支（b）命令。*label* 参数定义要跳转到的脚本位置。如果 *label* 参数不存在，分支（b）命令会跳过触发分支的那一行或多行数据，继续处理其他文本行。

下面是一个使用 *address* 参数和分支命令但不使用 *label* 的示例：

```bash
$ cat data2.txt
Header Line
First Data Line
Second Data Line
End of Data Lines
$
sed '{2,3b ;
> s/Line/Replacement/}
> ' data2.txt
Header Replacement
First Data Line
Second Data Line
End of Data Replacements
$
```

分支（b）命令跳过了数据流中第二行和第三行的替换命令。

你可以定义一个 *label*，为分支命令提供一个跳转位置，而不是跳转到脚本末尾。标签以冒号开头，长度最长为七个字符：

```text
:label2
```

要指定 *label*，只需在 b 命令后添加即可。使用标签允许你为匹配分支地址的数据提供备用命令，同时仍使用脚本中的原始命令处理其他文本行：

```bash
$ sed '{Firstb jump1 ;
> s/Line/Replacement/
> :jump1
> s/Line/Jump Replacement/}
> ' data2.txt
Header Replacement
First Data Jump Replacement
Second Data Replacement
End of Data Replacements
$
```

分支（b）命令指定如果行中出现匹配文本 First，程序应跳转到标记为 jump1 的脚本行。如果分支命令的地址不匹配，`sed` 编辑器继续处理脚本中的命令，包括分支标签 jump1 后的命令。（因此，对于不匹配分支地址的行，两个替换命令都会被处理。）

如果行匹配分支地址，`sed` 编辑器分支到标记行 jump1。因此，对于匹配分支地址的行，仅执行最后一个替换命令。

该示例展示了跳转到 `sed` 脚本中更下方的标签。你也可以跳转到脚本中较早出现的标签，从而产生循环效果：

```bash
$ echo "This, is, a, test, to, remove, commas." |
> sed -n {
> :start
> s/,,//1p
> b start
> }
This is, a, test, to, remove, commas.
This is a, test, to, remove, commas.
This is a test, to, remove, commas.
This is a test to remove, commas.
This is a test to remove commas.
^C
$
```

每次脚本迭代都会从字符串中移除第一个逗号的出现并打印该字符串。这个脚本有一个陷阱——它永远不会结束。这种情况会产生一个无限循环，不断寻找逗号，直到你手动通过 Ctrl+C 键组合发送信号停止它。

为了防止这个问题，请为分支（b）命令指定一个地址模式。如果模式不存在，分支就会停止：

```bash
$ echo "This, is, a, test, to, remove, commas." |
> sed -n {
> :start
> s/,//1p
> /,/b start
> }'
This is, a, test, to, remove, commas.
This is a, test, to, remove, commas.
This is a test, to, remove, commas.
This is a test to, remove, commas.
This is a test to remove, commas.
This is a test to remove commas.
$
```

现在分支命令只有当行中有逗号时才分支。在最后一个逗号被移除后，分支（b）命令不再执行，允许脚本正确结束。

## 测试

与分支命令类似，测试（t）命令也用于修改 `sed` 编辑器脚本的流程。与基于地址跳转到标签不同，测试（t）命令基于先前替换命令的结果跳转到标签。

如果替换命令成功匹配并替换了模式，测试命令会分支到指定的标签。如果替换命令未匹配指定模式，测试命令不会分支。

测试（t）命令使用与分支命令相同的格式：

```text
[address]t [label]
```

与分支命令一样，如果你不指定标签，`sed` 将跳转到脚本命令的末尾，但仅在测试成功时。

测试（t）命令提供了一种廉价的方法来对数据流中的文本执行基本的 if-then 语句。例如，如果另一个替换已经执行，你就不需要再进行替换，不带指定标签的测试命令可以帮助实现：

```bash
$ sed '{s/First/Matched/ ; t
> s/Line/Replacement/}
> ' data2.txt
Header Replacement
Matched Data Line
Second Data Replacement
End of Data Replacements
$
```

第一个替换命令寻找模式文本 First。如果它匹配行中的模式，则替换该文本，并且测试（t）命令跳过第二个替换命令。如果第一个替换命令不匹配文本模式，则处理第二个替换命令。

使用测试命令，我们可以清理我们尝试使用分支命令时创建的循环：

```bash
$ echo "This, is, a, test, to, remove, commas." |
> sed -n '{
> :start
> s/,/\1p
> t start
> }'
This is, a, test, to, remove, commas.
This is a, test, to, remove, commas.
This is a test, to, remove, commas.
This is a test to, remove, commas.
This is a test to remove, commas.
This is a test to remove commas.
$
```

当没有更多的逗号替换需要执行时，测试命令不会分支，处理结束。

## 通过模式替换

我们已经涵盖了如何使用模式在 `sed` 命令中替换数据流中的文本。然而，当使用通配符时，很难确切知道哪些文本会匹配模式。
例如，假设你想在一行中匹配的一个词周围加上双引号。如果你只是在模式中查找一个要匹配的词，那很简单：

```bash
$ echo "The cat sleeps in his hat." |
> sed 's/cat/"cat"/'
  The "cat" sleeps in his hat.
  $
```

但如果你在模式中使用通配符（.）来匹配多个词会怎样？

```bash
$ echo "The cat sleeps in his hat." |
> sed 's/.at/".at"/g'
  The ".at" sleeps in his ".at".
  $
```

替换字符串使用了点通配符来匹配“at”前的任何字符的任何出现。不幸的是，替换字符串中匹配的单词的通配符值并不匹配。

## 使用和号

`sed` 编辑器有一个解决方案。和号符号（&）用于在替换命令中表示匹配的模式。任何匹配定义的模式的文本，你都可以使用和号符号在替换模式中引用它。这允许你操纵任何匹配定义模式的单词：

```bash
$ echo "The cat sleeps in his hat." |
> sed 's/.at/"&"/g'
  The "cat" sleeps in his "hat".
  $
```

当模式匹配单词 cat 时，"cat" 出现在被替换的词中。当它匹配单词 hat 时，"hat" 出现在被替换的词中。

