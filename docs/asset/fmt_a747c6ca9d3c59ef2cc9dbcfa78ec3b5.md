
```bash
# cat namelist
Scott Bessler
Jason Nash
Angie Nash
Derek Stutsman
Jeff Arillano
Paul Ward
Alex Blauvelt
Peter Anapol
David Goolsby
Michael Craig
Johannes Erdelt
Thomus McCanta
Joakim Erdelt
Pete Gizzi
Neil Schroeder

# sort +1 +0 namelist
Peter Anapol
Jeff Arellano
Scott Bessler
Alex Blauvelt
Michael Craig
Joakim Erdelt
Johannes Erdelt
Pete Gizzi
David Goolsby
Thomus McCanta
Angie Nash
Jason Nash
Neil Schroeder
Derek Stutsman
Paul Ward
```

这些字段的使用为文件中的列表排序提供了极大的灵活性。重要的是要记住，`sort` 实用程序不会更改原始文件。输出被发送到标准输出，在那里可以查看或重定向到另一个命令或文件。

##### 截取文本

`cut` 实用程序用于将文件的选定部分写入标准输出。`cut` 实用程序可用于从指定文件中选择列或字段。可以选择特定的行地址、多个行地址或行地址范围。表 4-3 介绍了 `cut` 实用程序使用的各种选项。

**表 4-3 `cut` 使用的选项**

| 选项 | 用途 |
| :----- | :----- |
| `-b` | 仅输出指定的字节范围。 |
| `-c` | 仅输出指定的字符。 |
| `-f` | 仅输出指定的字段，字段以制表符分隔。 |
| `-help` | 显示帮助并退出。 |
| `-version` | 显示版本信息并退出。 |

以下是使用这些范围仅输出每行前 10 个字符的示例：

```bash
# cut -c 1-10 nameslist
Scott Bess
Jason Nash
Angie Nash
Derek Slut
Jeff Arell
Paul Ward
Alex Blauw
Peter Anap
David Gool
Michael Cr
Johannes E
Thomas McC
Joakin Erd
Pete Gizzi
Neil Schro
```

`cut` 实用程序可以指定要显示的字节、字符或字段。

##### 粘贴文本

`paste` 实用程序允许你连接多个文件的文本。指定文件的对应行以制表符字符分隔并写入标准输出。`paste` 实用程序使用的选项见表 4-4。

**表 4-4 `paste` 使用的选项**

| 选项 | 用途 |
| :----- | :----- |
| `-s` | 逐个粘贴来自一个文件的行。 |
| `-d delim-list` | 在分隔合并的文件时，依次使用 `delim-list` 中指定的字符，而不是制表符字符。 |

以下是使用 `paste` 实用程序的示例：

```bash
# paste alphanames nicks
Peter Anapol Bammage
Jeff Arellano Rexmortis
Scott Bessler Jackyl
Alex Blauvelt Dragonstr
Michael Craig Alchemist
Joakin Erdfelt Just_Joe
```

##### 将制表符转换为空格

在 Linux 上创建文件时，制表符（Tab）键被视为一个按键，但实际的制表符设置可能因系统而异。这会根据显示文件的系统改变文件的外观。为了在文件中创建统一的外观，您可能希望将文件中的制表符替换为指定数量的空格。这将使文件在所有系统上显示一致。`expand` 实用程序用于将制表符扩展为空格。该实用程序可以处理文件中的文本或标准输入上的文本。`expand` 实用程序的选项如表 4-5 所示。

**表 4-5：用于 `expand` 的选项**

| 选项 | 用途 |
| :--- | :--- |
| `-I` | 指定仅转换行首的制表符。 |
| `-t` | 使用一组数字来指定要转换的制表符位置。 |
| `--help` | 显示帮助信息然后退出。 |
| `--version` | 显示版本信息然后退出。 |

`expand` 实用程序的默认操作是将文件中的所有制表符转换为八个空格。`expand` 实用程序的一些示例如下：

```bash
# expand marital
Scott Bessler
Jason Nash M
Angie Nash M
Derek Stutsman M
Jeff Arellano S
Paul Ward M
Alex Blauvelt S
Peter Anapol M
David Goolsby S
Michael Craig S
Johannes Erdfelt S
Thomas McCanta S
Joakim Erdfelt S
Pete Gizzi M
Neil Schroeder S
```

在此示例中，使用了八个空格的默认设置。由于名字 Johannes Erdfelt 有 16 个字符，制表符被扩展到第 24 个字符字段。在接下来的示例中，制表符字段的 9 个空格设置使得婚姻状况字段能够整齐对齐。

```bash
# expand -t 9 marital
Scott Bessler S
Jason Nash M
Angie Nash M
Derek Stutsman M
Jeff Arellano S
Paul Ward M
Alex Blauvelt S
Peter Anapol M
David Goolsby S
Michael Craig S
Johannes Erdfelt S
Thomas McCanta S
Joakim Erdfelt S
Pete Gizzi M
Neil Schroeder S
```

##### 段落格式化

`fmt` 实用程序对文件中的每个段落进行格式化，并将输出发送到标准输出。该实用程序用于指定行的宽度，并尝试合并或拆分行，以产生长度一致的各行。`fmt` 实用程序尝试在句子末尾拆分行。当无法这样做时，它会避免在句子的第一个单词后或最后一个单词前断行。句子被确定为以句号、感叹号或问号（! ?）加上两个空格或换行符结尾。在进行任何换行之前，整个段落都会被读取。

与 `fmt` 一起使用的默认行宽为 75 个字符。默认宽度可以通过使用适当的选项覆盖。表 4-6 涵盖了与此实用程序一起使用的一些选项。

**表 4-6：用于 `fmt` 的选项**

| 选项 | 用途 |
| :--- | :--- |
| `-c` | 保留段落开头的缩进，并将段落与第二行的左边缘对齐。 |
| `-t` | 工作方式类似于 `-c` 选项，但如果段落中第二行的缩进与第一行匹配，则第二行被视为单行段落。 |
| `-s` | 指定仅拆分行，而不合并。 |
| `-u` | 指定使用均匀的空格；这将所有单词之间的空格减少为一个，句子之间的空格减少为两个。 |
| `-NUMBER` 或 `-w NUMBER` | 将行的宽度设置为指定的 `NUMBER`。 |
| `-p PREFIX` | 指定仅格式化以 `PREFIX` 开头的行。 |

`fmt` 实用程序还保留空白行、缩进和空格，以便文档中包含的任何特殊格式都不会改变。`fmt` 实用程序的使用示例如下所示。如示例中可见，段落之间的所有行都得以保留，并且该实用程序尝试产生所有宽度为 40 个字符的行。
