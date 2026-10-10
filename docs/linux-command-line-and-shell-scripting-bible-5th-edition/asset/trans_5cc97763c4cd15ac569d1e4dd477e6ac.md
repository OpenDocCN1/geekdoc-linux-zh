

# **第三部分：高级 Shell 脚本编程**

当您需要在一个或多个子字符串组件之间插入文本时，此功能特别有用。下面是一个使用子字符串组件在长数字中插入逗号的脚本示例：

```bash
$ echo "1234567" | sed '{
> \start
> s/\(.*[0-9])\([0-9]\{3}\)/\1,\2/
> t start}'
1,234,567
$
```

该脚本将匹配模式分为两个部分：

```text
.*[0-9]
[0-9]\{3}
```

此模式查找两个子字符串。第一个子字符串是任何以数字结尾的字符序列。第二个子字符串是一组三个数字（有关如何在正则表达式中使用花括号的信息，请参见第 20 章“正则表达式”）。如果在文本中找到该模式，替换文本会在两个部分之间插入一个逗号，每个部分都由其组件位置标识。脚本使用 `test (t)` 命令迭代处理数字，直到所有逗号都放到正确的位置为止。

## 在脚本中使用 sed 命令

既然您已经见过 `sed` 编辑器的各个部分，是时候将它们组合起来并在您的 Shell 脚本中使用它们了。本节演示了一些在使用 `sed` 编辑器于 Bash Shell 脚本中时应了解的功能。

### 使用封装器

您可能注意到，尝试实现一个 `sed` 编辑器脚本可能很繁琐，特别是当脚本较长时。无需每次使用都重新输入整个脚本，您可以将 `sed` 编辑器命令放入一个 Shell 脚本*封装器*中。该封装器充当 `sed` 编辑器脚本和命令行之间的中间人。第 19 章曾将一个名为 `ChangeScriptShell.sh` 的 Shell 脚本封装器作为实用示例使用。

进入 Shell 脚本后，您可以将普通的 Shell 变量和参数用于您的 `sed` 编辑器脚本。以下是一个使用命令行参数变量作为 `sed` 脚本输入的例子：

```bash
$ cat reverse.sh
#!/bin/bash
# Shell wrapper for sed editor script
# to reverse text file lines.
#
sed -n '{1!G; h; $p}' $1
#
exit
$
```

名为 `reverse.sh` 的 Shell 脚本使用 `sed` 编辑器脚本来反转数据流中的文本行。它使用 `$1` Shell 参数从命令行获取第一个参数，该参数应为要反转的文件名：

```bash
$ cat data2.txt
Header Line
First Data Line
Second Data Line
End of Data Lines
$
$ ./reverse.sh data2.txt
End of Data Lines
Second Data Line
First Data Line
Header Line
$
```

现在，您可以轻松地在任何文件上使用 `sed` 编辑器脚本，而无需不断重新输入整个 `sed` 命令行。

### 重定向 `sed` 输出

默认情况下，`sed` 编辑器将脚本的结果输出到 STDOUT。您可以在 Shell 脚本中使用所有标准方法来重定向 `sed` 编辑器的输出。

您可以使用美元符号/括号 `$( )` 将 `sed` 编辑器命令的输出重定向到变量中，以便在脚本稍后使用。以下是一个使用 `sed` 脚本为数值计算结果添加逗号的示例：

```bash
$ cat fact.sh
#!/bin/bash
# Shell wrapper for sed editor script
# to calculate a factorial, and
# format the result with commas.
#
factorial=1
counter=1
number=$1
#
while [ $counter -le $number ]
do
    factorial=$( $factorial * $counter )
    counter=$( $counter + 1 )
done
#
result=$(echo $factorial |
sed '{
:start
s/\(.\{0-9\}\)\([0-9]\{3\}\)/\1,\2/
t start
}'
#
echo "The result is $result"
#
exit
$
$ ./fact.sh 20
The result is 2,432,902,008,176,640,000
$
```

