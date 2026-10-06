
要移动到下一个文件，按 `:`（冒号）然后按 `n`。`less` 命令显示下一个文件的第一屏，屏幕底部的提示符显示的是哪个文件：

CivDis.txt (file 2 of 12)

如果你在查看一组文件时按 `:`（冒号）然后按 `e`，提示符变为 Examine（检查）；你可以输入文件名。文件名补全在这里有效；你可以输入文件名的几个字母并按 Tab 键补全。输入文件名或用 Tab 键补全后，按回车进入。你可以这样查看组中的任何文件，无论它是在组中当前位置之前还是之后。

`less` 命令提供了系列键盘快捷键或键绑定来导航文件。表 8.1：LESS 的键盘快捷键

| 快捷键 | 功能 |
| :--- | :--- |
| Space | 向前移动 |
| Return | 向前移动 |
| d | 向后移动 |
| b | 向后移动 |
| u | 向后移动 |
| y | 向后移动 |
| G | 移动到开头 |
| $ | 移动到末尾 |
| :n | 显示下一个出现处 |
| :e | 检查文件 |
| :p | 显示上一个出现处 |
| / | 向前搜索 |
| ? | 向后搜索 |
| N | 向前搜索 |
| n | 向后搜索 |
| q | 退出 |
| h | 帮助 |

## 动手实践：使用 LESS 查看 Macintosh 文本文件

## 第 9 章

### 编辑文本

OS X 的 Unix 版本包含许多处理文本的程序。在第 8 章“查看文件”中，我们看到了如何查看文件，以及特定程序如何让你翻页。还有另一组程序用于编辑和更改文本。无论你是想编辑自己创建的文本文件，还是编辑配置文件来更改工作工具，都是至关重要的。在本章中，我将向你展示如何对文本文件操作。我将介绍一些执行有限但价值任务的简单工具，例如数单词。我将查看从命令行运行的编辑器。

但我不会对这些命令进行过多详细说明。对于简单命令——那些执行单个任务的命令——了解它们的存在以及其基本功能是重要的。对于编辑器，我将给出简要介绍。这些是需要一些时间才能掌握的复杂程序；如果你想学习它们，取决于你个人。

在前面的示例中，文件 `pepys_diary.txt` 共有 129,095 行，包含 1,301,379 个单词，占用 6,796,982 字节。

`wc` 命令有多个可用选项，它们告诉命令只返回特定信息。使用 `-c` 选项，会显示字节数。`-l` 选项告诉 `wc` 只显示行数。`-w` 选项只显示单词数。`-m` 选项告诉命令只显示字符数：

```
$ wc -m pepys_diary.txt
6796982 characters pepys_diary.txt
```

注意，对于文件来说，字符数与字节数是相同的。

你可以对多个文件运行 `wc` 命令。如果你这样做做，命令将返回每个文件的统计信息，并给出所有文件的总计值：

```
$ wc pepys_diary.txt CivDiv.txt
129095 130179 6796982 pepys_diary.txt
1102 9372 5124 CivDiv.txt
130197 1310751 6848231 total
```

使用通配符，你可以让 `wc` 返回目录中所有文件的数据：

```
$ wc *
1102 9372 5124 CivDiv.txt
174366 122066 711193 Leaves_of_Grass.txt
8153 106718 580640 Walden.txt
129095 130179 6796982 pepys_diary.txt
155786 1539535 8140064 total
```

更多关于使用通配符的信息，请参阅交互 6，“通配符与匹配（Wildcards and Globbing）”。

`ls` 命令的 `-R` 选项是递归选项，告诉 `ls` 扫描并列出目标目录下所有子目录的信息。该命令只告诉你可见项目数，即名称不以 `.`（点）开头的项目。你可以为 `ls` 命令添加 `-a` 选项来包含隐藏项目；这将包括名为 `.` 和 `..` 的项目，它们出现在从当前工作目录开始的每个目录和子目录中。

# 使用 SORT 排序

`ls` 命令的 `-R` 选项是递归选项，告诉 `ls` 扫描并列出目标目录下所有子目录的信息。该命令只告诉你可见项目数，即名称不以 `.`（点）开头的项目。你可以为 `ls` 命令添加 `-a` 选项来包含隐藏项目；这将包括名为 `.` 和 `..` 的项目，它们出现在从当前工作目录开始的每个目录和子目录中。

# wc 命令概述

### 命令语法

```
wc [option(s)] [file ...]
```

## Finder 等效功能

文字处理程序或文本编辑器中的单词计数功能。

## wc 选项概述

- - wc `wc` 命令显示文件中包含的行、单词、字符和字节数。
- -c 此选项告诉 `wc` 命令只显示文件名对应的字节数。
- -l 此选项告诉 `wc` 命令只显示文件名对应的行数。
- -m 此选项告诉 `wc` 命令只显示文件名对应的字符数。
- -w 此选项告诉 `wc` 命令只显示文件名对应的单词数。

### 获取更多信息

在终端中输入 `man wc` 可以显示帮助页并学习更多关于 `wc` 的知识。

# 使用 sort 排序

