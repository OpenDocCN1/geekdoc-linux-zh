

```
root@kemal:~# cat test
Linux BackTrack 5
Kali Linux 2.0
Ethical Hacking
CentOS
RedHat System Mng.
root@kemal:~# sed "y/ieg/IEG/" test
Linux BackTrack 5
Kali Linux 2.0
Ethical Hacking
CentOS
REdHat SystEm Mng.
root@kemal:~# _
```

最后，让我们来看一个通过从文件中读取命令并对其执行的示例。我们在文本文件中输入 `y/ieg/IEG/` 并将其保存为 `change.sed`。然后使用 `sed -f change.sed test` 命令来对我们的测试文件进行更改。

```
root@kemal:~# cat test
Linux BackTrack 5
Kali Linux 2.0
Ethical Hacking
CentOS
RedHat System Mng.
root@kemal:~# cat change.sed
y/ieg/IEG/
root@kemal:~# sed -f change.sed test
Linux BackTrack 5
Kali Linux 2.0
Ethical Hacking
CentOS
REdHat SystEm Mng.
root@kemal:~# _
```

# Awk

Awk 是一种脚本语言，允许我们按照所需的格式对文本文件进行更改。它也是一种解释型语言。如果从文件中读取命令，它们将按照读取的顺序执行。通常 awk 用于根据标准对文件进行搜索和编辑。

在介绍之后，让我们来看 awk 的用法示例。例如，当我们在命令行输入 `awk "BEGIN {print \"command line\"}"` 时，命令输出将作为 `command line` 显示在屏幕上。

```
root@kemal:-# awk "BEGIN {print \"command line\"}"
command line
root@kemal:-# _
```

如果我们使用 `awk "{print}"` 命令，我们跟在命令后面的陈述将打印在屏幕上。我们可以使用 `Ctrl + D` 退出。

```
root@kemal:-# awk "{print}"
demirez
demirez
zeynep
zeynep
root@kemal:-# _
```

如果你想使用从文件中读取的命令，应该使用 `awk -f <script_file>` 命令。我们可以在文本文件中编写 awk 代码并保存，然后使用 `-f` 参数定位该文件位置。虽然文件不需要任何扩展名，但在保存时使用 `.awk` 扩展名有助于记住这是一个 awk 脚本文件。对于小规模处理，通过命令行输入命令更符合逻辑。然而，使用脚本文件在大文件中执行大量操作是有意义的。现在，让我们使用一个小文件的示例。将以下语句输入到文本文件中，扩展名为 `.awk`。

# BEGIN {print "linux commands"}

我使用命令 `awk -f sample.awk`，是因为我给文件命名为 `sample.awk`。

```
root@kemal:~# cat sample.awk
BEGIN {
  print "linux commands"
}
root@kemal:~# awk -f sample.awk
linux commands
root@kemal:~#
```

awk 有不同的版本。除了原始的 awk 外，你也可以使用 `gawk` (GNU awk)、`nawk`。我将提供 awk 的示例，但如果你愿意，可以使用 nawk。

```
root@kemal:~# which awk
/usr/bin/awk
root@kemal:~# which nawk
/usr/bin/nawk
root@kemal:~# nawk -f sample.awk
linux commands
root@kemal:~# -
```

由于我们将解释控制台的使用，我们的示例将关于 awk 命令的使用，即从控制台从文件中获取给定的命令。使用控制台有一些规则我们需要记住。这些是：

## 201 | Linux 命令精要

- `'` 命令写在双引号内，然后执行的文件将是指定的指定。
- `$` 引用文件中的列（将进行处理的）。如果没有进行更改，列将按空格分隔。`$0` 显示总行数（对应每行的整行），`$1` 显示行的第一列，`$2` 显示行的第二列。
- `NR`: 总记录数（行号）。
- `NF`: 列数/字段数。
- `-F`: 用于指定字段分隔符符号。
- `/..//`: 使用在两个 `/` 之间的正则表达式。
- `FS`: 字段分隔符。

