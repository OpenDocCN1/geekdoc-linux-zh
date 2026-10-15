
`sed` 编辑器将你指定的每个命令仅应用于匹配指定地址的行。本节演示了如何在你的 `sed` 编辑器脚本中使用这两种地址指定技术。

# 数字行地址

使用数字地址时，你通过行在文本流中的位置来引用行。`sed` 编辑器将文本流中的第一行分配为行号，并对每个新行按顺序递增。

你在命令中指定的地址可以是单个行号，也可以由起始行号、逗号和结束行号指定的行范围。这里有一个指定 `sed` 命令将应用的行号的示例：

```
$ sed '2s/dog/cat/' data.txt
The quick brown fox jumps over the lazy dog
The quick brown fox jumps over the lazy cat
The quick brown fox jumps over the lazy dog
The quick brown fox jumps over the lazy dog
```

`sed` 编辑器仅对每个指定的地址修改两行中的文本。这里是另一个使用行范围地址的示例：

```
$ sed '2,3s/dog/cat/' data.txt
The quick brown fox jumps over the lazy dog
The quick brown fox jumps over the lazy cat
The quick brown fox jumps over the lazy cat
The quick brown fox jumps over the lazy dog
```

如果你想将命令应用到从文本某处开始一直持续到文本结束的一组行，可以使用特殊地址美元符号 `$`：

```
$ sed '2,$s/dog/cat/' data.txt
The quick brown fox jumps over the lazy dog
The quick brown fox jumps over the lazy cat
The quick brown fox jumps over the lazy cat
The quick brown fox jumps over the lazy cat
```

# 第三部分：高级 Shell 脚本

因为你可能知道文本中有多少行数据，美元符号 `$` 通常非常派上用场。

# 使用文本模式过滤器

限制命令应用行的另一种方法稍微复杂一些。`sed` 编辑器允许你指定一个模式，并用该模式过滤命令所需的行。格式如下：

```
/pattern/command
```

你必须将指定的模式封装在正斜杠 `/` 之间。`sed` 编辑器仅允许包含你指定模式的行执行命令。例如，如果你只想为用户 Samantha 更改默认 shell，你会使用 `sed` 命令：

```
$ grep Samantha /etc/passwd
samantha:x:502:502:/home/Samantha:/bin/bash
$
$ sed '/Samantha/s|/bash|/csh/' /etc/passwd
root:x:0:root:/bin/bash
bin:x:1:/bin/nologin
[...
Christine:x:501:501:Christine B:/home/Christine:/bin/bash
samantha:x:502:502:/home/Samantha:/bin/csh
Timothy:x:503:503:/home/Timothy:/bin/bash
$
```

命令仅应用到匹配该文本模式的行。虽然使用固定文本模式对于过滤特定值（如 userid 示例所示）可能有用，但它的功能是有限的。`sed` 编辑器使用了一种名为“正则表达式”的功能，允许你创建可以不断改进的模式。

正则表达式允许你为各种数据创建高级的文本模式匹配公式。这些公式结合了一系列通配符、特殊字符和固定文本字符，产生一个简洁的模式，可以匹配任何文本情况。正则表达式是 Shell 脚本编程中最令人恐惧的部分之一，第 20 章将详细介绍它们。

# 命令分组

如果你需要对单行执行多个命令，请使用大括号将命令分组：

```
$ sed '2{
  s/dog/cat/
  s/fox/bird
}'
```

`sed` 编辑器将你指定的每个命令仅应用于匹配指定地址的行。这就是你分组的方式：

```
The quick brown fox jumps over the lazy dog
The quick brown fox jumps over the lazy cat
The quick brown fox jumps over the lazy dog
The quick brown fox jumps over the lazy dog
```

# 删除行

替换命令并不是 `sed` 编辑器中唯一的命令。如果你需要删除文本行，可以使用删除命令。删除命令与指定的地址结合使用显然有用：

```
$ sed 'd' data.txt
The quick brown fox jumps over the lazy dog
The quick brown fox jumps over the lazy cat
The quick brown fox jumps over the lazy dog
The quick brown fox jumps over the lazy dog
```

删除命令从流中删除行，既可以通过行号：

```
$ sed '2/d' data.txt
The quick brown fox jumps over the lazy dog
The quick brown fox jumps over the lazy cat
The quick brown fox jumps over the lazy dog
The quick brown fox jumps over the lazy dog
```

也可以通过特定的行范围：

```
$ sed '2,3d' data.txt
The quick brown fox jumps over the lazy dog
The quick brown fox jumps over the lazy dog
```

或者使用特殊的特殊末尾字符：

```
$ sed '3,$d' data.txt
The quick brown fox jumps over the lazy dog
The quick brown fox jumps over the lazy cat
```

`sed` 编辑器的模式匹配功能也适用于删除命令：

```
$ sed '/number 1/d' data.txt
The quick brown fox jumps over the lazy cat
The quick brown fox jumps over the lazy dog
The quick brown fox jumps over the lazy dog
```

`sed` 编辑器移除包含你指定模式的行。记住，`sed` 编辑器不会更改原始文件。你删除的行仅从 `sed` 编辑器的输出中消失。原始文件仍然包含这些“已删除”的行。

你也可以使用两个文本模式删除行范围，但这样做时要小心。你指定的第一个模式会“开启”行删除，而第二个模式会“关闭”行删除。`sed` 编辑器会删除指定行之间的所有行（包括指定的行）：

```
$ sed '/1/,/3/d' data6.txt
This is line number 4.
```

此外，你必须小心，因为每当 `sed` 编辑器在数据流中检测到起始模式时，删除功能就会开启。可能会产生意外的结果：

```bash
$ cat data7.txt
This is line number 1.
This is line number 2.
This is line number 3.
This is line number 4.
This is line number 1 again.
This is text you want to keep.
This is the last line in the file.
```

```bash
$ sed '/1/,/3/d' data7.txt
This is line number 4.
```

包含数字 1 的行的再次出现触发了删除命令，删除了数据流中的剩余所有行，因为停止模式没有被识别。此外另一个显而易见的问题是，如果你指定了一个在文中从未出现过的停止模式：

```bash
$ sed '/1/,/5/d' data7.txt
```

由于删除功能在第一次匹配到模式时被“开启”了，但从未找到过该模式匹配，因此整个数据流都被删除了。

## 插入和追加文本

正如你预期的那样，像任何其他编辑器一样，`sed` 编辑器允许你向数据流中插入和追加行。这两个操作之间的区别可能会让人产生困惑：

- 插入命令 (`i`) 在指定的行之前添加一个新行。
- 追加命令 (`a`) 在指定的行之后添加一个新行。

这两个命令中令人困惑的是它们的格式。你不能在单行上使用这些命令。你必须在单独的一行指定要插入或追加的行的位置。以下是执行此操作的格式：
