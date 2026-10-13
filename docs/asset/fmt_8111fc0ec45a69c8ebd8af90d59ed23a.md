
此命令将在当前目录及其所有子目录中搜索所有以 `.txt` 结尾的文本文件中的关键词 `"magic"`，并返回它们的文件名（因为在 `grep` 中使用了 `-l` 选项）。

```
find . -name \*.gif -atime -1 -exec ls -l {} \;
```

此命令将找到在过去 24 小时（一天）内被访问过的所有 GIF 文件，并使用 `ls -l` 命令显示它们的详细信息。

```
find . -type f -empty
```

这将显示当前目录层次结构中的所有空文件。

### grep

语法：

```
grep [-viw] pattern file(s)
```

### head

语法：

```
head [-count | -n number] filename
```

此命令将显示文件的前几行。默认情况下，显示文件的前 10 行。然而，你可以使用前面的选项来指定不同的行数。

```
head -2 doc.txt
## Outline of future projects
## Last modified: 02/02/99
```

## 第二部分：作为超级用户工作

上面的示例说明了如何查看文本文件 `doc.txt` 的两行。

### ln

语法：

```
ln [-s] sourcefile target
```

`ln` 命令创建两种链接：硬链接和软链接。链接可以被理解为同一个文件的两个名称。一旦创建了链接，它就与原始文件无法区分。一个拥有硬链接的文件在所有链接被删除之前，不会从硬盘上删除。不使用 `-s` 选项时会创建硬链接。

```
ln ./www /public_html
```

然而，硬链接有局限性。硬链接无法链接到另一个目录，硬链接无法链接到另一个文件系统上的文件。使用 `-s` 选项，我们可以创建一个软链接，从而消除这些限制。

```
ln -s /dev/fs02/jack/www /dev/fs01/foo/public_html
```

在这里，我们在文件系统 2 上的目录 `www` 和文件系统 1 上新创建的文件 `public_html` 之间创建了一个软链接。

### locate

语法：

```
locate keyword
```

`locate` 命令查找特定文件或命令的路径。`locate` 会查找精确匹配或子字符串匹配。例如：

```
locate foo
```

```
/usr/lib/texmf/tex/latex/misc/footnpag.sty
/usr/share/automake/footer.am
/usr/share/games/fortunes/food
/usr/share/games/fortunes/food.dat
/usr/share/gimp/patterns/moonfoot.dat
```

`locate` 输出的内容将在绝对路径中包含关键词 `foo`，或者没有任何输出。

### ls

语法：

```
ls [-aR] file or directory
```

`ls` 命令允许你列出目录中的文件（和子目录）。它是最常用的程序之一。当与 `-l` 选项配合时，它只显示当前目录下的文件和目录名称；使用 `-l` 选项时，会显示包含文件/目录权限信息、大小、修改日期等信息的详细列表；`-a` 选项允许你查看当前目录下所有的文件和目录（包括名称以点为前缀的文件）；`-R` 选项允许命令递归显示内容（如果有的话）。

### mkdir

语法：

```
mkdir directory . .
```

要创建目录，请使用 `mkdir` 命令。选择目录名时只有两个限制：(1) 文件名长度可达 255 个字符，(2) 目录名可以包含除 `/` 之外的任何字符。

```
mkdir dir1 dir2 dir3
```

上面的示例将在当前目录下创建三个目录，前提是当前目录已授予了写权限。

### mv

语法：

```
mv [-if]sourcefile targetfile
```

使用 `mv` 命令移动或重命名目录和文件。该命令将根据 `targetfile` 是否为已存在的目录来执行移动或重命名。为了说明，我们想重命名当前名为 `foo` 的现有目录。

### pico

语法：

```
pico [filename]
```

`pico` 是一个简单的文本编辑器。

### pwd

语法：

```
pwd
```

`pwd` 命令将打印当前工作目录。

## tail

语法：

```
tail [-count | -n number] filename
```

`tail` 命令将显示文件的最后几行。默认情况下，显示文件的最后 10 行。

### wc

语法：

```
wc [-lwc] file(s)
```

`wc` 命令用于统计行数、单词数和字节数。

## diff

语法：

```
diff [options] file1 file2
```

`diff` 命令用于比较两个文件的差异。

### echo

语法：

```
echo [options] string
```

`echo` 命令将字符串输出到终端。

### exit

语法：

```
exit [status]
```

`exit` 命令用于退出 shell 会话。

### help

语法：

```
help [command]
```

`help` 命令显示命令的帮助信息。

### man

语法：

```
man [command]
```

`man` 命令显示命令的手册页。

### nano

语法：

```
nano [filename]
```

此命令显示如下输出：

```
File: *foo.txt*
Size: 4447232  Filetype: Regular File
Mode: (0644-/rw-r--r--)Uid: (0/root) Gid: (0/root)
Device: 3,0  Inode: 16332  Links: 1
Access: Mon Mar 1 21:34:39 1999(00000.02:32:30)
Modify: Mon Mar 1 22:14:26 1999(00000.01:57:47)
Change: Mon Mar 1 22:14:26 1999(00000.01:57:47)
```

如你所示，显示了文件访问、修改、更改日期、大小、所有者和组信息、权限模式等内容。

## strings

语法：

```
strings filename
```

`strings` 命令打印至少四个四个字符的字符序列。该工具主要用于描述非文本文件的内容。

## tail

语法：

```
tail [-count | -fr] filename
```

`tail` 命令显示文件的末尾。默认情况下，`tail` 会显示文件的最后 10 行。要显示 `doc.txt` 文件的最后 50 行，我们执行以下命令：

```
tail -50 doc.txt
```

`-r` 选项以反序显示输出。默认情况下，`-r` 显示文件的所有行，而不仅仅是 10 行。例如，要反序显示 `doc.txt` 文件的全部内容，请使用：

```
tail -r doc.txt
```

要反序显示 `doc.txt` 文件的最后 10 行，请使用：

```
tail-10r doc.txt
```

最后，`-f` 选项在您监控文件时非常有用。使用此选项，`tail` 将等待新数据写入文件。随着新数据被添加到文件中，`tail` 将这些数据显示在屏幕上。要停止 `tail` 监控文件，请按 Ctrl+C（中断键），因为 `tail` 命令不会自动停止。

### touch

语法：

```
touch file or directory
```

此命令更新文件或目录的时间戳。如果指定的文件不存在，它将创建一个空文件。

### umask

请参阅第 4 章中关于用户默认文件权限的章节。

### uniq

语法：

```
uniq [-c] filename
```

`uniq` 命令将比较相邻行并仅显示唯一的行。当与 `-c` 选项一起使用时，`uniq` 会统计出现的次数。如果一个文件的内容如下：

- a
a
a
bb
a

当使用 `uniq` 处理时，它将产生以下结果：

```
uniq test.txt
a
b
a
```

## 第 5 章：常用命令

注意相邻的 a 是被删除了，但文件中并不是所有的 a 都被删除了。这是使用 `uniq` 时一个需要记住的重要细节。如果你想在名为 `test.txt` 的文件中找到所有唯一的行，可以运行以下命令：

```
sort test.txt | uniq
```

此命令将对 `test.txt` 文件进行排序，并将所有相似行相邻，允许 `uniq` 仅显示唯一的行。例如，假设你想快速找到有多少个独立访客访问了你的网站，你可以运行以下命令：

```
awk '(print $1)' access.log | sort | uniq
```
