

敏捷的棕色狐狸跳过了那只懒狗
敏捷的棕色狐狸跳过了那只懒狗
敏捷的棕色狐狸跳过了那只懒狗
$ sed 'd' data1

删除命令与特定地址配合使用显然是最用的。
这允许你从数据流中删除特定的文本行，可以通过行号：

```
$ sed '3d' data6
This is line number 1.
This is line number 2.
This is line number 4.
$
```

或者通过特定的行范围：

```
$ sed '2,3d' data6
This is line number 1.
This is line number 4.
$
```

或者通过使用特殊的文件结束字符：

```
$ sed '3,$d' data6
This is line number 1.
This is line number 2.
$
```

sed 编辑器的模式匹配功能也适用于删除命令：

```
$ sed '/number 1/d' data6
This is line number 2.
This is line number 3.
This is line number 4
$
```

sed 编辑器会删除包含你指定的模式文本的行。

> 注意：记住，sed 编辑器不会修改原始文件。你删除的任何行只会从 sed 编辑器的输出中消失。原始文件仍然包含那些“被删除”的行。

你也可以使用两个文本模式定义一个行范围，但这样做时要小心。第一个模式会“开启”行删除，第二个模式会“关闭”行删除。sed 编辑器会删除两个指定行之间的任何行（包括指定的行）：

```
$ sed '/1/,/3d' data6
This is line number 4.
$
```

# 第三部分 高级 Shell 脚本

我提到过你需要对此保持小心，因为每当 sed 编辑器检测到数据流中的起始模式时，删除功能就会“开启”。这可能会产生意想不到的结果：

```
$ cat data7
This is line number 1.
This is line number 2.
This is line number 3.
This is line number 4.
This is line number 1 again.
This is text you want to keep.
This is the last line in the file.
$ sed '/1/./3/d' data7
This is line number 4.
$
```

数据流中第二次出现带有数字 1 的行再次触发了删除命令，删除了剩余的行，因为停止模式没有被识别。当然，如果你指定的模式在文中从未出现过，也会另一个显而易见的问题：

```
$ sed '/1/./5/d' data7
```

由于删除功能在第一次模式匹配时已“开启”，但从未找到结束模式匹配，导致了整个数据流被处理。这两个操作之间的差异可能会令人困惑：

# 插入和追加文本

正如你所预期的，像任何其他编辑器一样，sed 编辑器允许你向数据流插入和追加文本行。这两个操作之间的差异可能会令人困惑：

- 插入命令 (i) 在指定行之前添加一个新行
- 追加命令 (a) 在指定行之后添加一个新行

关于这两个命令的一个令人困惑的地方是它们的格式。你不能在单行上使用这些命令。你必须单独另一行来指定要插入或追加的行。此操作格式为：

```
$ sed '[address]command\
new line
```

新行中的文本将出现在你指定的 sed 编辑器输出位置。记住，当你使用插入命令时，文本会出现在数据流中：

```
$ echo 'testing' | sed 'i\n> This is a test'
This is a test
testing
```

436

# 引入 sed 和 gawk

当你使用追加命令时，文本将出现在数据流文本之后：

```
$ echo "testing" | sed 'a\n> This is a test'
testing
This is a test
$
```

当你从命令行界面提示符使用 sed 编辑器时，你会收到二次提示输入新行数据。你必须在此行上完成 sed 编辑器命令，因为一旦你输入结束单引号，bash shell 就会处理该命令。

这在数据流文本之前或之后添加文本非常有效，但在数据流内部添加文本呢？

要在数据流行内部插入或追加数据，你必须使用地址来告诉 sed 编辑器你希望数据出现在哪里。在使用这些命令时，你只能指定单行地址。你可以匹配数字行或文本模式，但你不能使用地址范围（这是合理的，因为你只能在单行之前或之后插入或追加，而不能在一个范围内操作）。

这是一个在数据流的 3 之前插入新行的示例：

```
$ sed '3ia\n> is an inserted line.' data6
This is line number 1.
This is line number 2.
This is an inserted line.
This is line number 3.
This is line number 4.
$
```

这是一个在数据流的 3 之后追加新行的示例：

```
$ sed '3a\n> is an inserted line.' data6
This is line number 1.
This is line number 2.
This is line number 3.
This is an inserted line.
This is line number 4.
$
```

这使用的过程与插入命令相同；如果你有一个多行数据流，并且想在数据流的末尾追加新行文本，只需使用我们的新朋友美元符号，它代表最后一行数据：

```
$ sed '$a\n> This is a new line of text.' data6
```

437

# 第三部分 高级 Shell 脚本

This is line number 1.
This is line number 2.
This is line number 3.
This is line number 4.
This is a new line of text.

如果你想在数据流的开头添加新行，原理是相同的。
在第一行之前插入一个新行。

要插入或追加多行文本，你必须在每一行新文本后使用反斜杠，直到达到你想要插入或追加文本的最后一行：

```
$ sed 'li|
> This is one line of new text.\n> This is another line of new text.' data6
This is one line of new text.
This is another line of new text.
This is line number 1.
This is line number 2.
This is line number 3.
This is line number 4.
$
```

这两个指定的行都将添加到数据流中。

# 修改行

更改命令允许你修改整行的内容。它与插入和追加命令的方法相同，即必须单独指定新行：

```
$ sed '3c\n> This is a changed line.'
This is line number 1.
This is line number 2.
This is a changed line.
This is line number 4.
$
```

在这个例子中，sed 编辑器修改了第 3 行。你也可以使用文本作为地址：

```
$ sed '/number 3/\n> This is a changed line.'
This is line number 1.
This is line number 2.
This is a changed line.
This is line number 4.
$
```

# 引入 sed 和 awk 16

文本模式命令将更改数据流中匹配的任何行文本。

```
$ sed '/number/1c\
> This is a changed line.' data7
This is a changed line.
This is line number 2.
This is line number 3.
This is line number 4.
This is a changed line.
This is yet another line.
This is the last line in the file.
$
```

你可以在更改命令中使用地址范围，但结果可能不是你预期的：

```
$ sed '2,3c\
> This is a new line of text.' data6
This is line number 1.
This is a new line of text.
This is line number 4.
$
```

而不是修改这两行，sed 编辑器使用单行文本来替换这两行。

# 转换命令

转换命令 (y) 是 sed 编辑器唯一操作单个字符的。转换命令使用的格式为：

```
[address]/inchars/outchars/
```

转换命令对 inchars 和 outchars 的值执行一对一映射。inchars 中的第一个字符转换为 outchars 中的第一个字符。inchars 中的第二个字符转换为 outchars 中的第二个字符。这种映射持续到指定字符的长度。如果 inchars 和 outchars 的长度不相同，sed 编辑器将产生错误消息。

使用转换命令的简单示例是：

```
$ sed 'y/123/789/'
This is line number 7.
This is line number 8.
This is line number 9.
This is line number 4.
This is line number 7 again.
This is yet another line.
This is the last line in the file.
$
```

439

