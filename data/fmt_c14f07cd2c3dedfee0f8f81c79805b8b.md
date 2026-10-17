
![](img/3137cdda7122042e86dbeafe9840d4ed_210_0.png)

*Figure 7-13: Creating an HTML file with Gnotepad+*

![](img/3137cdda7122042e86dbeafe9840d4ed_211_0.png)

Figure 7-14: The gEdit editor

and replace, a toolbar, printing, cutting, copying, and pasting 等标准文本编辑器功能。如果你是一名程序员，你可能会因为 gEdit 可用的编程插件而更喜欢 gEdit 而不是 Gnotepad+。

要启动 gEdit，在 shell 提示符下输入命令

```
gedit
```

或选择 GNOME Foot • Applications • gEdit 菜单项。你也可以通过选择 Gnome Foot • Panel • Add new launcher 在你的 GNOME 任务栏上添加一个 gEdit 按钮。将 `gedit` 指定为程序名称，并选择你喜欢的图标。

## USING GEDIT

使用 gEdit 与使用 Gnotepad+ 或其他图形编辑器并没有太大区别。与其用又一篇“如何使用此编辑器”的说教来

![](img/3137cdda7122042e86dbeafe9840d4ed_215_0.png)

## 切分与切片

- `HEAD` 命令 186
- `TAIL` 命令 186
- `SORT` 命令 187
- `UNIQ` 命令 189
- `CUT` 命令 191
- `GREP` 命令 192
- `SED` 命令 194
- `AWK` 命令 196
- `FIND` 命令 197
- 管道连接 199

Linux 的好处之一是它自带了一套工具，可以在不编写程序的情况下帮助你操作文件和数据。例如，如果你想在大量文件中搜索，提取包含某个关键词的所有行，对这些行进行排序，去掉重复项，然后只打印每行的第三列，使用本章描述的工具其实并不麻烦。

用 C 语言编写一个程序来实现这一点，对于有经验的程序员来说也不是一个简单的练习。但你可以用这些切分与切片工具像搭积木一样操作数据并生成报表，而无需计算机科学学位。

下面是对每个工具如何工作的描述，并在本章末尾，你会找到一些将它们组合成更强大命令的技巧。

### HEAD 命令

`head` 命令显示文件顶部的几行。当你想快速预览一个大文件，而不是用文本编辑器打开它时，它会很有用。默认情况下，`head` 会显示文件的前十行，但你也可以告诉它显示多少行。以下是几个例子：

```
head some.file    Show first ten lines of some.file
head -5 some.file    Show first five lines of some.file
```

### TAIL 命令

`tail` 命令显示文件的最后几行。与 `head` 类似，它可以节省时间，因为比用文本编辑器打开文件然后滚动到最底部要快得多。默认情况下，`tail` 会显示文件的最后十行，但你也可以告诉它显示多少行：

```
tail some.file    Show last ten lines of some.file
tail -3 some.file    Show last three lines of some.file
```

下面是一个使用 `tail` 命令的实用例子。许多 Linux 程序在运行时会将诊断信息写入 `/var/log/messages` 文件，因此随着时间的推移，这个文件可能会变得相当大。要查看你最近的命令是否发出任何消息，请通过输入 `tail /var/log/messages` 命令查看此文件的末尾。

### SORT 命令

`sort` 命令根据字段对文件进行排序——每行上的各个数据片段。默认情况下，`sort` 假定字段只是用空格分隔的单词，但如果你愿意，也可以指定替代的字段分隔符（例如逗号或冒号）。`sort` 的输出会打印到屏幕上，除非你将其重定向到文件。如果你有一个像这里所示的文件，其中包含为你总统连任竞选捐款的人的信息，例如，你可能想按姓氏、捐款金额或地点对其进行排序。 （使用文本编辑器，输入那三行并将其保存为 `donor.data` 文件名。）

```
Bay Ching 500000 China
Jack Arta 250000 Indonesia
Cruella Lumper 725000 Malaysia
```

