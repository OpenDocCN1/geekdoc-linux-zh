

在前面的示例中，子目录内部没有其他子目录。如果还有更多层级的子目录，`-R` 参数也会继续遍历它们。不难想象，对于大型目录结构来说，这会生成相当冗长的列表。

## 显示长格式列表

在基本列表中，`ls` 命令不会为每个文件提供太多信息。要列出附加信息，另一个常用的参数是 `-l`。`-l` 参数会生成长格式列表，提供关于目录中每个文件的更多信息：

```bash
$ ls -l
total 8
drwxr-xr-x. 2 christine christine  6 Feb 20 14:23 Desktop
drwxr-xr-x. 2 christine christine  6 Feb 20 14:23 Documents
drwxr-xr-x. 2 christine christine  6 Feb 20 14:23 Downloads
drwxr-xr-x. 2 christine christine 28 Feb 29 15:42 Music
-rwxr-xr-x. 1 christine christine 74 Feb 29 15:49 my_script
drwxr-xr-x. 2 christine christine  6 Feb 20 14:23 Pictures
drwxr-xr-x. 2 christine christine  6 Feb 20 14:23 Public
drwxr-xr-x. 2 christine christine  6 Feb 20 14:23 Templates
-rw-rw-r--. 1 christine christine 74 Feb 29 15:50 test_file
drwxr-xr-x. 2 christine christine  6 Feb 20 14:23 Videos
$
```

长格式列表将每个文件和目录显示在单独的一行中。除了文件名外，列表还显示了其他有用的信息。输出的第一行显示了该目录内文件分配的总块数（8）。在此之后，每行包含关于每个文件（或目录）的以下信息：

-   文件类型，例如目录 (d)、文件 (-)、链接文件 (l)、字符设备 (c) 或块设备 (b)
-   文件权限（参见第 6 章）
-   文件硬链接数量（参见本章“链接文件”一节）
-   文件所有者用户名
-   文件主组名称
-   文件字节大小
-   文件最后修改时间
-   文件名或目录名

`-l` 参数是一个强大的工具。掌握这个参数后，你可以查看任何文件或目录所需的大部分信息。

> **提示**
>
> 如果你只想查看单个文件的长格式列表，只需将文件名附加到你的 `ls -l` 命令中即可。但是，如果你想查看目录本身的长格式列表（而非其内容），你不仅需要在命令中添加目录名称，还需要添加 `-d` 开关，例如：`ls -ld Directory-Name`。

在执行文件管理时，`ls` 命令有许多实用的参数。如果在 shell 提示符下输入 `man ls`，你会看到几页可用的参数，可以使用它们来修改 `ls` 命令的输出。

不要忘记，你还可以组合许多参数。你经常可以找到一种参数组合，不仅能显示所需的输出，而且易于记忆，例如 `ls -aiF`。

## 过滤列表输出

正如示例所示，默认情况下 `ls` 命令会列出所有非隐藏目录文件。有时，这样做可能过于繁琐，尤其是当你只是在查找少数几个文件的信息时。

幸运的是，`ls` 命令还提供了在命令行中定义过滤器的方法。它使用过滤器来确定应在输出中显示哪些文件或目录。

在使用过滤命令之前，让我们通过 `touch` 命令（在下一节中介绍）创建一些文件来操作。如果文件已经存在，该命令不会损坏文件：

```bash
$ touch my_script my_scrapt my_file
$ touch fall fell fill full
$ ls
  Desktop   Downloads  fell  full  my_file   my_script   Public   test_file
  Documents   fall     fill  Music my_scrapt Pictures  Templates  Videos
$
```

过滤器作为一个简单的文本匹配字符串工作。将过滤器放在你要使用的任何命令行参数之后：

```bash
$ ls -l my_script
-rwxr-xr-x   1 christine christine  74 Feb 29 16:12 my_script
$
```

当你指定特定文件名作为过滤器时，`ls` 命令仅显示该文件的信息。有时，你可能不知道确切要查找的文件名。`ls` 命令还识别标准通配符字符，并使用它们来匹配过滤器内的模式：

-   问号 (?) 代表一个字符。
-   星号 (*) 代表任意数量的字符。

问号可用于替换过滤器字符串中任意位置的恰好一个字符。例如：

