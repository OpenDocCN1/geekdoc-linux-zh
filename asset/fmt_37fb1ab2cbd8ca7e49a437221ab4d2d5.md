
## head

| head | 显示文件的开头 |
| 语法: | `head [options] [file-list]` |

### 总结

`head` 工具显示文件的开头（头部）。它从你在命令行上指定的一个或多个文件获取输入，或从标准输入获取输入。

### 参数

`file-list` 包含 `head` 显示的文件路径名。如果你指定了多个文件，`head` 在显示前几行之前会显示每个文件的文件名。如果你没有指定任何文件，`head` 将从标准输入获取输入。

### 选项

- `-bytes[+n]` (`-c`) 按字节（字符）计数。`n` 是可选的非零整数。`u` 是可选的计量单位，可以是 `b`（512 字节块）、`k`（1024 字节或 1KB 块）或 `m`（1MB 字节块）。如果你包含了计量单位，`head` 将按该单位代替字节进行计数。
- `-lines[+n]` (`-n`) 按行计数（默认）。你可以使用 `-n` 来指定行数，而无需使用 `lines` 关键字。
- `-quiet` (`-q`) 当你在命令行上指定了多个文件名时，抑制页头信息。
- `-help` 总结如何使用 `head`。

## Note

`head` 工具默认显示十行。

## 示例

示例基于以下包含十一行的文件：

```
$ cat eleven
line one
line two
line three
line four
line five
line six
line seven
line eight
line nine
line ten
line eleven
```

在这个示例中，`head` 显示了 `eleven` 文件的前十行（无参数）：

```
$ head
line one
line two
line three
line four
line five
line six
line seven
line eight
line nine
line ten
```

## 762 ispell

此表中的项出现在屏幕底部的菜单中（除非你使用 `-N` 选项）。还会显示包含可能拼写错误的单词（已高亮）的输入行以及一行或多行的上下文。

替换了单词而你没有给出 `q` 命令，`ispell` 会创建一个扩展名为 `.bak` 的备份文件。`-x` 选项会禁用此行为。

### 注意事项

某些 UNIX 版本使用 `spell` 工具。在不带选项的情况下，`spell` 会将拼写错误的单词列表写入标准输出。使用 `ispell` 编写的等效命令是：

```
$ ispell -l < inputfile
```

`ispell` 工具并不是寻找错误的万无一失的方法。也不会检查拼写正确但使用不当的单词（例如下面倒数第二个例子中的 `quiet`）。

`ispell` 工具的接口设计用于用于通过管道从其他程序调用。如需了解更多信息，请参阅 `ispell` 手页中的 `-a` `-A` 选项。

## 示例

以下示例使用 `ispell` 修正检查文件中的拼写。

```
$ cat check
Here's a document for teh ispell utilitee
to check. It obviously needs proving
quiet badly.
```

第一个示例使用了不带选项的 `ispell`。显示了第一个拼写错误的单词 `teh` 的屏幕界面。屏幕底部是此时可以给出的命令菜单。这七个数字都与拼写错误的单词略有不同。

```
$ ispell check          File: check
teh
0: eh
1: tea
2: tech
3: tee
4: ten
5: TeX
6: Tex
7: the
Here's a document for teh ispell utilitee
[SP] <number> R)epl A)cept Insert L)ookup Uncap Quit e(X)it or ? for help
```

下一个示例使用了 `-S` 选项，以便建议的替换项按正确概率进行排序。

```
$ ispell -S check
teh      File: check
0: tech
1: the
2: eh
3: tea
4: tee
5: ten
6: Tex
7: teX
Here's a document for teh ispell utiliteit
[SP] <number> R)ejpl A)cept Insert I)ookup U)ncap Quit e(X)it or ? for help
```

下一个示例使用列表模式来显示拼写错误的单词列表。单词 `quiet` 不在列表中——它虽然使用不当，但拼写是正确的。

```
$ ispell -l < check
teh
ispell
utiliteit
obviously
```

最后一个示例也使用了 `ispell` 命令的第二形式。它展示了用单个命令检查单词拼写的快速方法。给 `ispell` 的输入是拼错误的，因此 `ispell` 将其写入标准输出。

```
$ echo seperate | ispell -l
seperate
```

## kill

| kill | 终止进程 |
| :--- | :--- |
| 语法: | `kill [option] PID-list` |

### 总结

`kill` 工具通过向进程发送信号来终止一个或多个进程。默认情况下，`kill` 发软件终止信号（信号 15），尽管一个选项允许你发送不同的信号。进程必须属于执行 `kill` 的用户，超级用户可以终止任何进程。`kill` 在终止进程时会显示消息。

