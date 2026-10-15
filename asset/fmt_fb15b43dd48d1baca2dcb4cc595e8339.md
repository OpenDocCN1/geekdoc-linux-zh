
其中 `command` 是任何可执行程序（如应用程序或工具），`arguments` 是可选参数，`filename` 是壳从其重定向输入的普通文件的名称。

| $ cat stationery | 10/7/10 |
| 2,000 sheets letterhead ordered: | |
| $ cat tape | |
| 1 box masking tape ordered: | 10/14/10 |
| 5 boxes filament tape ordered: | 10/28/10 |
| $ cat pens | |
| 12 doz. black pens ordered: | 10/4/10 |

```前三个命令显示了三个文件的内容：stationery、tape 和 pens。下一个命令显示了带有三个文件名的 cat。当你带有多个文件名调用它时，cat 会逐个复制文件到标准输出。此命令将标准输出重定向到文件 supply_orders。最后的 cat 命令显示 supply_orders 包含了三个原始文件的内容。```

## 第7章 外壳

![](img/c8ae2cd4d550a81142a3ed64b0f61f6a_298_0.png)

**图 7-9** 重定向标准输入

图 7-10 显示了 `cat` 的输入重定向自图 7-8 中创建的 `supply_orders` 文件，而标准输出重定向到屏幕。这种设置使得 `cat` 将示例文件显示在屏幕上。系统在普通输入结束时会自动提供一个 EOF 信号。

实用程序从文件或标准输入获取输入

给 `cat` 提供一个从文件重定向的输入，与将文件名作为参数传递给 `cat` 命令的结果相同。`cat` 实用程序是 Linux 实用程序的一员，以这种方式工作。该类实用程序的其他成员包括 `lp`、`sort`、`grep` 和 `perl`。这些实用程序首先检查你调用的命令。如果你在命令行上提供文件名，实用程序将从你指定的文件获取输入。如果你没有指定文件名，实用程序将从标准输入获取输入。以这种方式工作的是实用程序或程序，而不是 shell 或操作系统。

### noclobber: 避免覆盖文件

shell 提供了 `noclobber` 功能，防止使用重定向覆盖文件。通过使用命令 `-o noclobber` 设置 `noclobber` 来启用此功能。使用相同的命令并配合 `+o` 则取消 `noclobber`。在设置了 `noclobber` 的情况下，如果你将输出重定向到一个现有文件，shell 将显示错误消息且不执行命令。以下示例使用 `touch` 创建文件，设置 `noclobber`，尝试将 `echo` 的输出重定向到新创建的文件，取消 `noclobber` 设置，然后执行重定向：

```bash
$ tmp
$ set -o noclobber
$ echo "hi there" > tmp
bash: tmp: cannot overwrite existing file
$ set +o noclobber
$ echo "hi there" > tmp
```

你可以通过在重定向符号 (`>`) 之后放置管道符号来覆盖 `noclobber`。在接下来的示例中，用户通过重定向 `date` 的输出创建一个文件。

```bash
$ cat supply_orders
2,000 sheets letterhead ordered: 10/7/10
1 box masking tape ordered: 10/14/1
5 boxes filament tape ordered: 10/28/10
12 doz. black pens ordered: 10/4/10
```

图 7-10 输入重定向的 cat

接下来用户设置了 `noclobber` 变量并将输出重定向到同一个文件。shell 显示了错误消息。然后用户在重定向符号后使用管道符号，shell 允许用户覆盖文件。

```bash
$ date > temp2
$ set -o noclobber
$ date > temp2
bash: temp2: cannot overwrite existing file
$ date > | temp2
```

### 重定向输出可能会破坏文件

取决于你的使用方式以及环境的设置，如下所示命令可能会产生意外的结果：

```bash
$ cat pear > orange
cat: orange: input file is output file
```

尽管 `cat` 显示了错误消息，但 shell 仍然破坏了现有 `orange` 文件的内容。新的 `orange` 文件将与 `pear` 同名，因为 shell 在看到重定向符号 (`>`) 时采取的首要操作是移除原始 `orange` 文件的内容。如果你想将两个文件合并为一个文件，可以将它们切到一个临时文件中，并使用 `mv` 重命名这个第三个文件：

```bash
$ cat orange > temp
$ mv temp orange
```

在下一个示例中发生的情况，用户可以通过命令搜索文件 `a`、`b` 和 `c` 中的单词 `"apple"`，并将 `grep`（第 166 页）的输出重定向到文件 `a.output` 来看到。遗憾的是，用户输入了文件名 `a output`，漏掉了点并在其位置插入了空格：

```bash
$ grep apple a b c > output
grep: output: No such file or directory
```

shell 顺从地删除 `a` 的内容，然后调用 `grep`。错误消息可能过了一会儿才会出现，让你觉得命令正在正常运行。即使在看到错误消息后，可能也需要一段时间才能意识到你已经破坏了 `a` 的内容。

### 将标准输出追加到文件

