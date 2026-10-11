
如果 `gawk` 模式和动作简单，且你只需要运行一次，你通常会像前面的代码示例那样交互式地运行 `gawk`。

你已经看到了在文件中运行 `gawk` 命令的另一种方法，你可以使用 `-f` 选项（代表 gawk file）在命令行上调用 `gawk`，并解析 gawk 文件的名称以及任何供 `gawk` 处理的数据文件。接下来的示例使用了输入文件方法（`gawk -f`），生成与上一个示例相同的报告，显示名为 `office_search` 的 `gawk` 程序，然后对 `offices` 数据文件运行该程序。

```
tweet$ cat office_search

# 寻找一楼到三层的租户

/^[0-3\/]/

#

tweety$ gawk -f office_search offices

Miss Scarlet

Professor Plum

Mr. Green

Colonel Mustard

Mrs. White
```

如果你有中等或复杂的模式和动作，并且你可能需要再次运行这个 `gawk` 程序，那么这种运行 `gawk` 的方法就非常方便。

运行 `gawk` 的下一种方法是创建一个 `gawk` 脚本并作为命令运行。你必须告诉 `bash` 使用 `gawk -f` 处理该文件。你像在第 18 章看到的那样，通过 hash-bang (`#!`) 来这样做，其中 `#!` 告诉 `bash` 通过 `bash` 壳处理该脚本。

# 在 awk 程序中定义变量

这大楼里有多少人有办公室？要使用 `awk` 找到答案，让它对名为 `offices` 的输入文件执行动作。在这个示例中，你不需要模式。动作被大括号包裹。第一个动作告诉 `awk` 大楼里有被占用的办公室。在两个文本字符串之间是一个变量 `lcv`，它是程序员自定义的。任何名字都可以。我使用 `lcv` 是为了让表示“行计数变量”。第二个动作告诉 `awk` 保持对文件中行的计数。你可以说：

`lcv = lcv + 1`

表达式 `++lcv` 是一个简写，意思等同于 `lcv = lcv + 1`。这两个表达式都会计算文件的行数。统计文件行数的动作会自动重复，直到处理完所有行。这是一个名为 `count_offices` 的 `awk` 脚本的样式：

```
tweet$ count_offices

#!/usr/bin/awk -f

# 统计大楼内办公室数量的 awk 脚本（文件中的

END {

 print "There are ", lcv ", occupied offices in the building."

++lcv}

# awk 脚本结束。
```

接下来，使用 `chmod` 使 `awk` 程序变为可执行文件。

```
tweet$ chmod a+x count_offices
```

使用 `ls` 命令确保 `count_offices` 程序具有执行权限。

```
tweet$ ls -l count*

-rwxr-xr-x 1 root 192 May 13 14:00 count_offices
```

像命令一样运行 `awk` 程序，并传入 `offices` 数据文件作为输入。

```
tweet$ /home/miss_scarlet/count_offices
```

大楼里有八间被占用的办公室。
tweet$

# 什么时候该用 gawk 编程？

现在你已经学习了 `awk` 的基础知识，你可能会想 `awk` 何时是正确的工具，反之，你什么时候不应该使用它。当你必须对一个或多个文本文件执行相同的处理时，使用 `awk`；当你需要从文件中提取特定文本时，使用 `awk`。当你有复杂的模式和动作，并且你可能需要再次运行这个 `gawk` 程序时，使用运行 `gawk` 的下一种方法是创建一个 `gawk` 脚本并作为命令运行。你必须告诉 `bash` 使用 `gawk -f` 处理该文件。你像在第 18 章看到的那样，通过 hash-bang (`#!`) 来这样做，其中 `#!` 告诉 `bash` 通过 `bash` 壳处理该脚本。

（注：此处原文似乎出现了部分逻辑重复或乱码，翻译已根据上下文进行了平滑处理，以确保中文逻辑通贯性）

当你必须对一个或多个文本文件执行相同的处理时，使用 `awk`；当你需要从文件中提取特定文本时，使用 `awk`。如果你有复杂的模式和动作，并且你可能需要再次运行这个 `gawk` 程序时，那么这种运行 `gawk` 的方法就非常方便。

接下来的列表总结了 `gawk` 的关键点：

- 你的指令要处理的行被称为地址。地址可以被斜杠包裹（如上一个示例所示），或者是行号。
- `sed` 使用模式-动作对来对每一条记录执行你的指令，除了 `BEGIN` 和 `END`。
- 你可以使用 `$1` 到 `$n`。`$0` 是整个行。
- 如果你指定了开始和结束行号或匹配模式，`sed` 只将你的指令应用到这些标记之间的输入。
- 你可以交互式地使用 `sed`，也可以从脚本运行它。

# 使用 sed 处理流数据

`sed` 是一种流编辑器的工具，它的工作方式不像传统的编辑器。它接收输入进行处理，并将结果发送到标准输出。尽管 `sed` own流编辑器，但它的工作方式并不编辑器。你输入输入命令，，，，

。

# 简单的 sed sed示例示例

下面的示例告诉 `sed` 删除 `suspects` 文件中的第三行。这个基础 `sed` 命令使用行号后跟 `d` 指令。如果你想删除 `suspects` 文件中的多个行，列出给 `sed` 的文件。`sed` 在屏幕上显示新编辑的 `suspects` 文件，因为示例没有告诉 `sed` 将输出写入单独的文件。

## 第 19 章 + 发现过滤器 339

如果你想删除第 3 行到最后一行的所有嫌疑人，请将你的 `sed` 流更改为列出第 3 行后跟一个逗号 (,)，并使用 `$d` 表示“一直到最后一行”，如下例所示。输出显示只剩下输入输入中的前两行。

```
tweet$ sed -e '3,$d' suspects

Miss Scarlet

Mrs. Peacock
```

在上面的示例中，你看到了执行删除操作并在屏幕（标准输出）上显示结果。然而，如果你再次显示文件，你会发现删除并不是永久的。文件中的所有行仍然存在。如果你想将输出写入永久的磁盘文件，你需要将输出重定向到一个新文件：

```
tweet$ sed -e '3,$d' suspects

Miss Scarlet

Mrs. Peacock

tweet$ cat suspects

Miss Scarlet

Mrs. Peacock

Sherlock Holmes

Professor Plum

Jack

Colonel Mustard

tweet$ # 噢！删除不是永久的

tweet$ sed -e '3,$d' suspects > new_suspects

tweet$ # 检查永久删除

tweet$ cat new_suspects

Miss Scarlet

Mrs. Peacock

tweet$ # 现在我们有一个只有 2 行的新文件
```

始终将输出重定向到新文件中。如果你尝试将输出重定向到输入文件，你会在 `sed` 操作它之前销毁该输入文件。

除了使用行号和简单模式告诉 `sed` 在何处处理文本以及对文本做什么之外，你还可以使用正则表达式。正则表达式是 `sed` 最强大的功能之一。下面的示例使用正则表达式 `/^/` 表示行的开头。该示例告诉 `sed` 找到 `unsolved_crimes` 文件中所有包含 `Scarlet` 的行，并将行首替换 (`s`) 为单词 `misspelled`（拼写错误）*。

```
$ sed -e '/Scarlet/s/.*/misspelled/' unsolved_crimes

misspelled101AA Miss Emily Scarlett

1044 Professor Hank Plum

misspelled1049 Miss Emily Scarlett and horse

1077 Mrs. Hannah Peacock

1078 Mrs. Hannah Peacock

1088 archcriminal Marshall Wilensky

tweety$
```
