

# 更结构化的命令

```
echo "The last state we visited $test"
test=Connecticut
echo "Wait, now we're visiting $test"
$ ./testlb
The next state is Alabama
The next state is Alaska
The next state is Arizona
The next state is Arkansas
The next state is California
The next state is Colorado
The last state we visited was Colorado
Wait, now we're visiting Connecticut
$
```

$test 变量保留了它的值，并且允许我们像使用其他变量一样，在 `for` 命令循环中更改并使用该值。

# 在列表中读取复杂值

`for` 循环并不总是像看起来那么简单。在循环时，有时会遇到引起问题的数据。这里有一个导致 shell 脚本程序员遇到问题的经典示例：

```
$ cat badtestl
!/bin/bash
# 另一个不当使用 for 命令的示例

for test in I don't know if this'll work
do
  echo "word:$test"
done
$ ./badtestl
word:I
word:dont know if thisisll
word:work
$
```

哎呀，疼。shell 看到列表值中的单引号，并尝试使用它们来定义一个单一数据值，这真的在处理过程中搞了一团糟。

解决这个问题有两种方法：

- 使用转义字符（反斜杠 `\`）来转义单引号。
- 使用双引号来定义包含单引号的值。

这两个解决方案都不算完美，但其中一种确实有助于解决问题：

```
$ cat test2
!/bin/bash
# 另一个不当使用 for 命令的示例
```

257

# 第二部分 Shell 脚本基础

```
for test in I don\'t know if "this\'ll" work
do
  echo "word:$test"
done
$ ././test2
word:I
word:don't
word:know
word:if
word:this\'ll
word:work
$
```

在第一个问题值中，我添加了反斜杠字符来转义 `don't` 值中的单引号。在第二个问题值中，我用用双引号括起了 `this'll` 值。这两种方法都能很好地区分值。

你可能会遇到的另一个问题是多单词值。记住，`for` 循环假设每个值是由空格分隔的。如果你有包含空格的数据值，你就会遇到另一个问题：

```
$ cat badtest2
!/bin/bash
# 另一个不当使用命令的示例

for test in Nevada New Hampshire New Mexico New York North Carolina
do
  echo "Now going to $test"
done
$ ./badtest1
Now going to Nevada
Now going to New
Now going to Hampshire
Now going to New
Now going to Mexico
Now going to New
Now going to York
Now going to North
Now going to Carolina
$
```

哦，这不完全是我们想要的。因为命令使用空格分隔列表中的每个值。如果单个数据值中包含空格，你必须使用双引号来适应它们：

```
$ cat test3
!/bin/bash
# 正确定义值的示例
```

for test in "New Hampshire" "New Mexico" "New York"
do
  echo "Now going to $test"
done
$ ./test3
Now going to New Hampshire
Now going to New Mexico
Now going to New York
$
```

现在命令可以正确区分不同的值了。此外，注意当你对一个值使用双引号时，shell 不会将双引号作为值的一部分。

# 从变量读取列表

在 shell 脚本中经常发生的情况是：积累了一个存储在变量中的值列表，然后需要遍历该列表。你也可以使用 `for` 命令来实现此。

```
$ cat test4
!/bin/bash
# 保存列表的变量

list="Alabama Alaska Arizona Arkansas Colorado"
list=$list"Connecticut"

for state in $list
do
  echo "Have you ever visited $state?"
$ ./test4
Have you ever visited Alabama?
Have you ever visited Alaska?
Have you ever visited Arizona?
Have you ever visited Arkansas?
Have you ever visited Colorado?
Have you ever visited Connecticut?
$
```

$list 变量包含了用于迭代的标准文本值列表。注意代码还使用了另一个赋值语句向 $list 变量包含的列表添加（或拼接）项。这是向存储在变量中的现有字符串添加文本的常用方法。

# 从命令读取值

生成列表所需值的另一种方法是使用命令的输出。你使用反引号（`` ` ``）来执行任何产生输出的命令，然后在 `for` 中使用命令的输出：

```
$ cat test5
#!/bin/bash
# 从文件中读取值

file="states"

for state in `cat $file`
do
  echo "Visit beautiful $state"
