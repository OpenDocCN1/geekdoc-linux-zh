
`sed` 编辑器会将所有命令应用于地址范围内的所有行。

### 删除行

文本替换命令并不是 `sed` 编辑器中唯一的命令。如果你需要删除文本流中的特定行，可以使用删除命令。

删除（d）命令基本上就是字面意思：它会删除任何符合所提供寻址方案（addressing scheme）的文本行。在使用 `d` 命令时要小心，因为如果你忘记包含寻址方案，流中的所有行都会被删除：

```
$ cat data1.txt
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy dog.
$
$ sed 'd' data1.txt
$ 
```

显然，当 `d` 命令与指定的地址结合使用时，它最为有用。这允许你从数据流中删除特定的文本行，可以通过行号：

```
$ cat data6.txt
This is line number 1.
This is line number 2.
This is the 3rd line.
This is the 4th line.
$
$ sed '3d' data6.txt
This is line number 1.
This is line number 2.
This is the 4th line.
$ 
```

或通过特定的行范围：

```
$ sed '2,3d' data6.txt
This is line number 1.
This is the 4th line.
$ 
```

或使用特殊的文件结束符：

```
$ sed '3,$d' data6.txt
This is line number 1.
This is line number 2.
$ 
```

*sed* 编辑器的模式匹配功能也适用于删除（d）命令：

```
$ sed '/number 1/d' data6.txt
This is line number 2.
This is the 3rd line.
This is the 4th line.
$ 
```

*sed* 编辑器会删除包含匹配你指定模式的文本的行。

# 注意

请记住，*sed* 编辑器不会修改原始文件。你删除的任何行只是从 *sed* 编辑器的输出中消失。原始文件仍然包含那些“已删除”的行。

你还可以使用两个文本模式来删除一行范围内的行，但这样做时要小心。你指定的第一个模式会“开启”行删除，而第二个模式会“关闭”行删除。*sed* 编辑器会删除两个指定行之间的任何行（包括指定的行）：

```
$ sed '/1/,/3/d' data6.txt
This is the 4th line.
$ 
```

此外，你必须小心，因为每当 *sed* 编辑器在数据流中检测到起始模式时，删除功能就会“开启”。这可能会产生意外的结果：

```
$ cat data7.txt
This is line number 1.
This is line number 2.
This is the 3rd line.
This is the 4th line.
This is line number 1 again; we want to keep it.
This is more text we want to keep.
Last line in the file; we want to keep it.
$ sed '/1/,/3/d' data7.txt
This is the 4th line.
$ 
```

包含数字 1 的行第二次出现时，再次触发了删除（d）命令，删除了数据流中剩余的行，因为停止模式未被识别。当然，另一个明显的问题是，如果你指定了一个在文本中从未出现的停止模式：

```
$ sed '/3/,/5/d' data7.txt
This is line number 1.
This is line number 2.
$ 
```

## 第三部分：高级 Shell 脚本

因为 `delete` 功能在第一个模式匹配时“开启”，但从未找到结束模式匹配，所以它没有“关闭”。数据流的其余部分全部被删除。

### 插入和追加文本

正如你所预期的，像其他编辑器一样，`sed` 编辑器允许你向数据流中插入和追加文本行。然而，这两个操作之间的区别可能会令人困惑：

- 插入（i）命令在指定行*之前*添加一个新行。
- 追加（a）命令在指定行*之后*添加一个新行。

这两个命令令人困惑的地方在于它们的格式。你并不总是能在单个命令行上使用这些命令。有时你必须将要插入或追加新行的行在单独的一行中指定。以下是执行此操作的格式：

```
sed '{address}command\
new_line'
```

`new_line` 中的文本会在 `sed` 编辑器输出中出现在你指定的位置。请记住，当你使用插入（i）命令时，文本会出现在数据流文本*之前*：

```
$ echo "Test Line 2" | sed 'i\Test Line 1'
Test Line 1
Test Line 2
$
```

当你使用追加（a）命令时，文本会出现在数据流文本*之后*：

```
$ echo "Test Line 2" | sed 'a\Test Line 1'
Test Line 2
Test Line 1
$
```

当你从命令行接口提示符使用 `sed` 编辑器时，你会看到一个二级提示符，用于输入新行数据。你必须在这一行上完成 `sed` 编辑器命令。输入结束的单引号后，Bash shell 会处理该命令：

```
$ echo "Test Line 2" | sed 'i\
> Test Line 1'
Test Line 1
Test Line 2
$
```

这对于在数据流文本之前或之后添加文本非常有效，那么在数据流内部添加文本呢？

要在数据流行内部插入或追加数据，你必须使用寻址来告诉 `sed` 编辑器你希望数据出现的位置。使用这些命令时，你只能指定单个行地址。你可以匹配数字行号或文本模式，但不能使用地址范围。这是合乎逻辑的，因为你只能在单个行之前或之后插入或追加，而不能针对一行范围。

以下是一个在数据流第 3 行之前插入新行的示例：

```
$ cat data6.txt
This is line number 1.
This is line number 2.
This is the 3rd line.
This is the 4th line.
$
$ sed '3i\
> This is an inserted line.
> ' data6.txt
This is line number 1.
This is line number 2.
This is an inserted line.
This is the 3rd line.
This is the 4th line.
$
```

以下是一个在数据流第 3 行之后追加新行的示例：

```
$ sed '3a\
> This is an appended line.
> ' data6.txt
This is line number 1.
This is line number 2.
This is the 3rd line.
This is an appended line.
This is the 4th line.
$
```

这与插入（i）命令的过程相同；它只是将新文本行放置在指定行号之后。如果你有一个多行数据流，并且你想在数据流末尾追加一行新文本，只需使用美元符号，它代表数据的最后一行：

```
$ sed '$a\
> This line was added to the end of the file.
> ' data6.txt
This is line number 1.
This is line number 2.
This is the 3rd line.
This is the 4th line.
This line was added to the end of the file.
$
```

如果你想在数据流的开头添加一行新文本，同样的原理也适用。只需在第 1 行之前插入（i）一行新文本。

如果要插入或追加多于一行的文本，你必须在新文本的每一行上使用反斜杠，直到你达到想要插入或追加文本的最后一行：

```
$ sed '1i\
> This is an inserted line.\
> This is another inserted line.
> ' data6.txt
This is an inserted line.
This is another inserted line.
This is line number 1.
This is line number 2.
This is the 3rd line.
This is the 4th line.
$
```

指定的两行都被添加到数据流中。

### 更改行

更改（`c`）命令允许你更改数据流中整行文本的内容。它的工作方式与插入和追加命令相同，即你必须将新行与 `sed` 命令的其余部分分开指定：

```
$ sed '2c\
> This is a changed line of text.
> ' data6.txt
This is line number 1.
This is a changed line of text.
This is the 3rd line.
This is the 4th line.
$
```

在上面的示例中，`sed` 编辑器更改了第 2 行的文本。你 также 可以使用文本模式作为地址：

```
$ sed '/3rd line/c\
> This is a changed line of text.
> ' data6.txt
This is line number 1.
This is line number 2.
This is a changed line of text.
This is the 4th line.
$
```

文本模式更改（`c`）命令会更改数据流中匹配的任何文本行。

```
$ cat data8.txt
I have 2 Infinity Stones
I need 4 more Infinity Stones
I have 6 Infinity Stones!
I need 4 Infinity Stones
I have 6 Infinity Stones...
I want 1 more Infinity Stone
$

$ sed '/have 6 Infinity Stones/c\
> Snap! This is changed line of text.
> ' data8.txt
```
