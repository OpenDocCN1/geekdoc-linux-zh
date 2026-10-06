
最近修改时间（目标文件比源文件新），mv 不会用源文件替换它。

- 标记命令行上选项的结束和文件名的开始。此选项使得移动以连字符开头名称的文件成为可能。如果没有此选项，mv 会报错该文件是一个无效选项。

# 注意事项

GNU `mv` 的实现方式与 `in` 和 `rm` 一。当你执行 `mv` 工具时，它首先为新文件创建一个链接（`ln`），然后删除（`rm`）现有文件。如果新文件已存在，`mv` 可能会在创建链接之前删除它。

与 `rm` 一样，你必须对现有文件的父目录具有写入和访问权限，但不需要对文件本身具有读取或写入权限。如果移动操作将覆盖一个你没有写入权限的现有文件，`mv` 将显示访问权限并等待响应。如果你输入 `y` 或 `yes`，`mv` 将重命名文件；否则，如果你没有使用 `-f` 选项，`mv` 不会提示你响应，而是直接覆盖该文件。

如果现有文件和新文件目录位于不同的文件系统，GNU `mv` 将复制文件而不是重命名它。在这种情况下，文件复制完成后，移动它的用户将成为该文件的所有者。

虽然早期版本的 `mv` 只能在文件系统之间移动普通文件，但 `mv` 现在可以将任何类型的文件（包括目录和设备文件）从一个文件系统移动到另一个。

# 示例

第一条命令行将工作目录下的 letter 重命名为 `letter.1201`：

```
$ mv letter.1201
```

下一条命令行重命名该文件，使其以相同的文件名出现在 `/usr/archives` 目录下：

```
$ mv letter.1201 /usr/archives
```

接下来的命令行将工作目录下所有名称以 `memo` 开头的文件重命名，以便它们出现在 `/usr/backup` 目录下：

```
$ mv memo* /usr/backup
```

下一个示例显示了 `-u` 选项如何防止 `mv` 用旧文件替换文件。在 `memo` 目录中的 `memo` 文件比父目录中的版本新，因此它不会被 `mv` 命令替换。此示例还显示了 `mv` 在替换由 Jenny 拥有的 `memos/memo1` 文件之前如何向 Alex（执行命令的人）发出提示：

```
$ ls -l
total 4
-rw-rw-r-- 1 alex group 14 Jul 30 01:38 memo1
-rw-rw-r-- 1 alex group 14 Jul 30 01:38 memo2
-rw-rw-r-- 1 alex group 14 Jul 30 01:35 memo3
drwxrwxr-x 2 alex group 1024 Jul 30 01:08 memos
```

```
$ ls -l memos
total 3
-rw-rw-r-- 1 jenny group 14 Jul 30 01:34 memo
-rw-rw-r-- 1 alex group 14 Jul 30 01:35 memo2
-rw-rw-r-- 1 alex group 20 Jul 30 01:36 memo3
```

```
$ mv -u memo[1-3] memos
mv: replace 'memos/memo1', overriding mode 0644? y
```

```
$ ls -l memos
total 2
-rw-rw-r-- 1 alex group 14 Jul 30 01:35 memo3
drwxrwxr-x 2 alex group 1024 Jul 30 01:08 memos
```

```
$ ls -l memos
total 3
-rw-rw-r-- 1 alex group 14 Jul 30 01:38 memo1
-rw-rw-r-- 1 alex group 14 Jul 30 01:38 memo2
-rw-rw-r-- 1 alex group 20 Jul 30 01:36 memo3
```

# nice

更改命令的优先级

nice [option] [command line]

`nice` 工具报告 shell 的优先级，或者更改命令行的优先级。普通用户可以降低命令的优先级。只有超级用户（Superuser）可以增加命令的优先级。TC Shell 具有一个 `nice` 内置命令，语法不同。请参阅“注意事项”。

命令行是你想要以不同优先级执行的命令。如果没有任何选项或参数，`nice` 会报告运行 `nice` 命令的 shell 的优先级。

# 参数

# 选项

如果没有指定选项，`nice` 默认调整值为 10，通常从 0 到 10。（随着优先级值的增加，`nice` 命令运行的优先级越低。）

- - n value 通过 `value` 调整来更改优先级。优先级范围从 -20（最高优先级）到 19（最低优先级）。正值降低优先级，而负值提高优先级。只有超级用户可以指定负值。当你指定的值超出此范围的任一端时，优先级将被设置为范围的限制值。

# 注意事项

TC Shell 有一个 `nice` 内置命令。在测试下，`nice ±value` 命令行会更改命令行运行的优先级。对于正值必须包含加号。

更高的（更正的）优先级值意味着内核调度任务的频率较低，而（更负的）值会导致任务被更频繁地调度。

当超级用户调度任务时，任务以更高的优先级运行。使用 `nice` 负值。

# 示例

以下命令以最低优先级运行 `find`：

```bash
nice -n 19 find / -name "core"
```

# nohup

在退出后继续运行命令

nohup [command line]

`nohup` 工具运行命令并在退出后保持运行。TC Shell 具有一个 `nohup` 内置命令。

# 参数

命令行是你想要执行的命令行。

# 注意事项

`nohup` 允许你在退出后继续运行命令。TC Shell 有一个 `nohup` 内置命令。

# 示例

以下命令在后台运行 `find`：

```bash
nohup find / -name core &
```

# od

转储文件内容

od [options] [file-list]

`od`（八进制 dump）工具导出文件的内容，对于查看可执行（对象）文件和带有非打印字符的文本文件有用。它从你指定的文件或标准输入读取内容。

# 参数

file-list 包括显示的文件路径。如果你没有指定 file-list，`od` 从标准输入读取。

# 选项

- --address-radix=base 显示偏移量时使用的基数。默认情况下，偏移量以八进制给出。
- --format=type t 显示文件数据时使用的输出格式。你可以重复此选项并使用不同类型查看文件的多种格式。`type` 的可能值为
- 命名字符。非打印字符使用其官方名称显示。例如，FEED 显示为 `ff`。
- ASCII 字符。
- d 有符号小数。
- f 浮点数。
- o 八进制（默认）。
- u 无符号小数。
- x 十六进制。

`od` 工具将某些非打印字符显示为带有反斜线的打印字符（见表 III-22）。它将文件中不在非打印字符显示为三位八进制数。

# 符号

| 符号 | |
| \0 | NULL |
| \a | BELL |
| \b | BACKSPACE |
| \f | FEED |
| \n | NEWLINE |
| \r | RETURN |
| \t | HORIZONTAL TAB |
| \v | VERTICAL TAB |

默认情况下，`od` 将文件转储为 2字节八进制数。你可以更改它转储的类型以及组成每个数字读取的字节数。表 III-23 中的类型可以加上表 III-24 中的长度指示器。

# type

| 类型 | 说明 |
| d (小数) | 以有符号小数显示数据 |
| o (八进制) | 以无符号八进制值显示数据 |
| u (无符号小数) | 以无符号小数显示数据 |
| x (十六进制) | 以无符号十六进制值显示数据 |

表 III-24 中的长度指示器可以跟在任何 d、o、u 或 x 类型之后，以指示组成每个数字应读取的字节数。