让我们以这个示例捐赠者文件为例，按姓氏对其进行排序。以下是按第二个字段（姓氏）对文件进行排序的命令以及命令的输出：

```
sort +1 -2 donors.data
Jack Arta 250000 Indonesia
Bay Ching 500000 China
Cruella Lumper 725000 Malaysia
```

`sort` 命令的语法相当奇怪，但如果你研究以下示例，应该能够将其改编为自己的用途。`sort` 命令的一般形式是

```
sort <flags> <sort fields> <file name>
```

最常用的标志如下：

- `-f` 在排序前将所有行转为大写（因此“Bill”和“bill”被视为相同）。
- `-r` 按逆序排序（因此“Z”开始列表而不是“A”）。
- `-n` 按数值顺序对一列进行排序。
- `-t x` 使用 `x` 作为字段分隔符（将 `x` 替换为逗号或其他字符）。
- `-u` 抑制每组具有相等排序字段的行中的所有行，但保留一行（因此如果按包含姓氏的字段排序，即使有多个“Smith”，也只会出现一个“Smith”）。

按如下方式指定排序键：

- `+m` 从第 `m+1` 个字段的第一个字符开始。
- `-n` 在第 `n` 个字段的最后一个字符处结束（如果省略 `-N`，则假定为行的末尾）。

看起来很奇怪，对吧？让我们用这里显示的示例 `company.data` 文件再看几个例子，你就会掌握它了。 （文件的每一行包含四个字段：名字、姓氏、序列号和部门名称。）

```
Jan Itorre 406378 Sales
Jim Nasium 031762 Marketing
Mel Ancholie 636496 Research
Ed Jucacion 396082 Sales
```

要按第三个字段（序列号）以逆序对文件进行排序并将结果保存到 `sorted.data` 中，请使用此命令：

```
sort -r +2 -3 company.data > sorted.data

Mel Ancholie 636496 Research
Jan Itorre 406378 Sales
Ed Jucacion 396082 Sales
Jim Nasium 031762 Marketing
```

现在让我们看一个字段由冒号而不是空格分隔的情况。在这种情况下，我们将使用 `-t:` 标志告诉 `sort` 命令如何在每行上找到字段。让我们从这个文件开始：

Ito­re, Jan:406378:Sales

Nasium, Jim:03762:Marketing

Ancholie, Mel:636496:Research

Jucacion, Ed:396082:Sales

要按第二个字段（序列号）对文件进行排序，请使用以下命令：

```
sort -t: +1 -2 company.data
Nasium, Jim:03762:Marketing
Jucacion, Ed:396082:Sales
Itore, Jan:406378:Sales
Ancholie, Mel:636496:Research
```

要按第三个字段（部门名称）对文件进行排序并抑制重复项，请使用以下命令：

```
sort -t: -u +2 company.data
Nasium, Jim:03762:Marketing
Ancholie, Mel:636496:Research
Itore, Jan:406378:Sales
```

（请注意，Ed Jucacion 的行没有打印出来，因为他属于 Sales，而我们要求命令（使用 `-u` 标志）抑制在排序字段中相同的行。）

`sort` 命令可以做很多花哨的（以及一些晦涩的）事情。如果您需要进行任何排序操作，而这些操作并不像这些示例那样直接，请尝试 `man sort` 命令以获取更多信息。

## THE UNIQ COMMAND

`uniq` 命令读取输入文件并比较相邻的行。任何与前一行相同的行将被丢弃。换句话说，重复项将被丢弃，只保留文件中的唯一行。

假设您是一家出版社，拥有 `my.books` 文件中所示的所有书籍的库存：

```
Atopic Dermatitis for Dummies
Atopic Dermatitis for Dummies
Chronic Rhinitis Unleashed
Chronic Rhinitis Unleashed
Chronic Rhinitis Unleashed
Learn Nasal Endoscopy in 21 Days
```

要从书籍列表中删除所有重复项，请使用以下命令：
