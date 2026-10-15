
向 `test17file` 文件发送一个数据字符串后，脚本使用 `cat` 命令显示文件内容。到目前为止良好。接下来，脚本重新打开输出文件并向其发送另一个数据字符串。当你显示输出文件的内容时，你只能看到第二个数据字符串。shell 覆盖了原始输出文件。

## 列出打开的文件描述符

由于你只有九个文件描述符可用，你可能会认为保持清爽并不困难。然而，在尝试跟踪哪个文件描述符被重定向到哪里时，很容易迷失。为了帮助你保持冷静，bash shell 提供了 `lsof` 命令。

`lsof` 命令列出整个 Linux 系统上的所有文件描述符。这是一个相当有争议的功能，因为它可以向非系统管理员提供有关 Linux 系统的信息。这就是为什么许多 Linux 系统隐藏了此命令，以防用户意外发现它。

在许多 Linux 系统（如 Fedora）上， `lsof` 命令位于 `/usr/sbin` 目录。要用普通用户账户运行它，我必须通过全路径引用它：`$/usr/sbin/lsof`

这会产生海量的输出。它显示了 Linux 系统上当前打开的每个文件的信息。这包括所有在后台运行的进程。

第 #3 行：这是第三行。
现在好了？y
再见
$

在这个示例中，文件描述符 6 被用于保存 STDIN 的位置。脚本将 STDIN 重定向到一个文件。`read` 命令的所有输入都来自重定向后的 STDIN，而它现在就是输入文件。

当所有行都被读取完毕后，脚本通过将 STDIN 重定向回文件描述符 6 将其恢复到原始位置。脚本通过使用另一个 `read` 命令来测试 STDIN 是否已恢复正常，该命令会等待来自的输入。

## 创建读/写文件描述符

尽管这看起来很奇怪，但你也可以打开一个同时用于输入和输出的文件描述符。然后你可以使用同一个文件描述符从同一个文件中读取数据并写入数据。

然而，你对这种方法需要格外小心。当你对文件读写数据时，shell 会维护一个内部指针，指示它在文件中的位置。任何读取或写入操作都会从文件指针停止的地方开始。如果你不小心，可能会产生有趣的结果。看这个示例：

```
$ cat test16

#!/bin/bash

# testing input/output file descriptor

exec 3<testfile

read line <3

echo "Read: $line"

echo "This is a test line" >&3

$ cat testfile

This is the first line.

This is the second line.

This is the third line.

$ ./test16

Read: This is the first line.

$ cat testfile

This is the first line.

This is a test line

line.

This is the third line.

$
```

此示例使用 `exec` 命令将文件描述符 3 分配给发送和来自文件的输入和输出。接下来，它使用 `read` 命令通过分配的文件描述符读取文件的第一行，并将该行数据显示在 STDOUT 中。之后，它使用 `echo` 语句将一行数据写入到使用相同文件描述符打开的文件。

当你运行脚本时，起初一切看起来都很正常。输出显示脚本读取了 `testfile` 文件中的第一行。然而，如果你在运行脚本后显示 `testfile` 的内容，你会发现写入文件的数据覆盖了现有的数据。

当脚本向文件写入数据时，它从文件指针所在的位置开始。`read` 命令读取了第一行数据，因此它让文件指针指向数据第二行的第一个字符。当 `echo` 语句将数据输出到文件时，它将数据放在文件指针当前的位置，覆盖那里的任何数据。

## 关闭文件描述符

如果你创建了新的输入或输出文件描述符，shell 会在脚本退出时自动关闭它们。但在某些情况下，你需要在脚本结束之前手动关闭文件描述符。

要关闭文件描述符，请将其重定向到特殊符号 `>&-`。这在脚本中的显示如下：
`exec 3>&-`

该语句关闭了文件描述符 3，防止它在脚本中继续使用。以下是尝试使用已关闭描述符时发生的情况示例：

```
$ cat badtest

#!/bin/bash

# testing closing file descriptors

exec 3> test17file

echo "This is a test line of data" >3

exec 3>&-

echo "This won't work" >3

$ ./badtest: 3: Bad file descriptor

$
```

关闭文件描述符后，你无法在脚本中向它写入任何数据，否则 shell 会产生错误消息。

关闭文件描述符时还有一点需要注意。如果你在脚本稍后又打开同一个输出文件，shell 会用新文件替换现有文件。这意味着如果你输出任何数据，它都会覆盖现有的文件。考虑以下关于此问题的示例：

```
$ cat test17file

#!/bin/bash

# testing closing file descriptors

exec 3> test17file

echo "This is a test line of data" >3

exec 3>&-

cat test17file

exec 3> test17file

echo "This'll be bad" >3

$ ./test17

This is a test line of data

$ cat test17file

This'll be bad

$
```
