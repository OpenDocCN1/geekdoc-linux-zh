
## 第二部分：Shell 脚本基础

这显示了当前进程（Bash 外壳）的默认文件描述符（0、1 和 2）。`lsof` 的默认输出包含若干列信息，如表 15.2 所述。

### 表 15.2 默认 `lsof` 输出

| 列名 | 描述 |
| :--- | :--- |
| COMMAND | 进程中命令名称的前九个字符 |
| PID | 进程 ID |
| USER | 拥有该进程的用户的登录名 |
| FD | 文件描述符编号和访问类型（r (读), w (写), u (读/写)) |
| TYPE | 文件类型（CHR (字符设备), BLK (块设备), DIR (目录), REG (普通文件)) |
| DEVICE | 设备编号（主设备和次设备） |
| SIZE | 如果可用，则是文件的大小 |
| NODE | 本地文件的节点号 |
| NAME | 文件名 |

与 STDIN、STDOUT 和 STDERR 关联的文件类型是字符模式。由于 STDIN、STDOUT 和 STDERR 文件描述符都指向终端，因此输出文件的名称是终端的设备名称。这三个标准文件既可以用于读取也可以用于写入（尽管能够向 STDIN 写入和从 STDOUT 读取似乎有些奇怪）。

现在，让我们看看在一个打开了一些替代文件描述符的脚本内部，`lsof` 命令的结果：

```bash
$ cat test18
#!/bin/bash
# testing lsof with file descriptors

exec 3> test18file1
exec 6> test18file2
exec 7< testfile

lsof -a -p $$ -d0,1,2,3,6,7
$ ./test18
COMMAND  PID USER   FD  TYPE DEVICE SIZE     NODE NAME
test18   3594 rich   0u   CHR  136,0        2 /dev/pts/0
test18   3594 rich   1u   CHR  136,0        2 /dev/pts/0
test18   3594 rich   2u   CHR  136,0        2 /dev/pts/0
test18   3594 rich   3w   REG  253,0     0 18 /home/rich/test18file1
test18   3594 rich   6w   REG  253,0     0 11 /home/rich/test18file2
test18   3594 rich   7r   REG  253,0    73 33 /home/rich/testfile
$ 
```

该脚本创建三个替代文件描述符，两个用于输出（3 和 6），一个用于输入（7）。当脚本运行 `lsof` 命令时，你可以看到输出中的新文件描述符。文件名显示了文件描述符中使用的文件的完整路径名。它将这些文件中的每一个都显示为 REG 类型，这表明它们是文件系统上的普通文件。

## 抑制命令输出

有时，你可能不希望脚本显示任何输出。如果你将脚本作为后台进程运行（参见第 16 章，“脚本控制”），这种情况经常发生。如果脚本在后台运行期间发生任何错误消息，外壳会将它们通过电子邮件发送给进程的所有者。这可能会变得烦人，特别是如果你运行那些会产生轻微烦人错误的脚本时。

为了解决这个问题，你可以将 `STDERR` 重定向到一个名为 `null file`（空文件）的特殊文件。空文件基本上就是它听起来的那样——一个不包含任何内容的文件。外壳输出到空文件的任何数据都不会被保存；因此，数据会丢失。

Linux 系统中空文件的标准位置是 /dev/null。你重定向到该位置的任何数据都会被丢弃，并且不会出现：

```bash
$ ls -al > /dev/null
$ cat /dev/null
$
```

这是一种常见的抑制错误消息而不实际保存它们的方法：

```bash
$ ls -al badfile test16 2> /dev/null
-rw-r--r-- 1 rich rich 135 Jun 20 19:57 test16
$
```

你还可以将 /dev/null 文件作为输入文件用于输入重定向。由于 /dev/null 文件不包含任何内容，程序员经常使用它来快速从现有文件中移除数据，而无需删除文件并重新创建它：

```bash
$ cat testfile
This is the first line.
This is the second line.
This is the third line.
$ cat /dev/null > testfile
$ cat testfile
$
```

文件 `testfile` 仍然存在于系统中，但现在它是空的。这是一种常见的方法，用于清空必须保留在原地以供应用程序运行的日志文件。

## 使用临时文件

