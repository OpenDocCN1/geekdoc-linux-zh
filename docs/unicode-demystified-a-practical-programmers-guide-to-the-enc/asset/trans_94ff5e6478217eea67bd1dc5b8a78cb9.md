

![](img/aa8214d49e1cf50152c432845129fb3b_195_0.png)

图 5-6 重定向标准输入

现在 `sample.txt` 文件包含了你输入的文本。你可以使用 `cat` 配合参数 `sample.txt` 来显示该文件。下一节将展示使用 `cat` 显示文件的另一种方法。

## 重定向输出可能会破坏文件

在将输出重定向到文件时要格外小心。如果文件存在，shell 将覆盖它并破坏其内容。更多信息请参阅第 149 页上名为“重定向输出可能会破坏文件 II”的警告。

图 5-7 显示了重定向 `cat` 的输出是一种无需使用编辑器创建文件的方便方法。缺点是一旦你输入了一行并按下回车键，你就无法编辑该文本了。在你输入行时，删除（erase）和杀死（kill）键可以删除文本。此程序适用于创建短简单的文件。

```
$ cat > sample.txt
This text is being entered at the keyboard.
Cat is copying it to a file.
Press CONTROL-D to indicate the
End of File.
$ 
```

图 5-7 输出重定向的 `cat`

图 5-8 显示了如何使用 `cat` 并重定向输出符号将多个文件合并（catenate，即一个接一个连接：这也是 `cat` 工具名称的由来）成一个更大的文件。前三个命令显示了三个文件的内容：

```
$ cat stationery
2000 sheets letterhead ordered: 10/7/02
$ cat tape
1 masking tape ordered: 10/14/02
5 boxes filament tape ordered: 10/28/02
$ cat pens
12 doz. black pens ordered: 10/4/02
$ cat stationery tape pens > supply_orders
$ cat supply_orders
2000 sheets letterhead ordered: 10/7/02
1 masking tape ordered: 10/14/02
5 boxes filament tape ordered: 10/28/02
12 doz. black pens ordered: 10/4/02
```

图 5-8 使用 `cat` 合并文件

stationary、tape 和 pens。下一条命令显示了带有三个文件名作为参数的 `cat`。当你带入一个或或多个文件名调用它时，`cat` 会逐个将文件复制到标准输出。在这种情况下，标准输出被重定向到文件 `supply_orders`。最后一个 `cat` 命令显示 `supply_orders` 包含了所有三个文件的内容。

## 重定向标准输入

就像你可以重定向标准输出一样，你也可以重定向标准输入。重定向符号 (`<`) 指示 shell 从指定的文件而不是键盘重定向命令的输入（图 5-9）。重定向输入的命令行格式如下：

```bash
command [arguments] < filename
```

其中 `command` 是任何可执行程序（如应用程序或工具），`arguments` 是可选参数，而 `filename` 是 shell 从其重定向输入的普通文件名称。

图 5-10 显示了 `cat` 的输入重定向自图 5-8 创建的 `supply_orders` 文件，而标准输出则去往屏幕。这种设置导致 `cat` 在屏幕上显示示例文件。系统在普通文件的末尾自动提供 EOF（文件结束）信号，因此不需要 CTRL-D。

提供输入重定向自文件的 `cat` 命令产生的结果与提供文件名作为参数的 `cat` 命令的结果相同。`cat` 工具是 GNU/Linux 工具类的一员，它们以这种方式工作。

![](img/aa8214d49e1cf50152c432845129fb3b_197_0.png)

图 5-9 重定向标准输入

此类工具的其他一些成员包括 `ip`、`sort` 和 `grep`。这些工具首先检查你用于调用它们的命令行。如果你在命令行中包含文件名，该工具将从你指定的文件获取输入。如果你不指定文件名，该工具将从标准输入获取输入。以这种方式工作的是工具或程序，而不是 shell 或操作系统。

```bash
$ cat supply_orders
2000 sheets letterhead ordered: 10/7/02
1 box masking tape ordered: 10/14/02
5 boxes filament tape ordered: 10/28/02
12 doz. black pens ordered: 10/4/02
```

图 5-10 输入重定向的 `cat`

shell 提供了一个名为 `nolobber`（第 554 页）的功能，防止你无意中通过重定向覆盖现有文件。当你通过设置 `nolobber` 变量来启用此功能并尝试将输出重定向到现有文件时，shell 会显示错误信息且不执行命令。如果前面的示例导致了以下消息之一，则说明 `nolobber` 功能正在生效。以下示例在每种主要的 shell 中设置了 `nolobber`，尝试将 `echo` 的输出重定向到现有文件，然后取消了 `nolobber`：

```bash
bash $ set -nlobber
bash $ echo "hi there" > tmp
bash: tmp: Cannot overwrite existing file
bash $ set +nlobber
```

## 重定向输出可能会破坏文件

取决于你正在使用哪种 shell 以及你的环境是如何设置的，如下命令可能会给你你不预期的结果：

```bash
$ cat orange > orange
cat: orange: is busy
```

尽管 `cat orange` 显示了错误消息，shell 仍然会继续并破坏 orange 文件的内容。当你看到重定向符号 (`>`) 时，shell 操作是移除 orange 文件的内容。如果你想合并两个文件，使用 `cat` 将两个文件放入临时文件，然后使用 `mv` 将其命名：

```bash
$ cat orange > temp
$ mv temp orange
```

在下一个示例中发生可能会更糟：

```bash
$ grep apple b > a
grep: b: No such file or directory
```

## 信任 nolobber

## 将标准输出追加到文件

追加符号 (`>>`) 会导致 shell 向文件末尾添加新信息，保留原有的任何信息。以下命令演示了追加输出：

```bash
$ cat orange
this is orange
$ cat pear >> orange
$ cat orange
this is orange
this is pear
```

你首先看到 orange 文件的内容。接下来，pear 文件的内容被添加到 orange 文件的末尾（与其合并）。

5-11 显示了如何创建一个包含日期和时间（`date` 的输出）的文件，随后是登录列表（`who` 的输出）。图 5-11 中的第一行将 `date` 的输出重定向到文件名 `whoson`。接下来，示例将 `who` 的输出追加到 `whoson` 文件。最后，`cat` 显示了包含两个工具输出的文件。

这种技术在使用两步程序更为简单，但你必须小心包含两个大于号。如果你不小心只用了一个，且 `nolobber` 功能未开启，你将覆盖 orange 文件。即使你开启了 `nolobber` 功能，对你正在操作的文件保留备份副本也是好主意，以防出错。

## /dev/null：数据汇点

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

