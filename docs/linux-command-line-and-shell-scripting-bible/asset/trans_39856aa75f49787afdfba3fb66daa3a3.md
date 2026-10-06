

## sed 编辑器基础

成功使用 sed 编辑器的关键在于了解它无数的命令和格式，这些格式可以用于自定义你的文本编辑。本节描述了你可以整合到脚本中的一些基本命令和功能，以开始使用 sed 编辑器。

## 更多替换选项

你已经看到了如何使用 `s` 命令将行中的文本替换为新文本。然而，替换命令还有其他可用选项，可以帮助你的工作变得更容易。

## 替换标志

替换命令在替换文本字符串中的匹配模式时有一个注意事项。请看这个示例中发生的情况：

```
$ cat data4
This is a test of the test script.
This is the second test of the test script.
$ sed 's/test/trial/' data4
This is a trial of the test script.
This is the second trial of the test script.
$
```

替换命令在替换多行时运行良好，但默认情况下，它只替换每行的第一次出现的内容。要让替换命令作用于文本的不同出现位置，你必须使用替换标志。替换标志设置在子命令字符串之后：

```
$ s/pattern/replacement/flags
```

- 数字，表示应替换为新文本的模式出现次数。
- g — 表示现有文本的所有出现处都替换为新文本。
- p — 表示打印原始行的内容。
- w file — 将替换结果写入文件。

在第一次替换中，你可以指定 sed 编辑器应该将匹配模式的哪一次出现替换为新文本：

```
$ sed 's/test/trial/2' data4
This is a test of the trial script.
This is the second test of the trial script.
$
```

由于指定了 `2` 作为替换标志，sed 编辑器只替换每行中第二次出现的模式。`g` 替换标志允许你替换文本中模式的每一次出现位置：

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

`-n` 选项抑制 sed 编辑器的输出。然而，`p` 替换标志会输出任何被修改过的行。将两者结合使用，会对被替换命令修改过的行产生输出。

`w` 替换标志产生相同的输出，但将其存储在指定文件中：

```
$ sed 's/test/trial/w' test data5
This is a trial line.
This is a different line.
$ cat test
This is a trial line.
$
```

sed 编辑器的正常输出出现在 STDOUT 中，但只有包含匹配模式的行会被存储在指定的输出文件中。

## 替换字符

有时你在文本字符串中运行字符在替换模式中并不容易使用。Linux 世界中一个著名的例子是正斜杠 `/`。

在文件中替换路径可能会变得很尴尬。例如，如果你想将 Cshell 替换为 bash shell，你必须这样做：

```
$ sed 's/\/bin\/bash\//bin\/csh/' /etc/passwd
```

由于正斜杠被用作字符串分隔符，如果它出现在模式文本中，你必须使用反斜杠对其进行转义。这通常会导致混淆和错误。

为了解决这个问题，sed 编辑器允许你在替换命令中选择一个不同的字符作为字符串分隔符：

```
$ sed '!/bin/bash!/bin/csh!' /etc/passwd
```

## 第三部分 高级 Shell 脚本

在这个示例中，感叹号 `!` 被用于字符串分隔符，使得路径变得更容易阅读和理解。

## 使用地址

默认情况下，你在 sed 编辑器中使用的命令适用于文本数据的所有行。如果你只想对特定的行或一组行应用命令，你必须使用行寻址。

sed 编辑器中有两种行寻址的形式：

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

sed 编辑器仅将你指定的每个命令应用到匹配指定地址的行。

本节在你的 sed 编辑器脚本中演示了这两种地址技术。

## 数字行寻址

使用数字行寻址时，你通过它们在文本流中的位置来引用行。sed 编辑器将文本流中的第一行分配为行号，并对每个新行顺序递增。

你在命令中指定的地址可以是单个行号，也可以是由起始行号、逗号和结束行号指定的行范围。这里有一个指定 sed 命令应用的行号的示例：

```
$ sed '2s/dog/cat/' dat
The quick brown fox jumps over the lazy dog
The quick brown fox jumps over the lazy cat
The quick brown fox jumps over the lazy dog
The quick brown fox jumps over the lazy cat
```

（注：由于原文中存在大量重复段落，译文已根据要求对内容进行了翻译并确保不重复输出。）

