

keyboard:

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

由于 sort 可以在命令行参数中接受多个文件，因此可以将其合并为单个排序后的整体。例如，如果我们有三个文本文件并想将其合并为单个排序文件，可以这样做：

```
sort file1.txt file2.txt file3.txt > final_sorted_list.txt
```

sort 有几个有趣的选项。以下是部分列表：

## Table 20-1: Common sort Options

| Option | Long Option | Description |
| -b | --ignore-leading-blanks | 默认情况下，排序是针对整行进行的，从行中的第一个字符开始。此选项会导致 sort 忽略行首的空格，并根据该行上的第一个非空白字符计算排序。 |
| -f | --ignore-case | 使排序不区分大小写。 |
| -n | --numeric-sort | 基于字符串的数值评估进行排序。使用此选项可以对数值而不是字母值进行排序。 |
| -r | --reverse | 按降序排序。结果为降序而不是升序。 |
| -k | --key=field1[,field2] | 基于从 field1 到 field2 所在的关键字段进行排序，而不是整行。见下文讨论。 |
| -m | --merge | 将每个参数视为预排序文件名的名称。将多个文件合并为单个排序结果，而不执行任何额外排序。 |
| -o | --output=file | 将排序后的输出发送到文件而不是标准输出。 |
| -t | --field-separator=char | 定义字段分隔符字符。默认情况下字段由空格或制表符分隔。 |

尽管上述大多数选项都很容易理解，但有些则不然。首先，让我们看一下用于数值排序的 -n 选项。有了此选项，可以根据数值对值进行排序。我们可以通过对 du 命令的结果进行排序来演示这一点，以确定磁盘空间的最大使用者。通常，du 命令按路径名顺序列出摘要结果：

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

在此示例中，我们将结果通过管道传输到 head 以将结果限制为前十行。我们可以通过以下方式生成按数值排序的列表，以显示占用空间最大的十个使用者：

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

通过使用 -nr 选项，我们生成了反向数值排序，最大的值首先出现在结果中。此排序之所以有效，是因为数值出现在每行的开头。但如果我们想根据行中某个值对列表进行排序怎么办？例如，ls -l 的结果：

```
[me@linuxbox ~]$ ls -l /usr/bin | head
total 152948
-rwxr-xr-x 1 root root     34824 2008-04-04 02:42 [
-rwxr-xr-x 1 root root    101556 2007-11-27 06:08 a2p
-rwxr-xr-x 1 root root     13036 2008-02-27 08:22 aconnect
-rwxr-xr-x 1 root root     10552 2007-08-15 10:34 acpi
-rwxr-xr-x 1 root root      3800 2008-04-14 03:51 acpi_fakekey
-rwxr-xr-x 1 root root     7536 2008-04-19 00:19 acpi_listen
-rwxr-xr-x 1 root root     3576 2008-04-29 07:57 addpart
-rwxr-xr-x 1 root root    20808 2008-01-03 18:02 addr2line
-rwxr-xr-x 1 root root    489704 2008-10-09 17:02 adept_batch
```

暂时忽略 ls 可以按大小排序其结果这一事实，我们也可以使用 sort 按文件大小对此列表进行排序：

```
[me@linuxbox ~]$ ls -l /usr/bin | sort -nr -k 5 | head
-rwxr-xr-x 1 root root   8234216 2008-04-07 17:42 inkscape
-rwxr-xr-x 1 root root   8222692 2008-04-07 17:42 inksview
-rwxr-xr-x 1 root root   3746508 2008-03-07 23:45 gimp-2.4
-rwxr-xr-x 1 root root   3654020 2008-08-26 16:16 quanta
-rwxr-xr-x 1 root root   2928760 2008-09-10 14:31 gdbtui
-rwxr-xr-x 1 root root   2928756 2008-09-10 14:31 gdb
-rwxr-xr-x 1 root root   2602236 2008-10-10 12:56 net
-rwxr-xr-x 1 root root   2304684 2008-10-10 12:56 rpcclient
-rwxr-xr-x 1 root root   2241832 2008-04-04 05:56 aptitude
-rwxr-xr-x 1 root root   2202476 2008-10-10 12:56 smbacls
```