done
$cat states
Alabama
Alaska
Arizona
Arkansas
Colorado
Connecticut
Delaware
Florida
Georgia
$ ./test5
Visit beautiful Alabama
Visit beautiful Alaska
Visit beautiful Arizona
Visit beautiful Arkansas
Visit beautiful Colorado
Visit beautiful Connecticut
Visit beautiful Delaware
Visit beautiful Florida
Visit beautiful Georgia$
```

这个示例使用了 `cat` 命令显示状态文件的内容。你会发现状态文件每个州单独占一行，而不是用空格分隔。`for` 将逐行遍历 `cat` 命令的输出，假设每个州都单独占一行。然而，这并没有解决数据中包含空格的问题。如果你列出一个包含空格的州，`for` 命令仍然会将每个州视为一个独立的值。这是有原因的，我们将在下一节中讨论。

> 注意：test5 代码直接使用文件名将其赋值给变量，而没有路径。这要求文件与脚本位于同一目录。如果不是这种情况，你需要使用完整路径（绝对或相对）来引用文件位置。

# 修改字段分隔符

这个问题的原因是特殊的环境变量 `IFS`，称为内部字段分隔符。`IFS` 环境变量定义了 bash shell 使用作为字段分隔符的字符列表。默认情况下，bash shell 将以下字符视为字段分隔符：

- 空格
- 制表符
- 换行符

如果 bash 在数据中看到这些任何字符，它就会认为你正在列表中开始一个新的数据字段。在处理可能包含空格的数据（如文件名）时，正如你在之前的脚本示例所示，这可能会非常麻烦。

要解决这个问题，你可以临时更改 shell 脚本中 `IFS` 环境变量的值，以限制 bash 识别为字段分隔符的字符。然而这种做法有点奇怪。例如，如果你想让 `IFS` 值只识别换行符，你需要这样做：

```
IFS='\n'
```

将此添加到脚本将告诉 bash 忽略数据值中的空格和制表符。将此应用于之前的脚本将得到以下结果：

```
$ cat test5b
!/bin/bash
# 从文件中读取值

file="states"

IFS='\n'
for state in `cat $file`
do
  echo "Visit beautiful $state"
done
$test5b
Visit beautiful Alabama
Visit beautiful Alaska
Visit beautiful Arizona
Visit beautiful Arkansas
Visit beautiful Colorado
Visit beautiful Connecticut
Visit beautiful Delaware
Visit beautiful Florida
Visit beautiful Georgia
Visit beautiful New York
Visit beautiful Hampshire
Visit beautiful Carolina
$
```

现在脚本可以使用包含空格的列表值。

> 注意：在编写长脚本时，可能会在某处更改 `IFS` 值，然后在其他地方忘记并假设它是默认值。一种安全的做法是在更改之前保存原始 `IFS` 值，并在完成后恢复它。

这种技术可以这样编写：

```
IFS.OLD=$IFS
IFS='\n'
<在代码中使用新的 IFS 值>
IFS=$IFS.OLD
```

这确保了 `IFS` 值返回默认值。

`IFS` 还有其他优秀的应用。假设你想遍历由冒号分隔的文件值（例如 `/etc/passwd` 文件）。你只需要将 `IFS` 值设置为冒号即可：

IFS=:

如果你想指定多个 `IFS` 字符，将它们在赋值行上连接在一起：

```
IFS='\n'::"
```

此赋值使用换行符、冒号、分号和双引号字符作为字段分隔符。使用 `IFS` 字符解析数据的方法没有限制。

# 使用通配符读取目录

最后，你可以使用 `for` 命令自动遍历目录中的文件。要实现此点，你必须在文件名或路径中使用通配符。这会强制 shell 使用文件通配（file globbing）。文件通配是产生匹配指定通配符的文件或路径名的的过程。

此功能对于处理目录中的文件非常有用，特别是当你不知道所有的文件名时：

```
$ cat test6
!/bin/bash
# 遍历目录中的所有文件

for file in /home/rich/test/*
do

if [ -d "$file" ]
then
techo "$file is a directory"
elif [ -f "$file" ]
then
```

