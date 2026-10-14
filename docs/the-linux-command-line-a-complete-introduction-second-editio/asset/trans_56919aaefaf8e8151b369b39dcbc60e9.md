
cat 也有用于修改文本的选项。其中最突出的两个是 -n，用于给行编号，以及 -s，用于抑制多个空行的输出。我们可以这样演示：

```
[me@linuxbox ~]$ cat > foo.txt
The quick brown fox

jumped over the lazy dog.
[me@linuxbox ~]$ cat -ns foo.txt
    1      The quick brown fox
    2
    3      jumped over the lazy dog.
[me@linuxbox ~]$
```

在此示例中，我们创建了 foo.txt 测试文件的新版本，其中包含两行文本，中间隔着两行空行。经过 cat 使用 -ns 选项处理后，多余的空行被删除，剩余的行被编号。虽然这并不是对文本进行的大量处理，但它确实是一种处理。

## sort

sort 程序对标准输入或命令行上指定的一个或多个文件的内容进行排序，并将结果发送到标准输出。使用与 cat 相同的方法，我们可以直接从键盘演示对标准输入的处理，如下所示：

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

输入命令后，我们输入字母 c、b 和 a，然后按 CTRL-D 表示文件结束。然后我们查看生成的文件，可以看到行现在按排序顺序出现。

由于 `sort` 可以在命令行参数中接受多个文件，因此可以将多个文件 *合并* 成一个排序后的整体。例如，如果我们有三个文本文件并希望将它们合并为一个排序文件，可以这样做：

```
sort file1.txt file2.txt file3.txt > final_sorted_list.txt
```

`sort` 有几个有趣的选项。表 20-1 提供了部分列表。

**表 20-1：** 常见的 `sort` 选项

| 选项 | 长选项 | 描述 |
|---|---|---|
| `-b` | `--ignore-leading-blanks` | 默认情况下，排序在整行上进行，从行的第一个字符开始。此选项使 `sort` 忽略行首的空格，并根据行上的第一个非空白字符计算排序。 |
| `-f` | `--ignore-case` | 使排序不区分大小写。 |
| `-n` | `--numeric-sort` | 基于字符串的数值评估进行排序。使用此选项可以对数值而不是字母值进行排序。 |
| `-r` | `--reverse` | 按降序排序。结果为降序而不是升序。 |
| `-k` | `--key=field1[,field2]` | 基于从 field1 到 field2 所在的关键字段进行排序，而不是整行。参见以下讨论。 |
| `-m` | `--merge` | 将每个参数视为预排序文件的名称。将多个文件合并为单个排序结果，而不执行任何额外排序。 |
| `-o` | `--output=file` | 将排序后的输出发送到文件而不是标准输出。 |
| `-t` | `--field-separator=char` | 定义字段分隔符字符。默认情况下字段由空格或制表符分隔。 |

虽然大多数这些选项都很容易理解，但有些则不然。首先，让我们看一下 -n 选项，用于数值排序。有了此选项，就可以在数值基础上而不是按字典顺序对值进行排序。我们可以通过对 du 命令的结果进行排序来演示这一点，以确定磁盘空间的最大使用者。通常，du 命令按路径名顺序列出摘要结果。

```
[me@linuxbox ~]$ du -s /usr/share/* | head
252	/usr/share/aclocal
96	/usr/share/acpi-support
8	/usr/share/adduser
196	/usr/share/alacarte
344	/usr/share/alsa
8	/usr/share/alsa-base
12488	/usr/share/anthy
8	/usr/share/apmdq
21440	/usr/share/app-install
48	/usr/share/application-registry
```

在此示例中，我们将结果通过管道传递给 head 以将结果限制为前 10 行。我们可以通过以下方式生成按数值排序的列表，以显示 10 个最大的空间使用者。

```
[me@linuxbox ~]$ du -s /usr/share/* | sort -nr | head
509940	/usr/share/locale-langpack
242660	/usr/share/doc
197560	/usr/share/fonts
179144	/usr/share/gnome
146764	/usr/share/myspell
144304	/usr/share/gimp
135880	/usr/share/dict
76508	/usr/share/icons
68072	/usr/share/apps
62844	/usr/share/foomatic
```

通过使用 n 和 r 选项，我们生成了反向数值排序，最大的值首先出现在结果中。此排序有效

