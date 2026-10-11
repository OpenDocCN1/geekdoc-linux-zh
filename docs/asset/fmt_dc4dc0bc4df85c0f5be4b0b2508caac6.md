
由于指定了 `2` 作为替换标志，`sed` 编辑器只替换每行中第二次出现的模式。`g` 替换标志允许你替换文本中模式的每一次出现位置：

```
$ sed 's/test/trial/g' data4
This is a trial of the trial script.
This is the second trial of the trial script.
$
```

`p` 替换标志打印包含替换命令中匹配模式的行。这通常与 `-n` 选项配合使用：

```
$ cat data5
This is a test line.
This is a different line.
$ sed -n 's/test/trial/p' data5
This is a trial line.
$
```

`-n` 选项抑制 `sed` 编辑器的输出。然而，`p` 替换标志会输出任何被修改过的行。将两者结合使用，会对被替换命令修改过的行产生输出。

`w` 替换标志产生相同的输出，但将其存储在指定文件中：

```
$ sed 's/test/trial/w' test data5
This is a trial line.
This is a different line.
$ cat test
This is a trial line.
$
```

`sed` 编辑器的正常输出出现在 STDOUT 中，但只有包含匹配模式的行会被存储在指定的输出文件中。

## 替换字符

有时你在文本字符串中运行字符在替换模式中并不容易使用。Linux 世界中一个著名的例子是正斜杠 `/`。

在文件中替换路径可能会变得很尴尬。例如，如果你想将 Cshell 替换为 bash shell，你必须这样做：

```
$ sed 's/\/bin\/bash\//bin\/csh/' /etc/passwd
```

由于正斜杠被用作字符串分隔符，如果它出现在模式文本中，你必须使用反斜杠对其进行转义。这通常会导致混淆和错误。

为了解决这个问题，`sed` 编辑器允许你在替换命令中选择一个不同的字符作为字符串分隔符：

```
$ sed '!/bin/bash!/bin/csh!' /etc/passwd
```

在这个示例中，感叹号 `!` 被用于字符串分隔符，使得路径变得更容易阅读和理解。

## 使用地址

默认情况下，你在 `sed` 编辑器中使用的命令适用于文本数据的所有行。如果你只想对特定的行或一组行应用命令，你必须使用行寻址。

`sed` 编辑器中有两种行寻址的形式：

- 数字行范围
- 过滤掉行的文本模式

这两种形式使用相同的格式来指定地址：

```
[address]command
```

你也可以为特定地址将多个命令组合在一起：

```
address {
command1
command2
command3
}
```

`sed` 编辑器仅将你指定的每个命令应用到匹配指定地址的行。

本节在你的 `sed` 编辑器脚本中演示了这两种地址技术。

### 数字行寻址

使用数字行寻址时，你通过它们在文本流中的位置来引用行。`sed` 编辑器将文本流中的第一行分配为行号，并对每个新行顺序递增。

你在命令中指定的地址可以是单个行号，也可以是由起始行号、逗号和结束行号指定的行范围。这里有一个指定 `sed` 命令应用的行号的示例：

```
$ sed '2s/dog/cat/' dat
The quick brown fox jumps over the lazy dog
The quick brown fox jumps over the lazy cat
The quick brown fox jumps over the lazy dog
The quick brown fox jumps over the lazy cat
```

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

`sed` 编辑器的模式匹配功能也适用于删除命令：

```
$ sed '/number 1/d' data6
This is line number 2.
This is line number 3.
This is line number 4
$
```

`sed` 编辑器会删除包含你指定的模式文本的行。

> 注意：记住，`sed` 编辑器不会修改原始文件。你删除的任何行只会从 `sed` 编辑器的输出中消失。原始文件仍然包含那些“被删除”的行。

你也可以使用两个文本模式定义一个行范围，但这样做时要小心。第一个模式会“开启”行删除，第二个模式会“关闭”行删除。`sed` 编辑器会删除两个指定行之间的任何行（包括指定的行）：

```
$ sed '/1/,/3d' data6
This is line number 4.
$
```

我提到过你需要对此保持小心，因为每当 `sed` 编辑器检测到数据流中的起始模式时，删除功能就会“开启”。这可能会产生意想不到的结果：

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

由于删除功能在第一次模式匹配时已“开启”，但从未找到结束模式匹配，导致了整个数据流被处理。

## 插入和追加文本

正如你所预期的，像任何其他编辑器一样，`sed` 编辑器允许你向数据流插入和追加文本行。这两个操作之间的差异可能会令人困惑：

- 插入命令 `i` 在指定行之前添加一个新行
- 追加命令 `a` 在指定行之后添加一个新行

关于这两个命令的一个令人困惑的地方是它们的格式。你不能在单行上使用这些命令。你必须单独另一行来指定要插入或追加的行。此操作格式为：

```
$ sed '[address]command\
new line
```

新行中的文本将出现在你指定的 `sed` 编辑器输出位置。记住，当你使用插入命令时，文本会出现在数据流中：

```
$ echo 'testing' | sed 'i\n> This is a test'
This is a test
testing
```

当你使用追加命令时，文本将出现在数据流文本之后：

```
$ echo "testing" | sed 'a\n> This is a test'
testing
This is a test
$
```

当你从命令行界面提示符使用 `sed` 编辑器时，你会收到二次提示输入新行数据。你必须在此行上完成 `sed` 编辑器命令，因为一旦你输入结束单引号，`bash` shell 就会处理该命令。

这在数据流文本之前或之后添加文本非常有效，但在数据流内部添加文本呢？

要在数据流行内部插入或追加数据，你必须使用地址来告诉 `sed` 编辑器你希望数据出现在哪里。在使用这些命令时，你只能指定单行地址。你可以匹配数字行或文本模式，但你不能使用地址范围。

这是一个在数据流的 3 之前插入新行的示例：