在命令的第二种形式中，`kill` 显示所有可用信号名称的列表。你可以在 `kill` 工具中使用数字或信号名称，尽管名称更具描述性。

### 参数

`PID-list` 包含 `kill` 要终止的进程的进程标识符 (`PID`)。

### 选项

你可以在 `PID-list` 之前指定一个带有连字符的信号数字或名称作为选项，导致 `kill` 向进程发送你指定的信号。

### 注意事项

当你启动进程时，shell 会显示后台进程的 `PID` 号。你也可以使用 `ps` 工具来确定 `PID` 号。

如果软件终止信号没有终止进程，请尝试使用 `KILL` 信号（信号 9）。进程可以选择忽略 `KILL` 之外的任何信号。

`kill` 内置于 `bash`、`tsh` 和 `zsh`。当你使用这些 shell 之一时，可以使用作业标识符代替 `PID-list`。作业标识符由百分比 (`%`) 后跟作业编号或唯一标识作业的字符串组成。内置的 `kill` 版本还允许你通过名称而非数字来指定信号。你可以使用 `kill -l` 命令列出信号名称。

要终止当前登录进程启动的所有进程并让操作系统注销，请执行命令 `kill -9 0`。

## 警告

如果你以超级用户身份并运行命令 `kill -9 0`，你将导致系统崩溃。

## 示例

第一个示例显示了命令行执行 `compute` 文件作为后台进程，以及 `kill` 工具终止它：

```
$ compute &
[2] 259
$ kill 259
$
[2] + terminated compute
```

下一个示例显示了 `ps` 工具确定运行名为 `xprog` 程序的后台进程的 `PID` 号，以及 `kill` 工具用 `KILL` 信号终止了 `xprog`：

```
$ ps
PID TTY STAT TIME COMMAND
116 1 S 0:00 -zsh
128 1 S N 0:00 xinit/home/alex/.xinitrc --
137 1 S N 0:01 fwwm
... (省略重复部分) ...
$ kill -l |
```

## less

- `h` 或 `H`: 显示所有可用命令的摘要。摘要使用 `less` 显示，因为命令列表可能跨越了典型显示器的多个屏幕。
- `nSPACE`: 显示后续 `n` 行文本。由于 `n` 的默认值是屏幕大小，单独使用 `SPACE` 会显示下一页内容。
- `nz`: 功能与 `nSPACE` 类似，但如果提供了 `n`，它将成为 `z` 和 `SPACE` 命令的新默认值。
- `nRETURN` 或 `nj`: 向前滚动 `n` 行。`n` 的默认值为 1。
- `nd` 或 `nCONTROL-D`: 向前滚动 `n` 行。`n` 的默认值是屏幕大小的一半。如果你指定了 `n`，它将成为该命令的新默认值。
- `nb` 或 `nCONTROL-B`: 向后滚动 `n` 行。`n` 的默认值是屏幕大小。
- `nw`: 向后滚动与上一个命令相同，但 `n` 的值成为该命令的新默认值。
- `ny` 或 `nk`: 向后滚动 `n` 行。`n` 的默认值为 1。
- `nu` 或 `nCONTROL-U`: 向后滚动 `n` 行。`n` 的默认值是屏幕大小的一半。如果你指定了 `n`，它将成为该命令的默认值。
- `ng`: 跳到第 `n` 行。如果文件是分部分读取的（readpart）且你还没有移动得太远，此命令可能有效。`n` 的默认值为 1。
- `/regular-expression`: 在文件中向前跳过查找 `regular-expression` 字符串。如果你用感叹号 (`!`) 开头正则表达式，则该命令将查找不匹配 `regular-expression` 的字符串。如果正则表达式以星号 (`*`) 开头，则该命令将继续搜索文件列表。如果正则表达式以脱号 (`^`) 开头，则该命令从文件列表开始搜索并持续到文件列表末尾。
- `?regular-expression`: 该命令与上一个相似，但它是反向搜索文件（以及文件列表）。正则表达式中以星号 (`*`) 作为第一个字符将使搜索继续向后穿过文件列表和第一个文件。`at` 符号 (`@`) 会使搜索从文件列表中文件的最后一行开始，并向文件的第一行进行推进。
- `{` 或 `(` 或 `|`: 如果这些字符出现在显示器的第一行，此命令将滚动到匹配的右大括号、括号或方括号（即输入 `{` 会导致 `less` 移动到匹配的 `}`）。
- `}` `)` 或 `|`: 与上述命令类似，这些命令将你向后移动到匹配的左大括号、括号或方括号。
- `CONTROL-L`: 重绘屏幕。如果屏幕上的文本变得乱码，此命令非常有用。
- `F`: 向前滚动。如果到达输入文件的结尾，此选项将等待更多输入然后继续滚动。此选项允许你以类似于 `tail -f` 的方式使用 `less`，但 `less` 会按输出出现的形式分页。
- `n:n`: 跳到文件列表中的下一个文件。如果给了 `n`，则跳到文件列表中的第 `n` 个文件。此命令将当前文件连同当前行进入编辑器。`less` 工具使用环境变量 `EDITOR` 中指定的编辑器。如果未设置 `EDITOR`，`less` 使用 `vi`。
- `v`: 此命令在 `SHELL` 环境变量指定的 shell（或默认的 `sh`，通常链接到 `bash`）下执行命令行。命令行上的百分号 (`%`) 会被替换为当前文件名。如果省略了命令行，`less` 将启动一个交互式 shell。
- `q` 或 `Q`: 此命令终止 `less`。

