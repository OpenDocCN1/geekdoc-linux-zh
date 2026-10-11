
这个示例使用了 `sed` 编辑器中的 `s` 命令。`s` 命令用第二个字符串替换指定的第一个字符串。在这个示例中，`big` 替换了 `test`。

当你运行它时，它应该会立即显示结果。这就是使用 `sed` 编辑器的威力。你可以在某些交互式编辑器启动所需的时间内完成编辑。

当然，这个简单的测试只编辑了一行数据。在编辑完整文件时，你应该也会获得同样快速的结果：

```bash
$ cat data1.txt

The quick brown fox jumps over the lazy dog.

The quick brown fox jumps over the lazy dog.

The quick brown fox jumps over the lazy dog.

The quick brown fox jumps over the lazy dog.

$
```

```bash
$ sed 's/dog/cat/' data1.txt

The quick brown fox jumps over the lazy cat.

The quick brown fox jumps over the lazy cat.

The quick brown fox jumps over the lazy cat.

The quick brown fox jumps over the lazy cat.

$
```

`sed` 命令执行并几乎立即运行数据。当它处理每一行数据时，结果就会显示。在 `sed` 编辑器完成处理整个文件之前，你就会看到结果。

```bash
$ cat data1.txt

敏捷的棕色狐狸跳过了懒惰狗。
敏捷的棕色狐狸跳过了懒惰狗。
敏捷的棕色狐狸跳过了懒惰狗。
敏捷的棕色狐狸跳过了懒惰狗。
$
```

# 在命令行中使用多个编辑器命令

要从命令行执行多个命令，只需使用 `-e` 选项即可：

```bash
$ sed -e 's/brown/green/; s/dog/cat/' data1.txt

敏捷的绿色狐狸跳过了懒惰的猫。

敏捷的绿色狐狸跳过了懒惰的猫。

敏捷的绿色狐狸跳过了懒惰的猫。

敏捷的绿色狐狸跳过了懒惰的猫。

$
```

两个命令都会应用于文件的每一行。命令之间必须用分号分隔，且命令结束与分号之间不应有空格。

与其使用分号分隔命令，你可以使用 bash shell 中的次级提示符。只需输入第一个引号打开程序脚本（编辑器命令列表），bash 就会继续提示你输入更多命令，直到你输入结束引号：

```bash
$ sed -e '
> s/brown/green/
> s/fox/elephant/
> s/dog/cat/' data1.txt

敏捷的绿色大象跳过了懒惰的猫。

敏捷的绿色大象跳过了懒惰的猫。

敏捷的绿色大象跳过了懒惰的猫。

敏捷的绿色大象跳过了懒惰的猫。

$
```

你必须记住在出现单引号的同一行上完成命令。在 bash shell 检测到结束引号后，它会处理该命令。`sed` 命令会将你指定的每个命令应用于文件的每一行数据。

# 从文件中读取编辑器命令

最后，如果你有许多想要处理的命令，将它们存储在单独的文件中通常更简单。在命令中使用 `-f` 来指定该文件：

```bash
$ cat script1.sed

s/brown/green/

s/fox/elephant/

s/dog/cat/

$
$ sed -f script1.sed data1.txt

敏捷的绿色大象跳过了懒惰的猫。

敏捷的绿色大象跳过了懒惰的猫。

敏捷的绿色大象跳过了懒惰的猫。

敏捷的绿色大象跳过了懒惰的猫。

$
```

在这种情况下，你不需要在每个命令后加分号。`sed` 编辑器知道每行包含一个独立的命令。与在命令行输入命令一样，`sed` 编辑器从指定文件读取命令并将其应用于数据文件的每一行。

## 提示

很容易混淆 `sed` 编辑器脚本文件和 bash shell 脚本文件。为了消除混淆，请为你的 `sed` 脚本文件使用 `.sed` 后缀。

在“sed 编辑器基础”部分我们将查看其他对处理数据非常有用的 `sed` 编辑器命令。在此之前，让我们快速看看另一个 Linux 数据编辑器。

# 认识 gawk 程序

虽然 `sed` 编辑器是即时修改文本文件的方便工具，但它也有局限性。通常，你需要一个更高级的工具来处理文件中的数据，一个提供更像编程的环境的环境，允许你修改和重新组织文件中的数据。这就是 `gawk` 大显身场的地方

