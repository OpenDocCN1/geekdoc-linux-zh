

# 抑制命令输出

有时，你不希望显示脚本输出的任何内容。这通常发生在你作为后台进程运行脚本时（参见第 13 章）。如果脚本在后台运行期间发生任何错误消息，shell 会向进程的所有者发送电子邮件。这可能会变得非常繁琐，尤其是当你运行那些会产生细微错误（性扰错误）的脚本时。

为了解决这个问题，你可以将 STDERR 重定向到一个名为“空文件”（null file）的特殊文件。空文件实际上正如其名一样，是一个内容为空的文件。shell 输出到空文件的任何数据都不会被保存，从而导致丢失。

Linux 系统上空文件的标准位置是 `/dev/null`。任何你重定向到该位置的数据都将被丢弃且不会显示：

```
$ ls -al > /dev/null
$ cat /dev/null
$
```

这是在不实际保存错误的情况下抑制任何错误消息的常用方法：

```
$ ls -al badfile test16 2> /dev/null
-rw-xr-r-- 1 rich      rich      135 Oct 29 19:57 test16*
$
```

你也可以将 `/dev/null` 文件作为输入重定向的文件。由于 `/dev/null` 文件不包含内容，程序员经常使用它来快速从现有文件中删除数据，而无需删除文件并重新创建：

```
$ cat testfile
This is the first line.
This is the second line.
This is the third line.
$ cat /dev/null > testfile
$
```

文件 `testfile` 仍然存在于系统中，但现在它是空的。这是清理必须留在原位以供应用程序运行的日志常用方法。

# 使用临时文件

Linux 系统包含一个用于临时文件的特殊目录位置。Linux 使用 `/tmp` 目录存放不需要永久保留的文件。大多数 Linux 发行版配置为在启动时自动删除 `/tmp` 目录中的任何文件。

# 数据演示 12

系统上的任何用户账户都有权限读写 `/tmp` 目录中的文件。此功能为你提供了一种简单的方法来创建临时文件，而不必担心清理工作。

甚至有特定的命令用于创建临时文件。`mktemp` 命令允许你轻松地在 `/tmp` 文件夹中创建一个唯一的临时文件。shell 会创建该文件，但不会使用你的默认 umask 值（参见第 6 章）。相反，它只为文件所有者分配读写权限，并让你成为文件的所有者。一旦你创建了文件，你就可以在脚本中完全访问并进行读写，但其他人将无法访问它（当然，root 用户除外）。

# 创建本地临时文件

默认情况下，`mktemp` 在本地目录中创建一个文件。要使用 `mktemp` 命令在本地目录中创建临时文件，你只需要指定文件名模板。该模板由任何文本文件名组成，并在文件名末尾附加六个 `X`：

```
$ mktemp testing.XXXXXX
$ ls -al testing*
-rw-------r 1 rich 0 Oct 29 21:30 testing.Ufii3
$
```

`mktemp` 命令将六个 `X` 替换为六位代码，以确保文件名在目录中是唯一的。你可以创建多个临时文件，并确保每一个都是唯一的：

```
$ mktemp testing.XXXXXX
testing.1DRLuV
$ mktemp testing.XXXXXX
testing.1VBtkw
$ mktemp testing.XXXXXX
testing.PqgKG
$ ls -l testing*
-rw------- 1 rich rich 0 Oct 29 21:57 testing.1DRLuV
-rw------- 1 rich rich 0 Oct 29 21:57 testing.PggKNG
-rw------- 1 rich rich 0 Oct 29 21:30 testing.Ufii3
-rw------- 1 rich rich 0 Oct 29 21:57 testing.1VBtkw
$
```

如你所示，`mktemp` 命令的输出是它创建的文件名。当你在脚本中使用 `mktemp` 命令时，你会希望将文件名保存到变量中，以便以后在脚本中引用它：

```
$ cat test19
#!/bin/bash
# creating and using a temp file
tempfile=`mktemp test19.XXXXXX`
```

# 第二部分 Shell 脚本基础

```
exec 3>$tempfile

echo "This script writes to temp file $tempfile"

echo "This is the first line" >&3
echo "This is the second line." >&3
echo "This is the last line." >&3
exec 3&-

echo "Done creating temp file. The contents are:"
cat $tempfile
rm -f $tempfile 2> /dev/null
./test19
This script writes to temp file test19.vCHoya
Done creating temp file. The contents are:
This is the first line
This is the second line.
This is the last line.
$ -al test19*
-rwxr-xr-r--      1 rich      rich      356 Oct 29 22:03 test19* 
```

该脚本使用 `mkdir` 命令创建一个临时文件，并将文件名赋值给变量 `$tempfile`。然后它将该文件作为文件描述符 3 的输出重定向文件。在 STDOUT 上显示临时文件名后，它向临时文件写入几行内容，然后关闭文件描述符。最后，它显示临时文件的内容并使用 `rm` 命令将其删除。

# 在 /tmp 中创建临时文件

`-t` 选项强制 `mkdir` 在系统的临时目录中创建文件。当你使用此功能时，`mkdir` 命令返回用于创建临时文件的完整路径，而不仅仅是文件名：

```
$ mkdir -t test.XXXXXX
/tmp/test.xG3374
$ -al /tmp/test*
-rw-r--      1 rich 0 2007-10-29 18:41 /tmp/test.xG3374 
```

`mkdir` 命令返回完整路径，然后你可以从 Linux 系统上的任何目录引用它，无论它将临时目录放在哪里：

```
$ mkdir -t test.XXXXXX
/tmp/test.xG3374
```

# 数据演示

系统上的任何用户账户都有权限读写 `/tmp` 目录中的文件。此功能为你提供了一种简单的方法来创建临时文件，而不必担心清理工作。

