
用户小组会议将举行。

所有桌面用户都应该参加。

这个示例展示了与 `N` 命令配合使用的感叹号，以及美元符号 (`$`) 特殊地址。美元符号代表数据流中的最后一行，因此当 `sed` 编辑器到达最后一行时，它不会执行 `N` 命令。然而，对于所有其他行，它都会执行该命令。

使用这种技术，你可以反转文本行在文本流中出现的顺序（先显示最后一行，再显示第一行）。

`branch` 命令指定：如果行中出现了匹配的 `first`，则程序应跳转到标记为 `jump1` 的脚本行。如果分支模式不匹配，`sed` 编辑器继续执行脚本中的命令，包括分支标签之后的命令。（因此，所有三个替换命令都会在不匹配分支模式的行上处理）。

如果某行匹配分支模式，`sed` 编辑器将跳转到分支行。因此，只有最后一个替换命令会被执行

示例展示了跳转到 `sed` 脚本中后续的标签。你也可以跳转到脚本中较早出现的标签，从而创建一个循环效果：

```
$ echo "This, is, a, test, to, remove, commas." | sed -n '\n:start\ns,\s////p\nb start\n}'
```

This is, a, test, to, remove, commas.

This is a, test, to, remove, commas.

This is a test, to, remove, commas.

This is a test to remove, commas.

This is a test to remove, commas.

```
^C\n$
```

脚本的每次迭代从文本字符串中删除第一个出现的逗号并打印字符串。这个脚本有一个陷阱：它永远不会结束。这种情况创建了一个无限循环，不断寻找逗号，直到你通过发送 `Ctrl+K` 组合键信号手动停止它。

为了防止这个问题，你应该为 `branch` 命令指定一个地址模式进行查找。如果该模式不存在，`branch` 命令应该停止：

```
$ echo "This, is, a, test, to, remove, commas." | sed -n '\n:start\ns,\s////p\nb start\n}'
```

This is, a, test, to, remove, commas.

This is a, test, to, remove, commas.

This is a test, to, remove, commas.

This is a test to remove, commas.

This is a test to remove, commas.

现在，`branch` 命令只在行中存在逗号时才跳转。在最后一个逗号被删除后，`branch` 命令不再执行，允许脚本正常结束。

# 测试

与 `branch` 命令类似，`test` 命令 (`t`) 也用于修改 `sed` 编辑器脚本的流。`test` 命令不是根据地址跳转到标签，而是根据替换命令的结果跳转到标签。

如果替换命令成功匹配并替换了模式，`test` 命令将跳转到指定的标签。如果替换命令没有匹配指定的模式，则 `test` 命令不会跳转。

`test` 命令使用与 `branch` 命令相同的格式：

`[address]t [label]`

与 `branch` 命令一样，如果你没有指定标签，当测试成功，`sed` 将跳转到脚本的末尾。

`test` 命令提供了一种廉价的方法，对数据流中的文本执行基础的 `if-then` 语句。例如，如果你在进行了另一个替换后就不需要再次进行替换，`test` 命令可以提供帮助：

```
$ sed {
> s/first/matched/
> t
> s/This the/No match on/
>}' data.txt
No match on header line
This is the matched data line
No match on second data line
No match on last line
$
```

第一个替换命令首先查找模式文本。如果它匹配该行，则会替换文本，并且 `test` 命令将跳过第二个替换命令。如果第一个替换命令没有匹配模式，则处理第二个替换命令。

使用 `test` 命令，你可以清理之前使用 `branch` 命令尝试的循环：

```
$ echo "This, is, a, test, to, remove, commas." | sed -n {
> :start
> //1p
> t start
>}
```

This is a, a, test, to, remove, commas.

This is a, test, to, remove, commas.

This is a test, to, remove, commas.

This is a test to remove, commas.

This is a test to remove, commas.

This is a test to remove commas.

$
```

当没有更多可以执行的替换时，`test` 命令不会跳转，而是继续执行脚本的剩余部分。

# 通过模式进行替换

你已经看到了如何在 `sed` 命令中使用模式来替换数据流中的文本。然而，当使用通配符时，很难确切地知道哪些文本会匹配模式。

例如，假设你想在行中匹配到的单词周围加上双引号。如果你只是在模式中寻找一个单词来匹配，这非常简单：

```
$ echo "The cat sleeps in his hat." | sed 's/cat/"cat"/'
The "cat" sleeps in his hat.
```

但如果你在模式中使用通配符 (`.`) 来匹配多个单词呢？

```
$ echo "The cat sleeps in his hat." | sed 's/..*/"at"/g'
The ."at" sleeps in his "at".
```

替换字符串使用了点通配符来匹配任何字母后跟 `at` 的出现情况。遗憾的是，替换字符串并没有匹配匹配单词的通配符值。

# 使用安符号 (&)

`sed` 编辑器为你提供了一个解决方案。安符号 (`&`) 用于在替换命令中表示匹配的模式。无论什么文本匹配了定义的模式，你都可以使用安符号在替换模式中调用它。这允许你操作任何匹配定义模式的单词：

```
$ echo "The cat sleeps in his hat." | sed 's/..*/"&"/g'
The "cat" sleeps in his "hat".
```

# 替换单个单词

安符号检索匹配模式的整个字符串。有时，你只想检索字符串的一个子。你可以这样做，但有点复杂。`sed` 编辑器使用括号来分组。然后你使用反斜杠和数字来引用每个组件。`sed` 编辑器将第一个组件分配给 `\1`，第二个组件分配给 `\2`，依此类推。

## 注意

在替换命令中使用括号时，必须转义以识别为分组而非普通。这与转义其他字符相反。

看一个在 `sed` 编辑器中使用此功能的示例：

```
$ echo "The System Administrator manual" | sed '\n > \(System\)Administrator\\1/'
The System user
```

此替换命令使用一组括号将其标识为子。它在替换模式中使用 `\` 来调用。这并不有趣，但在处理通配符模式时非常有用。

如果你需要用一个单词替换短语，子是救星：

```
$ echo "That furry cat is pretty" | sed 's/furry\(.*)/1'
That cat is pretty
```

```
$ echo "That furry hat is pretty" | sed 's/furry\(.*)/1'
That hat is pretty
```

当需要在多个子之间插入文本时，此功能特别有用。这是一个使用子组件在长数字中插入逗号的脚本：

```
$ echo "1234567" | sed '\n >start\n s/\.*([0-9])\\\([0-9]{3})\\\\1,\2\n > t start\n }'
1,234,567
$
```

脚本将匹配模式分为两个组件：

```
.*[0-9]
[0-9]{3}
```
