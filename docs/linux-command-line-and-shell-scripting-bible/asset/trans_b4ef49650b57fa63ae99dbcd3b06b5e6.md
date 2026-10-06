

> j' data2
This is the header test.
This is the starting data line.
This is the second data test.
This is the last test.
$

第一个替换命令首先查找模式文本。如果它匹配行中的模式，则替换该文本，并且测试命令将跳过后续的替换命令。如果第一个替换命令没有匹配模式，则处理第二个替换命令。

使用 test 命令，你可以清理掉之前尝试使用分支命令编写的循环：

```
$ echo "This, is, a, test, to, remove, commas." | sed -n '(
:start
s/,//lp
t test
)'
This is, a, test, to, remove, commas.
This is a, test, to, remove, commas.
This is a test, to, remove, commas.
This is a test to remove, commas.
This is a test to remove, commas.
This is a test to remove commas.
$
```

当没有更多替换需要执行时，test 命令不会进行分支，而是继续执行脚本的剩余部分。

## 模式替换

你已经看到了如何在 sed 命令中使用模式来替换数据流中的文本。然而，问题在于，当使用通配符字符时，很难确切知道哪些文本会匹配模式。

例如，假设你想在行中匹配到的单词周围加上双引号。如果你只是在模式中寻找一个匹配的单词，这非常简单：

```
$ echo "The cat sleeps in his hat." | sed 's/cat/"cat"/'
The "cat" sleeps in his hat.
$
```

但如果你在模式中使用通配符字符来匹配多个单词：

```
$ echo "The cat sleeps in his hat." | sed 's/.at/".at"/g'
The ".at" sleeps in his ".at".
$
```

## 第 III 部分 高级 Shell 脚本编写

额，这并不起作用。替换字符串使用了点 `.` 通配符来匹配任何跟在 `a` 后面的字母。遗憾的是，替换字符串并不匹配匹配单词的通配符值。

## 安培符号 (&)

sed 编辑器为你提供了一个解决方案。安培符号 (&) 用于表示替换命令中的匹配模式。无论什么文本匹配了定义的模式，你都可以使用安培符号在替换模式中调回它。这让你能够处理任何匹配定义模式的单词。

```
$ echo "The cat sleeps in his hat." | sed '/s/.at/"&/g'
The "cat" sleeps in his "hat"
$
```

当模式匹配 cat 时，cat 出现在替换后的单词中。当匹配 hat 时，hat 出现在替换后的单词中。

## 替换单个单词

安培符号检索了你在替换命令中指定的匹配模式的整个字符串。有时你可能只想检索字符串的子集。你也可以这样做，但这有点复杂。

sed 编辑器使用括号来在替换模式中定义子字符串组件。然后，你可以使用替换模式中的特殊字符来引用每个子字符串。替换字符由反斜杠和数字组成。数字表示子字符串组件的位置。sed 编辑器将第一个组件分配为 \1，第二个组件分配为 \2，依此类推。

![](img/adcbcf1053b52dbf22f3aa187738232f_519_0.png)

当你在替换命令中使用括号时，你必须使用转义字符将其识别为分组字符而不是普通括号。这与转义其他特殊字符时的逻辑恰相反。

看一个 sed 编辑器脚本中此特功能的示例：

```
$ echo "The System Administrator manual" | sed 's/\(System\)/\1 User/'
The System User manual
$
```

此替换命令在单词 system 周围使用了一组括号，将其识别为子字符串组件。它随后在替换模式中使用 \1 来调回第一个识别出的组件。这并不特别有趣，但在处理通配符模式时它确实非常有用。

如果你需要将一个短语替换为单个单词，而该单词是该短语的子集，但该子集恰好使用了通配符字符；那么使用子字符串组件就是救命稻星：

```
$ echo "That furry cat is pretty" | sed 's/furry\.(at)/\1'
That cat is pretty
$ echo "That furry hat is pretty" | sed 's/furry\.(at)/\1'
That hat is pretty
```

在这种情况下，你不能使用安培符号，因为它会替换匹配的模式。子字符串组件提供了答案，允许你选择模式的哪部分作为替换模式。

当你需要在两个或多个子字符串组件之间插入文本时，这个功能可能特别有用。这里有一个使用子字符串组件在长数字中插入逗号的脚本：

```
$ echo "1234567" | sed ' {
:start
s/\(.*[0-9])\([0-9]\(3\)\)/\1,\2/
t start
b;
'
1,234,567
```

脚本将模式匹配为两个组件：

```
.*[0-9]
[0-9]{3}
```

该模式查找两个子字符串。第一个子字符串是任意数量的字符，以数字结尾。第二个子字符串是一系列三个数字（参见第 17 章，关于如何在正则表达式中使用大括号的信息）。如果在文本中找到此模式，替换文本会在两个组件之间放置逗号，每个组件由其组件位置标识。脚本使用 test 命令遍历数字，直到所有逗号都放置完毕。

## 在脚本中使用 sed

现在你已经了解了 sed 编辑器的各个部分，是时候将它们整合起来并用在你的 shell 脚本中了。这一部分演示了在 shell 脚本中使用 sed 编辑器时应该了解的一些特性。

## 使用包装器 (Wrappers)

你可能已经注意到，实现 sed 编辑器脚本可能是麻烦的，特别是当脚本很长时。与其每次使用时都重输整个脚本，你可以将 sed 编辑器命令放在 shell 包装器中。包装器充当 sed 编辑器脚本和命令行之间的中间人。

一旦进入 shell 脚本，你就可以使用普通的 shell 变量和参数来处理你的 sed 编辑器脚本。这里有一个使用命令行参数变量作为 sed 脚本输入的示例：

```
$ cat reverse
#!/bin/bash
# 用于反转行的 shell 包装器

sed -n '
1G
h
$p
' "$1"
$
```

```
$ ./reverse data2
This is the last line.

This is the second data line.

This is the first data line.

This is the header line.
$
```

## 重定向 sed 输出

默认情况下，sed 编辑器将脚本结果输出到 stdout。你可以在 shell 脚本中使用所有的重定向方法。

你可以使用引号将 sed 命令的输出重定向到变量中供以后使用。这里有一个使用 sed 脚本为数值计算结果添加逗号的示例：

```
$ cat fact
#!/bin/bash
# 为阶号答案添加逗号

factorial=1
counter=-1
number=$1

while [ $counter -le $number ]
do
factorial=$[ $factorial * $counter ]
counter=$[ $counter + 1 ]
done

result=`echo $factorial | sed '(
:start
s/.*([0-9])\([0-9]\(3\)\)/\1,\2/
t'
'

echo "The result is $result"
./fact 20
The result is 2,432,902,008,176,640,000
$
```

## 创建 sed 工具

正如你在本章之前有很多酷的数据格式化操作。本节展示了几个执行常用数据处理函数的 sed 编辑器脚本。

### 行间倍距

作为开始，看一个在文本文件行之间插入空行的简单 sed 脚本：

```
$ sed 'G' data2
This is the header line.

This is the first data line.

This is the second data line.

This is the last line.

```
$
```

这非常简单！这个技巧的关键在于保持空间的默认值。记住，`G` 命令只是将保持空间的内容追加到当前模式空间的内容之后。当你启动 sed 编辑器时，保持空间包含一个空行。通过将它追加到现有行，你就在现有行之后创建了一个空行。

