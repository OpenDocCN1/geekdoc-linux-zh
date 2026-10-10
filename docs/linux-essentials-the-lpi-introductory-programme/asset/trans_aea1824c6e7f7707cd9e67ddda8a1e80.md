
传统上，你可以直接通过 `-n` 参数指定期望的行数 *n*。官方上这已不再被允许，但 `head` 和 `tail` 的 Linux 版本仍然支持该用法。

你可以使用 `-c` 选项来指定按字节而非行进行计数：`"head -c 20"` 会显示标准输入的前 20 个字节，无论它们占用多少行。如果在计数值后附加一个 `"b"`、`"k"` 或 `"m"`（分别代表 `"blocks"`（块）、`"kibibytes"`（ kibibytes）和 `"mebibytes"`（ mebibytes）），计数值将分别乘以 512、1024 或 1048576。

`head` 还允许你使用负号：`"head -c -20"` 会显示标准输入的所有内容，但排除最后 20 个字节。

作为一种报复，*tail* 可以执行 *head* 不支持的操作：如果行数前带有 `"+"`，它将显示*从*给定行开始的全部内容：

```
$ tail -n +3 file
Everything from line 3
```

`tail` 命令还支持重要的 `-f` 选项。这使得 `tail` 在输出当前文件末尾后继续等待，以输出后续追加的数据。如果你想监控某些日志文件，这将非常有用。如果你向 `tail -f` 传入多个文件名，它会在每个输出数据块前添加一行标题，说明新数据写入的是哪个文件。

# 练习

- 8.8 [2] 你如何仅输出标准输入的第 13 行？

- 8.9 [3] 试试 `tail -f`：创建一个文件并对其进行调用 `tail -f`。然后，在另一个窗口或虚拟控制台中，使用例如 `echo >>...` 向该文件追加内容，并观察 tail 的输出。当 tail 同时监控多个文件时，输出看起来是什么样子的？

- 8.10 [3] 如果被观察的文件大小变小，`tail -f` 会发生什么？

- 8.11 [3] 解释以下命令的输出：

```
$ echo Hello >/tmp/hello
$ echo "Hiya World" >/tmp/hello
```

假设你在上述第一个 echo 之后已在另一个窗口中启动了以下命令：

```
$ tail -f /tmp/hello
```

# 8.4 数据管理

## 8.4.1 排序文件——*sort* 和 *uniq*

sort 命令允许你根据预设标准对文本文件的行进行排序。默认设置是升序（从 A 到 Z），基于每行前几个字符的 ASCII 值¹。这就是为什么诸如德语变音符号等特殊字符经常被错误排序的原因。例如，字符 `"Ä"` 的字符代码为 143，因此该字符排在字符代码为 90 的 `"Z"` 之后很远的位置。即使小写字母 `"a"` 也被视为“大于”大写字母 `"Z"`。

> ¹ 当然，ASCII 仅涵盖 0 到 127。这里真正指的是 ASCII 加上当前用于代码 128 至 255 字符的扩展，例如 ISO-8859-1，也称为 ISO-Latin-1。

当然，sort 可以适应不同的语言和文化。要按照德语约定进行排序，将环境变量 LANG、LC_ALL 或 LC_COLLATE 设置为诸如 `"de"`、`"de_DE"` 或 `"de_DE@UTF-8"` 的值（具体值取决于你的发行版）。如果你只想为单次 sort 调用设置此选项，请执行以下操作：

```
$ _ | LC_COLLATE=de_DE.UTF-8 sort
```

LC_ALL 的值优先于 LC_COLLATE 的值，而后者又优先于 LANG 的值。作为副作用，德语排序规则会在排序时忽略字母的大小写。

除非你另行指定，否则 sort 会“按字典顺序”考虑整个输入行。也就是说，如果两行的开头字符比较相等，则行内第一个不同的字符将决定它们的相对位置。当然，sort 不仅可以按整行排序，还可以更具体地按（概念性）表格中某些“列”或字段的值进行排序。字段的编号从 1 开始；使用 `“-k 2”` 选项时，第一个字段将被忽略，而每行的第二个字段将用于排序。如果两行在第二个字段中的值相等，系统将查看行的剩余部分，除非你使用类似 `“-k 2,3”` 的格式指定最后一个要查看的字段。顺便提一下，允许在同一个 sort 命令中指定多个 -k 选项。

此外，sort 还支持一种已废弃的位置指定形式：这里字段的编号从 0 开始，初始字段指定为 `“+m”`，最终字段指定为 `“-n”`。为了与现代形式区分，最终字段是“排他性”指定的——你给出第一个不应被纳入排序考虑的字段。上述例子分别对应 `“+1”`、`“+1 -3”` 和 `“+1 2”`。

