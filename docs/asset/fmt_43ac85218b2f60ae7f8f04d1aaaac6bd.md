
## 重定向输出可能会破坏文件

取决于你正在使用哪种 shell 以及你的环境是如何设置的，如下命令可能会给你你不预期的结果：

```bash
$ cat orange > orange

cat: orange: is busy
```

尽管 `cat orange` 显示了错误消息，shell 仍然会继续并破坏 `orange` 文件的内容。当你看到重定向符号（`>`）时，shell 操作是移除 `orange` 文件的内容。如果你想合并两个文件，使用 `cat` 将两个文件放入临时文件，然后使用 `mv` 将其命名：

```bash
$ cat orange > temp

$ mv temp orange
```

在下一个示例中发生可能会更糟：

```bash
$ grep apple b > a

grep: b: No such file or directory
```

## 信任 `nolobber`

## 将标准输出追加到文件

追加符号（`>>`）会导致 shell 向文件末尾添加新信息，保留原有的任何信息。以下命令演示了追加输出：

```bash
$ cat orange

this is orange

$ cat pear >> orange

$ cat orange

this is orange

this is pear
```

你首先看到 `orange` 文件的内容。接下来，`pear` 文件的内容被添加到 `orange` 文件的末尾（与其合并）。

5-11 显示了如何创建一个包含日期和时间（`date` 的输出）的文件，随后是登录列表（`who` 的输出）。图 5-11 中的第一行将 `date` 的输出重定向到文件名 `whoson`。接下来，示例将 `who` 的输出追加到 `whoson` 文件。最后，`cat` 显示了包含两个工具输出的文件。

这种技术在使用两步程序更为简单，但你必须小心包含两个大于号。如果你不小心只用了一个，且 `nolobber` 功能未开启，你将覆盖 `orange` 文件。即使你开启了 `nolobber` 功能，对你正在操作的文件保留备份副本也是好主意，以防出错。

## `/dev/null`：数据汇点

`/dev/null` 设备是一个数据汇点，通常被称为比特桶。你可以将不想保留或查看的输出重定向到 `/dev/null`。输出将无痕消失：

```bash
$ echo "hi there" > /dev/null
```

当你从 `/dev/null` 读取时，你会得到一个空字符串。执行以下 `cat` 命令可以将名为 `messages` 的文件截断为零长度，同时保留文件的所有权和权限：

```bash
$ ls -1 messages

-rw-r--r-- 1 alex pubs 25315 Oct 24 10:55 messages

$ cat /dev/null > messages

$ ls -1 messages

-rw-r--r-- 1 alex pubs 0 Oct 24 11:02 messages
```

```bash
$ date >whoson

$ cat whoson

Thu Mar 27 14:31:18 PST 2003

$ who >>whoson

$ cat whoson

Thu Mar 27 14:31:18 PST 2003

root     console    Mar 27 05:00(::0)

alex      pts/4       Mar 27 12:23(::0)

alex      pts/5       Mar 27 12:33(::0)

jenny    pts/7       Mar 26 08:45 (bravo.tcorp.com)
```

**图 5-11 重定向和追加输出**

## 管道

Shell 使用管道（pipe）将一个命令的标准输出直接连接到另一个命令的标准输入。管道（有时称为流水）的效果与将一个命令的标准输出重定向到文件，并使用该文件作为另一个命令的标准输入相同。管道消除了单独的命令和中间文件。管道的符号是竖线（`|`）。使用管道的命令行语法为：

```bash
command_a [arguments] | command_b [arguments]
```

此命令行使用管道生成与以下一组命令行产生相同的结果：

```bash
command_a [arguments] > temp

command_b [arguments] < temp

trm temp
```

在上述命令序列中，第一行将 `command_a` 的标准输出重定向到名为 `temp` 的中间文件。第二行将 `command_b` 的标准输入重定向自 `temp`。最后一行删除 `temp`。使用管道的命令不仅更容易输入，而且通常效率，因为它不需要创建临时文件。