## 示例

以下示例显示了 `memo.txt` 文件。要查看文件的更多内容，用户在屏幕左下角的 `less` 提示处按下 `SPACE` 键。

```
$ less memo.txt
memo.txt SPACE
```

在下一个示例中，用户将提示符更改为更有意义的消息，并使用了 `-N` 选项显示行号。最后，用户指示 `less` 向前跳到包含该字符串的第一行。

```
$ less -P"to continue, q to quit" -N +/cut.ic
28 procedure main(args)
29 local filelist, arg, fields, delim
30 
31 filelist=[]
45 # Check for real field list
46 #
47 if /fields "-FIELD_LIST is required."
48
49 # Process the files and output the fields
ter SPACE to continue, q to quit
```

## In

| 语法 |
| :--- |
| `In [options] existing-file new-link` |
| `In [options] existing-file-list directory` |

### 摘要

默认情况下，`In` 创建硬链接。指向文件的硬链接与原始文件名没有区别。你可以通过其原始文件名或 `In` 命令赋予它的名称来引用该文件，无论是哪种情况，效果都是相同的。对文件的所有硬链接都必须与原始文件位于同一个文件系统中。

当你使用 `In` 时，你可以使用第一种格式在现有文件和新文件名之间创建链接。你可以使用第二种格式将文件链接到不同的目录。新链接与原始文件具有相同的文件名，但路径不同。

当你使用 `In` 创建符号链接（软链接）而硬硬链接时。与符号链接不同，符号链接可以存在于与链接文件不同的文件系统中。此外，符号链接可以连接到目录。关于符号链接的更多信息，请参阅第 85 页。

### 参数

`existing-file` 是你想要创建链接的文件路径。`new-link` 是新链接的名称。

### Options

- `-backup (-b)`: 如果 `In` 移除文件，则此选项创建一个备份。
- `-force (-f)`: 通常情况下，如果 `new-link` 已存在，才会创建链接。
- `-interactive (-i)`: 如果 `new-link` 已存在，此选项会询问你。
- `-symbolic (-s)`: 创建符号链接。当你使用此选项时，`existing-file` 可能位于不同的文件系统。参阅“符号链接”第 85 页。

### Notes

硬链接是目录中的一个项，指向一个文件。当你使用编辑器、程序或重定向输出创建文件时，操作系统创建该链接。`ls -l` 显示文件有多少个链接。参阅“链接”第 82 页。

如果 `new-link` 是一个现有文件名，`ln` 不创建链接（除非你使用 `-force` 选项）。

你可以使用符号链接跨文件系统并链接目录。当你使用 `ls -l` 命令列出符号链接的信息时，`ls` 显示链接的目标名称。

## Examples

第一个示例显示了 `memo.txt` 文件。要查看文件的更多内容，用户在屏幕左下角的 `less` 提示处按下 `SPACE` 键。

```
$ less memo.txt
memo.txt SPACE
```

在示例示例中，用户将提示符更改为更有意义的消息，并使用了 `-N` 选项显示行号。最后，用户指示 `less` 向前跳到包含该字符串的第一行。

```
$ less -P"to continue, q to quit" -N +/cut.ic
28 procedure main(args)
29 local filelist, arg, fields, delim
30
31 filelist=[]
45 # Check for real field list
46 #
47 if /fields "-FIELD_LIST is required."
48
```
