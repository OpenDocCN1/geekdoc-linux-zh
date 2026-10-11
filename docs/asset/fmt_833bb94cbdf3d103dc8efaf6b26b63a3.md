
该脚本使用 `echo` 命令将 STDOUT 重定向到文件 `testerror`（STDERR）。接下来，脚本使用 `echo` 语句向 STDOUT 显示几行。之后，使用 `echo` 命令将 STDOUT 重定向到 `testout` 文件。请注意，当 STDOUT 被重定向时，你仍然可以将 `echo` 语句的输出指向 STDERR，在这种情况下，它会被重定向到 `testerror` 文件。
当你只想将脚本部分内容的输出重定向到另一个位置（例如错误日志）时，这个功能非常有用。但在使用时你会遇到一个问题。
一旦重定向了 STDOUT 或 STDERR，你就无法轻松将它们重定向回原始位置。如果你需要在重定向之间来回切换，你需要学习一个技巧。本章稍后的“创建你自己的重定向”部分将讨论这个技巧以及如何在你的 Shell 脚本中使用它。

## 在脚本中重定向输入

你可以使用相同的技术在脚本中重定向 STDOUT 和 STDERR，从而将 STDIN 重定向键盘。`exec` 命令允许你从 Linux 系统中的文件重定向 STDIN：

```bash
exec 0< testfile
```

该命令告诉 shell 应该从文件 `testfile` 而不是 STDIN 获取输入。重定向在脚本请求输入时随时生效。以下是该操作的示例：

```bash
$ cat test12
#!/bin/bash
# redirecting file input

exec 0< testfile
count=1

while read line
do
    echo "Line #$count: $line"
    count=$((count + 1))
done
```

```bash
$ ./test12
Line #1: This is the first line.
Line #2: This is the second line.
Line #3: This is the third line.
$ 
```

第 14 章“处理用户输入”向你展示了如何使用 `read` 命令从用户的键盘读取数据。通过从文件重定向 STDIN，当 `read` 命令尝试从 STDIN 读取时，它将从文件中检索数据而不是键盘。
这是读取文件数据进行处理的极佳技术。Linux 系统管理员的一项常见任务是从日志文件中读取数据进行处理。这是完成该任务最简单的方法。

## 创建你自己的重定向

当你在脚本中重定向输入和输出时，并不局限于三个默认的文件描述符。我提到过，在 shell 中最多可以有 9 个打开的文件描述符。其他文件描述符的编号从 3 到 8，可供你输入或输出重定向。你可以将这些文件描述符中的任何一个分配给文件，然后在脚本中使用它们。本节向你展示如何在脚本中使用其他文件描述符。

## 创建输出文件描述符

你使用 `exec` 命令为输出分配文件描述符。对于标准描述符，在你向文件位置分配了备用文件描述符后，重定向将保持有效，直到你重新分配它。以下在脚本中使用备用描述符的简单示例：

```bash
$ cat test13
#!/bin/bash
# using an alternative test13out

echo "This should display on the monitor"
echo "This should be stored in the file" >&3
echo "This should be back on the monitor"
$ ./test13
```

```text
This should display on the monitor
Then this should be back on the monitor
cat test13out
and this should be stored in the file
$ 
```

## 第二部分：Shell 脚本基础

该脚本使用 `exec` 命令将文件描述符 3 重定向到备用文件位置。当脚本执行 `echo` 语句时，它们如你预期那样显示在 STDOUT 上。然而，重定向到文件描述符 3 的 `echo` 语句会进入备用文件。这允许你保留屏幕输出并将特殊信息（如日志文件）重定向到文件中。
你还可以使用 `exec` 命令将数据追加到现有文件而不是创建一个新文件：

```bash
exec >>>test13out
```

现在输出被追加到 `test13out` 文件，而不是创建一个新文件。

## 重定向文件描述符

这是一个找回重定向文件描述符的技巧。你可以将备用文件描述符分配给标准文件描述符，反之亦然。这意味着你可以将 STDOUT 的原始位置重定向到备用文件描述符，然后将文件描述符重定向回 STDOUT。这听起来有点复杂，但在实践中非常简单。这个示例将为你阐明一切：

```bash
$ cat test14
#!/bin/bash
# storing STDOUT, then coming back to it

exec 3>1
exec 1>test14out

echo "This should store in the output file"
echo "along with this line."

exec 1>&3

echo "Now things should be back to normal"
$ ./test14
```

```text
Now things should be back to normal
$ cat test14out
This should store in the output file
along with this line.
$
```

脚本将 STDIN 重定向到文件，这意味着该文件现在是输入的源。

## 演示数据

在从文件重定向 STDIN 后，`read` 命令尝试从 STDIN 读取时，它将从文件中检索数据而不是键盘。这是读取文件数据进行处理的极佳技术。Linux 系统管理员的一项常见任务是从日志文件中读取数据进行处理。这是完成该任务最简单的方法。

## 创建输入描述符

当你在脚本中重定向输入和输出时，并不局限于三个默认的文件描述符。我提到过，在 shell 中最多可以有 9个打开的文件描述符。其他文件描述符的编号从 3 到 8，可供你输入或输出重定向。你可以将这些文件描述符中的任何一个分配给文件，然后在脚本中使用它们。本节向你展示如何在脚本中使用其他文件描述符。

## 创建读写文件描述符

出乎意料的是，你还可以为输入和输出打开同一个文件描述符。你可以使用同一个描述符来读取和写入数据。然而，使用这种方法需要格外小心。当你对文件读写数据时，shell 会维护一个指针，指示其所在位置。看这个示例：

```bash
$ cat test16
#!/bin/bash
# testing input/output file descriptor

exec 3<>testfile
read line <3
echo "Read: $line"
echo "This is a test line" >3
$ cat test16
This is the first line.
This is the second line.
This is the third line.
$ ./test16
Read: This is the first line.
$ cat testfile
This is the first line.
This is a test line.
This is the third line.
$
```

当你运行脚本时，起初一切看起来正常。输出显示脚本读取了 `testfile` 中的第一行。然而，如果你在运行脚本后显示 `testfile` 的内容，你会发现写入文件的数据覆盖了原有数据。
当脚本向文件写入数据时，它从指针所在的位置开始。`read` 命令读取了第一行数据，因此它让指针指向了第二行的第一个字符。当脚本向文件写入数据时，它将数据放在指针的当前位置，覆盖掉那里的任何数据。

## 关闭文件描述符

如果你创建了新的输入或输出文件描述符，shell 在脚本退出时会自动关闭它们。然而，在某些情况下，你需要在脚本结束之前手动关闭文件描述符。
要关闭文件描述符，将其重定向到特殊符号 `&`。它在脚本中的显示形式如下：

```
exec 3>&-
```

该语句关闭文件描述符 3，使其在脚本中不再可用。以下是一个当你尝试使用已关闭的文件描述符时会发生的情况示例：

```bash
cat badtest
#!/bin/bash
# testing closing file descriptors

exec 3> test17file

echo "This is a test line of data" >&3
exec 3>&-

echo "This won't work" >&3
./badtest: 3: Bad file descriptor
$
```

关闭文件描述符后，你无法在脚本中向其写入任何数据，或者 shell 会产生错误信息。
