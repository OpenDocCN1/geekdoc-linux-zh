
此替换命令在 *Guide to* 周围使用了一组括号，将其标识为一个子字符串组件。然后，它在替换模式中使用 `\1` 来调用第一个标识的组件。这本身并不令人兴奋，但在处理通配符模式时，它可能非常有用。

假设你需要用一个单词替换一个短语，而这个单词恰好是该短语的一个子字符串，但该子字符串恰好使用了通配符字符。在这种情况下，使用子字符串组件是救星：

```bash
$ echo "That furry cat is pretty." | \
> sed 's/furry \(.at\)/\1/'
That cat is pretty.
$
$ echo "That furry hat is pretty." | \
> sed 's/furry \(.at\)/\1/'
That hat is pretty.
$
```

在这种情况下，你不能使用 `&` 符号，因为它会替换整个匹配模式。子字符串组件提供了答案，允许你选择模式中的哪一部分作为替换模式。

当需要在一到多个子字符串组件之间插入文本时，此功能可能特别有用。下面是一个使用子字符串组件在长数字中插入逗号的脚本：

```bash
$ echo "1234567" | sed '{ \
> :start \
> s/^(.*[0-9])\([0-9]\{3\}\)/\1,\2/2 \
> t start }'
1,234,567
$
```

脚本将匹配模式分为两个组件：

- `.*[0-9]`
- `[0-9]{3}`

此模式查找两个子字符串。第一个子字符串是以数字结尾的任意数量的字符。第二个子字符串是三个数字的序列（有关如何在正则表达式中使用花括号的信息，请参阅第 20 章“正则表达式”）。如果在文本中找到此模式，替换文本会在两个组件之间插入一个逗号，每个组件都通过其位置进行标识。脚本使用测试（`t`）命令遍历数字，直到所有逗号都放置到正确位置。

### 在脚本中使用 sed 命令

既然你已经了解了 `sed` 编辑器的各个部分，现在是时候将它们组合起来并在你的 shell 脚本中使用了。本节演示了在使用 Bash shell 脚本中的 `sed` 编辑器时你应该知道的一些功能。

#### 使用封装器（Wrapper）

你可能已经注意到，尝试实现 `sed` 编辑器脚本可能很麻烦，特别是当脚本很长时。与其每次想要使用脚本时都要重新输入整个脚本，不如将 `sed` 编辑器命令放在 shell 脚本*封装器*中。封装器充当 `sed` 编辑器脚本和命令行之间的中介。一个 shell 脚本封装器 `ChangeScriptShell.sh` 曾在**第 19 章**中作为一个实用示例被使用。

一旦进入 shell 脚本，你就可以在 `sed` 编辑器脚本中使用普通的 shell 变量和参数。下面是一个使用命令行参数变量作为 `sed` 脚本输入示例：

```bash
$ cat reverse.sh
#!/bin/bash
# Shell wrapper for sed editor script
# to reverse test file lines.
#
sed -n '{1!G; h; $p}' $1
#
exit
$
```

名为 `reverse.sh` 的 shell 脚本使用 `sed` 编辑器脚本来反转数据流中的文本行。它使用 `$1` shell 参数从命令行检索第一个参数，这应该是反转文件的名称：

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

现在，你可以轻松地在任何文件上使用 `sed` 编辑器脚本，而无需不断重新输入整个 `sed` 命令行。

#### 重定向 sed 输出

默认情况下，`sed` 编辑器将脚本的结果输出到 STDOUT（标准输出）。你可以在 shell 脚本中使用所有标准方法来重定向 `sed` 编辑器的输出。

你可以使用美元符号/括号，`$()`，将 `sed` 编辑器命令的输出重定向到一个变量，以便在脚本后面使用。下面是使用 `sed` 脚本为数字计算结果添加逗号的示例：

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
while [ $counter -le $number ]; do
    factorial=$[ $factorial * $counter ]
    counter=$[ $counter + 1 ]
done
#
result=$(echo $factorial | sed '{
:start
s/^\(.\*[0-9]\)\([0-9]\{3\}\)/\1,\2/
t start
}')
# echo "The result is $result"
#
exit
$ ./fact.sh 20
$ The result is 2,432,902,008,176,640,000
```

在使用普通的阶乘计算脚本之后，该脚本的结果被用作 `sed` 编辑器脚本的输入，该脚本添加逗号。然后，这个值在 `echo` 语句中用于产生结果。而且，在 Bash shell 脚本中包含这么长的 `sed` 脚本真是太好了，这样你可以再次使用它而无需再次输入所有 `sed` 命令！

#### 创建 sed 实用工具

正如本章前面展示的简短示例所示，你可以使用 `sed` 编辑器完成许多很酷的数据格式处理任务。本节展示了一些用于执行常见数据处理功能的方便的、众所周知的 `sed` 编辑器脚本。

##### 使用双行间距

首先，看看一个简单的 `sed` 脚本，用于在文本文件的行之间插入一个空行：

```bash
$ sed 'G' data2.txt
Header Line

First Data Line

Second Data Line

End of Data Lines

$
```

这很简单！这个技巧的关键在于保持空间（hold space）的默认值。请记住，`g` 命令只是将保持空间的内容追加到当前模式空间的内容中。当你启动 `sed` 编辑器时，保持空间包含一个空行。通过将其追加到现有行，你在现有行之后创建了一个空行。

你可能已经注意到，此脚本还会在数据流的最后一行添加一个空行，从而在文件末尾产生一个空行。如果你想消除这一点，你可以使用否定符号和最后一行符号，以确保脚本不会在数据流的最后一行添加空行：

```bash
$ sed '$!G' data2.txt
Header Line
First Data Line
Second Data Line
End of Data Lines
$
```

现在看起来好多了。只要该行不是最后一行，`g` 命令就会追加保持空间的内容。当 `sed` 编辑器到达最后一行时，它会跳过 `g` 命令。

##### 为可能包含空行的文件设置间距

为了将双行间距进一步向前推进，如果文本文件已经有几个空行，但你想让所有行都双行间距，该怎么办？如果你使用前面的脚本，你会得到一些空行过多的区域，因为每个现有的空行都被加倍了：

```bash
$ cat data6.txt
Line one.
Line two.
Line three.
Line four.
$
$ sed '$!G' data6.txt
Line one.
Line two.
Line three.
Line four.
$
```

现在我们在原来的空行位置有了三个空行。解决这个问题的方法是首先删除任何空行

从数据流中获取，然后使用 `g` 命令在所有行的后面插入新的空行。要删除现有的空行，我们只需要使用与匹配空行的模式一起配合的 `d` 命令：

```
/^$/d
```

该模式使用了行首标签（脱字符）和行尾标签（美元符号）。将此模式添加到脚本中即可产生期望的结果：

```
$ sed '/^$/d ; $!G' data6.txt
Line one.
Line two.
Line three.
Line four.
$
```

完美！它完全按预期工作。

##### 为文件中的行编号

第 19 章向你展示了如何使用等号显示数据流中各行的行号：

```
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

这在阅读上可能有点别扭，因为行号位于数据流中实际行的上方。一个更好的解决方案是将行号放在与文本相同的行上。

既然你已经看到了如何使用 `n` 命令组合行，那么利用该信息在 `sed` 编辑器脚本中应该不会太难。然而，这个实用技巧的窍门在于，你不能将这两个命令放在同一个脚本中。
