
```
$ cat Fall_OH
Office Hours for Fall 2014
Monday
9:00 - 10:00 A.M.
3:00 - 4:00 P.M.
Tuesday
10:00 - 11:00 A.M.
Wednesday
9:00 - 10:00 A.M.
3:00 - 4:00 P.M.
Thursday
11:00 A.M. - 12:00 P.M.
2:00 - 3:00 P.M.
4:00 - 4:30 P.M.
$ cat Spring_OH
Office Hours for Spring 2015
Monday
9:00 - 10:00 A.M.
3:00 - 4:00 P.M.
Tuesday
10:00 - 11:00 A.M.
1:00 - 2:00 P.M.
Wednesday
9:00 - 10:00 A.M.
Thursday
11:00 A.M. - 12:00 P.M.
$ diff Fall_OH Spring_OH
1c1
< Office Hours for Fall 2014
---
> Office Hours for Spring 2015
6a7
> 1:00 - 2:00 P.M.
9d9
< 3:00 - 4:00 P.M.
12,13d11
< 2:00 - 3:00 P.M.
< 4:00 - 4:30 P.M.
$
```

指令 `1c1` 要求 `ed` 编辑器将 `Fall_OH` 文件中的第一行（Office Hours for Fall 2014）更改为 `Spring_OH` 文件中的第一行（Office Hours for Spring 2015）。指令 `6a7` 要求 `ed` 编辑器在 `Fall_OH` 的第 6 行后追加 `Spring_OH` 中的第 7 行。指令 `12,13d11` 要求 `ed` 编辑器从 `Fall_OH` 中删除第 12 行和第 13 行。

以下会话说明了使用 `-e` 选项的 `diff` 命令以及如何将该命令的输出提供给 `ed` 编辑器以使 `Fall_OH` 与 `Spring_OH` 相同。该命令用于向您展示命令输出的样子。第二个 `diff` 命令（带 `> diff.script`）用于将命令输出（`ed` 脚本）保存到 `diff.script` 文件中。`cat >> diff.script` 命令用于通过添加包含 `w` 和 `q` 的两行，将 `diff.script` 文件转换为完整的 `ed` 编辑器工作脚本。如前所述，该命令以 `<Ctrl+D>` 结束。最后，运行 `ed` 命令根据 `diff -e` 命令生成的脚本更改 `Fall_OH` 的内容，使其与 `Spring_OH` 相同。数字 `209` 和 `177` 显示了执行 `ed` 命令前后 `Fall_OH` 文件的大小。最后一条命令 `diff Fall_OH Spring_OH` 用于确认两个文件相同。

```
$ diff -e Fall_OH Spring_OH
12,13d
9d
6a
1:00 - 2:00 P.M.
.
1c
Office Hours for Spring 2015
.
$ diff -e Fall_OH Spring_OH > diff.script
$ cat >> diff.script
w
q
<Ctrl+D>
$ ed Fall_OH < diff.script
209
177
$ diff Fall_OH Spring_OH
$
```

大多数系统都有一个名为 `diff3` 的命令，可用于进行三向比较；即可以组合三个文件。

## 6.7 在文本文件中定位和删除重复内容

您可以使用 `uniq` 命令删除文件中除一个副本外的所有连续重复行。该命令适用于排序后的文件，尽管它也可以在未排序的文件上工作，如示例所示。我们将在第 7 章讨论排序。以下是该命令的简要说明。

```
SYNTAX
uniq [options] [input-file] [output-file]

Purpose: Remove repetitious lines from the sorted input-file and send unique (nonrepeated) lines to output-file. The input-file does not change. If no output-file is specified, the output of the command is sent to standard output. If no input-file is specified, the command takes input from standard input.

Commonly used options/features:
-c  Precede each output line by the number of times it occurs
-d  Display the repeated lines
-f N Ignore the first N fields in input lines while doing comparisons
-i  Perform case-sensitive comparison of input lines
-s C Ignore the first C characters in input lines while doing comparisons
-u  Display the lines that are not repeated
```

以下会话说明了 `uniq` 命令的工作原理。`cat` 命令用于显示示例文件的内容。`uniq sample` 命令显示只有连续的重复行才被视为重复。`uniq -c sample` 命令显示文件中每行的行数。`uniq -d sample` 命令用于仅输出重复行。最后，`uniq -d sample out` 命令将命令的输出发送到 `out` 文件。`cat out` 命令用于显示 `out` 的内容。请注意，如果重复行相邻，`uniq` 命令仅适用于未排序的文件。

```
$ cat sample
This is a test file for the uniq command.
It contains some repeated and some nonrepeated lines.
Some of the repeated lines are consecutive, like this.
Some of the repeated lines are consecutive, like this.
```

Some of the repeated lines are consecutive, like this.

And, some are not consecutive, like the following.

Some of the repeated lines are consecutive, like this.

The above line, therefore, will not be considered a repeated

line by the uniq command, but this will be considered repeated!

$ uniq sample

This is a test file for the uniq command.

It contains some repeated and some nonrepeated lines.

Some of the repeated lines are consecutive, like this.

And, some are not consecutive, like the following.

Some of the repeated lines are consecutive, like this.

The above line, therefore, will not be considered a repeated

line by the uniq command, but this will be considered repeated!

$ uniq -c sample

1 This is a test file for the uniq command.

1 It contains some repeated and some nonrepeated lines.

3 Some of the repeated lines are consecutive, like this.

1 And, some are not consecutive, like the following.

1 Some of the repeated lines are consecutive, like this.

1 The above line, therefore, will not be considered a

repeated

2 line by the uniq command, but this will be considered

repeated!

$ uniq -d sample

Some of the repeated lines are consecutive, like this.
