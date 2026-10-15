

![](img/02e070097d401d3bf7de4bf1c470b267_206_0.png)

这里，**directory-names** 是要创建的目录的路径名。当你登录后，可以使用下面的命令在主目录中创建一个名为 **memos** 的子目录。新创建目录的访问权限由当前 umask 值决定（见 Chapter 5）。可以使用如下 `ls -ld memos` 命令确认目录是否创建成功：

```bash
$ mkdir memos
$ ls -ld memos
drwxr-xr-x 2 sarwar faculty 68 Aug 15 07:42 memos
$
```

同样，你也可以使用以下命令在 `/tmp` 目录中创建一个名为 **test_example** 的目录：

```bash
$ mkdir /tmp/test_example
$
```

在主目录中，你可以使用带有 `-p` 选项的 `mkdir` 命令创建 **professional** 目录及其子目录 **letters**，如下所示：

```bash
$ mkdir -p professional/letters
$
```

可以使用 `rmdir` 命令删除空目录。如果目录不为空，则必须先删除其中的文件和子目录，才能删除该目录。要删除非空目录，需要使用带有 `-r` 选项的 `rm` 命令（见 Chapter 6）。下面简要介绍 `rmdir` 命令。

![](img/02e070097d401d3bf7de4bf1c470b267_206_1.png)

以下命令从当前工作目录中删除 **letters** 目录。如果 **letters** 不为空，`rmdir` 命令会显示错误信息：`rmdir: letters: Directory not empty`。如果 **letters** 是一个文件，命令会显示错误信息：`rmdir: letters: Not a directory.`

```
$ rmdir letters
$
```

以下命令从当前工作目录中删除目录 letters，并从主目录中删除 memos。

```
$ rmdir letters ~/memos
$
```

如果 ~/personal 目录仅包含一个名为 diary 的空子目录，你可以使用以下命令删除这两个目录。

```
$ rmdir -p ~/personal/diary
$
```

## 4.5.5 Determining File Attributes

你可以通过使用带有各种选项的 ls 命令来确定文件的属性。这些选项可以一起使用，且顺序无关紧要。例如，你可以使用 -l 选项获取目录的长列表，从而显示文件的属性，如文件所有者，具体如下：

```
$ ls -l
total 5
drwxr-x--- 2 sarwar faculty 512 Jan 23 09:37 courses
drwxr-x--- 2 sarwar faculty 12 May 01 13:22 memos
drwxr-x--- 2 sarwar faculty 163 May 05 23:13 personal
$ ls -l ~/courses/ee446/exams
-rw-r--r-- 1 sarwar faculty 1512 Mar 12 11:10 mid1
-rw-r--r-- 1 sarwar faculty 1485 May 19 14:34 mid2
drwxrwxrwx 2 sarwar faculty 63 May 12 13:44 solutions
$
```

ls -l 命令显示的信息在表 4.3 中进行了总结。

在上述两次使用 ls -l 命令中，courses、memos、personal 和 solutions 是目录，而 mid1 和 mid2 是普通文件。如前所述，我们将在第 5 章讨论访问权限和用户类型。文件的拥有者是 sarwar，他属于 faculty 组。其余字段的值不言自明。

你可以使用 ls 命令的 -i 选项来显示文件和目录的 inode 编号。要显示目录的 inode 编号，需要使用 ls -id 命令。以下使用示例显示 greeting 文件的 inode 编号为 6278611，而目录 courses、memos 和 personal 的 inode 编号分别为 6555603、6555456 和 6555324。

```
$ ls -i greeting
6278611 greeting
```

建议你阅读系统上 ls 命令的在线手册页，或查阅本书在 CRC Press 网站上的命令附录，以获取该命令的详细描述。

通过使用 shell 元字符和正则表达式，你可以指定文件系统结构中的特定文件和目录集，或文件中或目录中的特定字符串集。例如，以下命令可在 C shell 中使用，以显示 ~/courses/ee446 目录中所有以 lab 开头后跟零个或多个字符的文件的长列表，其中第一个字符不能为 5，且文件扩展名为 .c。

```
$ ls -l ~/courses/ee446/lab[^5]*.c
...
$
```

同样，以下命令可用于显示当前目录中所有文件名长度为四个字符且扩展名为 .html 的文件 inode 编号和名称。文件名必须以字母开头，其后跟任意两个字符，并以 1 到 5 之间的数字结尾。

```
$ ls -i [a-zA-Z]??[1-5].html
...
$
```

以下命令在 C shell 下显示主目录中所有不以数字开头且以 .c 或 .C 结尾的文件名。换句话说，该命令显示所有不以数字开头 C 和 C++ 源程序文件的文件名。在 Bourne shell 下，你可以将 ^ 字符替换为 ! 字符。因此，ls ~/[^0-9]*.[c,C] 命令会产生相同的结果。

```
$ ls ~/[^0-9]*.[c,C]
...
$
```

## 4.5.6 Determining the Type of a File's Contents

由于 UNIX 不支持文件扩展名，你可以为任何文件使用任何扩展名。这意味着你可以使用 .jpg 扩展名为可执行程序文件。因此，你不能仅通过查看文件名来确定文件内容的类型。由于许多软件工具需要使用扩展名且用户可能依赖扩展名，因此扩展名仍然很重要。在 UNIX 中，你可以使用 file 命令找到文件内容的类型。该命令主要用于确定文件是否包含文本或二进制数据。做到这一点很重要，因为文本文件可以在终端屏幕上显示，而显示二进制文件的内容会在终端屏幕上显示“乱码”，并且可能冻结终端，因为它可能会将某些二进制值解释为控制代码。该命令的语法如下。

