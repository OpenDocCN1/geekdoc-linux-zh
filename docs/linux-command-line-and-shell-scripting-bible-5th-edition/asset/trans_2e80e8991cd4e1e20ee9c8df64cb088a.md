

## 第三部分：高级 Shell 脚本编程

在文本中，你必须使用一个*替换标志*。替换标志设置在替换命令字符串之后：

`s/pattern/replacement/flags`

有四种类型的替换标志可用：

-   一个数字，指示应进行新文本替换的模式出现位置
-   g，指示应为现有文本的所有出现位置替换新文本
-   p，指示应打印原始行的内容
-   w *文件*，意思是将替换结果写入文件

在第一类替换中，你可以指定**sed** 编辑器应对匹配模式的*哪个出现位置*进行新文本替换：

```
$ sed 's/test/trial/2' data4.txt
This is a test of the trial script.
This is the second test of the trial script.
$
```

指定 2 作为替换标志的结果是，**sed** 编辑器仅在每行的*第二个出现位置*替换该模式。g 替换标志允许你替换文本中该模式的所有出现位置（全局）：

```
$ sed 's/test/trial/g' data4.txt
This is a trial of the trial script.
This is the second trial of the trial script.
$
```

p 替换标志会打印出包含匹配模式的行，前提是该行是在替换命令中处理的。这通常与 -n **sed** 选项一起使用：

```
$ cat data5.txt
This is a test line.
This is a different line.
$
$ sed -n 's/test/trial/p' data5.txt
This is a trial line.
$
```

-n 选项会抑制 **sed** 编辑器的输出。然而，p 替换标志会输出任何已被修改的行。将这两者结合使用，只会为那些被替换命令修改过的行产生输出。

w 替换标志产生相同的输出，但将输出存储在指定的文件中：

```
$ sed 's/test/trial/w test.txt' data5.txt
This is a trial line.
This is a different line.
$
$ cat test.txt
This is a trial line.
$
```

`sed` 编辑器的正常输出显示在 `STDOUT` 中，但只有包含匹配模式的行才会存储在指定的输出文件中。

### 替换字符

有时，你遇到文本字符串中不易在替换模式中使用这些字符。在 Linux 世界中，一个常见的例子是前向斜杠（`/`）。

在文件中替换路径名可能会变得麻烦。例如，如果你想在 `/etc/passwd` 文件中用 Bash shell 替换 C shell，你必须这样做：

```
$ sed 's/\bin/\bash/\bin/\csh/' /etc/passwd
```

因为前向斜杠被用作字符串分隔符，如果它出现在模式文本中，你必须使用反斜杠进行转义。这常常导致混淆和错误。

为了解决这个问题，`sed` 编辑器允许你在替换命令中选择其他字符作为字符串分隔符：

```
$ sed 's!\bin/\bash!/bin/\csh!' /etc/passwd
```

在此示例中，感叹号 (!) 用作字符串分隔符，使得路径名更易于阅读和理解。

### 使用地址

默认情况下，你在 `sed` 编辑器中使用的命令适用于文本数据的所有行。如果你想将命令仅应用于特定行或一组行，你必须使用*行寻址*。

`sed` 编辑器中有两种形式的行寻址：

-   一个数字行范围
-   一个匹配行内文本的文本模式

两种形式都使用相同的格式来指定地址：

`[address] command`

你还可以将多个命令组合在一起，用于特定地址：

```
address {
command1
command2
command3
}
```

`sed` 编辑器将你指定的每个命令仅应用于匹配指定地址的行。本节演示如何在你的 `sed` 编辑器脚本中使用这两种寻址技术。

### 数字行寻址

使用数字行寻址时，你使用行在文本流中的位置来引用行。`sed` 编辑器将文本流中的第一行指定为行号 1，并为每个新行按顺序递增。

你在命令中指定的地址可以是单个行号，或者由起始行号、逗号和结束行号指定的行范围。这是一个指定 `sed` 命令将应用于某一行号的示例：

```
$ cat data1.txt
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy dog.
$
$ sed '2s/dog/cat/' data1.txt
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy cat.
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy dog.
$
```

`sed` 编辑器仅根据指定的地址修改了第 2 行的文本。这是另一个示例，这次使用了一个行地址范围（第 2 行到第 3 行）：

```
$ sed '2,3s/dog/cat/' data1.txt
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy cat.
The quick brown fox jumps over the lazy cat.
The quick brown fox jumps over the lazy dog.
$
```

如果你想将命令应用于从文本中某一点开始并持续到文本末尾的一组行，你可以使用美元符号代替最后一个地址范围数字：

```
$ sed '2,$s/dog/cat/' data1.txt
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy cat.
The quick brown fox jumps over the lazy cat.
The quick brown fox jumps over the lazy cat.
$
```

由于你可能不知道文本中有多少行数据，美元符号通常非常有用。

### 使用文本模式过滤器

限制命令应用行的另一种方法稍微复杂一些。`sed` 编辑器允许指定一个文本模式，并将其用作过滤器来确定命令应用于哪些行。格式如下：

`/pattern/command`

你必须用前向斜杠封装你指定的模式。`sed` 编辑器仅将命令应用于包含你指定的文本模式的行。

例如，如果你只想为用户 *rich* 更改默认 shell，你可以使用 *sed* 命令：

```
$ grep '/bin/bash /etc/passwd
root:x:0:0:root:/root:/bin/bash
christine:x:1001:1001:/home/christine:/bin/bash
rich:x:1002:1002:/home/rich:/bin/bash
$
$ sed 's/rich/s/bash/csh/' /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
[...]
christine:x:1001:1001:/home/christine:/bin/bash
sshd:x:126:65534::/run/sshd:/usr/sbin/nologin
rich:x:1002:1002:/home/rich:/bin/csh
$
```

该命令仅应用于包含匹配文本模式的行。虽然使用固定的文本模式可能有助于过滤特定值，如前一个示例所示，但它在使用上有一定的局限性。*sed* 编辑器在文本模式中使用一种称为*正则表达式*的功能，允许你创建相当复杂的模式。

正则表达式允许你创建高级文本模式匹配公式，以匹配各种类型的数据。这些公式将一系列通配符字符、特殊字符和*固定文本*字符组合在一起，生成一个简洁的模式，几乎可以匹配任何文本情况。正则表达式是 shell 脚本编程中较难的部分之一，第 20 章“正则表达式”将详细介绍它们。

### 组合命令

如果你需要在一行上执行多个命令，请使用花括号将命令组合在一起。*sed* 编辑器处理列在地址行上的每个命令：

```
$ sed '{
> s/fox/toad/
> s/dog/cat/
> }' data1.txt
The quick brown fox jumps over the lazy dog.
The quick brown toad jumps over the lazy cat.
The quick brown fox jumps over the lazy dog.
The quick brown toad jumps over the lazy cat.
$
```

两个命令都仅针对地址进行处理。当然，你可以在组合命令之前指定一个地址范围：

```
$ sed '3,${
> s/brown/green/
> s/fox/toad/
> s/lazy/sleeping/
> }' data1.txt
```

