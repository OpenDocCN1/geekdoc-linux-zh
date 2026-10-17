
### 取反命令

第 19 章表明，`sed` 编辑器将命令应用于数据流中的每一行文本，或者由单个地址或地址范围特别指示的行。你还可以配置命令不应用于数据流中的特定地址或地址范围。

**第三部分：高级 Shell 脚本编程**

感叹号 (`!`) 命令用于取反命令。这意味着在命令通常会激活的情况下，它不会激活。下面是一个演示此功能的示例：

```bash
$ sed - '!^Header/'p' data2.txt
First Data Line
Second Data Line
End of Data Lines
$
```

普通的 `p` 命令本应只打印 `data42` 文件中含有 `Header` 一词的行。通过添加感叹号，发生了相反的情况——除了含有 `Header` 一词的那一行，文件中的所有行都被打印出来。

在几种应用程序中使用感叹号非常有用。回想一下本章早些时候，“导航下一个命令”部分展示了一种情况，其中 `sed` 编辑器命令不会操作数据流中的最后一行文本，因为它后面没有行。你可以使用感叹号来修复该问题：

```bash
$ cat data4.txt
On Tuesday, the Linux System
Admin group meeting will be held.
All System Admins should attend.
$
$ sed '$N;
> s/System\\nAdmin/DevOps\\nEngineer/
> s/System Admin/DevOps Engineer/
> ' data4.txt
On Tuesday, the Linux DevOps
Engineer group meeting will be held.
All System Admins should attend.
$
$ sed 'S!N;
> s/System\\nAdmin/DevOps\\nEngineer/
> s/System\\nAdmin/DevOps\\nEngineer/
> ' data4.txt
On Tuesday, the Linux DevOps
Engineer group meeting will be held.
All System Engineers should attend.
$
```

此示例展示了将感叹号与 `N` 命令以及美元符号 (`$`) 特殊地址一起使用。美元符号代表数据流中的最后一行文本，因此当 `sed` 编辑器到达最后一行时，它不会执行 `N` 命令。然而，对于所有其他行，它会执行该命令。

使用这种技术，你可以反转数据流中行的顺序。要反转文本流中行的显示顺序（先显示最后一行，最后显示第一行），你需要使用保留空间做一些巧妙的操作。

为了完成这一点，使用 `sed` 执行以下操作：
- 1. 将一行文本放入模式空间。
- 2. 将行从模式空间复制到保留空间。
- 3. 将下一行文本放入模式空间。
- 4. 将保留空间追加到模式空间。
- 5. 将模式空间中的所有副本复制到保留空间。
- 6. 重复步骤 3 到 5，直到将所有行按相反顺序放入保留空间。
- 7. 检索并打印行。

图 21.1 更详细地展示了其外观。

**图 21.1**

使用保留空间反转文本文件顺序。

![](img/0798d50a0e5dbf1265fbda3832b3e015_542_0.png)

使用此技术时，你不希望在处理行时打印它们。这意味着对 `sed` 使用 `-n` 命令行选项。接下来要确定的是如何追加保留空间文本到模式空间文本。这是通过使用 `G` 命令完成的。唯一的问题是你不想将保留空间追加到处理的第一行文本。通过使用感叹号命令可以轻松解决这个问题：

```
1!G
```

下一步是将新的模式空间（包含追加的反转行的文本行）复制到保留空间。这很简单；只需使用 `h` 命令即可。

当整个数据流按相反顺序位于模式空间时，你只需打印结果。当你到达数据流中的最后一行时，你就知道整个数据流都在模式空间中。要打印结果，只需使用以下命令：

```
$p
```

这些是创建行反转 `sed` 编辑器脚本所需的组件。现在你可以尝试测试运行：

```bash
$ cat data2.txt
Header Line
First Data Line
Second Data Line
End of Data Lines
$
$ sed -n '{1G; h; $p}' data2.txt
End of Data Lines
Second Data Line
First Data Line
Header Line
$
```

`sed` 编辑器脚本按预期执行。脚本的输出反转了文本文件中的原始行。这演示了在 `sed` 脚本中使用保留空间的功能。它提供了一种简单的方式来操作脚本输出中行的顺序。

> **注意**
> 如果你想知道的话，Bash shell 命令可以执行反转文本文件的功能。`tac` 命令以相反顺序显示文本文件。你可能注意到这个命令巧妙的名字，因为它执行 `cat` 命令的相反功能。

### 改变流程

通常，`sed` 编辑器从顶部开始处理命令，并向脚本的末尾推进（例外是 `D` 命令，它强制 `sed` 编辑器返回脚本顶部而不读取新的文本行）。`sed` 编辑器提供了一种改变命令脚本流程的方法，产生类似于结构化编程环境的结果。

#### 分支

在上一节中，你看到了叹号命令如何用于否定某行文本上命令的效果。`sed` 编辑器提供了一种基于地址、地址模式或地址范围来否定整个命令段的方法。这允许你仅对数据流中的特定子集执行一组命令。

以下是分支（`b`）命令的格式：

```
[address]b [label]
```

地址参数决定了哪一行或多行数据触发分支（`b`）命令。标签参数定义了分支跳转到的脚本位置。如果未提供标签参数，分支（`b`）命令将跳过触发分支的那一行或多行数据，并继续处理其他文本行。

下面是一个使用分支命令的地址参数但未使用标签的示例：

```bash
$ cat data2.txt
Header Line
First Data Line
Second Data Line
End of Data Lines
$ sed '{2,3b; s/Line/Replacement/}' data2.txt
Header Replacement
First Data Replacement
Second Data Replacement
End of Data Replacements
$
```

分支（`b`）命令跳过了数据流中第二行和第三行的替换命令。

除了跳转到脚本末尾，你还可以定义一个标签，为分支命令提供一个跳转位置。标签以冒号开头，长度最多为七个字符：

```
:label2
```

要指定标签，只需在 `b` 命令后添加即可。使用标签允许你为匹配分支地址的数据提供替代命令，同时仍使用脚本中的原始命令处理其他文本行：

```bash
$ sed '{/First/b jmp1; s/Line/Replacement/; :jmp1 s/Line/Jump Replacement/}' data2.txt
Header Replacement
First Data Jump Replacement
Second Data Replacement
End of Data Replacements
```

分支（`b`）命令指定，如果匹配文本 `First` 出现在行中，程序应跳转到标记为 `jmp1` 的脚本行。如果分支命令的地址不匹配，`sed` 编辑器将继续处理脚本中的命令，包括分支标签 `jmp1` 之后的命令。（因此，在不匹配分支地址的行上，两个替换命令都会被处理。）

如果某一行匹配分支地址，`sed` 编辑器将分支到带有标签的行，即 `jmp1`。因此，对于匹配分支地址的行，仅执行最后一个替换命令。

该示例展示了分支到 `sed` 脚本中更下方的标签。你也可以分支到脚本中较早出现的标签，从而产生循环效果：

```bash
$ echo "This, is, a, test, to, remove, commas." |
> sed -n '{
> :start
> s/,//
> 1p
> b start
> }'
This is a, test, to, remove, commas.
This is a test, to, remove, commas.
This is a test to, remove, commas.
This is a test to remove, commas.
This is a test to remove commas.
^C
$
```

每次脚本迭代都会从字符串中移除第一个出现的逗号并打印该字符串。这个脚本有一个陷阱——它永远不会结束。这种情况创建了一个无限循环，持续查找逗号，直到你通过发送 `Ctrl+C` 按键组合的信号手动停止它。

为防止此问题，请为分支（`b`）命令指定一个地址模式。如果模式中不存在逗号，分支将停止：