你可以将管道与 GNU/Linux 工具类的成员结合，这些工具接受从命令行指定的文件或从标准输入的内容。你也可以将管道与仅接受标准输入命令结合使用。例如，`tr`（翻译）工具（第三部分第 1362 页）从标准输入获取输入。在最简单的情况下，`tr` 具有以下格式：

```bash
tr string1 string2
```

```bash
$ ls > temp

$ lpr temp

$ rm temp

或者

$ ls | lpr

$
```

**图 5-12 管道**

`tr` 工具从标准输入接受输入，并寻找与 `string1` 中字符匹配的字符。找到匹配后，`tr` 将 `string1` 中的字符翻译为 `string2` 中对应的字符。（`string1` 中的第一个字符翻译为 `string2` 中的第一个字符，依此类推）。在接下来的示例中，`tr` 显示抽象文件的内容，其中字母 a、b 和 c 分别被翻译为 A、B 和 C：

```bash
$ cat abstract | tr abc ABC
```

```bash
$ tr abc ABC < abstract
```

`tr` 不改变原始文件的内容。`lpr`（行打印机）工具是接受来自文件或标准输入输入的工具之一。当你在命令行上输入文件名并执行 `lpr` 时，它会将文件放入打印队列。当你没有在命令行上指定文件名时，`lpr` 从标准输入获取输入。此功能使我们能够使用管道将输入重定向到 `lpr`。图 5-12 中的第一组命令显示了如何使用 `ls` 和 `lpr` 配合中间文件（`temp`）将工作目录中的文件列表发送到打印机。如果 `temp` 文件存在，则第一个命令将覆盖其内容。第二组命令使用管道将相同的列表（`temp` 除外）发送到打印机。

图 5-13 中的命令将 `who` 工具的输出重定向到 `temp`，然后按排序顺序显示此文件。`sort` 工具（第 66 页）从以下位置获取输入：

```bash
| who > temp |
| $ sort < temp |
| alex pts/4 Mar 27 12:23 |
| alex pts/5 Mar 27 12:33 |
| jenny pts/7 Mar 26 08:45 |
| root console Mar 27 05:00 |
```

**图 5-13 使用临时文件存储中间结果**

```bash
$ who | sort

alex pts/4 Mar 27 12:23

alex pts/5 Mar 27 12:33

jenny pts/7 Mar 27 08:45

root console Mar 27 05:00
```

**图 5-14** 替代临时文件工作的管道

从命令行指定的文件，或者在未指定文件时，从标准输入的命令行，并将其输出发送到标准输出。图 5-13 中的 `sort` 命令行从标准输入获取输入，重定向（`<`）自 `temp`。`sort` 发送到屏幕的输出列出了按排序（字母顺序）排列的用户。

由于 `sort` 可以从标准输入或文件名获取输入，你可以省略图 5-13 中的 `<` 符号以获得相同的结果。

图 5-14 在不创建 `temp` 文件的情况下实现了相同的结果。通过使用管道，Shell 将 `who` 的输出重定向到 `sort` 的输入。`sort` 工具从标准输入接受输入，因为命令行中后面没有文件名。

当有许多人正在使用系统，而你只想获取其中一个人的信息时，可以将 `who` 的输出发送到 `grep`：

```bash
$ who | grep 'root'

root console Mar 27 05:00
```

处理长到屏幕无法显示的输出（例如文件列表）的另一种方法是使用 `less`：

```bash
$ ls | less
```

## 过滤器

过滤器是一个处理输入流以产生输出流的程序。Shell 使用管道将一个命令的标准输出直接连接到另一个命令的标准输入。管道（有时称为流水）的效果与将一个命令的标准输出重定向到文件，并使用该文件作为另一个命令的标准输入相同。管道消除了单独的命令和中间文件。管道的符号是竖线（`|`）。使用管道的命令行语法为：

```bash
```