空格字符充当字段之间的分隔符。如果连续出现多个空格，只有第一个被视为分隔符；其余的空格被视为后续字段值的一部分。下面是一个小例子，即 Lameborough 田径俱乐部年度马拉松赛的参赛者名单。首先，我们通过重置相应环境变量来确保使用系统的标准语言环境（`“POSIX”`）。（顺便提一下，第四列给出的是选手的号码布编号。）

```
$ unset LANG LC_ALL LC_COLLATE
$ cat participants.dat
Smith Herbert Pantington AC 123 Men
Prowler Desmond Lameborough TFC 13 Men
Fleetman Fred Rundale Sportsters 217 Men
Jumpabout Mike Fairing Track Society 154 Men
de Leaping Gwen Rundale Society 26 Ladies
Runninton Vivian Lameborough TFC 117 Ladies
Sweat Susan Rundale Sportsters 93 Ladies
Runninton Kathleen Lameborough TFC 119 Ladies
Longshanks Loretta Pantington AC 55 Ladies
O'Finnar Jack Fairing Track Society 45 Men
Oblomovsky Katie Rundale Sportsters 57 Ladies
```

让我们尝试按姓氏排序的列表。原则上这很简单，因为姓氏位于每行的开头：

```
$ sort participants.dat
Fleetman Fred Rundle Sportsters 217 Men
Jumpabout Mike Fairing Track Society 154 Men
Longshanks Loretta Pantington AC 55 Ladies
O’Finnan Jack Fairing Track Society 45 Men
Oblomovsky Katie Rundle Sportsters 57 Ladies
Prowler Desmond Lameborough TFC 13 Men
Runnigton Kathleen Lameborough TFC 119 Ladies
Runnigton Vivian Lameborough TFC 117 Ladies
Smith Herbert Pantington AC 123 Men
Sweat Susan Rundle Sportsters 93 Ladies
de Leaping Gwen Fairing Track Society 26 Ladies
```

你一定会注意到这个列表中的两个小问题：`“Oblomovsky”` 应该排在 `“O’Finnan”` 之前，而 `“de Leaping”` 应该出现在列表的开头，而不是结尾。如果我们指定 `“English”`（英语）排序规则，这些问题就会消失：

```
$ LC_COLLATE=en_GB sort participants.dat
de Leaping Gwen Fairing Track Society 26 Ladies
Fleetman Fred Rundle Sportsters 217 Men
Jumbabout Mike Fairing Track Society 154 Men
Longshanks Loretta Pantington AC 55 Ladies
Oblomovsky Katie Rundle Sportsters 57 Ladies
O’Finnan Jack Fairing Track Society 45 Men
Prowler Desmond Lameborough TFC 13 Men
Runnigton Kathleen Lameborough TFC 119 Ladies
Runnigton Vivian Lameborough TFC 117 Ladies
Smith Herbert Pantington AC 123 Men
Sweat Susan Rundle Sportsters 93 Ladies
```

（en_GB 是 `“British English”`（英式英语）的缩写；这里使用 en_US，即 `“American English”`（美式英语），也可以正常工作。）接下来让我们按名字排序：

```
$ sort -k 2,2 participants.dat
Smith Herbert Pantington AC 123 Men
Sweat Susan Rundle Sportsters 93 Ladies
Prowler Desmond Lameborough TFC 13 Men
Fleetman Fred Rundle Sportsters 217 Men
O’Finnan Jack Fairing Track Society 45 Men
Jumbabout Mike Fairing Track Society 154 Men
Runnigton Kathleen Lameborough TFC 119 Ladies
Oblomovsky Katie Rundle Sportsters 57 Ladies
de Leaping Gwen Fairing Track Society 26 Ladies
Longshanks Loretta Pantington AC 55 Ladies
Runnigton Vivian Lameborough TFC 117 Ladies
```

这说明了上述提到的 sort 的一个特性：一连串空格中的第一个空格被视为分隔符，其余空格成为后续字段值的一部分。如你所见，名字按字母顺序列出，但仅限于姓氏长度相同的情况下。使用 -b 选项可以修复这个问题，该选项将连续的多个空格视为单个空格：

```
$ sort -b -k 2,2 participants.dat
Prowler Desmond Lameborough TFC 13 Men
Fleetman Fred Rundle Sportsters 217 Men
Smith Herbert Pantington AC 123 Men
O’Finnan Jack Fairing Track Society 45 Men
Runnigton Kathleen Lameborough TFC 119 Ladies
Oblomovsky Katie Rundle Sportsters 57 Ladies
de Leaping Gwen Fairing Track Society 26 Ladies
Longshanks Loretta Pantington AC 55 Ladies
Jumbabout Mike Fairing Track Society 154 Men
```