`sort` 命令对文本文件的行进行排序，并为排序方式和输出类型提供了许多选项。在基本形式下，它按 a 到 z 的字母顺序对行。从此列表开始：

| Thoreau, Henry David | 555-1542 |
| Emerson, Ralph Waldo | 555-9210 |
| Pepys, Samuel | 555-2945 |
| Bach, Johann Sebastian | 555-1685 |
| James, Henry | 555-8307 |
| Joyce, James | 555-8844 |
| Handel, Georg Friedrich | 555-1999 |
| Hume, Tobias | 555-2498 |

运行 `sort` 命令返回：

```
$ sort telephone.txt
Bach, Johann Sebastian 555-1685
Emerson, Ralph Waldo 555-9210
Handel, Georg Friedrich 555-1999
Hume, Tobias 555-2498
James, Henry 555-8307
Joyce, James 555-8844
Pepys, Samuel 555-2945
Thoreau, Henry David 555-1542
```

`sort` 命令默认将输出返回到终端。如果你正在排序的文件并想查看输出，这很有用。要将输出重定向到文件，请使用 `-o`（output）选项：

```
$ sort -o sorted_telephone.txt telephone.txt
```

或者，覆盖现有文件可以这样运行命令：

```
$ sort -o telephone.txt telephone.txt
```

你还可以通过 `-r` 选项进行 z 到 a 的倒序排序：

```
$ sort -r telephone.txt
Thoreau, Henry David 555-1542
Pepys, Samuel 555-2945
Joyce, James 555-8844
James, Henry 555-8307
Hume, Tobias 555-2498
Handel, Georg Friedrich 555-1999
Emerson, Ralph Waldo 555-9210
Bach, Johann Sebastian 555-1685
```

有时你想要的文件某些行开头有空格。`-b` 选项告诉 `sort` 命令在排序时忽略领先空格：

```
$ sort -b telephone.txt
Bach, Johann Sebastian 555-1685
Emerson, Ralph Waldo 555-9210
Handel, Georg Friedrich 555-1999
Hume, Tobias 555-2498
James, Henry 555-8307
Joyce, James 555-8844
Pepys, Samuel 555-2945
Thoreau, Henry David 555-1542
```

`sort` 命令显示带有空格的结果，但仅根据空格后的字符进行排序。

`sort` 命令有许多选项，允许你指定输入字段的显著性、用于分隔字段的字符等。

## 命令行

## sort 命令概述

### 命令语法

```
sort [option(s)] [file ...]
```

## Finder 等效功能

文字处理程序、文本编辑器或电子表格中的排序功能。

# sort 选项概述

- - sort `sort` 命令对文件的行进行排序。
- - o 此选项后跟文件名，告诉 `sort` 命令将其输出保存到指定文件中。
- - r 此选项告诉 `sort` 命令进行倒序排序。
- - b 此选项告诉 `sort` 命令在排序时忽略领先空格。

### 获取更多信息

在终端中输入 `man sort` 可以显示帮助页并学习更多关于 `sort` 的知识。

# 使用 uniq 删除行

`uniq`（唯一）命令是一个过滤器，可以移除相邻的输入行。例如，如果你有一个名称或单词列表，你可以先用 `sort` 排序，然后用 `uniq` 过滤，每行只保留一次。

如果你有一个包含以下内容的文件

```
tell
about
Anna
Livia
to
hear
about
Anna
```

你可以运行以下命令进行排序然后删除重复项：

```
$ sort list.txt | uniq
Anna
Livia
all
hear
tell
want
```

你可以使用 `-c` 选项显示每行，并统计文件中每行出现的次数：

```
$ sort list.txt | uniq -c
2 Anna
1 Livia
2 all
1 hear
1 tell
1 want
```

或者，你可以使用 `-d` 选项打印重复行：

```
$ sort list.txt | uniq -d
Anna
Livia
```

你可以这样将 `uniq` 命令的结果重定向到文件：

```
$ sort list.txt | uniq > new_list.txt
```

`uniq` 命令是处理日志或数据库时非常有强大的工具。它提供了一个选项让你忽略每行的前 n 个字符，允许你处理在不同时间出现的重复行。在这样的文件中：

```
10.0.1.201 [28/May/2004:16:42:23] "GET /HTTP/1.0" 304
10.0.1.201 [28/May/2004:16:42:32] "GET /HTTP/1.0" 304
10.0.1.201 [28/May/2004:16:42:23] "GET /HTTP/1.0" 304
10.0.1.201 [28/May/2004:16:42:33] "GET /HTTP/1.0" 304
10.0.1.201 [28/May/2004:16:42:25] "GET /HTTP/1.0" 304
```

`uniq` 命令提供了一个选项让你忽略每行的前 n 个字符，允许你处理在不同时间出现的重复行。在这样的文件中：

```
10.0.1.201 [28/May/2004:16:42:23] "GET /HTTP/1.0" 304
10.0.1.201 [28/May/2004:16:42:32] "GET /HTTP/1.0" 304
10.0.1.201 [28/May/2004:16:42:23] "GET /HTTP/1.0" 304
10.0.1.201 [28/May/2004:16:42:33] "GET /HTTP/1.0" 304
10.0.1.201 [28/May/2004:16:42:25] "GET /HTTP/1.0" 304
```

