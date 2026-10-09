
![](img/243613168ac865b539f12460d966088e_209_0.png)

（这是你）输入的内容。cat 实用工具正在工作。由于 shell 将 cat 的标准输入与键盘关联，并将 cat 的标准输出与屏幕关联，因此当你输入一行文本时，cat 会将文本从标准输入（键盘）复制到标准输出（屏幕）。下一个示例展示了这一交互过程。

```
$ cat
This is a line of text.
This is a line of text.
Cat keeps copying lines of text
Cat keeps copying lines of text
until you press CONTROL-D at the beginning
until you press CONTROL-D at the beginning
of a line.
of a line.
CONTROL-D
$
```

cat 实用工具会不断复制文本，直到你在单独的一行中输入 CONTROL-D。按下 CONTROL-D 会导致 tty 设备驱动程序向 cat 发送一个 EOF（文件结束）信号。此信号告知 cat 它已达到标准输入的末尾，没有更多文本可供复制。然后，cat 实用工具结束执行并将控制权返回给 shell，shell 随后显示提示符。

## 重定向

“重定向”一词涵盖了你可以让 shell 改变命令的标准输入来源和标准输出去处的各种方式。默认情况下，shell 将命令的标准输入和标准输出分别与键盘和屏幕关联。通过将输入或输出与代表键盘或屏幕的设备文件以外的命令或文件进行关联，你可以让 shell 重定向任何命令的标准输入或标准输出。本节演示如何对文本文件和实用工具进行输入/输出重定向。

![](img/243613168ac865b539f12460d966088e_210_0.png)

图 5-4 重定向标准输出

### 重定向标准输出

*重定向输出符号*（`>`）指示 shell 将命令的输出重定向到指定的文件，而不是输出到屏幕（图 5-4）。重定向输出的命令行语法为

```
command [arguments] > filename
```

其中 *command* 是任何可执行程序（例如应用程序或实用工具），*arguments* 是可选参数，*filename* 是 shell 将输出重定向到的普通文件的名称。

下一个示例使用 *cat* 来演示输出重定向。此示例与第 153 页的示例形成对比，在该示例中，标准输入 *和* 标准输出都与键盘和屏幕关联。以下示例中的输入来自键盘。命令行上的重定向输出符号导致 shell 将 *cat* 的标准输出与此符号后指定的 *sample.txt* 文件关联。

```
$ cat > sample.txt
This text is being entered at the keyboard and
cat is copying it to a file.
Press CONTROL-D to indicate the
end of file.
CONTROL-D
$
```

### 重定向输出可能会破坏文件！

在将输出重定向到文件时要谨慎。如果文件存在，shell 将覆盖该文件并破坏其内容。更多信息请参阅第 156 页的技巧“重定向输出可能会破坏文件！”。

在输入完命令并键入上一个示例中显示的文本后，*sample.txt* 文件将包含你输入的文本。你可以使用带有 *sample.txt* 作为参数的 *cat* 来显示此文件。下一节展示了另一种使用 *cat* 显示文件的方法。

前面的示例表明，从 *cat* 重定向标准输出是一种创建文件而无需使用编辑器的便捷方式。缺点是，一旦你输入一行并按下 RETURN 键，在你完成创建文件之前就无法编辑文本。在输入某一行时，擦除键和终止键可用于删除该行的文本。此步骤对于创建简短、简单的文件非常有用。

![](img/243613168ac865b539f12460d966088e_211_0.png)

图 5-5 重定向标准输入

下一个示例展示了如何运行 `cat` 并使用重定向输出符号将几个文件*串联*（catenate，即依次连接——这是 *cat* 实用工具名称的由来）到一个更大的文件中。前三个命令显示了三个文件的内容：*stationery*、*tape* 和 *pens*。下一条命令显示了带有三个文件名作为参数的 `cat`。当你调用它并指定多个文件名时，*cat* 逐个将这些文件复制到标准输出。该命令将标准输出重定向到名为 *supply_orders* 的文件。最后的 `cat` 命令表明 *supply_orders* 包含这三个原始文件的内容。

