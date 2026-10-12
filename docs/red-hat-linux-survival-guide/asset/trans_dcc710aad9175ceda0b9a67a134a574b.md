
The man command allows you to view the online manuals. The syntax for this command is as follows:

```
man [-k] [section] keyword
```

The keyword is usually the name of the program, utility, or function. The default action is to search in all of the available sections following a predefined order and to show only the first page found, even if the keyword exists in several sections.

Because commands may appear in several sections, the first page found might not be the man page you are looking for. The command printf is a good example.

Say you are writing a program and would like to know more about the ANSI C library function printf(). Just by typing

```
man printf
```

you get information about printf. However, the man pages for this printf are for the shell command printf. Obviously, this is the wrong information. A reasonable solution is to list all of the sections covering printf (if it exists in multiple sections) and to select the correct one. You can search the keywords of the man pages with the -k option:

```
man -k printf
fprintf    printf (3)    - formatted output conversion
fprintf    printf (3)    - print formatted output
printf     printf (1)    - write formatted output
printf     printf (3)    - formatted output conversion
printf     printf (3)    - print formatted output
```

The printf you are interested in this example is a library function that can be found in section 3 (from Table B-4) or, more specifically, in section 3b or 3s (as you can see from the preceding output). To specify a particular section of a man page, you pass it to man at the command line to find the correct information you are looking for:

```
man 3b printf
```

## 通用文件和目录命令

在本节中，你将学习有关文件和目录特定命令的知识，这些命令你很可能会在日常使用中用到。

### cat

**语法：** `cat file [> | >>] [destination_file]`

cat 命令将文件的内容显示到标准输出，使你能够检查文件的内容。你传递给 cat 的参数是你想要查看的文件。要查看名为 name 的文件的全部内容，你可以使用以下命令（命令下方显示示例输出）：

```
cat name
Kiwee
Joe
Ricardo
Charmaine
```

cat 也可以将多个现有文件合并为一个：

```
cat name1 name2 name3 > allnames
```

此示例将文件 name1、name2 和 name3 合并以生成最终文件 allnames。你通过在命令行输入文件的顺序来确定合并的顺序。

使用 cat，你可以将一个文件追加到另一个文件。例如，如果你在上一个命令中忘记添加文件 name4，你可以通过执行以下命令将其添加到 allnames 文件中：

```
cat name4 >> allnames
```

### chmod

**语法：** `chmod [-R] permission_mode file_or_directory`

使用此命令更改文件或目录的权限模式。权限模式指定为三位或四位八进制数。例如：

```
chmod 755 myscript.pl
```

上述命令将 myscript.pl 脚本的权限更改为 755 (rwxr-xr-x)，这允许文件所有者读取、写入和执行，而其他人只有读取和执行权限。以下是另一个示例：

```
chmod -R 744 public_html
```

上述命令将 public_html 目录及其所有内容（文件和子目录）的权限更改为 744 (rwxr--r--)，这是在使用 Apache 服务器通过 http://server/~username URL 访问个人 Web 目录时典型的权限设置。-R 选项告诉 chmod 递归地更改指定目录下所有文件和目录的权限。

### chown

```
Syntax: chown [ -f h R ] owner [ :group ] { file . . . | directory . . . }
```

chown 命令将 File 参数指定的文件的拥有者更改为 Owner 参数指定的用户。Owner 参数的值可以是 /etc/passwd 文件中的用户 ID 或登录名。可选地，你还可以指定一个组。group 参数的值可以是 /etc/group 文件中的组 ID 或组名。

只有 root 用户可以更改文件的拥有者。你只能在你是 root 用户或拥有该文件时更改文件的组。如果你拥有该文件但不是 root 用户，你只能将其组更改为你所属的组。表 A-2 讨论了 chown 选项的细节。

### 表 A-2 chown 选项

| 选项 | 描述 |
|---|---|
| -f | 仅抑制使用信息之外的所有错误消息。 |
| -h | 更改遇到的符号链接的拥有权，但不更改该符号链接指向的文件或目录的拥有权。 |
| -R | 递归遍历目录，更改每个文件的拥有权。当遇到符号链接且链接指向目录时，该目录的拥有权会被更改，但不会进一步遍历该目录。 |

以下示例将文件的拥有者更改为另一用户：

```
chown bert hisfile.txt
```

### clear

语法: clear

clear 命令清除你的终端并将命令行提示符返回到屏幕顶部。

### cmp

语法: cmp [-ls] file1 file2

此命令比较两个文件的内容。如果两个文件之间没有差异，cmp 默认保持沉默。

为了演示，假设 file1.txt 包含以下内容：

```
this is file 1
the quick brown fox jumps over the lazy dog.
```

而 file2.txt 包含以下内容：

```
this is file 2
the quick brown fox jumps over the lazy dog.
```

两个文件之间的唯一区别是第一行的最后一个字符。在一个文件中，该字符是“1”，而另一个文件中有“2”。现在使用 cmp 按如下方式比较文件：

```
cmp file1.txt file2.txt
file1.txt file2.txt differ: char 14, line 1
```

如前所述，cmp 的结果正确地将字符 14、第 1 行识别为两个文件之间不相等字符。-l 选项打印每个文件的字节编号和不同的字节值。

```
cmp -l file1.txt file2.txt
14 61 62
```

前述示例的结果显示字节 14 不同，第一个文件为八进制 61，第二个文件为八进制 62。最后，-s 选项不显示任何内容。-s 选项仅返回指示文件相似性的退出状态。如果文件相同，则返回 0 (zero)，如果文件不同，则返回 1。最后，当发生错误时，-s 选项返回一个 number >1 (greater than 1) 的数字。

### cp

**语法：** `cp [-R] source_file_or_directory file_or_directory`

使用 cp 命令制作文件的精确副本。cp 命令至少需要两个参数：第一个参数是你想要复制的文件，第二个参数是新文件的位置或文件名。如果第二个参数是现有目录，cp 会将源文件复制到该目录中。

```
cp main.c main.c.bak
```

上述示例复制现有文件 main.c file 并在同一目录中创建一个名为 main.c.bak 的新文件。这两个文件在位上完全相同。

### cut

语法: cut [-cdf list] file

cut 命令提取数据列。数据可以是文件中每一行的字节、字符或字段。例如，一个名为 names 的文件包含一群人的信息。每一行包含一个人的数据：

```
Fast Freddy:Sacramento:CA:111-111-1111
Joe Smoe:Los Angeles:CA:222-222-2222
Drake Snake:San Francisco:CA:333-333-3333
Bill Steal:New York:NY:444-444-4444
```

要列出文件中所有个人的姓名和电话号码，请按如下方式使用 -f 和 -d 选项：

```
cut -f 1,4 -d : names
Fast Freddy:111-111-1111
Joe Smoe:222-222-2222
Drake Snake:333-333-3333
Bill Steal:444-444-4444
```

-f list 选项指定你选择显示的字段。-d 选项定义每个字段。在前面的示例中，-d : 表示冒号分隔每个字段。使用 : 作为字段分隔符使字段 1 和 4 成为姓名和电话号码字段。

要显示特定列的内容，请使用 -c list 选项。以下示例显示如何列出文件名 names 中的第 1 到第 5 列，而不显示其他内容：

```
cut -c 1-5 names
Fast
Joe
Drake
Bill
```
