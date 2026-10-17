
除了将数据重定向到文件外，有时你可能还希望使用其他命令。这可以通过使用管道字符（`|`）来完成。这允许你使用一行命令将一个命令的输出数据作为输入数据发送到另一个命令。在以下示例中，文件`namelist`按字母顺序排序，然后使用`nl`命令为每个名称添加行号。

```
# sort +1 namelist | nl
1 Peter Anapol
2 Jeff Arellano
3 Scott Bessler
4 Alex Blauvelt
5 Michael Craig
6 Joakim Erdfelt
7 Johannes Erdfelt
8 Pete Gizzi
9 David Goolsby
10 Thomas McCanta
11 Angie Nash
12 Jason Nash
13 Neil Schroeder
14 Derek Stutsman
15 Paul Ward
```

这些数据也可以通过管道传输到另一个实用工具或重定向到文件。

```
# sort +1 namelist | nl > numberrednames
# more numberrednames
1 Peter Anapol
2 Jeff Arellano
3 Scott Bessler
4 Alex Blauvelt
5 Michael Craig
6 Joakim Erdfelt
7 Johannes Erdfelt
8 Pete Gizzi
9 David Goolsby
10 Thomas McCanta
11 Angie Nash
12 Jason Nash
13 Neil Schroeder
14 Derek Stutsman
15 Paul Ward
```

此示例展示了如何使用管道和重定向一起使用多个实用工具处理数据，然后将输出保存到另一个文件。除了通过管道符号发送到另一个实用工具的`stdout`外，`stderr`也可以被包含并使用`1>&2`符号发送到该实用工具。例如，以下命令对`namelist`的内容进行排序，添加行号，并附加任何错误信息。

```
sort +1 namelist 1>&2
```

### `tee`

`tee`实用工具将标准输入复制到标准输出，同时也复制到作为参数给出的任何文件，因此`stdin`既出现在`stdout`中，也出现在文件中。当你不仅希望将一些数据通过管道传输，还希望将其副本保存到文件时，这将非常有用。如果你要写入的文件尚不存在，它将被创建。如果你要写入的文件已经存在，之前包含的数据将被覆盖，除非使用追加选项。与此实用工具一起使用的选项如表 4-1 所示。

| 选项 | 用途 |
| :--- | :--- |
| `-a` | 将标准输入追加到指定文件。 |
| `-i` | 忽略用于停止或重启进程的中断信号。 |

![](img/96d9ccd181675a8ae8b6a1146c919d2b_197_0.png)

`tee`实用工具对于在处理实用工具时沿途保存输出非常有用。你可以稍后引用此输出，这对故障排除可能很有用。

在以下示例中，文件`namelist`首先按字母顺序排序，然后管道传输到`tee`，使得输出也被保存到文件`abcnames`。然后数据被管道传输到`nl`，使得每行都有编号，输出然后被重定向到名为`abc123names`的文件。

### `xargs`

`xargs`实用程序用于向其他命令传递大量参数。`xargs`实用程序从标准输入读取参数，参数之间由空格（当与双引号、单引号或反斜杠一起使用时，空格作为普通字符处理）或换行符分隔，并执行一次或多次该命令，初始参数后跟从标准输入读取的参数。标准输入中的空行会被忽略。这使得命令能够处理比通常情况更多的参数。在以下示例中，使用`locate`链接搜索`locate`数据库中的所有`README`文件。使用`xargs`后，文件名随后被发送到`cat`实用程序，然后显示文件内容。这些文件的所有文本都被发送到`fmt`实用程序，该实用程序以 60 个字符的行宽对数据进行格式化。输出随后被重定向到文件`/home/angie/readmes`。

```bash
locate README | xargs cat | fmt -60 > /home/angie/readmes
```

![image](img/96d9ccd181675a8ae8b6a1146c919d2b_199_0.png)

`xargs`实用程序用于以其他实用程序能够处理的速率向其提供参数。在不需要时使用此命令不会产生任何错误。

## 使用过滤器修改文本

![image](img/96d9ccd181675a8ae8b6a1146c919d2b_199_1.png)

1.3 GNU 和 Linux 命令

- **使用文本处理过滤器处理文本流。** 将文本文件和输出流通过文本实用程序过滤器，以有用地修改输出。包括使用 GNU `textutils`包中发现的标准`unix`命令，如`sed`、`sort`、`cut`、`expand`、`fmt`、`head`、`join`、`nl`、`od`、`paste`、`pr`、`split`、`tac`、`tail`、`tr`和`wc`。
- **执行文本文件的搜索并利用正则表达式。** 包括创建简单的正则表达式，并使用相关工具（如`grep`和`sed`）执行搜索。

`Linux`提供了多种用于处理和过滤文本的工具。这些工具使您能够搜索数据，然后根据您使用的工具对其进行操作。这些工具可以从命令行使用，也可以放在脚本中执行所需任务。输出随后要么发送到标准输出，在那里可以重定向或管道到另一个实用程序，要么发送到文件。这些工具在输入和输出上的灵活性使您能够为各种用途定制文本。无论运行了多少个过滤器，原始文本都保持完整。

在处理文本文件时，你可能会使用*pager*（分页器），例如`more`或`less`。这些实用程序用于逐页显示文本。`cat`实用程序也可以用于显示文本文件的内容。这些实用程序不是过滤器，但在处理文本时通常很有帮助。

### 对文件中的行进行排序

`sort`实用程序对文本行进行排序并将其显示到标准输出。它用于对文件或标准输入中的行进行排序、合并和比较。该实用程序使用以下语法：

```bash
sort -option filename
```

表 4-2 列出了`sort`实用程序常用的选项。

**表 4-2 `sort`使用的选项**

| 选项 | 用途 |
| :----- | :----- |
| `-b` | 忽略前导空格。 |
| `-c` | 检查文件是否已排序。 |
| `-d` | 仅考虑字母数字字符，并按电话簿顺序排序。 |
| `-f` | 将小写字符折叠为大写字符。 |
| `-m` | 合并已排序的文件，而不重新排序。 |
| `-M` | 比较已排序的文件。 |
| `-n` | 按数值排序。 |
| `-o FILE` | 将输出写入指定文件，而不是标准输出。 |
| `-r` | 反转结果。 |
| `--help` | 显示帮助并退出。 |
| `--version` | 显示版本并退出。 |

`sort`实用程序的使用示例及其输出如下：

```bash
# sort list
3
32
41
5
90
Celestial
Seasons
Centrum
Whiskas
bread
butter
eggs
flour
ice
milk
sugar
```

如本例所示，默认情况下，列表首先按数字顺序排序，然后按字母顺序排序，大写字母在小写字母之前。在以下示例中，`-f`选项告诉`sort`忽略大小写。

```bash
# sort -f list
3
32
41
5
90
bread
butter
Celestial Seasons
Centrum
eggs
flour
ice
milk
sugar
Whiskas
```

在以下示例中，两个已排序的文件被合并。如你所见，文件并没有重新排序，而是简单地结合在一起。

```bash
# sort -m alphanumeric alphanames
angle
birdgrlmon
crystalmoon
denise
desteve
jcfaggle
jill
judy
katrina
kim
lma
loudhouse
monica
netchickie
nikki
nikks
trinityz
```

还可以基于字段对文件进行排序。字段可以通过空格或制表符分隔，并从零开始编号。在基于字段排序时，`+`符号位于字段编号之前，每个字段之间用空格分隔。在以下示例中，`namelist`文件先按第二个字段（`+1`）排序，然后按第一个字段（`+0`）排序：