```bash
$ ls -l my_scri?t
-rw-rw-r--   1 christine christine    0 Feb 29 16:12 my_scrapt
-rwxr-xr-x   1 christine christine  74 Feb 29 16:12 my_script
$
```

# 第 3 章：基本 Bash Shell 命令

```bash
$ ls -l my*
-rw-rw-r-- 1 christine christine 0 Feb 29 16:12 my_file
-rw-rw-r-- 1 christine christine 0 Feb 29 16:12 my_scrapt
-rwxr-xr-x 1 christine christine 74 Feb 29 16:12 my_script
$
```

使用星号找到了以 my 开头的三个不同文件。与问号一样，你可以将星号放在过滤器中的任何位置：

```bash
$ ls -l my*?pt
-rw-rw-r-- 1 christine christine 0 Feb 29 16:12 my_scrapt
-rwxr-xr-x 1 christine christine 74 Feb 29 16:12 my_script
$
```

在过滤器中使用星号和问号被称为*文件通配*（file globbing）。文件通配是使用通配符进行模式匹配的处理过程。通配符正式称为*元字符通配符*。除了星号和问号外，你还可以使用更多的元字符通配符进行文件通配。你还可以使用方括号：

```bash
$ touch my_scr[y]pt
$ ls -l my_scr[ay]pt
-rw-rw-r-- 1 christine christine 0 Feb 29 16:12 my_scrapt
-rw-rw-r-- 1 christine christine 0 Feb 29 16:18 my_scr[y]pt
$
```

这个示例使用了方括号以及该位置单个字符的两个可能选项：a 或 y。方括号代表单个字符位置，并为文件通配提供多种选择。你可以列出字符选项，如前面的示例所示，也可以指定字符范围，例如字母范围 [a-i]：

```bash
$ ls f*ill
fall fill filli full
$ ls f[a-i]ill
fall fill filli
$
```

此外，你可以使用感叹号 (!) 指定哪些内容*不应*包含在模式匹配中：

```bash
$ ls -l f[!a]ll
-rw-rw-r-- 1 christine christine 0 Feb 29 16:12 fill
-rw-rw-r-- 1 christine christine 0 Feb 29 16:12 filli
-rw-rw-r-- 1 christine christine 0 Feb 29 16:12 full
$
```

在搜索文件时，文件通配是一个强大的功能。除了 ls 之外，它还可以与其他 shell 命令一起使用。你将在本章后面了解更多关于这一点的内容。

# 处理文件

Shell 在 Linux 文件系统上提供了许多文件操作命令。本节将带你了解处理文件所需的基本 shell 命令。

## 创建文件

偶尔你会遇到需要创建一个空文件的情况。例如，有时应用程序期望在写入日志文件之前该文件必须存在。在这种情况下，你可以使用 `touch` 命令轻松创建空文件：

```bash
$ touch test_one
$ ls -l test_one
-rw-rw-r--. 1 christine christine 0 Feb 29 17:24 test_one
$
```

`touch` 命令创建你指定的新文件，并将你的用户名分配为文件所有者。注意前面的示例中，文件大小为零，因为 `touch` 命令刚刚创建了一个空文件。

`touch` 命令还可用于更改修改时间。这是在不更改文件内容的情况下完成的：

```bash
$ ls -l test_one
-rw-rw-r--. 1 christine christine 0 Feb 29 17:24 test_one
$ touch test_one
$ ls -l test_one
-rw-rw-r--. 1 christine christine 0 Feb 29 17:26 test_one
$
```

`test_one` 的修改时间已从原始时间 `17:24` 更新为 `17:26`。

在 Linux 系统中，创建空文件和更改文件时间戳并不是每天都会做的事情。然而，在使用 shell 时，复制文件是你经常执行的操作。

## 复制文件

将文件和目录从文件系统中的一个位置复制到另一个位置是系统管理员的常见做法。`cp` 命令提供了此功能。

在最基本形式下，`cp` 命令使用两个参数——源对象和目标对象：`cp source destination`。

当*源*和*目标*参数都是文件名时，`cp` 命令将源文件复制到新的目标文件。新文件表现为一个新文件，具有更新的修改时间：

```bash
$ cp test_one test_two
$ ls -l test_one test_two
-rw-rw-r--. 1 christine christine 0 Feb 29 17:26 test_one
-rw-rw-r--. 1 christine christine 0 Feb 29 17:46 test_two
$
```