在使用普通的阶乘计算段落后，该脚本的结果被用作 *sed* 编辑器脚本的输入，该脚本添加了逗号。然后该值在 *echo* 语句中用于生成结果。现在，将那个长的 *sed* 脚本包含在 Bash Shell 脚本中是多么方便，您可以再次使用它而无需重新输入所有 *sed* 命令！

## 创建 sed 实用工具

正如在本章前面提供的简短示例中您所见，您可以使用 *sed* 编辑器执行许多很酷的数据格式化操作。本节介绍了一些用于执行常见数据处理功能的知名且方便的 *sed* 编辑器脚本。

### 使用双行进行间距处理

首先，看看一个简单的 *sed* 脚本，用于在文本文件的行之间插入空行：

```bash
$ sed 'G' data2.txt
Header Line

First Data Line

Second Data Line

End of Data Lines

$
```

这非常简单！这一技巧的关键在于保持空间（hold space）的默认值。请记住，*G* 命令只是将保持空间的内容追加到当前模式空间的内容中。当您启动 *sed* 编辑器时，保持空间包含一个空行。通过将其追加到现有行，您在现有行之后创建了一个空行。

您可能注意到，此脚本还会在数据流的最后一行添加一个空行，从而在文件末尾产生一个空行。如果您想消除这种情况，可以使用*否定符号*和最后一行符号，以确保脚本不会在数据流的最后一行添加空行：

```bash
$ sed '$!G' data2.txt
Header Line
First Data Line
Second Data Line
End of Data Lines
$
```

现在看起来好多了。只要该行不是最后一行，`G` 命令就会追加保持空间的内容。当 `sed` 编辑器到达最后一行时，它会跳过 `G` 命令。

### 处理可能包含空白的文件

为了将双倍间距进一步扩展，如果文本文件已经有一些空行，但您希望双倍间距所有行怎么办？如果使用之前的脚本，您会发现有些区域空行太多，因为每个现有的空行都被加倍了：

```bash
$ cat data6.txt
Line one.
Line two.

Line three.
Line four.
$
```

```bash
$ sed 'gIG' data6.txt
Line one.

Line two.


Line three.
Line four.
$
```

现在，在原本有一个空行的地方出现了三个空行。解决此问题的方法是首先删除数据流中的所有空行，然后使用 `G` 命令在所有行之后插入新的空行。要删除现有的空行，您只需使用匹配空行的模式的 `d` 命令：

```text
/^$/d
```

此模式使用行开始标记（脱字符）和行结束标记（美元符号）。将此模式添加到脚本中即可产生所需结果：

```bash
$ sed '/^$/d ; $!G' data6.txt
Line one.

Line two.

Line three.

Line four.
$
完美！它就像期望的那样工作。
```

## 为文件行编号

第 19 章向您展示了如何使用等号来显示数据流中行的行号：

```bash
$ sed '=' data2.txt
1
Header Line
2
First Data Line
3
Second Data Line
4
End of Data Lines
$
```

这可能有点难以阅读，因为行号位于数据流中实际行的上方。更好的解决方案是将行号放在与文本相同的行上。

既然您已经看到了如何使用 N 命令组合行，在 sed 编辑器脚本中利用这些信息应该不会太难。然而，这个实用工具的技巧在于，您不能在同一脚本中组合这两个命令。

在获得等号命令的输出后，您可以将输出管道传输到另一个使用 N 命令组合两行的 sed 编辑器脚本。您还需要使用替换 (s) 命令将换行符替换为空格或 Tab 字符。以下是最终解决方案的样子：

```bash
$ sed '=' data2.txt | sed 'N; s/\n/ '
1 Header Line
2 First Data Line
3 Second Data Line
4 End of Data Lines
$
```

现在看起来好多了。当您在处理需要查看错误消息中使用的行号的程序时，这是一个很棒的小实用工具。

还有一些 Bash Shell 命令也可以添加行号。但是，它们会添加一些额外的（且可能不需要的）间距：

```bash
$ nl data2.txt
1 Header Line
```

