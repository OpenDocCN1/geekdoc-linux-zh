
总结来说，如果归档包含绝对路径，`tar` 将将这些文件（从磁带或磁盘）恢复到它们的原始位置。如果归档包含相对路径，`tar` 将通过将当前目录添加到 tar 路径中将文件恢复到相应的路径。

## 考虑绝对文件名的变通方法

如果你使用绝对文件名创建 tar 归档，`tar`（通常情况下）只能将这些文件恢复到它们的原始位置。这是 `tar` 的一个非常大且令人沮丧的限制。因此，关于 `tar` 的文档通常建议您在进行 tar 备份时使用相对路径。本章早期关于“使用 tar 备份目录子树”的部分仅记录了如何使用相对路径进行备份。

在 Linux/GNU 系统下，`tar` 在创建 tar 备份时会自动剥离开头的斜杠，以便 tar 归档始终使用相对路径。然而，在 Linux/GNU `tar` 下，你仍然可能通过两种方式遇到绝对路径带来的烦恼：你可以使用特殊的 Linux/GNU `tar -P` 选项来保留开头的斜杠，或者你可能会收到来自另一个系统且是使用绝对路径写入的磁带。

在 SCO UNIX 下，`tar` 有一个非常有用的 `-A` 选项，可以在恢复时抑制开头的斜杠。你可以像恢复 tar 归档中的相对路径一样恢复绝对路径。只要在初始 `x` 选项之后，你可以在 tar 选项列表的任何位置添加 `-A` 选项。AIX、Solaris 或 Linux/GNU 上并不存在 `-A` 选项。

如果 tar 中的绝对路径对你来说是一个大问题，请检查你的系统是否支持 `pax` 命令，该命令应该能够读取 tar 归档，并支持通过 `-s` 选项修改找到的文件。

## 切换到正确的目录

如果 tar 归档中的文件使用绝对路径，那么在执行 `tar` 恢复命令之前切换到哪个目录都没有区别。

如果 tar 归档中的文件是相对的，那么在使用 `tar` 恢复文件时，关键且危险的决策之一是在开始执行 tar 恢复之前选择切换到哪个目录。因为你正在恢复一个或多个旧归档文件，存在无意中覆盖这些文件当前版本的危险。要确定切换到哪个目录，请将路径与你想要恢复文件的位置的绝对路径进行比较：

示例 1

```
tar 归档上的路径：
./mori/pegasus/1997/expenses
恢复后的期望绝对路径：
/tmp/restoredata/mori/pegasus/1997/expenses
tar 恢复前要切换的目录：
/tmp/restoredata
```

示例 2

```
tar 归档上的路径：
./mori/pegasus/1997/expenses
恢复后的期望绝对路径：
./mori/pegasus/1997/expenses
即我们确实想将文件恢复到其原始位置
tar 恢复前要切换的目录：
/
```

示例 3

```
tar 归档上的路径：
./mori/pegasus/1997/expenses
恢复后的期望绝对路径：
/pegasus/1997/expenses
tar 恢复前要切换的目录：
我们无法仅通过设置当前目录来完成这个示例。这可以通过更复杂的步骤来实现——例如，创建一个子目录 mori 作为根目录 (/) 的符号链接，或者将文件恢复到某些临时目录并将它们移动到目标位置。
```

## 将所有文件恢复到原始目录

恢复文件可能是复杂且危险的：你可能会覆盖错误的文件。本节将向你展示恢复的几种方法，并讨论这些方法的优缺点。

你可能不想使用最简单的恢复方法，即将所有文件放回它们来源的地方。如果你这样做，你就会毁掉包含最新信息的文件，并用来自备份的带有旧信息的文件替换它们。

这种操作很少执行。例如，如果某项重大更新操作出现问题导致所有当前文件都损坏了，你可能希望从备份中较旧但未损坏的版本恢复文件。

要将 tar 备份中的所有文件恢复到原始目录，请切换到你最初备份的目录。在这里执行 `tar` 恢复命令：

```
$ cd /usr/fred/projects
$ tar xvf /dev/???
```