## 注意

并不是所有的发行版都默认安装了 `gawk` 程序。如果你的 Linux 发行版没有 `gawk` 程序，请参考第 9 章作为指南安装 `gawk` 包。

`gawk` 程序是 Unix 中原始 `awk` 程序的 GNU 版本。`gawk` 程序通过提供编程语言而非简单的编辑器命令，比 `sed` 编辑器更进一步。在 `gawk` 编程中，你可以执行以下操作：

- 定义变量来存储数据。
- 使用算术和字符串运算符对数据进行操作。
- 使用结构化编程概念（如 if-then 语句和循环）为你的数据处理添加逻辑。
- 通过提取数据文件中的数据元素并重新排列为另一种顺序或格式，生成格式化报告。

`gawk` 程序的报告生成能力通常用于从大型文本文件中提取数据元素并将其格式化为可读的报告。一个完美的例子就是格式化日志文件。尝试探测日志文件中的错误行可能是困难的。`gawk` 程序允许你从日志文件中过滤出想要查看的数据元素，然后你可以以使阅读重要数据更容易的方式对其进行格式化。

# 访问 gawk 命令格式

这里是 `gawk` 程序的标准格式：
`gawk options program`

表 19.2 显示了 `gawk` 程序可用的选项。

表 19.2 gawk 选项

| 选项 | 说明 |
|---|---|
| -F fs | 指定用于划分行内数据字段的文件隔符 |
| -f file | 指定要从哪个文件读取程序文件 |
| -v var=value | 定义 `gawk` 程序中使用的变量和默认值 |
| -mf N | 指定数据文件中要处理的最大字段数 |
| -mr N | 指定数据文件中记录的最大大小 |
| -W keyword | 指定 `gawk` 的兼容模式或警告级别 |

命令行选项提供了一种自定义 `gawk` 程序功能的简单方法。我们将在探索 `awk` 时更深入地查看这些内容。

`awk` 的强大之处在于能够用复杂的逻辑处理数据。`awk` 的强大之处在于它处理结构化和非结构化数据的能力。`gawk` 程序是一个强大的文本处理工具。

# 从文件中读取编辑器命令

（注：此部分在 OCR 中似乎重复或重叠，根据提供的文本继续）

# 访问 gawk 命令格式

这里是 `gawk` 程序的标准格式：
`gawk options program`

表 19.2 显示了 `gawk` 程序可用的选项。

表 19.2 gawk 选项

| 选项 | 说明 |
|---|---|
| -F fs | 指定用于划分行内数据字段的文件隔符 |
| -f file | 指定要从哪个文件读取程序 |
| -v var=value | 定义 `gawk` 程序中使用的变量和默认值 |
| -mf N | 指定数据文件中要处理的最大字段数 |
| -mr N | 指定数据文件中记录的最大大小 |
| -W keyword | 指定 `gawk` 的兼容模式或警告级别 |

打印整个数据字段。从输出中可以看出，`gawk` 程序将原始文本中的第四数据字段替换为新值。

你也可以使用次级提示符逐行输入你的程序脚本命令：

```bash
$ gawk '{
> S4="Christine"
> print $0'
My name is Rich

My name is Christine

$
```

在打开单引号后，bash shell 会向你提供次级提示符以输入更多内容。你可以一次添加一个命令，直到你输入闭合的引号。由于命令行中没有定义文件名，`gawk` 程序从 STDIN 检索数据。当你运行程序时，它会等待文本从 STDIN 输入。要退出程序，只需按下 Ctrl+D 键键组合来发送数据结束的信号。

## 从文件读取程序

与 `sed` 编辑器一样，`gawk` 编辑器允许你将程序存储在文件中并在命令行中引用它们：

```bash
$ cat script2.gawk

{print $1 "s home directory is " $6}

$
$ gawk -f script2.gawk /etc/passwd

root's home directory is /root

bin's home directory is /bin

daemon's home directory is /sbin

adm's home directory is /var/adm

lp's home directory is /var/sp/lpd

[...]

Christine's home directory is /home/Christine

Samantha's home directory is /home/Samantha
```