甚至有特定的命令用于创建临时文件。`mktemp` 命令允许你轻松地在 `/tmp` 文件夹中创建一个唯一的临时文件。shell 会创建该文件，但不会使用你的默认 umask 值（参见第 6 章）。相反，它只为文件所有者分配读写权限，并让你成为文件的所有者。一旦你创建了文件，你就可以在脚本中完全访问并进行读写，但其他人将无法访问它（当然，root 用户除外）。

# 创建本地临时文件

默认情况下，`mktemp` 在本地目录中创建一个文件。要使用 `mktemp` 命令在本地目录中创建临时文件，你只需要指定文件名模板。该模板由任何文本文件名组成，并在文件名末尾附加六个 `X`：

```
$ mktemp testing.XXXXXX
$ ls -al testing*
-rw-------r 1 rich 0 Oct 29 21:30 testing.Ufii3
$
```

`mktemp` 命令将六个 `X` 替换为六位代码，以确保文件名在目录中是唯一的。你可以创建多个临时文件，并确保每一个都是唯一的：

```
$ mktemp testing.XXXXXX
testing.1DRLuV
$ mktemp testing.XXXXXX
testing.1VBtkw
$ mktemp testing.XXXXXX
testing.PqgKG
$ ls -l testing*
-rw------- 1 rich rich 0 Oct 29 21:57 testing.1DRLuV
-rw------- 1 rich rich 0 Oct 29 21:57 testing.PggKNG
-rw------- 1 rich rich 0 Oct 29 21:30 testing.Ufii3
-rw------- 1 rich rich 0 Oct 29 21:57 testing.1VBtkw
$
```

如你所示，`mktemp` 命令的输出是它创建的文件名。当你在脚本中使用 `mktemp` 命令时，你会希望将文件名保存到变量中，以便以后在脚本中引用它：

```
$ cat test19
#!/bin/bash
# creating and using a temp file
tempfile=`mktemp test19.XXXXXX`
```

---

脚本使用 `mkdir` 命令创建一个临时文件，并将文件名赋值给变量 `$tempfile`。然后它将该文件作为文件描述符 3 的输出重定向文件。在 STDOUT 上显示临时文件名后，它向临时文件写入几行内容，然后关闭文件描述符。最后，它显示临时文件的内容并使用 `rm` 命令将其删除。

# 在 /tmp 中创建临时文件

`-t` 选项强制 `mkdir` 在系统的临时目录中创建文件。当你使用此功能时，`mkdir` 命令返回用于创建临时文件的完整路径，而不仅仅是文件名：

```
$ mkdir -t test.XXXXXX
/tmp/test.xG3374
$ -al /tmp/test*
-rw-r--      1 rich 0 2007-10-29 18:41 /tmp/test.xG3374 
```

`mkdir` 命令返回完整路径，然后你可以从 Linux 系统上的任何目录引用它，无论它将临时目录放在哪里：

（此处原文存在重复内容，已按要求进行处理）

# 数据演示

系统上的任何用户账户都有权限读写 `/tmp` 目录中的文件。此功能为你提供了一种简单的方法来创建临时文件，而不必担心清理工作。

甚至有特定的命令用于创建临时文件。`mktemp` 命令允许你轻松地在 `/tmp` 文件夹中创建一个唯一的临时文件。shell 会创建该文件，但不会使用你的默认 umask 值（参见第 6 章）。相反，它只为文件所有者分配读写权限，并让你成为文件的所有者。一旦你创建了文件，你就可以在脚本中完全访问并进行读写，但其他人将无法访问它（当然，root 用户除外）。

# 创建本地临时文件

默认情况下，`mktemp` 在本地目录中创建一个文件。要使用 `mktemp` 命令在本地目录中创建临时文件，你只需要指定文件名模板。该模板由任何文本文件名组成，并在文件名末尾附加六个 `X`：

```
$ mktemp testing.XXXXXX
$ ls -al testing*
-rw-------r 1 rich 0 Oct 29 21:30 testing.Ufii3
$
```

`mktemp` 命令将六个 `X` 替换为六位代码，以确保文件名在目录中是唯一的。你可以创建多个临时文件，并确保每一个都是唯一的：

```
$ mktemp testing.XXXXXX
testing.1DRLuV
$ mktemp testing.XXXXXX
testing.1VBtkw
$ mktemp testing.XXXXXX
testing.PqgKG
$ ls -l testing*
-rw------- 1 rich rich 0 Oct 29 21:57 testing.1DRLuV
-rw------- 1 rich rich 0 Oct 29 21:57 testing.PggKNG
-rw------- 1 rich rich 0 Oct 29 21:30 testing.Ufii3
-rw------- 1 rich rich 0 Oct 29 21:57 testing.1VBtkw
$
```

如你所示，`mktemp` 命令的输出是它创建的文件名。当你在脚本中使用 `mktemp` 命令时，你会希望将文件名保存到变量中，以便以后在脚本中引用它：

```
$ cat test19
#!/bin/bash
# creating and using a temp file
tempfile=`mktemp test19.XXXXXX`
```

# 第二部分 Shell 脚本基础

```
exec 3>$tempfile

echo "This script writes to temp file $tempfile"

echo "This is the first line" >&3
echo "This is the second line." >&3
echo "This is the last line." >&3
exec 3&-

echo "Done creating temp file. The contents are:"
cat $tempfile
rm -f $tempfile 2> /dev/null
./test19
This script writes to temp file test19.vCHoya
Done creating temp file. The contents are:
This is the first line
This is the second line.
This is the last line.
$ -al test19*
-rwxr-xr-r--      1 rich      rich      356 Oct 29 22:03 test19* 
```

