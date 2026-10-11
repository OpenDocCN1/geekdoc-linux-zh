

以下示例根据访问时间列出了文件名，并附加了一个字符 / 来表示目录。

```
# ls -pu
morestuff/ nicks list readme alphanames namelist
```

以下示例列出了 /home/angie/stuff 目录及其所有子目录的内容。

```
# ls -R /home/angie/stuff
alphanames list morestuff namelist newstuff nicks oldstuff readme

/home/angie/stuff/morestuff:

/home/angie/stuff/newstuff:
newnamelist newnicks

/home/angie/stuff/oldstuff:
oldnameslist oldnicks
```

正如在这些示例中所见，ls 命令可以成为收集文件和目录信息的强大工具。该命令通常与其他命令和文件结合使用，通过管道和重定向来实现。这允许将输出保存到文件或供其他实用程序处理。理解 ls 命令的单独使用以及与其他实用程序配合使用，将为考试和从事 Linux 系统工作做好准备。

## 确定文件类型

ls 命令在检查文件时提供了高度的功能性。然而，它提供的关于文件内容的信息有限。file 命令可用于更多地了解 Linux 系统上文件的内容。file 命令的输出包括以下单词之一：text（文本）、executable（可执行文件）、data（数据）或 directory（目录）。该命令接受参数以指定要检查哪些文件。可以使用该命令的各种选项；这些选项在表 6-5 中显示。

### 表 6-5
file 命令使用的选项

| 选项 | 用途 |
| ------ | --- |
| -b | 指定输出中不包括文件名。 |
| -f <FILENAME> | 指定 <FILENAME> 文件包含将由 file 命令检查的文件名称。 |
| -n | 在检查完文件后刷新 `stdout`。当处理正在发送到另一个命令的文件列表时，这可能很有用。 |
| -v | 显示版本信息并退出。 |
| -z | 尝试检查压缩文件的内容。 |

以下是 `file` 命令及其选项的一些使用示例。在第一个示例中，使用了 `*` 通配符，因此该命令检查 `pwd` 中的所有文件。

```
# file *
alphenames: ASCII text
list:         ASCII text
morestuff:    directory
namelist:     ASCII text
newstuff:     directory
nickstuffs:   ASCII text
oldstuff:     directory
readmes:      English text
```

在以下示例中，输出中不包含文件名：

```
# file -b /etc/lilo.conf
ASCII text
```

在以下示例中，使用 `file` 命令检查压缩文件的内容：

```
# file -z /usr/info/tar.info.gz
/usr/info/tar.info.gz: English text (gzip compressed data,
   deflated, last modified: Wed Dec 31 19:00:00 1969, max
   compression, os: Unix)
```

## 更改文件时间戳

`touch` 命令允许你更改文件的时间戳。如果指定了文件名，但该文件不存在，则创建一个具有该名称的空文件。表 6-6 介绍了可用于 `touch` 命令的选项。

| 选项 | 用途 |
| ------ | --- |
| -a | 仅更改文件的访问时间。 |
| -c | 如果不存在文件，则不创建文件。 |
| -d <STRING> | 用于指定文件上的 <STRING> 时间戳，而不是使用当前时间。 |
| r <file> | 使用 <file> 的时间，而不是当前时间。 |
| -t <TIME> | 使用参数来指定时间，而不是使用当前时间。 |

由此可见，`touch` 命令允许你使用当前时间或为时间戳指定时间。该命令通常用于创建指定名称的空文件。当运行预期文件存在的其他脚本时，这可能很有用。日志文件是一种典型的文件类型，它会被自动写入，并且有时必须存在以避免日志记录中的错误。如果文件已在其他地方归档，你可能希望删除原始文件。然后你可以使用 `touch` 创建一个用于存储日志信息的空文件。该命令通常作为 `cron` 作业在指定时间通过脚本运行。`touch` 命令允许此过程自动运行，无需用户干预，也不会因缺少文件而生成错误消息。

以下示例展示了一个脚本，其中使用 `touch` 命令创建了一个空文件。

