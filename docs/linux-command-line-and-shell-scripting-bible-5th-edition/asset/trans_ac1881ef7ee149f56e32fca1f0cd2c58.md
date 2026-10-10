

## 重定向错误和数据
如果你想同时重定向错误信息和正常输出，需要使用两个重定向符号。你需要在每个符号前加上相应的文件描述符，以指定你要重定向的数据类型，并将它们指向合适的输出文件来保存数据：

```bash
$ ls -al test test2 test3 badtest 2> test6 1>test7
$ cat test6
ls: cannot access test: No such file or directory
ls: cannot access badtest: No such file or directory
$ cat test7
-rw-rw-r-- 1 rich rich 158 2025-06-20 11:32 test2
-rw-rw-r-- 1 rich rich   0 2025-06-20 11:33 test3
$
```

shell 使用 `1>` 符号将原本流向 `STDOUT` 的 `ls` 命令的正常输出重定向到 `test7` 文件。使用 `2>` 符号，原本流向 `STDERR` 的错误消息被重定向到 `test6` 文件。

你可以使用这种技术将脚本的正常输出与脚本中发生的任何错误消息分离开来。这让你可以轻松地识别错误，而不必在数千行正常输出数据中费力查找。

或者，如果你愿意，可以将 `STDERR` 和 `STDOUT` 的输出重定向到同一个输出文件。Bash shell 为此目的提供了一个专门的重定向符号，即 `&>` 符号：

```bash
$ ls -al test test2 test3 badtest &> test7
$ cat test7
ls: cannot access test: No such file or directory
ls: cannot access badtest: No such file or directory
-rw-rw-r-- 1 rich rich 158 2025-06-20 11:32 test2
-rw-rw-r-- 1 rich rich   0 2025-06-20 11:33 test3
$
```

当你使用 `&>` 符号时，命令生成的所有输出（包括数据和错误）都会被发送到同一个位置。注意，其中一条错误消息的顺序与你预期的不同。`badtest` 文件的错误消息（列出的最后一个文件）出现在输出文件中的第二位。Bash shell 自动将错误消息的优先级设为高于标准输出。这让你可以集中查看错误消息，而不是让它们散布在整个输出文件中。

## 在脚本中重定向输出
你可以在脚本中使用 `STDOUT` 和 `STDERR` 文件描述符，通过重定向相应的文件描述符来轻松地在多个位置生成输出。在脚本中重定向输出有两种方法：

-   临时重定向每一行
-   永久重定向脚本中的所有命令

接下来的部分将描述每种方法的工作方式。

### 临时重定向
如果你想在脚本中故意生成错误消息，可以将单个输出行重定向到 *STDERR*。你只需要使用输出重定向符号将输出重定向到 *STDERR* 文件描述符即可。当重定向到文件描述符时，必须在文件描述符编号前加上一个 &（&amp;）符号：

```bash
echo "This is an error message" >&2
```

这一行会在 *STDERR* 文件描述符当前指向的位置显示文本，而不是在正常的 *STDOUT* 上显示。以下是一个使用此功能的脚本示例：

```bash
$ cat test8
#!/bin/bash
# testing STDERR messages

echo "This is an error" >&2
echo "This is normal output"
$
```

如果你按常规运行脚本，你不会注意到任何差异：

```bash
$ ./test8
This is an error
This is normal output
$
```

请记住，默认情况下，Linux 将 *STDERR* 输出指向 *STDOUT*。但是，如果你在运行脚本时重定向了 *STDERR*，脚本中指向 *STDERR* 的任何文本都会被重定向：

```bash
$ ./test8 2> test9
This is normal output
$ cat test9
This is an error
$
```

完美！使用 *STDOUT* 显示的文本出现在监视器上，而发送到 *STDERR* 的 *echo* 语句文本被重定向到输出文件。

这种方法非常适合在脚本中生成错误消息。如果有人使用你的脚本，他们可以像上面所示的那样，使用 *STDERR* 文件描述符轻松重定向错误消息。