在这里，`/usr/fred/projects` 只是一个示例目录名。请替换为你制作备份的目录。如果 tar 归档包含绝对路径，切换到哪个目录都无关。

`x` 意味着从备份中提取文件。此 tar 选项列表中的第一个字母必须 `c`、`x` 或 `t`。提取（恢复）始终是一个危险的选项，因为你必须确保没有覆盖错误的文件。

`/dev/???` 应该替换为 tar 归档的文件或设备名称。

此示例显示了运行此命令时屏幕显示的内容：

```
$ cd /usr/fred/projects
$ tar xvf /dev/???
x ., 0 bytes tape blocks
x /acme, 0 bytes tape blocks
x /acme/report6, 29 bytes tape blocks
x /pegasus, 0 bytes tape blocks
x /pegasus/1997, 0 bytes tape blocks
x /pegasus/1997/expenses, 135 bytes tape blocks
x /pegasus/1998, 0 bytes tape blocks
x /pegasus/1998/expenses, 7995 bytes tape blocks
x /pegasus/1998/sales, 9463 bytes tape blocks
$
```

注意每行都以 `x` 开头，表示该文件正在从 tar 提取。

## 将所有文件恢复到不同的目录

警告，从 tar 归档将所有文件恢复到不同目录的过程只有在归档中使用相对路径时才有效。查看前面的章节以检查绝对与相对路径。

## 使用 tar 备份和恢复文件

选择一个磁盘空间充足的文件系统。然后切换到正确的目录。这是一个示例：

```
$ cd /tmp
$ tar xvf /dev/XXX?
x ., 0 bytes tape blocks
x ./acme, 0 bytes tape blocks
x ./acme/report6, 29 bytes tape blocks
x ./pegasus, 0 bytes tape blocks
x ./pegasus/1997, 0 bytes tape blocks
x ./pegasus/1997/expenses, 135 bytes tape blocks
x ./pegasus/1997/sales, 3281 bytes tape blocks
x ./pegasus/1998, 0 bytes tape blocks
x ./pegasus/1998/expenses, 7995 bytes tape blocks
x ./pegasus/1998/sales, 9463 bytes tape blocks
$
```

在这个示例中，tar 备份中的 `acme` 和 `pegasus` 目录恢复到了 `/tmp` 目录。再次警告：如果 tar 归档包含绝对路径，你的当前目录将被忽略，文件将恢复到原始位置，这可能是灾难性的。

## 仅恢复选定的目录或文件

如本示例所示，可以只恢复选定的目录或文件。重要的是按照 tar 列表中出现的格式指定目录或文件，包括任何开头的斜杠 (`/`) 或点斜杠 (`.`)。任何目录都是递归恢复的。

考虑以下命令：

```
$ cd desired-dir
$ tar xvf /dev/XXX? ./acme/report6 ./pegasus
```

在这里，`desired-dir` 应该替换为你想要执行 tar 命令的目录目录。

`/dev/XXX` 应该替换为 tar 文件或设备名称。

`./acme/report6` 展示了如何恢复一个文件。

`./pegasus/1997` 展示了如何恢复一个目录及其所有的文件和子目录。

注意，恢复选定文件的时间与最初写入 tar 归档的时间一样长。

# 设置和使用 tar 备份设备表

许多如 Solaris 和 SCO UNIX 的 UNIX 系统允许将常用的 tar 设备放置在名为 `/etc/default/tar` 的文件中。

这是来自 Solaris 2.6 的该文件示例：

| device | block | size |
| :--- | :--- | :--- |
| archive0=/dev/rmt/0 | 20 | 0 |
| archive1=/dev/rmt/0 | 20 | 0 |
| archive2=/dev/rmt/1 | 20 | 0 |
| archive3=/dev/rmt/1n | 20 | 0 |
| archive4=/dev/rmt/0 | 126 | 0 |
| archive5=/dev/rmt/1 | 126 | 0 |
| archive6=/dev/rmt/0 | 126 | 0 |
| archive7=/dev/rmt/1n | 126 | 0 |

系统管理员可以在此文件中显示的设备名称处输入常用的 tar 设备名称。这允许在 tar 命令中使用单个数字来指定目标设备：

```
$ tar cv2 .
```