有时你想要文件某些行开头有空格。`-b` 选项告诉 `sort` 命令在排序时忽略领先空格：

```
$ sort -b telephone.txt
Bach, Johann Sebastian 555-1685
Emerson, Ralph Waldo 555-9210
Handel, Georg Friedrich 555-1999
Hume, Tobias 555-2498
James, Henry 555-8307
Joyce, James 555-8844
Pepys, Samuel 555-2945
Thoreau, Henry David 555-1542
```

## 使用 diff 比较文件

`diff`（差异）命令允许你比较两个文件或目录并找到它们之间的差异。在比较文件时，diff 会检查单独的行以及包含差异的行——它不会突出显示单个单词或字符串。`diff` 命令是比较文件版本（例如原始版本和编辑版本）的优秀工具，但它只适用于文本文件，不会比较来自文字处理器或其他程序的专用格式二进制文件。

要使用 `diff`，你必须指定一个源文件（from-file，原始文件）和一个目标文件（to-file，编辑后的文件）。以下是使用 `diff` 的示例：

```
$ diff Song_Of_Myself.txt Song_Of_Myself_edit.txt
4c4
---
< I celebrate myself, and sing myself,
---
> I celebrate myself, and sing of myself,
6c6
< For every atom belonging to me as good belongs to you.
> For every atom that belongs to me also belongs to you.
14c4
< I, now thirty-seven years old in perfect health begin,
---
> I, now thirty-seven years old, in perfect health begin,
51c51
< Have you practiced so long to learn to read?
---
> Have you practiced so long to learn to read?
```

如你所示，`diff` 命令返回了发生变化的行列表。让我们来看其中第一行以及输出告诉了我们什么。

```
4c4
< I celebrate myself, and sing myself,
> I celebrate myself, and sing of myself,
```

首先，`4c4` 告诉我们与第一个文件的第 4 行相比，第二个文件的第 4 行发生了变化（c）。它显示了以 `<` 符号开头的第一个文件。在分隔符（---）之后，它显示了以 `>` 符号开头的第二个文件。检查这两行，你可以发现第二个文件的文本包含一个新增的单词：`of`。

如果添加或删除了任何行，显示方式如下：

```
71a72
> The fault is not in your stars but in yourself.
84d84
< I and mystery here we stand.
```

第一行（72）被添加到目标文件（>）；其文本显示在 `71a72` 之后，意味着第 72 行在第 71 行之后添加（a）。第二行从源文件的第 84 行被删除（d），这通过 `84d84` 显示。

注意，如果两个文件之间没有差异，`diff` 将不返回任何内容。`diff` 有几十种选项可以让你忽略空格、空行或大小写，显示额外的上下文，或与多个文件一起工作。更多信息请参阅命令页面。这是一个难以操作的命令，如果你经常需要比较文件，你可能倾向于使用 BBEdit 的“查找差异”功能，它可以更简单、更灵活地完成相同的功能。

## 命令行

### diff 命令概述

### 命令语法

```bash
diff [options] from-file to-file
```

### Finder 等效功能

文字处理器或文本编辑器中的比较文件功能。

### diff 选项概述

`diff` 命令比较文件并显示它们之间的差异。

### 获取更多信息

要显示帮助页并学习更多关于 `diff` 的信息，请在 Terminal 中输入 `man diff`。

## 使用 tr 替换字符

`tr`（翻译）命令在替换或删除选定字符后将标准输入复制到标准输出。这就像字符层面的查找/替换函数；例如，如果你想将所有的 `$` 替换为 `%`，可以运行以下命令：

```
$ tr '$' '%' < file
```

由于 `tr` 作用于标准输入，如果你想让它作用于文件，必须使用重定向（`< file`）。此外，`tr` 将更改后的文本返回到标准输出（默认是 Terminal），如果你想保存更改，需要将其写入新文件：

```bash
$ tr '$' '%' < file2
```

除了单个字符，你还可以在 `tr` 命令中使用字符范围。该命令的一个常用用途是更改字符的大小写。以下命令将所有大写字母转换为小写：

```bash
$ tr 'A-Z' 'a-z' < file
```

## 命令行

### tr 命令概述

### 命令语法

```bash
tr [option(s)] string1 string2
```

### Finder 等效功能

文字处理器或文本编辑器中针对单个字符的查找/替换功能。

### tr 选项概述

- tr：`tr` 用其他字符替换特定字符。
- -d：此选项告诉 `tr` 命令删除指定的字符。

### 获取更多信息

要显示帮助页并学习更多关于 `tr` 的信息，请在 Terminal 中输入 `man tr`。

你可以使用 `tr` 命令更改特殊字符，如换行符、制表符等。例如，如果你有一个由 Mac 格式化的文本文件（带有 Macintosh 换行符），并想用 Unix 工具查看或编辑它，你需要更改这些换行符：
