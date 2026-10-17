
这是一个帮助你找回重定向文件描述符的技巧。你可以将备用文件描述符分配给标准文件描述符，反之亦然。这意味着你可以将 `STDOUT` 的原始位置重定向到备用文件描述符，然后将该描述符重回 `STDOUT`。这听起来有点复杂，但在实践中非常简单。这个示例将为你解释清楚：

```bash
$ cat test14
#!/bin/bash
# storing STDOUT, then coming back to it
exec 3>&1
exec 1>test13out
echo "This should store in the output file"
echo "along with this line." >3
exec 1>&3
echo "Now things should be back to normal"
$ ./test14
Now things should be back to normal
$ cat test13out
This should store in the output file
along with this line.
$
```

# 第 15 章：数据演示

这个例子有点疯狂，所以让我们逐一分析。首先，脚本将文件描述符 `3` 重定向到文件描述符 `1` 的当前位置，即 `STDOUT`（标准输出）。这意味着任何发送到文件描述符 `3` 的输出都将进入显示器。

第二个 `exec` 命令将 `STDOUT` 重定向到输出文件。现在，shell 将任何发送到 `STDOUT` 的输出重定向到该文件。然而，文件描述符 `3` 仍然指向 `STDOUT` 的原始位置，即显示器。如果此时你向文件描述符 `3` 发送输出数据，它仍然会去显示器，即使 `STDOUT` 已经被重定向。

在向 `STDOUT`（此时指向一个文件）发送了一些输出后，脚本将 `STDOUT` 重定向到文件描述符 `3` 的当前位置，该位置仍然被设置为显示器。这意味着现在 `STDOUT` 指向了它的原始位置——显示器。

这种方法可能会让人困惑，但它是脚本文件中临时重定向输出并将输出恢复正常设置的常用方法。

## 创建输入文件描述符

你可以完全按照输出文件描述符的方式重定向输入文件。在将输入重定向到文件之前，先将 `STDIN` 文件描述符的位置保存到另一个文件中；当读取完文件后，可以将 `STDIN` 恢复到它的原始位置：

```bash
$ cat test15
#!/bin/bash
# 重定向输入文件描述符

exec 0< testfile

count=1
while read line
do
  echo "Line $count: $line"
  count=$(( count + 1 ))
done
exec 0<&6
read -p "Are you done now? " answer
case $answer in
  Y|y) echo "Goodbye";
  N|n) echo "Sorry, this is the end."
esac
$ ./test15
Line #1: This is the first line.
Line #2: This is the second line.
Line #3: This is the third line.
Are you done now? y
Goodbye
$
```

## 第二部分：Shell 脚本基础

在这个例子中，文件描述符 `6` 用于存储 `STDIN` 的位置。脚本随后将 `STDIN` 重定向到一个文件。`read` 命令的所有输入都来自重定向后的 `STDIN`，而它现在就是输入文件。

当所有行读取完毕后，脚本通过将 `STDIN` 重定向回文件描述符 `6`，将其其恢复到原始位置。脚本使用另一个命令（使用 `time` 命令等待键盘输入）进行测试，以确保 `STDIN` 已恢复正常。

## 创建读写文件描述符

尽管看起来很奇怪，但你也可以打开一个单一的文件描述符同时用于输入和输出。然后你可以使用同一个文件描述符从文件中读取数据并将数据写入同一个文件。

使用这种方法时需要格外小心。然而，当你对文件读写数据时，shell 会维护一个内部指针，指示它在文件中的位置。任何读取或写入操作都会发生在文件指针上次停止的地方。如果你不小心，这可能会产生一些有趣的结果。看这个例子：

```bash
$ cat test16
#!/bin/bash
# 测试输入/输出文件描述符
exec 3> testfile
read line <&3
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
This is a test line.
This is the third line.
$
```

这个例子使用 `exec` 命令将文件描述符 `3` 分配给发送到和来自 `testfile` 文件的输入和输出。接下来，它使用 `read` 命令通过分配的文件描述符读取文件的第一行，然后将读取到的数据行显示在 `STDOUT` 中。之后，它使用 `echo` 语句向用相同文件描述符打开的文件写入一行数据。

当你运行脚本时，起初一切看起来正常。输出显示脚本读取了 `testfile` 文件中的第一行。然而，如果你在运行脚本后显示 `testfile` 的内容，你会发现写入文件中的数据覆盖了已有的数据。

当脚本向文件写入数据时，它从文件指针所在的位置开始。命令读取了第一行数据，因此它文件指针指向第二行数据的第一个字符。当 `echo` 语句向文件输出数据时，它会将数据放在文件指针的当前位置，覆盖那里的任何数据。

## 关闭文件描述符

如果你创建了新的输入或输出文件描述符，shell 在脚本退出时会自动关闭它们。然而，在某些情况下，你需要在脚本结束之前手动关闭文件描述符。

要关闭文件描述符，将其重定向到特殊符号 `&&-`。这在脚本中的写法如下：

```bash
exec 3>&-
```

该语句关闭了文件描述符 `3`，防止它在脚本中被再次使用。这是一个尝试使用已关闭的文件描述符时发生的情况示例：

```bash
$ cat badtest
#!/bin/bash
# 测试关闭文件描述符
exec 3> testfile1
echo "This is a test line of data" >&3
exec 3>&-
echo "This won't work" >&3
$ ./badtest
./badtest: 3: Bad file descriptor
$
```

关闭文件描述符后，你就无法再次使用它。如果你需要使用它，必须重新打开它。

## 列出打开的描述符

有很多命令行参数和选项可以过滤 `lsof` 的输出。最常用的是 `-p`（允许你指定进程 ID，PID）和 `-d`（允许你指定文件描述符）。为了方便确定进程的 PID，你可以使用特殊环境变量 `$$`，shell 会将其设置为当前的 PID。`-a` 选项用于对其他两个选项执行布尔与操作，如下所示：

```bash
$ /usr/bin/lsof -p $$ -d 0,1,2
COMMAND PID USER FD TYPE SIZE NODE
bash 3344 0u CH 136,0 2 /dev/pts/0
bash 3344 1u CH 136,0 2 /dev/pts/0
bash 3344 2u CH 136,0 2 /dev/pts/0
```

这显示了进程（`bash` shell）的默认描述符（`0`、`1` 和 `2`）。`lsof` 的输出包含几列信息，如表 15-2 所示。

表 15-2 默认输出

| 列名 | 描述 |

|---|---|

| COMMAND | 进程中命令名称的前九个字符 |

| PID | 进程 ID |

| USER | 拥有进程的用户登录名 |

| FD | 文件描述符编号和访问类型 [r-(读), w-(写), u-(读/写)] |

| TYPE | 文件类型 [CHR—字符), BLK—块), DIR—目录), REG—普通文件)] |

| DEVICE | 设备的设备（主号和次号） |

| SIZE | 如果可用，文件的大小 |

| NODE | 本地文件的节点号 |

| NAME | 文件名 |

`STDIN`、`STDOUT` 和 `STDERR` 相关的文件类型是字符模式。由于 `STDIN`、`STDOUT` 和 `STDERR` 描述符都指向终端，因此输出文件的名称是终端设备名称。这三个标准文件均可读写（尽管向 `STDIN` 写入并从 `STDOUT` 读取似乎很奇怪）。

现在，让我们在一个打开了两个替代文件描述符的脚本内部执行 `lsof` 命令的结果：

## 第二部分：Shell脚本基础