```
$ cat stationery
2,000 sheets letterhead ordered:      October 7
$ cat tape
1 box masking tape ordered:           October 14
5 boxes filament tape ordered:        October 28
$ cat pens
12 doz. black pens ordered:           October 4
```

```
$ cat stationery tape pens > supply_orders
```

```
$ cat supply_orders
2,000 sheets letterhead ordered:      October 7
1 box masking tape ordered:           October 14
5 boxes filament tape ordered:        October 28
12 doz. black pens ordered:           October 4
```

### 重定向标准输入

就像你可以重定向标准输出一样，你也可以重定向标准输入。*重定向输入符号*（`<`）指示 shell 将命令的输入重定向为来自指定文件，而不是来自键盘（图 5-5）。重定向输入的命令行语法为

```
command [arguments] < filename
```

其中 *command* 是任何可执行程序（如应用程序或实用工具），*arguments* 是可选参数，*filename* 是 shell 从中重定向输入的普通文件的名称。

下一个示例显示了 `cat` 的输入从上一个示例中创建的 `supply_orders` 文件重定向，标准输出则去屏幕。这种设置导致 `cat` 在屏幕上显示 `supply_orders` 文件。系统会在普通文件末尾自动提供一个 EOF 信号。

```
$ cat < supply_orders
2,000 sheets letterhead ordered:	October 7
1 box masking tape ordered:		October 14
5 boxes filament tape ordered:		October 28
12 doz. black pens ordered:		October 4
```

使用从文件重定向输入的 `cat` 命令所产生的结果与使用文件名作为参数的 `cat` 命令所产生的结果相同。`cat` 实用工具是一类按此方式工作的实用工具的成员。此类实用工具的其他成员包括 `ls`、`sort`、`grep` 和 Perl。这些实用工具首先检查调用它们的命令行。如果命令行包含文件名作为参数，实用工具将从指定文件获取输入。如果没有文件名参数，实用工具将从标准输入获取输入。是实用工具或程序——而不是 shell 或操作系统——以这种方式工作。

### 重定向输出可能会破坏文件

根据你使用的 shell 以及环境设置方式，如下命令可能会产生意外结果：

```
$ cat orange pear > orange
cat: orange: input file is output file
```

尽管 `cat` 显示了一条错误消息，但 shell 破坏了现有 `orange` 文件的内容。新的 `orange` 文件将与 `pear` 具有相同的内容，因为 shell 看到重定向符号（`>`）时采取的第一个动作是删除原始 `orange` 文件的内容。如果你想将两个文件串联成一个，请使用 `cat` 将两个文件放入一个临时文件，然后使用 `mv` 重命名该临时文件：

```
$ cat orange pear > temp
$ mv temp orange
```

在下一个示例中发生的事情可能更糟。输入命令的用户想要搜索文件 `a`、`b` 和 `c` 中的单词 `apple`，并将 `grep`（第 232 页）的输出重定向到文件 `a.output`。不幸的是，用户将文件名输入为 `a output`，省略了句点并在其位置插入了一个空格：

```
$ grep apple a b c > a output
grep: output: No such file or directory
```

Shell 忠实地删除了 `a` 的内容，然后调用 `grep`。错误消息可能需要片刻时间才会出现，给人一种命令正常运行的错觉。即使你看到了错误消息，也可能需要一段时间才能意识到你已经破坏了 `a` 的内容。

### NoClobber：防止覆盖文件

shell 提供 `noclobber` 功能，可防止你使用重定向覆盖文件。使用 `set -o noclobber` 命令设置 `noclobber` 来启用此功能。带有 `+o` 的相同命令取消设置 `noclobber`。如果设置了 `noclobber`，当你将输出重定向到现有文件时，shell 会显示一条错误消息并且不执行该命令。以下示例使用 `touch` 创建一个文件，