### 永久重定向
如果你在脚本中重定向大量数据，每次都要重定向每个 *echo* 语句会显得很繁琐。相反，你可以使用 *exec* 命令告知 shell 在脚本运行期间重定向特定的文件描述符：

```bash
$ cat test10
#!/bin/bash
# redirecting all output to a file
exec 1>testout

echo "This is a test of redirecting all output"
echo "from a script to another file."
echo "without having to redirect every individual line"
$ ./test10
$ cat testout
This is a test of redirecting all output
from a script to another file.
without having to redirect every individual line
$
```

`exec` 命令启动一个新的 shell，并将 `STDOUT` 文件描述符重定向到一个文件。脚本中所有流向 `STDOUT` 的输出都会改为重定向到该文件。

你也可以在脚本中间重定向 `STDOUT`：

```bash
$ cat test11
#!/bin/bash
# redirecting output to different locations

exec 2>testerror

echo "This is the start of the script"
echo "now redirecting all output to another location"

exec 1>testout

echo "This output should go to the testout file"
echo "but this should go to the testerror file" >&2
$

$ ./test11
This is the start of the script
now redirecting all output to another location
$ cat testout
This output should go to the testout file
$ cat testerror
but this should go to the testerror file
$
```

该脚本使用 `exec` 命令将流向 `STDERR` 的任何输出重定向到文件 `testerror`。接下来，脚本使用 `echo` 语句向 `STDOUT` 显示几行内容。之后，再次使用 `exec` 命令将 `STDOUT` 重定向到 `testout` 文件。请注意，即使 `STDOUT` 已被重定向，你仍然可以指定 `echo` 语句的输出流向 `STDERR`，在本例中，它仍然被重定向到 `testerror` 文件。

当你希望将脚本中部分输出重定向到替代位置（例如错误日志）时，这个功能会很有用。使用此功能时，你只会遇到一个问题。

在重定向 `STDOUT` 或 `STDERR` 之后，你无法轻松地将它们重定向回原始位置。如果你需要来回切换重定向，你需要学习一个技巧。本章后面的“创建自己的重定向”部分将讨论这个技巧及其在 shell 脚本中的使用方法。

# 第 15 章：呈现数据

### 在脚本中重定向输入
你可以使用在脚本中重定向 *STDOUT* 和 *STDERR* 的相同技术来从键盘重定向 *STDIN*。`exec` 命令允许你从 Linux 系统上的文件重定向 *STDIN*：

```bash
exec 0< testfile
```

此命令告知 shell 应该从 *testfile* 文件而不是 *STDIN* 获取输入。此重定向适用于脚本请求输入的任何时候。以下是该技术的实际示例：

```bash
$ cat test12
#!/bin/bash
# redirecting file input

exec 0< testfile
count=1

while read line
do
    echo "Line #$count: $line"
    count=$[ $count + 1 ]
done
$ ./test12
Line #1: This is the first line.
Line #2: This is the second line.
Line #3: This is the third line.
$
```

第 14 章“处理用户输入”向你展示了如何使用 *read* 命令读取用户从键盘输入的数据。通过从文件重定向 *STDIN*，当 *read* 命令尝试从 *STDIN* 读取时，它会从文件而不是键盘检索数据。

这是一种读取文件中数据以在脚本中处理的优秀技术。Linux 系统管理员的常见任务之一是读取日志文件中的数据进行处理。这是完成该任务的最简单方法。

### 创建自己的重定向
在脚本中重定向输入和输出时，你并不局限于这三个默认的文件描述符。我提到过，在 shell 中你可以拥有多达九个打开的文件描述符。其他六个文件描述符编号从 3 到 8，可供你用作输入或输出重定向。你可以将这些文件描述符中的任意一个分配给一个文件，然后在脚本中使用它们。本节向你展示如何在脚本中使用其他文件描述符。