数学运算符 (`+`, `-`, `=`, `++`, `--`, `*`, `*`, `/`, `/=` 等) 可以在 awk 中使用。比较表达式 `<`, `<= `>=`, `=`, `!=` 也可以使用。

现在让我们做一些练习。例如，要原样显示文件内容，使用 `awk '{print $0}' <file` 命令。

```
root@kemal:~# cat test
Linux BackTrack 5
Kali Linux 2.0
Ethical Hacking
CentOS
RedHat System Mng.
root@kemal:~# awk '{print $0}' test
Linux BackTrack 5
Kali Linux 2.0
Ethical Hacking
CentOS
RedHat System Mng.
```

要检查文件中的任何语句，我们必须使用 `/../` 模式。包含查询词的单行或多行将被显示。

```
root@kemal:~# cat test1
Linux BackTrack 5
RedHat System Mng.
root@kemal:~# awk '/Red/' test1
RedHat System Mng.
root@kemal:~# _
```

为了查看每个分配空间开头处的特定区域，必须使用通过通过文件的行来查看任何表达式的 `awk '/string/ {print $1}'` 模板。

```
root@kemal:~# cat test
Linux BackTrack 5
Kali Linux 2.0
Ethical Hacking
CentOS
RedHat System Mng.
root@kemal:~# awk '/Kali/ {print $1}' test
Kali
root@kemal:~# _
```

如果我们想查看字段的头部，我们使用 `awk '{print $1}'` 命令。

## 206 | Linux 命令精要

```
root@kemal:~# cat test
Linux BackTrack 5
Kali Linux 2.0
Ethical Hacking
CentOS
RedHat System Mng.
root@kemal:~# awk '{print $1}' test
Linux
Kali
Ethical
CentOS
RedHat
root@kemal:~# _
```

如果表达式之间是 `:` 而不是空格，我们应该使用 `awk -F` 点符号：

```
root@kemal:~# cat personal
Ali:312:Ankara
Veli:212:İstanbul
Kemal:232:İzmir
root@kemal:~# awk -F: '{print $1}' personal
Ali:312
Veli:212
Kemal:232
root@kemal:~# _
```

如你所见，`'{print $1}' personal` 无法得到预期的结果。我们使用 `-F: '{print $1}' personal` 因为 `:` 被用作分隔符。要查看保留区域的短语，例如查看第一和第三区域的短语，应该使用 `'{print $1,$3}'` 命令，如果你忘记在 `$1` 和 `$3` 之间放置逗号，所有的表达式将在一起显示。

## Kemal Demirez | 207

```
root@kemal:~# cat personal
Ali:312:Ankara
Veli:212:İstanbul
Kemal:232:İzmir
root@kemal:~# awk -F: '{print $1, $3}' personal
Ali Ankara
Veli İstanbul
Kemal İzmir
root@kemal:~# awk -F: '{print $1$3}' personal
AliAnkara
Veliİstanzbul
Kemalİzmir
root@kemal:~# _
```

在接下来的示例中，我们将看到 `-F:` 表达式，它用于区域工作相当于 `FS=":"`。

```
root@kemal:~# cat personal
Ali:312:Ankara
Veli:212:İstanbul
Kemal:232:İzmir
root@kemal:~# awk -F: '{print $3}' personal
Ankara
İstanbul
İzmir
root@kemal:~# awk '{print $3}' FS=":" personal
Ankara
İstanbul
İzmir
root@kemal:~# _
```

你不仅可以使用表达式 `FS=":"` 形式，还可以使用 `FS=''` 或 `FS=:`。当将所需的短语作为输出显示在屏幕上时，如果你想，可以使用另一个短语输出。例如，`awk -F: '{print "city: $3}' personal` 命令的输出将如下。

## 208 | Linux 命令精要

```
root@kemal:~# cat personal
Ali:312:Ankara
Veli:212:İstanbul
Kemal:232:İzmir
root@kemal:~# awk -F: '{print "city: $3}' personal
city: Ankara
city: Istanbul
city: İzmir
root@kemal:~# _
```

