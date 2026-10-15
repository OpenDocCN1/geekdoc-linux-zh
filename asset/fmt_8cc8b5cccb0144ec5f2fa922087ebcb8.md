
在类 Unix 系统上，发送到打印机的输出以纯文本形式发送，或者如果页面包含图形，则会转换为一种称为 PostScript 的文本格式页面描述语言，然后发送到生成要打印的图形点的程序。

## 程序源代码

在类 Unix 系统上找到的许多命令行程序都是为支持系统管理和软件开发而创建的，文本处理程序也不例外。其中许多程序旨在解决软件开发问题。文本处理对软件开发人员很重要的原因是所有软件都始于文本。源代码，即程序员实际编写的部分，始终以文本格式存在。

## 重温一些老朋友

在第 6 章（重定向）中，我们学习了一些能够接受标准输入作为命令行参数补充的命令。当时我们只是简单地提到了它们，但现在我们将更仔细地研究它们如何用于执行文本处理。

## cat

`cat` 程序有许多有趣的选项。其中许多用于更好地可视化文本内容。一个例子是 `-A` 选项，用于在文本中显示不可打印字符。有时我们想知道控制字符是否嵌入在我们 otherwise 可见的文本中。其中最常见的是制表符（与空格相对）和回车符，通常作为 MS-DOS 风格文本文件中的行尾字符存在。另一个常见情况是包含带有尾随空格的文本行的文件。

让我们使用 `cat` 作为原始文字处理器创建一个测试文件。为此，我们只需输入命令 `cat`（连同指定重定向输出的文件）并输入我们的文本，然后按 Enter 正确结束该行，然后按 Ctrl-d，指示 `cat` 我们已到达文件末尾。在此示例中，我们输入一个前导制表符，并在该行后跟一些尾随空格：

```
[me@linuxbox ~]$ cat > foo.txt
	The quick brown fox jumped over the lazy dog.
[me@linuxbox ~]$
```

接下来，我们将使用 `-A` 选项使用 `cat` 显示文本：

```
[me@linuxbox ~]$ cat -A foo.txt
^IThe quick brown fox jumped over the lazy dog.  $
[me@linuxbox ~]$
```

正如我们在结果中看到的那样，我们文本中的制表符由 `^I` 表示。这是一种常见的表示法，意思是“Control-I”，事实证明它与制表符相同。我们还看到 `$` 出现在行的真正末尾，表明我们的文本包含尾随空格。

## MS-DOS 文本与 Unix 文本

你可能想要使用 `cat` 来查找文本中不可打印字符的一个原因是发现隐藏的回车符。隐藏的回车符从何而来？来自 DOS 和 Windows！Unix 和 DOS 在文本文件中定义行尾的方式不同。Unix 使用换行符（ASCII 10）结束一行，而 MS-DOS 及其衍生产品使用回车（ASCII 13）和换行序列来终止每一行文本。

有几种方法可以将文件从 DOS 转换为 Unix 格式。在许多 Linux 系统上，有名为 `dos2unix` 和 `unix2dos` 的程序，可以在 DOS 格式之间转换文本文件。但是，如果你的系统上没有 `dos2unix`，也不用担心。将文本从 DOS 转换为 Unix 格式的过程非常简单；它只是涉及删除有问题的回车符。这很容易通过本章后面讨论的几个程序完成。

`cat` 还有用于修改文本的选项。最突出的两个是 `-n`，用于编号行，以及 `-s`，用于抑制多个空行的输出。我们可以这样演示：

```
[me@linuxbox ~]$ cat > foo.txt
The quick brown fox


jumped over the lazy dog.
[me@linuxbox ~]$ cat -ns foo.txt
1       The quick brown fox
2
3       jumped over the lazy dog.
[me@linuxbox ~]$
```

在此示例中，我们创建了 `foo.txt` 测试文件的新版本，其中包含两行文本，中间隔有两个空行。在使用 `-ns` 选项由 `cat` 处理后，多余的空行被删除，剩余的行被编号。虽然这不是对文本执行的太多处理，但它是一种处理。

## sort

`sort` 程序对标准输入或命令行上指定的一个或多个文件的内容进行排序，并将结果发送到标准输出。使用与 `cat` 相同的技术，我们可以直接从 keyboard:

```
[me@linuxbox ~]$ sort > foo.txt
c
b
a
[me@linuxbox ~]$ cat foo.txt
a
b
c
```

输入命令后，我们键入字母 "c"、"b" 和 "a"，再次按下 Ctrl-d 以表示文件结束。然后我们查看生成的文件，看到行现在按排序顺序出现。

由于 `sort` 可以在命令行参数中接受多个文件，因此可以将其合并为单个排序后的整体。例如，如果我们有三个文本文件并想将其合并为单个排序文件，可以这样做：

```
sort file1.txt file2.txt file3.txt > final_sorted_list.txt
```

`sort` 有几个有趣的选项。以下是部分列表：

### Table 20-1: Common sort Options

| Option | Long Option | Description |
| -b | --ignore-leading-blanks | 默认情况下，排序是针对整行进行的，从行中的第一个字符开始。此选项会导致 `sort` 忽略行首的空格，并根据该行上的第一个非空白字符计算排序。 |
| -f | --ignore-case | 使排序不区分大小写。 |
| -n | --numeric-sort | 基于字符串的数值评估进行排序。使用此选项可以对数值而不是字母值进行排序。 |
| -r | --reverse | 按降序排序。结果为降序而不是升序。 |
| -k | --key=field1[,field2] | 基于从 `field1` 到 `field2` 所在的关键字段进行排序，而不是整行。见下文讨论。 |
| -m | --merge | 将每个参数视为预排序文件名的名称。将多个文件合并为单个排序结果，而不执行任何额外排序。 |
| -o | --output=file | 将排序后的输出发送到文件而不是标准输出。 |
| -t | --field-separator=char | 定义字段分隔符字符。默认情况下字段由空格或制表符分隔。 |

尽管上述大多数选项都很容易理解，但有些则不然。首先，让我们看一下用于数值排序的 `-n` 选项。有了此选项，可以根据数值对值进行排序。我们可以通过对 `du` 命令的结果进行排序来演示这一点，以确定磁盘空间的最大使用者。通常，`du` 命令按路径名顺序列出摘要结果：

```
[me@linuxbox ~]$ du -s /usr/share/* | head
252       /usr/share/aclocal
96        /usr/share/acpi-support
8         /usr/share/adduser
196       /usr/share/alacarte
344       /usr/share/alsa
8         /usr/share/alsa-base
12488     /usr/share/anthy
8         /usr/share/apmd
21440     /usr/share/app-install
48        /usr/share/application-registry
```

在此示例中，我们将结果通过管道传输到 `head` 以将结果限制为前十行。我们可以通过以下方式生成按数值排序的列表，以显示占用空间最大的十个使用者：

```
[me@linuxbox ~]$ du -s /usr/share/* | sort -nr | head
509940      /usr/share/locale-langpack
242660      /usr/share/doc
197560      /usr/share/fonts
179144      /usr/share/gnome
146764      /usr/share/myspell
144304      /usr/share/gimp
135880      /usr/share/dict
76508       /usr/share/icons
68072       /usr/share/apps
62844       /usr/share/foomatic
```

通过使用 `-nr` 选项，我们生成了反向数值排序，最大的值首先出现在结果中。此排序之所以有效，是因为数值出现在每行的开头。但如果我们想根据行中某个值对列表进行排序怎么办？例如，`ls -l` 的结果：