追加输出符号 (`>>`) 会导致 shell 将新添加到文件末尾，同时保持现有信息完整。该符号提供了一种将两个文件合并为一个方便方法。以下命令演示了追加输出符号的作用。第二个命令完成了上述警告框中描述的合并操作：

```bash
$ date > whoson
$ cat whoson
Sat Mar 27 14:31:18 PST 2010
$ who >> whoson
$ cat whoson
Sat Mar 27 14:31:18 PST 2010
sam      console      2010-03-27 05:00(:0)
max      pts/4       2010-03-27 12:23(:.0)
max      pts/5       2010-03-27 13:33(:.0)
zach     pts/7       2010-03-26 08:45 (bravo.example.com)
```

图 7-11 重定向并追加输出

```bash
$ cat orange
this is orange
$ cat pear >> orange
$ cat orange
this is orange
this is pear
```

第一个命令显示 `orange` 文件的内容。第二个命令将 `pear` 文件的内容追加到 `orange` 文件中。最后的 `cat` 显示了结果。

### 不要信任 noclobber

追加输出比上述警告框中描述的两个步骤程序要简单，但你必须对这两个符号都小心。如果你不小心只使用其中一个且未设置 `noclobber` 功能，shell 将覆盖 `orange` 文件。即使你开启了 `noclobber` 功能，为你正在操作的文件保留备份副本以防出错也是个好主意。

尽管 `noclobber` 可以防止你使用重定向覆盖文件，但它并阻止你使用 `cp -i`（交互式）选项覆盖文件，该选项通过在你尝试覆盖文件时验证意图来帮助你防止此类错误。欲更多信息请参阅第 164 页的提示“cp destroy a file”。

下一个示例显示了如何创建一个包含日期和时间（`date` 的输出）的文件，随后是登录用户列表（`who` 的输出）。图 7-11 中的第一行将 `date` 的输出重定向到文件 `whoson`。然后 `cat` 显示该文件。接下来的示例将 `who` 的输出追加到 `whoson` 文件。

### /dev/null: 让数据消失

`/dev/null` 设备是一个接收器，通常被称为黑洞。你可以将不想保留或看到的输出重定向到 `/dev/null`，输出将不会留下痕迹：

```bash
$ echo "hi there" > /dev/null
```

当你从 `/dev/null` 读取时，你得到的是空字符串。使用以下 `cat` 命令将名为 `messages` 的文件截断为零，同时保留所有权和权限：

```bash
$ ls -l messages
-rw-r--r-- 1 max 25315 2010-10-24 10:55 messages
$ cat /dev/null > messages
$ ls -l messages
-rw-r--r-- 1 max 0 2010-10-24 11:02 messages
```

管道

管道 连接到另一个命令。管道（有时被称为 pipeline）的效果与标准输出重定向到文件然后作为命令输入相同。管道消除了独立的命令和中间文件。管道的符号是竖线 (`|`)。使用管道的命令行格式为：

```bash
command_a [arguments] | command_b [arguments]
```

上述命令行使用管道处理单个命令，产生与以下三个命令相同的结果：

```bash
command_a [arguments] > temp
command_b [arguments] < temp
rm temp
```

在上述命令序列中，从 `command_a` 到名为 `temp` 的中间文件。第二行将命令_b 的标准输入重定向自 `temp`。最后一行删除 `temp`。使用管道的命令不仅更容易输入，而且通常效率更高因为它因为它创建临时文件。

`tr` 可以与任何接受从命令行指定的文件或标准输入的 Linux 实用程序配合管道使用。你也可以与只接受标准输入的命令配合管道。例如，`tr`（翻译）实用程序只从标准输入获取输入。简单的 `tr` 格式如下：

```bash
tr string1 string2
```

`tr` 接受标准输入并查找与 `string1` 中任意字符匹配的字符。找到匹配项，它会将 `string1` 中匹配的字符转换为 `string2` 中对应的字符。（`string1` 中的第一个字符转换为 `string2` 中的第一个字符，依此类推。）`tr` 实用程序将其输出发送到标准输出。在以下两个示例中，`tr` 显示

```bash
$ ls > temp
$ lpr temp
$ rm temp
$ ls | lpr
```

**图 7-12** 管道

将 **abstract** 文件中的字母 a、b、c 分别翻译为 A、B 和 C，内容如下：

```bash
$ cat abstract | tr abc ABC
$ tr abc ABC < abstract
```

`tr` 实用程序改变原始文件的内容；它无法更改原始文件，因为它“不知道”其内容的来源。

`lpr`：`lpr`（行打印机）程序也接受来自文件或标准输入的输入。当你在命令行上输入 `lpr` 后跟一个文件名时，它会将该文件放入打印队列。当你没有在命令行上指定文件名时，`lpr` 将从标准输入获取输入。此功能允许你使用管道将输入重定向到 `lpr`。图 7-12 中的第一组命令显示了你如何使用中间文件（**temp**）配合 `lpr` 将工作目录下的文件列表发送到打印机。如果 `temp` 文件存在，第一条命令将覆盖其内容。第二组命令使用管道将相同的列表（**temp** 除外）发送到打印机。