```
cp mylogs stuff/mylogs.\`date +%m.%d.%y`
rm -f mylogs
touch mylogs
```

这将把 `mylogs` 文件的内容复制到位于 `stuff` 目录中、文件名为 `mylogs.month.day.year`（例如，`mylogs.12.11.0D`）的文件中。原始的 `mylogs` 文件被删除，然后使用 `touch` 命令创建一个名为 `mylogs` 的空文件。这是 `touch` 命令的一种常见用途。

## 复制文件

在系统上处理文件时，你经常需要复制文件。Linux 包含两个用于文件复制的命令。`cp` 命令用于复制文件和目录。这是在系统的一个位置复制文件到另一个位置时使用的标准命令。当从一种文件格式复制到另一种文件格式时，使用 `dd` 命令。

### cp

cp 命令（copy 的缩写）用于 Linux 系统中的标准文件复制。该命令用于创建原始文件或目录的新独立副本。使用几个选项与 cp 命令配合使用，以定制创建的副本。这些选项在下面的表 6-7 中介绍。

### 表 6-7
cp 命令使用的选项

| 选项 | 用途 |
| ------ | --- |
| -a | 指定原始文件的链接和属性将传输到新副本。 |
| -d | 指定复制时保留链接。 |
| -f | 覆盖任何现有的目标文件。 |
| -i | 在覆盖任何现有目标文件前提示。 |
| -l | 指定将创建硬链接（在本书后续章节中讨论），而不是文件的副本。 |
| -p | 保留原始文件的所有者、组、权限和时间戳。 |
| -r | 递归复制目录及其内容，同时将所有文件作为标准文件复制。不应将此选项用于特殊文件。 |
| -R | 递归复制目录及其内容，保留非目录项。 |
| -s | 为非目录文件创建符号链接（在本书后续章节中介绍）。 |
| -v | 显示所有正在复制的文件的名称。 |

这些选项可以在复制文件时组合使用。除了这些选项外，cp 命令还使用参数。cp 命令的正确语法如下：

```
cp -option source target
```

当指定的目标是目录时，源文件将复制到该目录中，文件名与原始文件相同。当指定的目标不是目录时，原始文件将被复制到指定位置，并使用目标名称。以下是一些使用 cp 命令的示例。在第一个示例中，文件 marital 被复制到目录 stuff。

```
# cp marital stuff
```

在第二个示例中，目录 `/home/angie/stuff` 及其内容被复制到目录 `/home/angie/otherstuff`。这特别有用，因为它允许使用一条命令复制整个目录及其内容。

```
# cp -r /home/angie/stuff /home/angie/otherstuff
```

这是一个重要的选项，你很可能会在考试问题中看到。

在第三个示例中，位于 `/home/angie/stuff` 目录中的文件和目录被冗长地（详细显示）复制到 `/home/angie/otherstuff` 目录。

```
# cp -rv /home/angie/stuff/* /home/angie/morestuff
/home/angie/stuff/abcnames -> /home/angie/morestuff/abcnames
/home/angie/stuff/alphanames -> /home/angie/morestuff/alphanames
/home/angie/stuff/list -> /home/angie/morestuff/list
/home/angie/stuff/marital -> /home/angie/morestuff/marital
/home/angie/stuff/morestuff -> /home/angie/morestuff/morestuff
/home/angie/stuff/mycommands.12.11.00 -> /home/angie/morestuff/mycommands.12.11.00
/home/angie/stuff/nameslist -> /home/angie/morestuff/nameslist
/home/angie/stuff/newstuff -> /home/angie/morestuff/newstuff
/home/angie/stuff/newstuff/newnameslist -> /home/angie/morestuff/newstuff/newnameslist
/home/angie/stuff/newstuff/newnicks -> /home/angie/morestuff/newstuff/newnicks
/home/angie/stuff/nicks -> /home/angie/morestuff/nicks
/home/angie/stuff/oldstuff -> /home/angie/morestuff/oldstuff
/home/angie/stuff/oldstuff/oldnameslist -> /home/angie/morestuff/oldstuff/oldnameslist
/home/angie/stuff/oldstuff/oldnicks -> /home/angie/morestuff/oldstuff/oldnicks
/home/angie/stuff/readmes -> /home/angie/morestuff/readmes
```

### dd

`dd` 命令（direct dump 的缩写）用于同时复制和将文件转换为不同的文件类型。该命令具有与 `cp` 命令不同的选项和语法。`dd` 命令使用的语法如下：

```
dd [Options]
```

默认情况下，`dd` 命令将数据从标准输入写入标准输出。可以使用选项来覆盖这些默认设置。`dd` 命令使用的选项在表 6-8 中显示。