Linux 系统包含一个保留用于临时文件的特殊目录位置。Linux 使用 `/tmp` 目录来存储不需要永久保留的文件。大多数 Linux 发行版都配置了系统在启动时自动移除 `/tmp` 目录中的任何文件。

系统上的任何用户账户都有权限在 /tmp 目录中读写文件。此功能提供了一种简单的方法，让你创建不需要担心清理的临时文件。

甚至有一个特定命令用于创建临时文件。`mktemp` 命令允许你轻松地在 `/tmp` 文件夹中创建唯一的临时文件。外壳创建该文件，但不使用你的默认 `umask` 值（参见第 7 章，“理解 Linux 文件权限”）。相反，它仅向文件的所有者分配读写权限，并将你设为文件的所有者。创建文件后，你可以在脚本中完全访问该文件的读写权限，但其他人无法访问该文件（当然，root 用户除外）。

### 创建本地临时文件

默认情况下，`mktemp` 在本地目录中创建文件。要使用 `mktemp` 命令在本地目录中创建临时文件，你只需要指定一个文件名模板。模板由任何文本文件名组成，并在文件名的末尾附加六个 X：

```bash
$ mktemp testing.XXXXXX
$ ls -al testing*
-rw-------    1 rich       rich       0 Jun 20 21:30 testing.Uffff33
$ 
```

`mktemp` 命令用六个字符的代码替换六个 X，以确保文件名在目录中是唯一的。你可以创建多个临时文件，并确信每一个都是唯一的：

```bash
$ mktemp testing.XXXXXX
testing.1DRluV
$ mktemp testing.XXXXXX
testing.1vBtkW
$ mktemp testing.XXXXXX
testing.PggNKG
$ ls -l testing*
-rw-------    1 rich       rich       0 Jun 20 21:57 testing.1DRluV
-rw-------    1 rich       rich       0 Jun 20 21:57 testing.PggNKG
-rw-------    1 rich       rich       0 Jun 20 21:30 testing.Uffff33
-rw-------    1 rich       rich       0 Jun 20 21:57 testing.1vBtkW
$ 
```

如你所见，`mktemp` 命令的输出是它创建的文件的名称。在脚本中使用 `mktemp` 命令时，你需要将该文件名保存在一个变量中，以便稍后在脚本中引用它：

```bash
$ cat test19
#!/bin/bash
# creating and using a temp file

tempfile=$(mktemp test19.XXXXXX)

exec 3>tempfile

echo "This script writes to temp file $tempfile"

echo "This is the first line" >&3
echo "This is the second line." >&3
echo "This is the last line." >&3
exec 3>&-

echo "Done creating temp file. The contents are:"
cat $tempfile
rm -f $tempfile 2> /dev/null
$ ./test19
This script writes to temp file test19.vCDoYa
Done creating temp file. The contents are:
This is the first line.
This is the second line.
This is the last line.
$ ls -al test19*
-rwxr--r-- 1 rich rich 356 Jun 20 22:03 test19
$ 
```

该脚本使用 mktemp 命令创建临时文件，并将文件名分配给 `tempfile` 变量。然后，它将临时文件用作文件描述符 3 的输出重定向文件。在 STDOUT 上显示临时文件名后，它向临时文件写入几行内容，然后关闭文件描述符。最后，它显示临时文件的内容，然后使用 rm 命令将其删除。

## 在 /tmp 中创建临时文件

-t 选项强制 mktemp 在系统的临时目录中创建文件。使用此功能时，mktemp 命令返回用于创建临时文件的完整路径名，而不仅仅是文件名：

```bash
$ mktemp -t test.XXXXXX
/tmp/test.xG3374
$ ls -al /tmp/test*
-rw------- 1 rich rich 0 2025-06-20 18:41 /tmp/test.xG3374
$ 
```

由于 mktemp 命令返回完整的路径名，你可以从 Linux 系统上的任何目录引用该临时文件，无论它将临时目录放在哪里：

```bash
$ cat test20
#!/bin/bash
# creating a temp file in /tmp

tempfile=$(mktemp -t tmp.XXXXXX)

echo "This is a test file." > $tempfile
echo "This is the second line of the test." >> $tempfile
```