图 7-13 中的命令将 **who** 的输出重定向到 **temp**，然后按排序顺序显示此文件。`sort` 实用程序（第 168 页）从命令行指定的文件获取输入，或者在未指定文件时从标准输入获取输入；它将其输出发送到标准输出。图 7-13 的命令行从标准输入获取输入，该输入是从 **temp** 重定向（<）的。排序到屏幕上的输出按字母顺序列出了用户。

由于 **sort** 可以从标准输入或命令行上的文件名获取输入，因此在图 7-13 中省略 `<` 符号会产生相同的结果。

图 7-14 在不创建 **temp** 文件的情况下实现了相同的结果。使用管道，shell 将 `who` 的输出重定向到 `sort` 的输入。`sort` 实用程序从标准输入获取输入，因为命令行上它后面没有跟文件名。

当许多人正在使用系统而你只想获取其中一个人的信息时，你可以使用管道将 **who** 的输出发送到 `grep`（第 166 页）。**grep** 实用程序显示包含你指定的字符串的行——在下面的示例中为 **sam**：

```bash
$ who | grep 'sam'
sam console 2010-03-24 05:00
```

```bash
$ who > temp
$ sort < temp
max pts/4      2010-03-24 12:23
max pts/5      2010-03-24 12:33
zach pts/7      2010-03-23 08:45
sam console     2010-03-24 05:00
```

**图 7-13** 使用临时文件存储中间结果

处理屏幕屏幕无法显示的输出（例如拥挤目录中的文件列表）的另一种方法是使用管道将输出通过 `less` 或 `more`（第 162 页）发送。

```bash
$ ls | less
```

`less` 程序每次显示一个屏幕。要查看另一个屏幕，请按空格键。要多看一行，按回车键。按 h 键帮助，按 q 退出。

某些实用程序在重定向输出时会更改其格式。比较它单独运行时输出与将其通过管道发送到 `less` 时的输出。

# 过滤器 (FILTERS)

过滤器是一个处理数据输入流以产生数据输出流的命令。包含过滤器的命令行使用管道将一个命令的标准输出连接到过滤器的标准输入。另一个管道将过滤器的标准输出连接到另一个命令的标准输入。所有实用程序都可以作为过滤器。

在下面的示例中，`sort` 是一个过滤器，它从 `who` 的标准输出获取标准输入，并使用管道将标准输出重定向到 `lpr` 的标准输出。命令行将 `who` 的排序输出发送打印机：

```bash
$ who | sort | lpr
```

前面的示例展示了 shell 的强大结合 Linux 实用程序的通用性。`who`、`sort` 和 `lpr` 这三个实用程序并不是专门为相互配合而设计的，但它们都以传统方式使用标准输入和标准输出。通过使用 shell 处理输入和输出，你可以在命令行上组合标准实用程序以实现你想要的结果。

```bash
$ who | sort
max pts/4      2010-03-24 12:23
max pts/5      2010-03-24 12:33
zach pts/7      2010-03-23 08:45
sam console     2010-03-24 05:00
```

**图 7-14** 代替临时文件工作的管道

# 254 第7 章 SHE

| sam | tee who.out | grep sam |
| :--- | :--- | :--- |
| sam | console | 2010-03-24 05:00 |
| $ cat who.out | | |
| sam | console | 2010-03-24 05:00 |
| max | console | 2010-03-24 05:00 |
| max | pts/4 | 2010-03-24 12:23 |
| max | pts/5 | 2010-03-24 12:33 |
| zach | pts/7 | 2010-03-23 08:45 |
| sam | console | 2010-03-24 05:00 |

# tee: 双向输出

`tee` 实用程序将输入复制到文件并发送到标准输出。图 7-15 显示了 `tee` 的工作原理。该程序的命名非常贴切，因为它将输出分成两个方向：一个标准输出，一个文件。在下面的示例中，`who` 的输出被重定向到 `who.out` 并由 `grep` 过滤：

```bash
$ who | tee who.out | grep sam
max pts/4      2010-03-24 12:23
max pts/5      2010-03-24 12:33
zach pts/7      2010-03-23 08:45
sam console     2010-03-24 05:00
```

# 在后台运行命令 (RUNNING A COMMAND IN BACKGROUND)

当许多人正在使用系统而你只想获取关于其中一个人的信息时，你可以使用管道将 **who** 的输出发送到 **grep**（第 166 页）。**grep** 实用程序显示包含你指定的字符串的行——在下面的示例中为 **sam**：

```bash
$ who | grep 'sam'
sam console 2010-03-24 05:00
```

```bash
$ who > temp
$ sort < temp
max pts/4      2010-03-24 12:23
max pts/5      2010-03-24 12:33
zach pts/7      2010-03-23 08:45
sam console     2010-03-24 05:00
```

**图 7-13** 使用临时文件存储中间结果

处理长长输出（例如拥挤目录中的文件列表）的另一种方法是使用管道将输出通过 `less` 或 `more`（第 162 页）。

```bash
$ ls | less
```
