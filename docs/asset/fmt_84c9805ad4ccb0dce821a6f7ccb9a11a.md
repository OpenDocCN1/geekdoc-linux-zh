
### 常用命令

### 通用文件和目录命令

本节回顾您可能每天都会用到的特定于文件和目录的命令。

### cat

**语法：** `cat file [> [>>] [destination file]]`

`cat`命令将文件内容显示到标准输出。使用`cat`命令查看文件内容通常很有帮助。传递给`cat`的参数是您要查看的文件。要查看名为`myfile`的文件内容，请运行：

```
cat myfile
```

`cat`还可以将多个现有文件合并为一个：

```
cat name1 name2 name3 > allnames
```

此示例将文件`name1`、`name2`和`name3`合并以生成最终文件`allnames`。合并顺序由命令行中输入文件的顺序决定。

使用`cat`，您可以将一个文件追加到另一个现有文件。例如，如果您在上一个命令中忘记添加`names4`，仍可通过执行以下命令获得相同结果：

```
cat names4 >> allnames
```

将`names4`追加到`allnames`。

### chmod

**语法：** `chmod [ -R ] *permission-mode*  *file or directory*`

`chmod`命令用于更改文件或目录的权限模式。权限模式指定为三位或四位八进制数。例如：

```
chmod 755 myscript.pl
```

将`myscript.pl`脚本的权限更改为`755` (`rwxr-xr-x`)，允许文件所有者读、写和执行，而其他人仅拥有读和执行权限。再如：

```
chmod -R 744 public_html
```

将`public_html`目录及其所有内容（文件和子目录）的权限更改为`744` (`rwxr-r--`)，这是 Apache 服务器下通过`http://server/~username` URL 访问的个人 Web 目录的典型权限设置。`-R`选项告诉`chmod`递归地更改指定目录下所有文件和目录的权限。

### chown

**语法：** `chown [ -fhr ] *Owner* [ : *Group* ] [ *File* ... ] [ *Directory* ... ]`

`chown`命令将`File`参数指定的文件的所有者更改为`Owner`参数指定的用户。`Owner`参数的值可以是用户 ID 或在`/etc/passwd`文件中找到的登录名。也可以选择性地指定组。`Group`参数的值可以是组 ID 或在`/etc/group`文件中找到的组名。

只有`root`用户可以更改文件的所有者。只有当您是`root`用户或拥有该文件时，才能更改文件的组。如果您拥有该文件但不是`root`用户，则只能将组更改为您所属的组。表 A-1 列出并描述了`chown`选项。

### 表 A-1 `chown` 选项

| 选项 | 说明 |
| :--- | :--- |
| `-f` | 除用法消息外，抑制所有错误消息。 |
| `-h` | 更改遇到的符号链接的所有权，而不更改符号链接指向的文件或目录的所有权。 |
| `-R` | 递归地遍历目录，更改每个文件的所有权。当遇到符号链接且该链接指向目录时，将更改该目录的所有权，但不再进一步遍历该目录。 |

以下示例将文件的现有所有者更改为另一用户：

```
chown bert hisfile.txt
```

### clear

**语法：** `clear`

`clear`命令清除您的终端，并将命令行提示符返回到屏幕顶部。仅当名为`TERM`的环境变量设置为适当的终端类型时，此命令才能正常工作。通常，终端类型为`vt100`。如果`clear`命令不起作用，请使用 Shell 的`set`命令设置`term`。例如，要为`tcsh` Shell 会话设置`TERM`，请使用：

```
set TERM = vt100
```

### cmp

**语法：** `cmp [ -ls ] file1 file2`

`cmp`命令比较两个文件的内容。默认情况下，如果两个文件中不存在差异，`cmp`将保持静默。

为演示此功能，`file1.txt`包含：

```
this is file 1
the quick brown fox jumps over the lazy dog.
```

而`file2.txt`包含：

```
this is file 2
the quick brown fox jumps over the lazy dog.
```

两个文件的唯一区别在于第一行的最后一个字符。一个文件中该字符为`1`，而另一个文件中为`2`：

```
cmp file1.txt file2.txt
file1.txt file2.txt differ: char 14, line 1
```

`cmp`的结果正确地将字符 14、第 1 行识别为两个文件之间不相等的字符。`-l`选项将打印每个文件不同字节的字节编号和不同字节值：

```
cmp -l file1.txt file2.txt
14 61 62
```

前面示例的结果显示字节 14 在两个文件中不同，第一个文件在该位置为八进制 61，第二个文件为八进制 62。

最后，`-s`选项将不显示任何内容。`-s`选项仅返回指示文件间相似性的退出状态。如果文件相同，返回 0（零）。如果文件不同，返回 1。发生错误时返回大于 1 的数字。顺便说一下，如果`cmp`不是您要找的命令，您可能想看看`diff`和`uniq`命令。

### cp

**语法：** `cp [-R] source file or directory file or directory`

使用`cp`命令创建文件的精确副本。`cp`命令至少需要两个参数。第一个参数是您要复制的文件，第二个参数是目标文件的位置或文件名。如果第二个参数是现有目录，`cp`将把源文件复制到该目录中，并保留目标文件的名称。

```
cp main.c main.c.bak
```

前面的示例将复制现有文件`main.c`，并在同一目录下创建一个名为`main.c.bak`的新文件。这两个文档将完全相同，逐位对应。

### cut

**语法：** `[ -cdf list ] *file*`

`cut`命令提取数据列。数据可以是文件中每一行的字节、字符或字段。例如，一个名为`names`的文件包含一组人的信息。每行包含关于一个人的数据：

```
Fast    Freddy:Sacramento:CA:111-111-1111
Joe     Smoe:Los Angeles:CA:222-222-2222
Drake   Snake:San Francisco:CA:333-333-3333
Bill    Steal:New York:NY:444-444-4444
```

要列出文件中所有人的姓名和电话号码，选项`-f`和`-d`就足够了：

```
cut -f 1,4 -d : names
```

```
Fast    Freddy:111-111-1111
Joe     Smoe:222-222-2222
Drake   Snake:333-333-3333
Bill    Steal:444-444-4444
```

`-f list`选项指定您选择显示的字段。每个字段由`-d`选项定义。在前面的示例中，`-d :`表示每个字段由冒号分隔。使用 1 作为字段分隔符使字段 1 和 4 成为姓名和电话号码字段。

## 516 附录

### cut

要显示特定列的内容，请使用`-c list`选项：

```bash
cut -c 1-5 names
Fast
Joe
Drake
Bill
```

前面的示例展示了如何列出文件`names`中第 1 列到第 5 列的内容，而不显示其他内容。

### diff

**语法**：`diff [-iqb] file1 file2`

`diff`命令用于确定文件之间的差异。默认情况下，如果文件相同，`diff`不会产生任何输出。

`diff`命令与`cmp`命令在比较文件的方式上有所不同。`diff`逐行报告两个文件之间的差异，而`cmp`逐字符报告两个文件之间的差异。因此，`cmp`比`diff`更适合比较二进制文件。对于文本文件，`cmp`主要用于当你只想知道两个文件是否相同时。

为了说明逐字符考虑变化与逐行考虑变化的区别，请设想在文件开头添加一个换行符会发生什么。如果将该文件与另一个在其他方面完全相同但开头没有换行符的文件进行比较，`diff`将报告文件中添加了一个空行，而`cmp`将报告这两个文件几乎在每个字符上都不同。

正常输出格式由一个或多个差异块组成；每个块显示文件存在差异的一个区域。正常格式的差异块如下所示：

```
change-command
< from-file-line
< from-file-line...
---
> to-file-line
> to-file-line...
```
